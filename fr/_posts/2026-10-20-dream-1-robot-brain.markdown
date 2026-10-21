---
lng_pair: id_20261020_dream1-robot-brain
title: "Un cerveau de robot à 3 dollars de l'heure"
author: OpenSI-Labs
category: robotics
tags: [robotique, modèles de fondation, modèles du monde, API robotique, Dream Labs]
date: 2026-10-20 03:30:00 -0700
img: /assets/img/posts/2026-10-20-dream-1-robot-brain.png
meta_description: "Dream-1 de Dream Labs transforme la vidéo humaine en cerveau de robot à louer : 3 dollars de l'heure, zéro-shot sur des robots inédits — un pari sur la distribution plutôt que sur l'échelle."
---

Avec trois dollars, on achète une bouteille d'eau. Depuis le 19 octobre 2026, on peut aussi louer l'heure d'un cerveau de robot.

Dream Labs est sortie de sa clandestinité en annonçant 90 millions de dollars de seed (B Capital, Kindred Ventures) et surtout Dream API : la première interface publique pour un modèle de fondation robotique. Vous envoyez le flux d'une caméra et une instruction en langage naturel (« range les chaussettes bleues »), l'API renvoie les commandes moteurs — sur des robots que le modèle n'a jamais vus, sans aucun entraînement préalable.

Fondateurs : Joel Jang (ex-NVIDIA, équipe des modèles du monde du GEAR Lab, projet GR00T) et You Liang Tan.

## Le mécanisme : apprendre en regardant les humains

Dream-1 est un « World Action Model ». Les cerveaux actuels apprennent sur des démonstrations téléopérées d'un matériel précis ; Dream-1 s'est entraîné sur des vidéos humaines à la première personne — mains qui plient du linge, emballent des cartons. Il prédit la suite de la scène et en déduit l'action. Comme la connaissance vient d'observer des humains et non de mémoriser une machine, les compétences se transfèrent d'un matériel à l'autre.

Le modèle prédit la position cible des pinces, que le solveur de cinématique inverse du robot convertit en commandes articulaires : tout robot à deux bras et pinces parallèles est contrôlable dès sa sortie de boîte, zéro-shot.

Antécédent : DreamZero (février 2026, 14 milliards de paramètres) s'adaptait à un robot inédit avec trente minutes de « jeu » libre. Dream-1 en est la mise en production.

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Schéma du pipeline Dream-1 : de la vidéo humaine à la commande du robot">
  <rect x="0" y="0" width="720" height="400" fill="#faf7f0" rx="12"/>
  <text x="360" y="32" text-anchor="middle" font-size="19" font-weight="bold" fill="#1a1a2e">Le pipeline de Dream-1</text>
  <g>
    <rect x="20" y="70" width="130" height="200" fill="#e8f0fe" stroke="#4a6fa5" stroke-width="2" rx="8"/>
    <text x="85" y="95" text-anchor="middle" font-size="15" font-weight="bold" fill="#1a1a2e">Vidéo humaine</text>
    <rect x="35" y="110" width="100" height="60" fill="#4a6fa5" rx="4"/>
    <rect x="35" y="180" width="100" height="60" fill="#6a8fc5" rx="4"/>
    <circle cx="85" cy="140" r="14" fill="#f5d0a9"/>
    <circle cx="85" cy="210" r="14" fill="#f5d0a9"/>
    <text x="85" y="262" text-anchor="middle" font-size="14" fill="#333">plie du linge,</text>
    <text x="85" y="280" text-anchor="middle" font-size="14" fill="#333">emballe, range…</text>
  </g>
  <path d="M150 170 L205 170" stroke="#888" stroke-width="3" marker-end="url(#arr)"/>
  <defs><marker id="arr" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6" fill="#888"/></marker></defs>
  <g>
    <rect x="205" y="70" width="160" height="200" fill="#f3e8fd" stroke="#7b4fa5" stroke-width="2" rx="8"/>
    <text x="285" y="95" text-anchor="middle" font-size="15" font-weight="bold" fill="#1a1a2e">Modèle du monde</text>
    <rect x="225" y="115" width="120" height="70" fill="#7b4fa5" opacity="0.7" rx="6"/>
    <text x="285" y="145" text-anchor="middle" font-size="14" fill="#fff">prédit l'image</text>
    <text x="285" y="165" text-anchor="middle" font-size="14" fill="#fff">suivante</text>
    <text x="285" y="225" text-anchor="middle" font-size="14" fill="#333">…puis en déduit</text>
    <text x="285" y="243" text-anchor="middle" font-size="14" fill="#333">l'action à faire</text>
  </g>
  <path d="M365 170 L420 170" stroke="#888" stroke-width="3" marker-end="url(#arr)"/>
  <g>
    <rect x="420" y="70" width="130" height="200" fill="#e8f5e9" stroke="#3d8b40" stroke-width="2" rx="8"/>
    <text x="485" y="95" text-anchor="middle" font-size="15" font-weight="bold" fill="#1a1a2e">Pose cible</text>
    <circle cx="485" cy="150" r="30" fill="none" stroke="#3d8b40" stroke-width="3" stroke-dasharray="6,4"/>
    <line x1="485" y1="150" x2="520" y2="120" stroke="#3d8b40" stroke-width="4"/>
    <text x="485" y="215" text-anchor="middle" font-size="14" fill="#333">position visée</text>
    <text x="485" y="233" text-anchor="middle" font-size="14" fill="#333">des pinces</text>
    <text x="485" y="262" text-anchor="middle" font-size="14" fill="#333">aucune donnée</text>
    <text x="485" y="280" text-anchor="middle" font-size="14" fill="#333">spécifique au robot</text>
  </g>
  <path d="M550 170 L605 170" stroke="#888" stroke-width="3" marker-end="url(#arr)"/>
  <g>
    <rect x="605" y="70" width="100" height="200" fill="#fff3e0" stroke="#c77800" stroke-width="2" rx="8"/>
    <text x="655" y="95" text-anchor="middle" font-size="15" font-weight="bold" fill="#1a1a2e">Robot</text>
    <text x="655" y="140" text-anchor="middle" font-size="14" fill="#333">cinématique</text>
    <text x="655" y="158" text-anchor="middle" font-size="14" fill="#333">inverse</text>
    <line x1="655" y1="190" x2="655" y2="230" stroke="#c77800" stroke-width="8"/>
    <circle cx="655" cy="240" r="10" fill="#c77800"/>
    <text x="655" y="280" text-anchor="middle" font-size="14" fill="#333">commandes</text>
    <text x="655" y="298" text-anchor="middle" font-size="14" fill="#333">articulaires</text>
  </g>
  <text x="360" y="330" text-anchor="middle" font-size="15" font-style="italic" fill="#555">La connaissance vient des humains ; le robot, quel qu'il soit, n'a rien à apprendre.</text>
  <text x="360" y="356" text-anchor="middle" font-size="15" font-style="italic" fill="#555">Aucune démonstration téléopérée sur ce matériel n'est nécessaire.</text>
</svg>
Figure 1 — De la vidéo humaine à la commande : le modèle prédit l'image suivante, en déduit la position cible des pinces, et le robot convertit cette consigne en mouvements. La compétence est découplée du corps.

## Les preuves : vingt-sept robots inédits, dont un vieux de dix-huit ans

En simulation, Dream-1 a contrôlé zéro-shot vingt-sept robots inédits — dont le PR2, vieux de dix-huit ans. Le découplage cerveau-corps devient tangible. Jang résume : « Quand vous montez dans une voiture de location, vous ne réapprenez pas à conduire… Dream-1 aborde un nouveau robot de la même manière. »

Côté évaluation, Robocurve : 59 contre 48 sur RoboDojo-RC niveau 1, à un coût par tentative seize fois inférieur à Gemini 4 Argon — chiffres cités par l'entreprise.

Tarifs publics : 3 dollars de l'heure pour Dream-1, 2 pour Dream-1-flash. Chaque appel d'API renvoie 1,6 seconde d'actions, soit environ 2 250 appels par heure — à peu près 0,0013 dollar l'action. Ryan Chan, directeur général de MakerMods (bras bimanuels à 2 000 dollars) : son robot, « branché sur Dream-1, a été opérationnel en quelques minutes et tentait des tâches que nous n'avions jamais programmées ». Daisy Cai (B Capital) : « Un bras robotique capable est passé du prix d'une voiture de luxe à celui d'un ordinateur portable haut de gamme. Ce qu'il lui faut maintenant, c'est de l'intelligence. »

## Pourquoi ça compte : le goulet des données robotiques

Le vrai problème de la robotique n'est pas le matériel — déjà bon marché — mais l'apprentissage : enseigner une tâche exige des spécialistes et des mois de démonstrations, tout à recommencer à chaque nouveau matériel.

Dream Labs attaque ce goulet : la vidéo humaine est pratiquement infinie et gratuite. Si le transfert tient, l'économie s'inverse — le matériel devient marchandise, l'intelligence ressource partagée.

Et le pari se distingue : les rivaux misent sur l'échelle (Physical Intelligence : 600 millions à 5,6 milliards ; Skild AI : 1,4 milliard ; Generalist : 400 + 200 millions). Dream Labs, avec 90 millions, mise sur la distribution : API au compteur, fine-tuning en quelques heures, « Robot Playground » public à San Francisco. L'intelligence devient une utilité mesurée, comme Stripe ou AWS. Le fabricant n'a plus besoin d'équipe ML.

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Comparaison : l'ancienne approche un robot un cerveau contre l'approche Dream-1 un cerveau plusieurs corps">
  <rect x="0" y="0" width="720" height="400" fill="#faf7f0" rx="12"/>
  <line x1="360" y1="55" x2="360" y2="380" stroke="#bbb" stroke-width="2" stroke-dasharray="8,6"/>
  <text x="180" y="32" text-anchor="middle" font-size="18" font-weight="bold" fill="#8b3a2e">Avant : un robot, un cerveau</text>
  <g>
    <rect x="60" y="70" width="100" height="110" fill="#e0e0e0" stroke="#8b3a2e" stroke-width="2" rx="8"/>
    <circle cx="110" cy="110" r="18" fill="#c4a49c"/>
    <rect x="95" y="135" width="30" height="30" fill="#c4a49c"/>
    <rect x="45" y="75" width="30" height="20" fill="#8b3a2e" opacity="0.5"/>
    <text x="110" y="205" text-anchor="middle" font-size="14" fill="#333">petit cerveau</text>
    <text x="110" y="223" text-anchor="middle" font-size="14" fill="#333">sur mesure</text>
  </g>
  <g>
    <rect x="200" y="70" width="100" height="110" fill="#e0e0e0" stroke="#8b3a2e" stroke-width="2" rx="8"/>
    <circle cx="250" cy="110" r="18" fill="#a9b8c4"/>
    <rect x="235" y="135" width="30" height="30" fill="#a9b8c4"/>
    <rect x="185" y="75" width="30" height="20" fill="#8b3a2e" opacity="0.5"/>
    <text x="250" y="205" text-anchor="middle" font-size="14" fill="#333">autre cerveau</text>
    <text x="250" y="223" text-anchor="middle" font-size="14" fill="#333">sur mesure</text>
  </g>
  <text x="180" y="265" text-anchor="middle" font-size="14" fill="#333">mois de formation</text>
  <text x="180" y="283" text-anchor="middle" font-size="14" fill="#333">par des spécialistes</text>
  <text x="180" y="310" text-anchor="middle" font-size="14" font-weight="bold" fill="#8b3a2e">nouveau matériel</text>
  <text x="180" y="328" text-anchor="middle" font-size="14" font-weight="bold" fill="#8b3a2e">= tout recommencer</text>
  <text x="540" y="32" text-anchor="middle" font-size="18" font-weight="bold" fill="#2e6b3a">Dream-1 : un cerveau, des corps</text>
  <g>
    <ellipse cx="540" cy="120" rx="48" ry="38" fill="#d9f2dd" stroke="#2e6b3a" stroke-width="3"/>
    <circle cx="525" cy="115" r="6" fill="#2e6b3a"/>
    <circle cx="555" cy="115" r="6" fill="#2e6b3a"/>
    <path d="M525 132 Q540 142 555 132" stroke="#2e6b3a" stroke-width="3" fill="none"/>
    <path d="M505 145 L470 190 M575 145 L610 190 M540 158 L540 205" stroke="#2e6b3a" stroke-width="2"/>
    <rect x="448" y="190" width="44" height="60" fill="#c4a49c" stroke="#555" stroke-width="2" rx="6"/>
    <rect x="608" y="190" width="44" height="60" fill="#a9b8c4" stroke="#555" stroke-width="2" rx="6"/>
    <rect x="518" y="205" width="44" height="60" fill="#d9c4a9" stroke="#555" stroke-width="2" rx="6"/>
    <text x="540" y="70" text-anchor="middle" font-size="14" fill="#333">cerveau partagé</text>
  </g>
  <text x="540" y="295" text-anchor="middle" font-size="14" fill="#333">27 robots inédits</text>
  <text x="540" y="313" text-anchor="middle" font-size="14" fill="#333">contrôlés zéro-shot en sim</text>
  <text x="540" y="331" text-anchor="middle" font-size="14" fill="#333">dont le PR2, vieux de 18 ans</text>
  <text x="540" y="360" text-anchor="middle" font-size="15" font-weight="bold" fill="#2e6b3a">3 $/heure, au compteur</text>
</svg>
Figure 2 — L'ancien monde (chaque robot réclame son cerveau dressé à la main) contre le pari de Dream Labs (un seul cerveau loué au compteur, branché sur n'importe quel corps).

## Les réserves, honnêtement

Cartes sur table : c'est une bêta de recherche, « il fera des erreurs », non validée pour un usage critique. Périmètre étroit : deux bras, pinces parallèles, tâches de table. Bases roulantes et mains dextres : feuille de route, pas produit. Le financement ira surtout au calcul. Et les chiffres Robocurve sont cités par l'entreprise.

Mais le signal est clair : la robotique sort de son âge artisanal — la question n'est plus qui construit le meilleur robot, mais qui contrôle l'intelligence qu'il emprunte.

Alors, une question pour finir : quand le cerveau d'un robot se loue à l'heure, la valeur de la machine réside-t-elle dans ses mains ou dans l'esprit qu'elle emprunte — et qui répond des erreurs de cet esprit loué ?
