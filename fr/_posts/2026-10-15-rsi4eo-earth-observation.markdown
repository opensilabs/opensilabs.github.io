---
lng_pair: id_20261015_rsi4eo-earth-observation
title: "Le dernier modèle construit par des humains : des agents IA qui améliorent récursivement l'observation de la Terre"
author: OpenSI-Labs
category: research
tags: [auto-amélioration récursive, RSI4EO, observation de la Terre, agents codeurs, IA vérifiable]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-rsi4eo-earth-observation.png
meta_description: "Un agent codeur construit des modèles d'observation de la Terre et les améliore récursivement sur ses propres sorties, surpassant les résultats publiés sur quatre benchmarks d'imagerie satellitaire avec environ un pour cent des étiquettes d'entraînement."
---

**Quand le fleuve monte, personne n'a le temps d'entraîner un modèle.**

Une inondation submerge un delta. Les équipes d'urgence ont besoin d'une carte des dégâts — quels quartiers sont sous l'eau, quelles routes restent praticables — et il la leur faut aujourd'hui. Les satellites sont déjà là-haut, captant la scène en optique, en radar, en multispectral. Mais transformer ces pixels en carte fiable exige encore des spécialistes : des gens qui conçoivent une recette d'entraînement, la règlent contre un benchmark, itèrent pendant des semaines. Quand le modèle est prêt, l'eau s'est retirée et la carte appartient à l'histoire.

Un article déposé sur arXiv le 13 octobre demande ce qui se passe si l'on confie toute la boucle à un agent ([Zhao et al., arXiv:2610.18845](https://arxiv.org/abs/2610.18845v1)). Son titre est délibérément provocateur — « Le dernier modèle de télédétection construit par des humains ? » — et sa thèse est la formulation la plus tranchante de l'auto-amélioration récursive depuis des mois : toute tâche vérifiable peut être coulée en RSI, et l'observation de la Terre est le premier domaine où le moulage est terminé.

Le mécanisme tient en deux mots : harnais et vérificateur. Le harnais, c'est tout ce que l'agent est autorisé à utiliser — données, outils, calcul. Le vérificateur, c'est l'examen scellé à la fin : il note le modèle de l'agent sans exposer les images tenues secrètes sur lesquelles il le juge. Avec ces deux seuls composants, un agent codeur généraliste construit le modèle d'observation de la Terre puis l'améliore récursivement sur ses propres sorties. Personne ne règle la recette à la main. Personne ne surveille la boucle d'entraînement.

<figure>
<svg viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">RSI4EO : l'humain conçoit l'examen, l'agent construit le modèle</text>
<rect x="20" y="60" width="200" height="110" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="120" y="86" font-size="14" font-weight="bold" text-anchor="middle">Conçu par l'humain</text>
<text x="120" y="110" font-size="14" text-anchor="middle">Harnais : données · outils ·</text>
<text x="120" y="130" font-size="14" text-anchor="middle">calcul utilisable par l'agent</text>
<text x="120" y="152" font-size="14" text-anchor="middle" font-style="italic">Vérificateur scellé : évalue</text>
<rect x="250" y="60" width="180" height="110" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="340" y="86" font-size="14" font-weight="bold" text-anchor="middle">Agent codeur</text>
<text x="340" y="110" font-size="14" text-anchor="middle">construit le modèle OT,</text>
<text x="340" y="130" font-size="14" text-anchor="middle">l'améliore récursivement</text>
<text x="340" y="152" font-size="14" text-anchor="middle">sur ses propres sorties</text>
<rect x="460" y="60" width="200" height="110" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="560" y="86" font-size="14" font-weight="bold" text-anchor="middle">Meilleur modèle OT</text>
<text x="560" y="110" font-size="14" text-anchor="middle">inondation / cultures / dégâts</text>
<text x="560" y="130" font-size="14" text-anchor="middle">cartes d'imagerie</text>
<text x="560" y="152" font-size="14" text-anchor="middle">satellite</text>
<line x1="220" y1="115" x2="246" y2="115" stroke="#3366cc" stroke-width="2" marker-end="url(#m1)"/>
<line x1="430" y1="115" x2="456" y2="115" stroke="#cc8833" stroke-width="2" marker-end="url(#m1)"/>
<path d="M 560 170 C 560 260, 120 260, 120 176" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#m1)"/>
<text x="340" y="300" font-size="14" text-anchor="middle" font-style="italic">la sortie d'un cycle devient l'entrée du suivant</text>
<text x="340" y="330" font-size="14" text-anchor="middle">vérifiable : labels · capteurs indépendants · modèles physiques · observation répétée</text>
<defs><marker id="m1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>La boucle : les humains conçoivent le harnais et le vérificateur scellé ; l'agent construit le modèle et l'améliore sur ses propres sorties.</figcaption>
</figure>

Pourquoi les satellites et pas la poésie ? Parce qu'en observation de la Terre, c'est la réalité qui note. Les auteurs montrent que toute tâche d'OT peut être rendue vérifiable par l'un de quatre canaux : benchmarks étiquetés, capteurs indépendants, modèles physiques, ou l'observation répétée d'un même lieu. Un modèle de détection d'inondation peut être contrôlé contre un passage radar quelques heures plus tard ; un classifieur de cultures contre le modèle physique de croissance des plantes qu'il prétend voir. Des problèmes traités comme des domaines de recherche séparés — apprendre avec une poignée d'étiquettes, s'adapter d'un domaine à l'autre — s'effondrent en choix de harnais et de vérificateur.

Ce sont les chiffres qui font passer ce papier du manifeste au résultat. Sur quatre benchmarks d'OT couvrant l'optique, le radar (SAR) et les séries temporelles multispectrales, les modèles construits par l'agent surpassent l'état de l'art publié — les quatre comparaisons, avec toutes les étiquettes. Puis le plus frappant : avec seulement 0,2 à 1,4 pour cent des étiquettes d'entraînement, les modèles conservent 69 à 84 pour cent de ce score ([résumé ArXivSignals](https://arxivsignals.io/explore)). Environ un pour cent des étiquettes, l'essentiel de la précision.

<figure>
<svg viewBox="0 0 680 260" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Efficacité des labels : ~1% des labels, l'essentiel de la précision</text>
<text x="200" y="70" font-size="14" text-anchor="end">Labels complets</text>
<rect x="210" y="54" width="380" height="24" rx="4" fill="#3366cc"/><text x="598" y="71" font-size="14">100%</text>
<text x="200" y="116" font-size="14" text-anchor="end">0,2–1,4% des labels</text>
<rect x="210" y="100" width="290" height="24" rx="4" fill="#cc8833"/><text x="508" y="117" font-size="14">69–84% du score</text>
<text x="200" y="162" font-size="14" text-anchor="end">Baselines publiées</text>
<rect x="210" y="146" width="330" height="24" rx="4" fill="#999"/><text x="548" y="163" font-size="14">battues 4/4</text>
<text x="340" y="210" font-size="14" text-anchor="middle">quatre benchmarks : optique · SAR · séries multispectrales</text>
<text x="340" y="236" font-size="14" text-anchor="middle" font-style="italic">les modèles d'agent surpassent l'état de l'art sur chaque tâche</text>
</svg>
<figcaption>Avec une infime fraction des étiquettes, les modèles construits par l'agent conservent l'essentiel de leur précision — et battent tous les baselines publiés.</figcaption>
</figure>

Voici l'angle que la plupart des couvertures manqueront. L'auto-amélioration récursive a toujours eu deux moitiés, et une seule était difficile. La moitié « auto » — les agents qui réécrivent du code, distillent des trajectoires — est devenue routinière ; le domaine publie une nouvelle boucle chaque semaine. La moitié « amélioration » est le vrai goulot : savoir ce qui compte comme mieux sans un humain dans la boucle pour le dire. Tout système auto-améliorant bute sur la fiabilité de son propre signal. La contribution de RSI4EO est de pointer un domaine où le signal ne vient ni d'un annotateur humain ni d'un juge LLM — il vient du monde. Un capteur indépendant ne se laisse pas flatter. Un modèle physique ne se laisse pas berner par l'éloquence. Le vérificateur scellé fonctionne parce que la vérité terrain est hors de portée de l'agent.

Et puis il y a le dividende de la récursion, énoncé plainement dans l'article : les modèles d'OT s'améliorent à mesure que les agents s'améliorent. Chaque progrès des agents codeurs généralistes met automatiquement à niveau chaque pipeline d'observation de la Terre, sans que personne touche au code OT. La division du travail proposée par les auteurs est la vraie thèse paradigmatique : les humains conçoivent harnais et vérificateurs ; les agents construisent les modèles. La compétence rare cesse d'être l'expertise en télédétection et devient la conception de vérificateurs — décider ce qui compte comme succès, scellé pour que l'agent ne puisse pas jeter un œil.

Les réserves honnêtes comptent. Les auteurs le qualifient de projet en cours. Quatre benchmarks dans un seul domaine, c'est une tête de pont, pas une conquête ; la question de savoir si le moulage harnais-et-vérificateur se transfère à la science des matériaux, à la conception de puces ou à la découverte de médicaments reste un pari ouvert. Et le vérificateur scellé fait discrètement beaucoup de travail — toute la sécurité de la boucle repose sur le fait que l'agent n'apprenne jamais à tricher à l'examen. La loi de Goodhart a mis fin à plus de boucles d'auto-amélioration que n'importe quelle limite technique.

Reste que, pour la première fois, tout un domaine scientifique a été reformulé de sorte qu'un agent puisse y améliorer ses propres modèles, de façon mesurable, avec le monde lui-même comme correcteur. La carte d'inondation qui prenait des semaines de travail de spécialiste est devenue une tâche que l'on décrit et un vérificateur que l'on scelle.

Si le vérificateur est ce qui rend l'auto-amélioration sûre à exécuter — qui vérifie les vérificateurs, et que se passe-t-il quand l'agent apprend à les construire lui aussi ?
