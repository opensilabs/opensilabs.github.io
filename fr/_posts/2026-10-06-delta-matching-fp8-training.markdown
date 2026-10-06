---
lng_pair: id_20261006_delta-matching-fp8-training
title: "Le dernier facteur 2 : comment Delta-Matching a bouclé l'entraînement natif FP8 des LLM"
author: OpenSI-Labs
category: research
tags: [FP8, entraînement-LLM, quantification, NVIDIA]
date: 2026-10-06 00:30:00 -0700
meta_description: "Un article CMU/NVIDIA prouve la cause racine de l'écart de précision du FP8 — un invariant du softmax violé — et le répare sous forme close."
---
# Le dernier facteur 2 : comment Delta-Matching a bouclé l'entraînement natif FP8 des LLM

Le 29 septembre, une équipe de cinq chercheurs de CMU et de NVIDIA a publié un article qui règle discrètement l'une des questions les plus coûteuses de l'entraînement des LLM. [« Delta-Matching: Closing the Final Gap of Native 8-bit Training for LLMs »](https://arxiv.org/pdf/2609.37852) (arXiv:2609.37852) affirme ce que le domaine poursuit depuis la sortie des tensor cores FP8 : un entraînement entièrement natif en 8 bits, sans aucune perte de qualité. [La couverture de TechTimes](https://www.techtimes.com/articles/328385/20261001/eight-bit-llm-training-now-matches-full-precision-mit-nvidia-fix-root-cause.htm) a retenu le titre ; l'article lui-même fournit la preuve.

Commençons par le prix. Un H100 délivre 3 958 TFLOPS en arithmétique FP8 creuse contre 1 979 en BF16 — à peu près deux fois plus d'opérations par puce, par watt, par dollar. Les préentraînements de pointe coûtent des dizaines de millions de dollars ; encaisser ce facteur 2, c'est diviser la facture matérielle par deux, ou doubler la taille de batch effective sur le même cluster. L'industrie le savait. Ce qu'elle n'avait jamais eu, c'est un moyen de l'encaisser intégralement.

Le blocage n'a jamais été l'arithmétique. C'était les mathématiques autour.

En 2026, l'entraînement basse précision était un problème résolu presque partout dans le modèle. Les couches linéaires — les grosses multiplications de matrices denses des réseaux feed-forward — s'adaptent sans peine aux opérandes 8 bits. Le récalcitrant, c'était l'attention. Les piles de production comme Transformer Engine et cuDNN de NVIDIA fonctionnaient en hybride : FP8 sur la passe avant, repli discret vers BF16 ou FP32 sur les opérations sensibles de la passe arrière. Ces hybrides marchaient, à peu près. Mais le facteur 2 n'était jamais vraiment encaissé, et le dernier écart restait ouvert par définition — personne n'avait entraîné un grand modèle de bout en bout avec la passe arrière de l'attention en pur FP8.

## Une loi de conservation violée

L'apport de l'article est un diagnostic assorti d'une preuve formelle. La panne est une incohérence avant-arrière : dans l'attention, les opérandes de la passe avant et de la passe arrière sont quantifiés indépendamment, sous des facteurs d'échelle différents. De ce décalage naît un terme corrompu que les auteurs appellent le delta périmé, δˢᵗᵃˡᵉ = ⟨dOᵢ, Ôᵢ⟩ — le produit scalaire du gradient de sortie avec la sortie avant périmée, mise à l'échelle différemment. Il brise une quantité qui doit tenir : l'invariant de somme nulle par ligne du gradient du softmax.

Voici ce que cela signifie. Chaque ligne de la matrice d'attention est une distribution de probabilités ; les lignes somment à un. Si les probabilités doivent toujours sommer à un, alors toute modification — tout gradient — doit sommer à zéro sur la ligne. C'est une loi de conservation, pas une heuristique : les lignes du gradient du softmax doivent s'annuler en somme, sinon la mise à jour ne respecte plus la géométrie de l'attention. Le delta périmé injecte un biais systématique exactement dans ce terme. Les gradients cessent d'être des corrections honnêtes et deviennent, ligne par ligne, une dérive lente. L'entraînement ne plante pas ; il s'empoisonne.

Cela explique aussi pourquoi le bug est resté caché des années. À 569 millions de paramètres, les dégâts se lisent comme un modeste écart de perte — le genre de chiffre qu'une équipe pressée arrondit au bruit ou impute au réglage. À 1,67 milliard et 5,29 milliards, la dégradation devient substantielle. Les petits modèles et les runs courts ont parfaitement dissimulé le mode de défaillance, si bien que la réponse d'ingénierie standard — régler les échelles plus fort, retomber en BF16 — n'a jamais localisé la cause. La cause était structurelle, et la preuve le dit formellement : la quantification indépendante avant/arrière brise l'invariant par construction.

## La correction, sous forme close

Le remède est mathématique lui aussi. Le delta-matching est une correction de forme close qui ajuste le facteur d'échelle périmé — pas une approximation, pas un ordonnancement heuristique, mais une correction qui restaure exactement l'invariant de somme nulle. Avec elle, chaque multiplication de matrices de l'attention tourne nativement en FP8 sous mise à l'échelle par blocs : Q·Kᵀ et P·V sur la passe avant, leurs transposées sur la passe arrière. Aucun changement d'architecture, aucune réduction des batchs globaux, aucune sortie avant auxiliaire conservée pour la passe arrière. C'est une amélioration d'entraînement « drop-in » — l'espèce la plus rare.

Un paragraphe sur les deux dialectes du 8 bits, car le remède doit les réconcilier. Le FP8 existe en deux saveurs : E4M3 (quatre bits d'exposant, trois de mantisse) offre une précision plus fine sur une plage plus étroite, ce qui convient aux activations et aux poids de la passe avant ; E5M2 (cinq bits d'exposant, deux de mantisse) sacrifie la précision pour une plage dynamique plus large, ce dont les gradients ont besoin. La passe arrière de l'attention veut du E5M2, sa passe avant veut du E4M3, et le delta périmé naît dans le passage de relais entre les deux dialectes. Le delta-matching est, à un certain niveau, un protocole pour les faire s'accorder sur un grand livre commun.

## Les chiffres

Ils sont sans détour. En entropie croisée de validation, le delta-matching atteint 1,4162 contre une référence BF16/FP32 de 1,4178 — parité, la variante FP8 devançant même d'un cheveu la référence pleine précision. Le FP8 naïf s'effondre à 1,8970 ; l'hybride cuDNN/Transformer Engine de NVIDIA, le meilleur compromis de production, n'atteint que 1,6105. La parité tient sur 569M, 1,67B et 5,29B paramètres, sur les benchmarks de sens commun en aval à un point de pourcentage près, sur les scores RULER-8K de contexte long (47,8 contre 52,3, avec l'analyse d'extension de contexte dans l'article), et même sous l'optimiseur Muon — le résultat n'est pas un accident de la dynamique d'Adam. Les auteurs publieront l'implémentation, les modèles entraînés et les recettes de données.

## Au-delà des chiffres

D'abord, l'économie. Quand la contrainte qui mord sur l'entraînement de pointe, c'est le dollar par token, diviser par deux le coût matériel d'un préentraînement ne fait pas qu'économiser de l'argent — cela change l'ensemble des organisations capables de se payer la frontière. Laboratoires universitaires, startups bien financées, laboratoires nationaux à budget fixe : un dividende arithmétique de facteur 2 redistribue le droit d'entraîner. Il y a une longue lignée ici, des travaux de Song Han sur Deep Compression — élagage et quantification — il y a dix ans jusqu'à cet article, et chaque étape a discrètement fait la même chose. La précision d'entraînement devient un troisième axe de mise à l'échelle aux côtés des paramètres et des données — non parce que les petits nombres sont à la mode, mais parce que l'arithmétique, c'est le budget.

Ensuite, remarquez la forme de la percée. Le dernier écart n'a pas été comblé par un meilleur kernel, un ordonnancement plus malin ou un réglage plus soigneux — le registre d'ingénierie dans lequel l'industrie travaillait depuis des années. Il a été comblé en nommant un invariant mathématique violé et en le réparant sous forme close. C'est le motif récurrent du dernier kilomètre en travail système : le résidu que l'ingénierie n'arrive pas à raboter est presque toujours un morceau de mathématiques supposé acquis puis brisé. Ceux qui le trouvent sont ceux qui partent à la recherche de l'invariant plutôt que de l'hyperparamètre.

Les auteurs énoncent la réserve franchement : l'analyse couvre la passe arrière standard de l'attention, et l'écart RULER-8K (47,8 contre 52,3) suggère que l'extension de contexte a encore sa propre histoire. Mais l'affirmation centrale — l'attention, dernier bastion, s'entraîne désormais nativement en FP8 à qualité pleine — repose à la fois sur la preuve et sur l'expérience.

**Discussion :** si diviser par deux le coût du préentraînement permet à dix nouveaux laboratoires au lieu de trois d'entraîner à la frontière, qu'est-ce qui change le plus vite — la science elle-même, ou la politique de qui a le droit de la faire ?
