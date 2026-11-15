---
layout: post
lng_pair: id_20261113_conversation
title: "Pourquoi certaines conversations deviennent-elles de plus en plus prenantes, et d'autres de plus en plus ennuyeuses ?"
author: OpenSI-Labs
category: Society
tags: [conversation, psychologie, Dartmouth, Science Advances, communication, bruit rose]
date: 2026-11-13 06:00:00 -0800
img: /assets/img/posts/2026-11-13-conversation-rhythm.png
---

## Pourquoi certaines conversations prennent, et d'autres non

Tout le monde connaît les deux scènes. Dans l'une, on parle à quelqu'un qu'on vient de rencontrer, et le temps passe sans qu'on s'en aperçoive. Dans l'autre, rien ne cloche vraiment — les phrases sont polies, les réponses correctes — mais au bout de deux minutes, on cherche déjà une porte de sortie.

Qu'est-ce qui sépare les deux ? Pas le sujet, pas forcément l'humour, pas même le fait d'être d'accord. On repart souvent d'une conversation réussie avec une impression claire, mais sans pouvoir dire d'où elle vient. Était-ce un mot juste au bon moment, un silence bien placé, un détour qui a relancé l'échange au lieu de le casser ?

Une étude parue en novembre 2026 dans *Science Advances*, signée Kathryn C. O'Nell, Emily S. Finn et Kiara L. Sanchez, de Dartmouth College, propose une réponse inattendue : ce qui compte, c'est le rythme avec lequel les deux personnes se rapprochent et s'éloignent, au fil des mots (DOI : 10.1126/sciadv.aeb2684). Pour le voir, il fallait arrêter de juger une conversation dans son ensemble et la regarder seconde par seconde, échange après échange.

## Mesurer une conversation, tour après tour

Les chercheuses ont travaillé sur le corpus CANDOR : 1 656 conversations vidéo, libres, entre des personnes qui ne se connaissaient pas. Chacune dure en moyenne 34,1 minutes et compte environ 320 tours de parole.

Pour chaque tour, elles ont mesuré la proximité sémantique entre les deux interlocuteurs. Dit simplement, il s'agit de savoir à quel point ce que dit l'un rejoint, par le sens, ce que vient de dire l'autre. Cette proximité n'est jamais fixe : elle monte, elle descend, elle remonte. Toute la question est de savoir comment elle bouge.

Pour décrire ce mouvement, les auteures empruntent un langage venu de l'étude des signaux : les couleurs du bruit. Un bruit blanc, c'est le grésillement d'une radio mal réglée : chaque instant saute au hasard, sans mémoire de celui d'avant. Un bruit rouge, à l'inverse, bouge à peine : c'est un disque rayé, bloqué presque au même endroit. Entre les deux se trouve le bruit rose. Il a une structure à plusieurs échelles à la fois : il s'éloigne, puis revient, dérive encore, un peu comme une respiration ou le cours d'une rivière.

## Le rythme rose prédit le plaisir de parler

Le résultat central est net. Dans 94 % des conversations, la trajectoire de la proximité sémantique présentait une structure de bruit rose. L'exposant moyen, qui situe chaque conversation sur cette échelle, était de 0,62 — entre le bruit blanc, à 0,5, et le bruit rose pur, à 1,0. Autrement dit, ni chaos, ni immobilité : quelque chose d'organisé, mais de souple.

<figure>
<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Schéma du rythme d'une conversation">
<line x1="60" y1="250" x2="610" y2="250" stroke="#888" stroke-width="1.5"/>
<line x1="60" y1="30" x2="60" y2="250" stroke="#888" stroke-width="1.5"/>
<line x1="60" y1="55" x2="610" y2="55" stroke="#bbb" stroke-width="1.5" stroke-dasharray="6 6"/>
<text x="430" y="45" font-size="14" fill="#777">Toujours d'accord — plat</text>
<path d="M60,180 C110,120 150,90 200,130 C250,170 280,200 330,160 C380,120 420,80 470,110 C520,140 560,180 610,150" fill="none" stroke="#c94f7c" stroke-width="3"/>
<text x="200" y="285" font-size="14" fill="#333">Tours de parole</text>
<text x="10" y="150" font-size="14" fill="#333" transform="rotate(-90 20 150)">Proximité des propos</text>
</svg>
<figcaption>Schéma illustratif, pas les données de l'étude : la proximité monte et descend à plusieurs échelles au lieu de rester plate.</figcaption>
</figure>

Surtout, ce rythme n'était pas qu'une curiosité statistique. Plus le caractère de bruit rose était marqué — ce que les auteures appellent le « pink noise ratio » — plus les participants disaient avoir pris plaisir à la conversation et s'être sentis en lien avec l'autre.

Le point mérite d'être souligné, parce qu'il va contre une intuition tenace. On imagine souvent qu'une conversation réussie est une conversation où l'on se comprend immédiatement et où l'on reste sur la même longueur d'onde du début à la fin. Ici, une trajectoire complètement plate, sans écarts ni retours, n'est pas celle qui ressort. Ce qui ressort, c'est une proximité qui respire.

On peut le lire ainsi, et c'est une interprétation, pas l'affirmation de l'article : une bonne conversation ne serait pas une synchronisation parfaite. Être d'accord du début à la fin, rester collés l'un à l'autre, n'est pas ce qui gagne ici. Ce qui semble compter, c'est un mouvement partagé : se rejoindre, s'écarter un peu, puis se retrouver.

## Deux détails curieux

Ce rythme n'est pas figé chez une personne. Il se renforçait avec la pratique : au fil de l'expérience, la structure de bruit rose devenait plus nette.

Autre détail : quand les chercheuses ont demandé à de grands modèles de langage de générer des conversations agréables, les dialogues obtenus présentaient, eux aussi, un bruit rose plus marqué que les dialogues de référence. On y reviendra dans les limites, car ce point est facile à surinterpréter.

Le phénomène ne tient pas non plus à un seul jeu de données. Il a été retrouvé dans un second ensemble indépendant de conversations, dans des podcasts à deux voix et dans des conversations de type speed dating.

## Ce que l'étude ne dit pas

Les auteures sont claires sur les limites, et il faut l'être aussi. D'abord, il s'agit d'une étude d'observation : les liens sont des corrélations. L'article ne prétend pas que le bruit rose cause le plaisir d'une conversation.

Ensuite, la proximité sémantique n'est qu'un canal parmi d'autres. Le ton de la voix, le contact visuel et le langage corporel n'ont pas été mesurés ici.

Troisième limite : CANDOR, ce sont des inconnus en appel vidéo. On ne sait pas encore si le même rythme vaut pour un dîner entre amis ou en famille, ou pour une réunion de travail.

Enfin, le résultat sur les modèles de langage porte sur des scripts générés. Il ne prouve pas que ces modèles comprennent ce qu'est une conversation.

Reste une idée simple, et assez belle, à garder pour la prochaine fois qu'un échange s'essouffle : peut-être qu'il ne manque pas un sujet, ni même un point d'accord. Peut-être qu'il manque juste un peu de mouvement — s'éloigner, puis se retrouver.

## Références

O'Nell, K. C., Finn, E. S., & Sanchez, K. L. "Pink noise in dyads' semantic similarity trajectories predicts conversation enjoyment." Science Advances (2026). DOI : [10.1126/sciadv.aeb2684](https://doi.org/10.1126/sciadv.aeb2684)
