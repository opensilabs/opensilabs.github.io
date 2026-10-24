---
lng_pair: id_20261022_recursive-flint
title: "40 milliards de paramètres dans la poche"
author: OpenSI-Labs
category: research
tags: [Recursive, Flint, mixture-of-experts, open weights, local inference]
date: 2026-10-22 06:00:00 -0700
img: /assets/img/posts/2026-10-22-recursive-flint.png
meta_description: "Flint, le modèle de code ouvert de Recursive : 39,8 milliards de paramètres, 2,5 milliards actifs par token, 131 tokens/s sur MacBook Pro — des poids que chacun peut télécharger, des chiffres que chacun peut vérifier."
---

Le 21 octobre, Recursive, la jeune pousse de Richard Socher, a dévoilé sa première création : Flint, un modèle de langage mixture-of-experts de 39,8 milliards de paramètres qui ne mobilise qu'environ 2,5 milliards par token — juste assez pour tourner à [~131 tokens/s](https://teckhustlers.com/recursive-flint-local-coding-model/) sur un MacBook Pro. Les poids sont publiés sous licence Apache 2.0 sur Hugging Face : téléchargeables, utilisables hors ligne, modifiables à des fins commerciales, sans rien payer. Un modèle de code de cette trempe qui tourne sur la machine de son utilisateur — sans cloud, sans abonnement, sans que le code source quitte le disque dur — change la donne bien au-delà du simple exploit technique.

Le mixture-of-experts fonctionne comme l'accueil d'un hôpital : au lieu de soumettre chaque patient à tous les médecins, on oriente chacun vers les quelques spécialistes les plus pertinents. Flint empile 49 couches, dont 47 sont des couches MoE ; chacune abrite 256 experts, et le routeur n'en sollicite que 6 par token, épaulés par un expert partagé toujours actif. Le coût de calcul suit les paramètres activés, non le total — voilà comment une capacité de 40 milliards tient dans un ordinateur portable. Le revers, c'est la mémoire : stocker 256 experts par couche coûte cher, même si on n'en consulte que six. Le tour de force de Flint n'est donc pas seulement architectural, il est logistique — faire tenir cette machinerie dans 23 Go quantifiés.

<figure>
<div style="text-align:center">
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">Routage clairsemé : 256 experts, 6+1 actifs par token</text>
<rect x="30" y="150" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="85" y="181" font-size="14" fill="#fff" text-anchor="middle">Token d'entrée</text>
<rect x="170" y="150" width="110" height="54" rx="8" fill="#6b46c1"/>
<text x="225" y="181" font-size="14" fill="#fff" text-anchor="middle">Routeur</text>
<line x1="140" y1="177" x2="170" y2="177" stroke="#a0aec0" stroke-width="2"/>
<circle cx="330" cy="80" r="9" fill="#4a5568"/>
<circle cx="364" cy="80" r="9" fill="#4a5568"/>
<circle cx="398" cy="80" r="9" fill="#4a5568"/>
<circle cx="432" cy="80" r="9" fill="#4a5568"/>
<circle cx="466" cy="80" r="9" fill="#4a5568"/>
<circle cx="500" cy="80" r="9" fill="#4a5568"/>
<circle cx="534" cy="80" r="9" fill="#4a5568"/>
<circle cx="568" cy="80" r="9" fill="#4a5568"/>
<circle cx="330" cy="114" r="9" fill="#4a5568"/>
<circle cx="364" cy="114" r="9" fill="#4a5568"/>
<circle cx="398" cy="114" r="9" fill="#f6ad55"/>
<circle cx="432" cy="114" r="9" fill="#4a5568"/>
<circle cx="466" cy="114" r="9" fill="#4a5568"/>
<circle cx="500" cy="114" r="9" fill="#4a5568"/>
<circle cx="534" cy="114" r="9" fill="#4a5568"/>
<circle cx="568" cy="114" r="9" fill="#4a5568"/>
<circle cx="330" cy="148" r="9" fill="#4a5568"/>
<circle cx="364" cy="148" r="9" fill="#4a5568"/>
<circle cx="398" cy="148" r="9" fill="#4a5568"/>
<circle cx="432" cy="148" r="9" fill="#4a5568"/>
<circle cx="466" cy="148" r="9" fill="#4a5568"/>
<circle cx="500" cy="148" r="9" fill="#4a5568"/>
<circle cx="534" cy="148" r="9" fill="#f6ad55"/>
<circle cx="568" cy="148" r="9" fill="#4a5568"/>
<circle cx="330" cy="182" r="9" fill="#4a5568"/>
<circle cx="364" cy="182" r="9" fill="#4a5568"/>
<circle cx="398" cy="182" r="9" fill="#4a5568"/>
<circle cx="432" cy="182" r="9" fill="#4a5568"/>
<circle cx="466" cy="182" r="9" fill="#4a5568"/>
<circle cx="500" cy="182" r="9" fill="#f6ad55"/>
<circle cx="534" cy="182" r="9" fill="#4a5568"/>
<circle cx="568" cy="182" r="9" fill="#4a5568"/>
<circle cx="330" cy="216" r="9" fill="#4a5568"/>
<circle cx="364" cy="216" r="9" fill="#4a5568"/>
<circle cx="398" cy="216" r="9" fill="#4a5568"/>
<circle cx="432" cy="216" r="9" fill="#4299e1"/>
<circle cx="466" cy="216" r="9" fill="#4a5568"/>
<circle cx="500" cy="216" r="9" fill="#4a5568"/>
<circle cx="534" cy="216" r="9" fill="#4a5568"/>
<circle cx="568" cy="216" r="9" fill="#4a5568"/>
<circle cx="330" cy="250" r="9" fill="#4a5568"/>
<circle cx="364" cy="250" r="9" fill="#f6ad55"/>
<circle cx="398" cy="250" r="9" fill="#4a5568"/>
<circle cx="432" cy="250" r="9" fill="#4a5568"/>
<circle cx="466" cy="250" r="9" fill="#4a5568"/>
<circle cx="500" cy="250" r="9" fill="#4a5568"/>
<circle cx="534" cy="250" r="9" fill="#4a5568"/>
<circle cx="568" cy="250" r="9" fill="#4a5568"/>
<circle cx="330" cy="284" r="9" fill="#4a5568"/>
<circle cx="364" cy="284" r="9" fill="#4a5568"/>
<circle cx="398" cy="284" r="9" fill="#4a5568"/>
<circle cx="432" cy="284" r="9" fill="#4a5568"/>
<circle cx="466" cy="284" r="9" fill="#4a5568"/>
<circle cx="500" cy="284" r="9" fill="#4a5568"/>
<circle cx="534" cy="284" r="9" fill="#f6ad55"/>
<circle cx="568" cy="284" r="9" fill="#4a5568"/>
<circle cx="330" cy="318" r="9" fill="#4a5568"/>
<circle cx="364" cy="318" r="9" fill="#4a5568"/>
<circle cx="398" cy="318" r="9" fill="#4a5568"/>
<circle cx="432" cy="318" r="9" fill="#f6ad55"/>
<circle cx="466" cy="318" r="9" fill="#4a5568"/>
<circle cx="500" cy="318" r="9" fill="#4a5568"/>
<circle cx="534" cy="318" r="9" fill="#4a5568"/>
<circle cx="568" cy="318" r="9" fill="#4a5568"/>
<line x1="280" y1="177" x2="398" y2="114" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="534" y2="148" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="534" y2="284" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="364" y2="250" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="500" y2="182" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="432" y2="318" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="432" y2="216" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<rect x="610" y="150" width="60" height="54" rx="8" fill="#2f855a"/>
<text x="640" y="181" font-size="14" fill="#fff" text-anchor="middle">→</text>
<text x="330" y="336" font-size="14" text-anchor="middle" fill="#cbd5e0">39,8 Md de paramètres · ~2,5 Md actifs par token</text>
<circle cx="120" cy="300" r="8" fill="#f6ad55"/>
<text x="134" y="305" font-size="14" fill="#cbd5e0">6 routés</text>
<circle cx="300" cy="300" r="8" fill="#4299e1"/>
<text x="314" y="305" font-size="14" fill="#cbd5e0">1 expert partagé</text>
</svg>
</div>
</figure>

Le plus fascinant, c'est la manière dont Flint a été fabriqué. Recursive affirme que son système de recherche automatisée, Eureka Machine, a contribué à « presque tous les aspects » : recherche de la configuration d'experts depuis une base de 35B/3B jusqu'à 40B/2,5B ; une quantification anticonformiste de la couche de sortie en 4 bits ([NVFP4](https://www.marktechpost.com/2026/10/21/recursive-flint-local-coding-model/)), dont la précision a été récupérée par distillation depuis un modèle 16 bits — à 0,7 point près ; et un « megakernel » Metal écrit pour les puces M4 et M5, qui fusionne l'intégralité du décodage en un seul noyau. En moins de quatre mois, une petite équipe entourée d'agents a construit ce modèle de zéro.

La vitesse est l'argument de vente de Flint. Recursive revendique plus de 125 tokens/s sur un MacBook Pro M4 Pro (~131 selon les tests internes cités par la presse), plus de 150 sur une RTX Spark 64 Go, soit environ le double des modèles comparables. La version quantifiée via Ollama ne pèse que 23 Go : tout Mac doté de 48 Go de mémoire unifiée peut la faire tourner. Côté benchmarks, Flint atteint 74,2 % sur SWE-Bench Verified, le meilleur score des MoE de moins de 50 milliards de paramètres ; mais il plafonne à 54,9 % sur Terminal-Bench 2.1, loin derrière le dense Qwen 3.8 (73,0 %). La fenêtre de contexte s'étend à 262 144 tokens, avec 256K comme usage recommandé.

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">Tokens par seconde sur MacBook Pro (M4 Pro)</text>
<text x="200" y="80" font-size="14" text-anchor="end" fill="#e2e8f0">Flint</text>
<rect x="215" y="60" width="332" height="30" rx="4" fill="#f6ad55"/>
<text x="555" y="81" font-size="14" fill="#e2e8f0">131</text>
<text x="200" y="135" font-size="14" text-anchor="end" fill="#e2e8f0">Gemma 4</text>
<rect x="215" y="115" width="175" height="30" rx="4" fill="#718096"/>
<text x="398" y="136" font-size="14" fill="#e2e8f0">69</text>
<text x="200" y="190" font-size="14" text-anchor="end" fill="#e2e8f0">Nemotron 3.5 Lightning</text>
<rect x="215" y="170" width="147" height="30" rx="4" fill="#718096"/>
<text x="370" y="191" font-size="14" fill="#e2e8f0">58</text>
<text x="340" y="278" font-size="14" text-anchor="middle" fill="#a0aec0">Données : tests de Recursive, via TechCrunch</text>
</svg>
</div>
</figure> L'écart entre SWE-Bench et Terminal-Bench en dit long : Flint excelle à générer des correctifs ciblés, mais trébuche sur les tâches longues à outils multiples, là où les modèles denses gardent leur avantage.

Le véritable enjeu se joue autour du mot « vérifiable ». Quand un laboratoire fermé annonce une vitesse, il faut le croire sur parole ; les poids de Flint, eux, sont téléchargeables par tout le monde, et le chiffre de 131 peut être remesuré par quiconque s'offre un M4 Pro — l'ouverture devient ici une discipline de marché. Chaque concurrent devra désormais affronter des chiffres que la communauté peut vérifier elle-même, et non plus des diapositives. Mais [WIRED](https://startupfortune.com/recursive-says-ai-built-most-of-its-new-flint-coding-model/) le rappelle : tous les benchmarks sont auto-déclarés, sans vérification indépendante à ce jour ; Flint n'est qu'un instantané fini, pas la preuve qu'un système de recherche capable de s'auto-améliorer progresse vraiment. Recursive l'admet d'ailleurs : son modèle exige des instructions plus claires que les grands modèles fermés.

Quand 40 milliards de paramètres emménagent pour la première fois dans l'ordinateur qu'on glisse dans un sac, la géographie du pouvoir, en programmation, va-t-elle s'en trouver changée ?

---

*Discussion : quand chaque affirmation de performance peut être remesurée, combien de temps le marketing des benchmarks auto-déclarés peut-il encore survivre ?*
