---
layout: post
lng_pair: id_20261111_alphagenome2
title: "AlphaGenome 2 : dites-lui quelle cellule vous interrogez, il lit le même ADN autrement"
author: OpenSI-Labs
category: Bio AI
tags: [AlphaGenome 2, DeepMind, génomique, ADN, cellule unique, effets de variants]
date: 2026-11-11 06:00:00 -0800
img: /assets/img/posts/2026-11-11-alphagenome-2.png
---

## Le même livre, mais pas le même chapitre ouvert

L'ADN est comme un très long livre d'instructions, identique dans presque chaque cellule. Les gènes en sont les recettes. Pourtant, une cellule de l'intestin et une cellule du sang ne font pas le même travail : chacune n'ouvre qu'un chapitre et n'utilise que certaines recettes.

Autour des recettes, des interrupteurs et des variateurs règlent leur niveau d'activité. Un variant, c'est une seule lettre changée dans le livre. Or la plupart des variants liés à une maladie ne touchent pas une recette, mais un de ces réglages. La même lettre peut donc ne rien changer dans une cellule, et tout changer dans une autre.

## Ce que faisait la première version, et son angle mort

AlphaGenome, la première version, lisait déjà un million de lettres d'ADN et prédisait ce qui s'y passe : pistes d'activité des gènes (ARN, les copies de travail des recettes ; épissage ; accessibilité de l'ADN ; marques chimiques d'ouverture ou de fermeture ; fixation de protéines de contrôle ; méthylation), valeurs d'expression et cartes 3D des contacts.

Son angle mort : il n'avait appris que sur des données « en vrac », mélangeant des tissus entiers — comme moyenner un smoothie au lieu de goûter chaque fruit. Il prédisait tous les tissus en parallèle : une réponse moyennée, sans adaptation à une cellule précise.

## Le changement : la cellule devient une partie de la question

AlphaGenome 2, annoncé par DeepMind le 11 novembre 2026 (auteurs : Gayoso, Mottram, Karollus, Hassabis, Kohli, Avsec, notamment), inverse la démarche : on lui donne le segment d'ADN, l'espèce — humain ou souris — et une seule condition, un tissu, un type ou un état de cellule. Il prédit ce que cet ADN fait dans cette cellule-là, seulement là.

Cette condition devient un résumé chiffré qui ajuste le réseau à chaque étape, via des couches dites de normalisation adaptative. Le résumé peut venir d'un dictionnaire de conditions de référence apprises par le modèle. Plus nouveau : un module séparé, l'encodeur de cellule, peut le construire à partir des propres données du chercheur — ses mesures d'ARN cellule par cellule, l'activité des gènes une cellule à la fois. On peut ainsi interroger un type ou un état de cellule jamais vu comme catégorie nommée, sans réentraîner le modèle.

<figure>
<svg viewBox="0 0 720 250" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Schéma : le même ADN, lu différemment selon la cellule" style="width:100%;height:auto;font-family:sans-serif;">
<rect x="20" y="95" width="200" height="36" rx="18" fill="#eef2ff" stroke="#334155" stroke-width="1.5"/>
<text x="42" y="120" font-size="17" fill="#1e293b">A</text>
<text x="72" y="120" font-size="17" fill="#1e293b">C</text>
<text x="102" y="120" font-size="17" fill="#1e293b">G</text>
<circle cx="142" cy="113" r="14" fill="none" stroke="#dc2626" stroke-width="2.5"/>
<text x="135" y="120" font-size="17" fill="#dc2626" font-weight="bold">T</text>
<text x="172" y="120" font-size="17" fill="#1e293b">A</text>
<text x="120" y="75" font-size="20" fill="#334155" text-anchor="middle">→</text>
<text x="120" y="165" font-size="15" fill="#1e293b" text-anchor="middle">Un même ADN,</text>
<text x="120" y="187" font-size="15" fill="#1e293b" text-anchor="middle">une lettre changée</text>
<circle cx="300" cy="85" r="32" fill="#dbeafe" stroke="#334155" stroke-width="1.5"/>
<circle cx="300" cy="85" r="13" fill="#93c5fd" stroke="#334155" stroke-width="1"/>
<circle cx="420" cy="85" r="32" fill="#dcfce7" stroke="#334155" stroke-width="1.5"/>
<circle cx="420" cy="85" r="13" fill="#86efac" stroke="#334155" stroke-width="1"/>
<text x="300" y="140" font-size="14" fill="#1e293b" text-anchor="middle">Cellule sanguine ?</text>
<text x="420" y="140" font-size="14" fill="#1e293b" text-anchor="middle">Cellule intestinale ?</text>
<text x="360" y="185" font-size="15" fill="#475569" text-anchor="middle">Laquelle pose la question ?</text>
<text x="478" y="120" font-size="20" fill="#334155" text-anchor="middle">→</text>
<rect x="505" y="62" width="60" height="20" rx="6" fill="#cbd5e1" stroke="#64748b" stroke-width="1"/>
<text x="505" y="50" font-size="15" fill="#1e293b">Gène éteint</text>
<rect x="505" y="130" width="180" height="20" rx="6" fill="#22c55e" stroke="#15803d" stroke-width="1"/>
<text x="505" y="118" font-size="15" fill="#1e293b">Gène actif</text>
<text x="595" y="185" font-size="15" fill="#475569" text-anchor="middle">Deux réponses possibles</text>
</svg>
<figcaption>Figure 1 — Le même segment d'ADN peut faire des choses très différentes selon la cellule. AlphaGenome 2 fait de la cellule une partie de la question.</figcaption>
</figure>

L'architecture, en forme de U, reste proche de la première version. L'entraînement s'est fait en quatre étapes : pré-entraînement, affinage de la condition, distillation, post-entraînement. Huit modèles enseignants ont été distillés en un seul élève, entraîné sur des séquences modifiées au hasard pour imiter leur réponse moyenne, puis post-entraîné sur des données unicellulaires : 3 977 pistes de 36 études humain-souris ; méthylation pour 185 conditions ; échantillon de 107 millions de profils d'ARN unicellulaires humains. L'encodeur de cellule a appris sur plus de 100 millions de profils, couvrant 68 tissus.

## Ce que montrent les résultats, en termes simples

Tous les chiffres suivants sont ceux de DeepMind, tirés de son article. Le test le plus parlant : TenK10K, des données cellule par cellule. Tâche : retrouver quels variants changent vraiment l'expression d'un gène. Face à une première version adaptée à ces données (AG1-sc), le rappel — la part des vrais variants retrouvés — passe de 16 % à 30 %, à précision de 90 % : neuf réponses sur dix correctes. Pour le sens du changement, hausse ou baisse, le rappel passe de 23 % à 43 %. Dit autrement : sur 10 variants réellement causaux, AG1 en trouvait environ 2, AG2 en trouve 3 — mieux, mais 7 lui échappent encore. Sur les données en vrac (49 tissus), gains plus modestes : 17 % → 26 %, 32 % → 40 %.

Sur le chromosome 21, à un endroit lié aux maladies inflammatoires de l'intestin, des expériences avaient montré que le variant rs2836882 augmente le risque en activant davantage un gène, ETS2, situé à environ 290 000 lettres, et seulement dans les monocytes et macrophages, deux familles de cellules du sang. Donnés sept variants candidats, AlphaGenome 2 n'a désigné que rs2836882, l'a relié à ETS2 malgré la distance, et a limité l'effet à ces cellules : trois éléments justes à la fois. L'équipe a aussi pré-calculé environ 7 millions de variants dans 510 conditions : les variants causaux identifiés ensuite y étaient environ 280 fois plus concentrés qu'au hasard.

## Les limites, dites clairement — et un accès restreint

L'article reste lucide. Même amélioré, le modèle ne retrouve qu'une minorité des variants causaux à haute précision : un rappel de 30 % signifie 70 % manqués. Il sous-estime les variants hors des régions accessibles, à très grande distance, ou après la transcription, la copie d'ARN déjà fabriquée. Les états passagers, stimulés ou malades sont peu représentés dans ses données ; il peut aussi confondre des sous-types proches de neurones. Ses résumés de condition apprennent des corrélations, pas des causes : on ignore s'il gère la suppression complète d'un gène ou le passage dynamique d'un état à un autre.

L'accès recule par rapport à la première version. Il est disponible dès maintenant pour la recherche non commerciale, mais seulement via une interface de programmation, une API. Le code et les poids — les réglages internes pour le faire tourner chez soi — ne seront partagés qu'« à la publication finale » : pas publiés, donc, alors que la première version les avait fournis. Restent téléchargeables des prédictions déjà calculées : un atlas éléments régulateurs–gènes (640 conditions) et des scores de variants (510 conditions). Usage de recherche uniquement, sans validation clinique.

Pourquoi cela compte : la question n'est plus « que fait cet ADN ? », mais « que fait cet ADN dans cette cellule précise — y compris une cellule décrite par le chercheur avec ses propres données ? ». Un pas réel, mais un instrument prometteur, pas une réponse définitive.
