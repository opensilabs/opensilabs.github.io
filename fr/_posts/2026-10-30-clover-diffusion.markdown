---
layout: post
lng_pair: id_20261030_clover-diffusion
title: "Clover écrit par blocs, pas mot à mot : le modèle de diffusion de 35 milliards de DiffuSpace revendique 73,6 à SWE-bench"
author: OpenSI-Labs
category: Modèles d'IA
tags: [modèle de diffusion, Clover, DiffuSpace, poids ouverts, SWE-bench]
date: 2026-10-30 20:00:00 -0700
img: /assets/img/posts/2026-10-30-clover-diffusion.png
---

Les 28 et 29 octobre 2026, une entreprise nommée DiffuSpace a publié son premier modèle, Clover-35B-A3B-Preview. C'est un modèle de langage, mais il n'écrit pas comme les modèles de langage sont censés écrire. Les poids sont sur Hugging Face, sous licence Apache 2.0 — environ 69 Go en BF16, téléchargeables par n'importe qui. DiffuSpace présente Clover comme le plus puissant modèle de diffusion ouvert publié à ce jour. Curieusement, c'est la partie vérifiable du lancement. Le score mis en avant, lui, ne l'est pas.

## Une page de blancs, remplie dans n'importe quel ordre

Depuis GPT, tous les modèles dominants écrivent un jeton à la fois, de gauche à droite. Chaque jeton — un mot ou un morceau de mot — est choisi, écrit, jamais reconsidéré : un mauvais mot au début oblige tout le reste à composer avec l'erreur. La vitesse est plafonnée : le jeton 500 attend les 499 premiers.

Clover écrit par blocs de 32 jetons. Un bloc neuf commence comme 32 emplacements masqués — des blancs. Le modèle lit le bloc entier d'un coup, dans les deux sens, et remplit ses blancs les plus sûrs, plusieurs à la fois. Certains blancs remplis, leurs voisins deviennent plus faciles, et le passage suivant en remplit d'autres. Bloc terminé, il se fige et devient le texte fixe sur lequel le bloc suivant s'appuie. Imaginez un éditeur devant un brouillon plein de trous, qui écrit d'abord les mots certains — pas un dactylo sans touche retour.

<figure>
<img src="/fr/assets/img/posts/2026-10-30-clover-diffusion-fig1.svg" alt="Deux façons d'écrire : un jeton à la fois, ou un bloc de 32 cases vides">
<figcaption>Figure 1 — Les modèles autorégressifs fixent chaque jeton au fur et à mesure ; Clover part de 32 blancs et remplit d'abord les positions les plus sûres.</figcaption>
</figure>

## La règle de remplissage

Le schéma de décodage s'appelle LowConfidence. Un blanc est rempli quand la confiance du modèle dans sa meilleure proposition dépasse un seuil, fixé par défaut à 0,95. Si aucun blanc ne passe la barre, le plus sûr est rempli quand même : un bloc ne peut jamais rester bloqué. Réglages par défaut : bloc de 32, seuil 0,95.

Deux détails distinguent l'ingénierie du tour de passe-passe. Dans un bloc, l'attention fonctionne dans les deux sens : un blanc est éclairé par les mots des deux côtés. Mais le texte avant le bloc reste causal — aucun aperçu des blocs non encore écrits. Et pendant qu'un bloc se résout, le routage peut être restreint à un sous-ensemble d'experts partagé par tout le bloc, qui touche alors moins d'experts distincts.

<figure>
<img src="/fr/assets/img/posts/2026-10-30-clover-diffusion-fig2.svg" alt="Un bloc de 32 cases masquées se résolvant en trois tours">
<figcaption>Figure 2 — Un bloc se remplit en plusieurs tours : les positions dont la confiance dépasse 0,95 sont remplies, et le bloc terminé devient le préfixe du suivant.</figcaption>
</figure>

## Ce qu'il y a sous le capot

Clover compte 35 milliards de paramètres, dont environ 3 milliards actifs par jeton. C'est un mélange d'experts : 40 couches, 256 experts routés dont les 8 premiers sont consultés par jeton, plus un expert partagé par couche. Contexte : 128K jetons, texte uniquement.

Il n'a pas été construit de zéro. Clover dérive du Qwen3.6-35B-A3B d'Alibaba et conserve son squelette hybride, fait de couches Gated DeltaNet et d'attention complète. Les ajouts de DiffuSpace : l'attention bidirectionnelle par bloc — des paramètres appris, dont des poids de convolution à droite, pour que les jetons d'un bloc inachevé s'observent mutuellement pendant que le préfixe reste causal — l'inférence par diffusion en blocs, et des contrôles de génération.

## Un score impossible à vérifier pour l'instant

DiffuSpace annonce 73,6 à SWE-bench Verified, 51,7 à Terminal-Bench 2.1, et 515 jetons par seconde sur un seul H200. Pour un modèle ouvert de 35 milliards de paramètres, ce seraient des chiffres remarquables.

Le problème, dit simplement : il n'existe aucun moyen de vérifier ce 73,6. Une analyse indépendante de Daily Inference (29 octobre) — son titre dit tout : « 73.6 on SWE-bench, and Not One Way to Check It Yet » — relève que les documents de lancement ne précisent ni l'échafaudage d'agent, ni les outils, ni le nombre d'essais, ni les réglages derrière ce score. On peut inspecter les poids et lire la licence ; le résultat ne peut pas être reproduit à partir de ce qui est public. Le 73,6 doit donc se lire comme une affirmation imprimée sur la boîte, pas comme une mesure. Même réserve pour les deux autres chiffres.

## Téléchargeable ne veut pas encore dire exécutable

Que les poids soient publics signifie aussi moins que l'annonce ne le suggère. Cette semaine, la seule façon de faire tourner Clover passe par Hugging Face Transformers, sur un GPU d'environ 69 Go de mémoire. Pas de version GGUF, donc Ollama et LM Studio ne peuvent pas le charger, et la prise en charge par SGLang n'est pas intégrée en amont. DiffuSpace recommande sa propre implémentation SGLang pour le service et l'évaluation, mais les chemins locaux simples ne sont pas encore là. Personne ne fera tourner ce modèle sur un portable cette semaine.

La fiche du modèle reconnaît un autre défaut : les générations très longues peuvent dériver vers la répétition. Clover est donc livré avec des contre-mesures activées par défaut — pénalité de présence de 0,9, pénalité de répétition de 1,05, et des biais qui poussent de plus en plus vers la fin à mesure qu'elle s'allonge. C'est, comme son nom l'indique, une Preview.

## Pourquoi cela compte quand même

Écrire un jeton à la fois est la plus vieille habitude de l'IA moderne, et deux de ses limites sont natives : la vitesse est plafonnée par l'écriture en séquence, et les erreurs précoces sont verrouillées pour de bon. La diffusion par blocs s'attaque aux deux. Remplir les blancs en parallèle pourrait aller beaucoup plus vite, et un bloc peut prendre forme comme un tout — chaque mot conscient de ses voisins — avant que quoi que ce soit soit figé.

Clover est l'affirmation la plus forte à ce jour que cela fonctionne à échelle réelle : 35 milliards de paramètres, des benchmarks de codage agentique, des poids téléchargeables et inspectables par tous. Le mécanisme est réellement là, dans le code. Le score est un billet à ordre. Si des exécutions indépendantes atterrissent près de 73,6, l'habitude d'écriture fondamentale du domaine est remise en question. Sinon, Clover reste le modèle de diffusion ouvert le plus capable publié à ce jour — simplement pas la révolution que son article de lancement annonce.
