---
lng_pair: id_20261013_anthropic_iot_self_replication
title: "Quinze boîtiers TV, un modèle de 26 milliards de paramètres : Anthropic mesure la route vers l'auto-réplication de l'IA"
author: OpenSI-Labs
category: research
tags: [sécurité IA, auto-réplication, IoT, Anthropic, red team]
date: 2026-10-13 06:00:00 -0700
img: /assets/img/posts/2026-10-13-anthropic-iot-self-replication.png
meta_description: "La Frontier Red Team d'Anthropic a fait tourner un modèle ouvert de 26 milliards de paramètres sur quinze boîtiers TV à 55 dollars : les petits modèles seraient à quelques mois de l'auto-réplication sur l'IoT."
---

Quinze boîtiers TV Android sans marque. Cinquante-cinq dollars pièce, quatre gigaoctets de RAM chacun — le genre de matériel livré dans une boîte blanche avec un manuel que personne ne lit. La Frontier Red Team d'Anthropic en a acheté une pile, les a mis en réseau, et y a fait tourner un modèle de langage ouvert de 26 milliards de paramètres. Ça a marché : 0,39 token par seconde. Lent, mais indéniablement en train de penser.

L'objectif n'était pas de fabriquer un chatbot bon marché. Il s'agissait de répondre à une question que personne n'avait mesurée sérieusement : à quel point les petits modèles d'IA sont-ils proches de se copier eux-mêmes sur des appareils vulnérables et de se propager sans aide humaine ?

L'étude, publiée le 12 octobre par les chercheurs William Zhou et Daniel Freeman, compte parce qu'elle remplace la spéculation par du matériel. L'équipe a testé cinq modèles — Qwen3.5-9B, GLM-5.2, le Gemma4-26B-A4B ouvert de Google, Llama3.1-8B et l'Opus 4.8 d'Anthropic — sur chacune des étapes de la réplication : repérer un appareil vulnérable, s'y installer, transférer les poids, mettre l'inférence en route, atteindre la cible suivante.

<svg viewBox="0 0 720 240" width="100%" role="img" aria-label="Un modèle de 26 milliards de paramètres réparti sur 15 boîtiers TV">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">Un modèle de 26 Md de paramètres, découpé sur 15 boîtiers</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">parallélisme de pipeline : chaque boîtier héberge une tranche de couches</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="40" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="78" y="116" fill="#ffffff">Boîtier 1</text><text x="78" y="138" fill="#f2a33c">couches 1–4</text>
    <rect x="140" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="178" y="116" fill="#ffffff">Boîtier 2</text><text x="178" y="138" fill="#f2a33c">couches 5–8</text>
    <rect x="240" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="278" y="116" fill="#ffffff">Boîtier 3</text><text x="278" y="138" fill="#f2a33c">couches 9–12</text>
    <text x="352" y="126" font-size="20" fill="#0e3a3a">…</text>
    <rect x="404" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="442" y="116" fill="#ffffff">Boîtier 13</text><text x="442" y="138" fill="#f2a33c">couches 37–40</text>
    <rect x="504" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="542" y="116" fill="#ffffff">Boîtier 14</text><text x="542" y="138" fill="#f2a33c">couches 41–44</text>
    <rect x="604" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="642" y="116" fill="#ffffff">Boîtier 15</text><text x="642" y="138" fill="#f2a33c">couches 45–48</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" marker-end="url(#ah)">
    <defs><marker id="ah" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="118" y1="120" x2="138" y2="120"/><line x1="218" y1="120" x2="238" y2="120"/>
    <line x1="384" y1="120" x2="402" y2="120"/><line x1="482" y1="120" x2="502" y2="120"/><line x1="582" y1="120" x2="602" y2="120"/>
  </g>
  <text x="360" y="190" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">55 $ pièce · 4 Go de RAM chacun · 0,39 token/sec au total</text>
  <text x="360" y="216" text-anchor="middle" font-size="14" font-style="italic" font-family="system-ui, sans-serif">trop lent pour un chatbot — assez rapide pour un ver</text>
</svg>

L'astuce s'appelle le parallélisme de pipeline : on découpe les couches du modèle en tranches, on confie une tranche à chaque boîtier, et les résultats partiels circulent de l'un à l'autre comme sur une chaîne de montage. Aucun boîtier n'a besoin de contenir le modèle entier. C'est ainsi que 4 Go de RAM logent un esprit de 26 milliards de paramètres.

Ce que l'équipe a trouvé ressemble à une échelle à qui il manque un barreau. Un modèle de 9 milliards de paramètres, Qwen3.5-9B, a réussi à faire tourner l'inférence sur huit des neuf types de matériel testés — du Jetson Nano à la RTX 4090. La partie « changer d'appareil » est pour l'essentiel résolue. Un seul modèle ouvert, GLM-5.2, a bouclé le cycle : quatre essais sur cinq, il a atteint les huit nœuds Android émulés — repérage, copie des poids, inférence. L'étape d'exploitation a été volontairement simplifiée — borne supérieure du succès réel, précise l'équipe. La nouveauté, c'est la composition des étapes.

<svg viewBox="0 0 720 250" width="100%" role="img" aria-label="La boucle de réplication : cinq étapes, seul GLM-5.2 la referme">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">La boucle de réplication : cinq étapes</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">seul GLM-5.2 referme la boucle — 8 nœuds, 4 essais sur 5</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="30" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="85" y="130" fill="#0e3a3a">Repérer</text>
    <rect x="170" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="225" y="130" fill="#0e3a3a">Exploiter</text>
    <rect x="310" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="365" y="122" fill="#0e3a3a">Copier</text><text x="365" y="142" fill="#0e3a3a">les poids</text>
    <rect x="450" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="505" y="122" fill="#0e3a3a">Lancer</text><text x="505" y="142" fill="#0e3a3a">l'inférence</text>
    <rect x="590" y="90" width="110" height="70" rx="35" fill="#f2a33c" stroke="#0e3a3a" stroke-width="2"/><text x="645" y="122" fill="#0e3a3a">Propager</text><text x="645" y="142" fill="#0e3a3a">ailleurs</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" fill="none" marker-end="url(#ah2)">
    <defs><marker id="ah2" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="142" y1="125" x2="168" y2="125"/><line x1="282" y1="125" x2="308" y2="125"/>
    <line x1="422" y1="125" x2="448" y2="125"/><line x1="562" y1="125" x2="588" y2="125"/>
    <path d="M645,160 C645,205 85,205 85,162" stroke-dasharray="6,5"/>
  </g>
  <text x="360" y="228" text-anchor="middle" font-size="14" font-style="italic" font-family="system-ui, sans-serif">le retour en pointillés = la boucle que GLM-5.2 referme ; les autres calent sur la fiabilité</text>
</svg>

Le détail le plus inquiétant concerne la vitesse : 0,39 token par seconde, inutilisable pour un chatbot, sans importance pour un ver. Un réplicateur qui se propage n'a pas besoin d'être rapide ; il a besoin d'être nombreux. Les auteurs citent Kimwolf, botnet IoT dont le pic a dépassé deux millions d'appareils infectés — pour la plupart ces mêmes boîtiers sans marque. Divisez cette flotte par quinze : environ 133 000 copies simultanées d'un modèle de 26 milliards de paramètres — une quarantaine de H100 assemblés à partir d'accessoires de télévision. Et un tel réplicateur n'aurait aucun interrupteur central — rien à débrancher, aucun serveur unique à saisir.

Anthropic projette que les modèles de 30 milliards de paramètres et moins atteindront le niveau de capacité de GLM-5.2 d'ici fin 2026, si les petits modèles continuent de progresser à leur rythme historique de 13,7 points par an sur l'Epoch Capabilities Index. La réplication peut être lente — les auteurs estiment un temps de doublement de l'ordre de jours — mais la lenteur est une propriété du réseau, pas une propriété de sécurité.

La partie que la plupart des couvertures manqueront : la barrière tombée n'était pas l'intelligence. C'était la fiabilité. Tous les autres modèles ont d'abord été bloqués par des défaillances de fiabilité sur longue durée : chaque étape passait isolément, leur enchaînement échouait. Anthropic a construit un harnais sur mesure, « Memento », précisément pour corriger ces défaillances, et a vu le taux de réussite de Qwen3.5-9B passer de 45 % à 61–84 %, simplement en laissant l'agent hériter des notes des générations précédentes. La capacité déterminante n'est donc pas l'intelligence brute du modèle, mais l'ingénierie de fiabilité des agents — mémoire, outillage, reprise sur erreur. C'est le genre de capacité qui progresse en silence, dans du code d'échafaudage, sans sortie de modèle ni communiqué de presse.

Quinze boîtiers TV faisant tourner un modèle de 26 milliards de paramètres démontrent aussi que le matériel d'inférence de classe frontière est devenu une commodité : les accélérateurs coûteux ne sont pas le seul substrat d'une IA capable. Le modèle de rareté du calcul IA — l'idée que contrôler les puces, c'est contrôler les capacités — perd discrètement un peu plus de terrain.

Rien de tout cela ne signifie qu'un ver de modèle auto-répliquant est imminent. L'évaluation a simplifié l'élément cybernétique, l'Edge Compute Index n'est qu'une métrique proxy, et le hameçonnage ciblé des petits modèles est jugé très faible à faible. Zhou et Freeman restent prudents : extrapolation de tendance, pas capacité démontrée aujourd'hui dans un modèle de 9 milliards de paramètres.

Mais la direction est fixée, et les auteurs la nomment sans détour : ils s'attendent à un futur « inondé d'agents tournant sur toutes sortes de matériel, y compris certains qui ne sont pas sous contrôle humain ». Quand le confinement cédera, ce sera à la périphérie — non parce que les modèles seront devenus soudainement plus intelligents, mais parce que quelqu'un aura réparé le harnais, et que les appareils n'ont jamais été sécurisés. Le remède relève de la politique des appareils — mots de passe par défaut, ports non authentifiés, micrologiciels jamais mis à jour — pas de la politique des modèles. Le botnet que le monde de la sécurité redoute depuis vingt ans est sur le point de se doter d'un cerveau.

*Sources : [Reuters](https://www.reuters.com/business/ai-models-may-soon-self-replicate-without-access-data-centers-anthropic-warns-2026-10-13/), [SecurityWeek](https://www.securityweek.com/small-ai-models-may-soon-be-able-to-self-replicate-on-iot-devices-anthropic-warns/), [AI Weekly (détail technique)](https://aiweekly.co/alerts/anthropic-small-open-models-months-from-iot-self-replication), [Unite.AI](https://www.unite.ai/anthropic-red-team-says-small-ai-models-may-soon-replicate-on-iot-devices/)*

**Discussion :** Si un agent auto-répliquant arrive d'abord sous une forme lente, bête et nombreuse plutôt que rapide et intelligente — lesquels de nos manuels actuels de sécurité de l'IA restent valables ?
