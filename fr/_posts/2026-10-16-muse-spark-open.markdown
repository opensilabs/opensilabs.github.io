---
lng_pair: id_20261016_muse_spark_open
title: "Muse Spark Open : le modèle à 816B qui tient sur un bureau"
author: OpenSI-Labs
category: models
tags: [poids ouverts, mixture of experts, Meta, Apple, MLX]
date: 2026-10-16 06:00:00 -0700
img: /assets/img/posts/2026-10-16-muse-spark-open.png
meta_description: "Le modèle ouvert de Meta à 816B paramètres tourne sur deux Mac Studio — la vraie histoire est une percée système contre le mur de la mémoire, plus une licence qui a des dents."
---

Le 15 octobre, Meta a fait ce qu'il refusait de faire tout le printemps : publier les poids. Muse Spark Open — 816 milliards de paramètres, 42 milliards actifs par token, une fenêtre de contexte d'un million de tokens — est, selon Meta, « le modèle américain à poids ouverts le plus capable à ce jour ». Téléchargeable dès aujourd'hui sur Hugging Face. [\[1\]](https://www.macrumors.com/2026/10/15/meta-muse-spark-open-mac-studio/) [\[2\]](https://particle.news/story/meta-releases-muse-spark-open-and-partners-with-apple-to-run-it-on-m5-ultra-macs)

Mais les poids ne sont que la moitié de l'histoire. L'autre moitié, c'est le bureau. Meta s'est associé à Apple pour optimiser le modèle sur MLX, le framework de machine learning d'Apple, et l'a démontré tournant sur deux Mac Studio équipés de puces M5 Ultra — deux ordinateurs de bureau se comportant, selon Meta, « comme un supercalculateur avec un téraoctet de mémoire unifiée ». Un modèle d'échelle frontière, en local, sur du matériel qu'on peut commander. Il y a deux ans, cette phrase aurait été absurde. Il vaut la peine de demander ce qui a changé.

## La sparsité rencontre les gros tuyaux

Le chiffre de 816 milliards fait du marketing ; celui de 42 milliards fait de l'ingénierie. Muse Spark Open est un modèle à mélange d'experts : pour chaque token, un réseau de routage ne réveille qu'un petit sous-ensemble de sous-réseaux « experts » — environ cinq pour cent des paramètres totaux. Imaginez une bibliothèque de 816 milliards de livres où chaque question ne vous envoie que dans une seule allée. Vous possédez toute la bibliothèque, mais vous ne portez jamais qu'une brassée.

<svg viewBox="0 0 640 220" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Schéma de sparsité du mélange d'experts" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,sans-serif" fill="#1a1a1a">Seuls ~5 % des paramètres s'activent par token</text>
  <g font-family="system-ui,-apple-system,sans-serif">
    <rect x="40" y="60" width="560" height="70" rx="8" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="60" y="88" font-size="14" fill="#444">816B paramètres totaux (tous les experts)</text>
    <text x="60" y="112" font-size="14" fill="#444">dormants jusqu'au routage</text>
    <rect x="40" y="150" width="560" height="40" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <rect x="40" y="150" width="29" height="40" rx="8" fill="#2f6df6"/>
    <text x="80" y="176" font-size="14" fill="#1a1a1a">42B actifs par token</text>
    <text x="470" y="176" font-size="14" fill="#555">le routeur choisit l'allée</text>
  </g>
</svg>
*Figure 1 : la sparsité du mélange d'experts — le routeur ne réveille qu'une fine tranche du modèle par token, le calcul par token reste à l'échelle des 42B.*

C'est cette sparsité qui rend le calcul mémoire survivable. En basse précision, 816 milliards de paramètres exigent de l'ordre d'un téraoctet de mémoire — et c'est là qu'Apple entre en scène. Chaque Mac Studio M5 Ultra offre jusqu'à 512 Go de mémoire unifiée que le GPU adresse directement, sans copie entre mémoire CPU et GPU (la taxe que paie chaque configuration à GPU discret), avec 1,2 To/s de bande passante. Deux Studios mettent en commun un téraoctet. Et comme seule une fine tranche de paramètres est touchée par token, cette bande passante suffit à alimenter les experts actifs à une vitesse utilisable. Modèle clairsemé, gros tuyau mémoire, pas de plafond de mémoire GPU discrète : les trois contraintes qui cloîtraient les modèles de classe 800B dans les centres de données se sont relâchées d'un coup.

<svg viewBox="0 0 640 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Schéma de mutualisation de la mémoire unifiée" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,sans-serif" fill="#1a1a1a">Deux bureaux, un téraoctet de mémoire</text>
  <g font-family="system-ui,-apple-system,sans-serif">
    <rect x="40" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="150" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 1</text>
    <text x="150" y="106" text-anchor="middle" font-size="14" fill="#444">512 Go de mémoire unifiée</text>
    <text x="150" y="130" text-anchor="middle" font-size="14" fill="#444">le GPU l'adresse directement</text>
    <rect x="380" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="490" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 2</text>
    <text x="490" y="106" text-anchor="middle" font-size="14" fill="#444">512 Go de mémoire unifiée</text>
    <text x="490" y="130" text-anchor="middle" font-size="14" fill="#444">bande passante 1,2 To/s</text>
    <path d="M260 105 L360 105" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <path d="M380 135 L280 135" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <defs><marker id="arr" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><path d="M0,0 L8,4 L0,8 z" fill="#2f6df6"/></marker></defs>
    <rect x="180" y="185" width="280" height="36" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <text x="320" y="209" text-anchor="middle" font-size="14" fill="#1a1a1a">1 To mutualisé — contient tout le modèle 816B</text>
  </g>
</svg>
*Figure 2 : la mémoire unifiée mutualisée — deux Studios se comportent comme une seule machine avec un téraoctet de mémoire adressable par le GPU, via MLX.*

C'est la vraie histoire technique, et c'est une histoire de systèmes, pas de modèle. Le calcul d'entraînement fait les gros titres, mais la contrainte qui lie l'*usage* des modèles géants a toujours été le mur de la mémoire — garder les poids assez près du calcul, et les alimenter assez vite. Muse Spark Open compte moins pour son nombre de paramètres que comme preuve que le mur est attaqué des deux côtés : des modèles plus clairsemés d'un côté, des architectures à mémoire unifiée de l'autre.

## Le bémol, et la stratégie

Maintenant, l'eau froide. « Poids ouverts » n'est pas « open source », et l'écart compte. La licence du modèle Muse exige une attribution visible « Built with Muse Spark Open », et toute entreprise de plus de 20 millions de dollars de revenus doit notifier Meta et signer un accord commercial avant de proposer le modèle en service. Relisez bien : les poids sont gratuits au téléchargement, mais les conditions commerciales gardent Meta dans la boucle de chaque déploiement sérieux. C'est l'ouverture comme stratégie de distribution — semer l'écosystème, posséder le standard, garder le péage. Un playbook plus malin que le pur open source comme l'API purement fermée, et quiconque bâtit sur des poids ouverts devrait comprendre à quel jeu il joue.

Il y a un deuxième indice dans les petits caractères de l'annonce. Le superlatif est « le modèle *américain* à poids ouverts le plus capable » — et les propres benchmarks de Meta montrent des scores de code inférieurs à certains modèles ouverts chinois de premier plan. La frontière des poids ouverts est multipolaire désormais, et cet adjectif porte une charge.

Et un troisième : « tourne sur votre bureau » signifie pour l'instant deux Mac Studio à plus de 10 000 dollars pièce, dans une configuration 512 Go qu'Apple n'a même pas encore commencé à livrer — elle arrive plus tard ce mois-ci. L'IA de bureau est réelle, et elle coûte encore 20 000 dollars. La démocratisation est une direction, pas une destination.

Rien de tout cela ne diminue l'ingénierie. Un MoE à un million de contexte, 42B actifs, avec de solides scores agentiques et d'utilisation d'outils, tournant en local sur mémoire unifiée mutualisée, est une vraie réussite système — et la détente Apple–Meta qui le sous-tend est elle-même un signal. « Nous sommes ravis que papa et maman s'entendent à nouveau », a dit le chef IA de Meta, Alexandr Wang. Deux entreprises qui se battent d'habitude se sont accordées sur une chose : l'avenir qu'elles veulent toutes deux est celui où l'IA frontière n'a pas besoin de tourner sur la pile de NVIDIA.

**Discussion :** Si les poids sont ouverts mais que la licence garde le contrôle commercial et que le matériel coûte 20 000 dollars, pour qui exactement cette « ouverture » est-elle faite — et cela change-t-il votre façon de construire dessus ?
