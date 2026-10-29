---
lng_pair: id_20261028_nemotron-transcribe
title: "Nemotron 3.5 Transcribe : le modèle vocal ouvert de NVIDIA qui n'éveille que 4 milliards de paramètres sur 30"
author: OpenSI-Labs
category: research
tags: [NVIDIA, Nemotron, reconnaissance vocale, ASR, poids ouverts, mélange d'experts, diarisation]
date: 2026-10-28 09:00:00 -0700
img: /assets/img/posts/2026-10-28-nemotron-transcribe.png
meta_description: "Nemotron 3.5 Transcribe de NVIDIA, en poids ouverts, transcrit 40 langues, traduit entre l'anglais et 31 langues, et tient sur une seule puce parce qu'environ 4 milliards seulement de ses 30 milliards de paramètres travaillent sur un audio donné. Les chiffres de tête sont ceux de NVIDIA — et les limites sont bien réelles."
---

Le 28 octobre 2026, NVIDIA a publié Nemotron 3.5 Transcribe, un modèle de parole dont les poids sont téléchargeables et utilisables commercialement. Il transcrit des enregistrements dans 40 langues, traduit entre l'anglais et 31 langues, accepte des fichiers d'une heure et distingue jusqu'à huit locuteurs. Les points de contrôle sont sur Hugging Face et ModelScope, en trois précisions (BF16, FP8, NVFP4) ; le modèle tourne sous vLLM ou NeMo-Speech.cpp, et Baseten, DeepInfra et Simplismart le proposent en service hébergé.

La nouveauté, c'est qu'on peut lui parler. D'ordinaire, la transcription est une machine figée : de l'audio entre, du texte sort. Ici, une consigne en langage clair choisit le style de sortie — une transcription mot à mot qui garde chaque « euh » et chaque faux départ, ou une version nettoyée qui les supprime. On peut lui remettre un vocabulaire à surveiller, des noms de médicaments ou de produits, et lui poser des questions sur le contenu d'un enregistrement. Il fait aussi la diarisation : étiqueter qui parle à quel moment, pour qu'une réunion revienne sous forme de conversation plutôt que de bloc de texte.

## Un modèle de 30 milliards qui dort la plupart du temps

La taille affichée est de 30 milliards de paramètres. La taille qui travaille est bien moindre : c'est un mélange d'experts, un modèle fait de nombreux sous-réseaux spécialistes, dont un routeur n'éveille que quelques-uns pour chaque tranche d'audio ; les autres restent au repos et ne coûtent rien sur ce passage. Environ 4 milliards de paramètres sont actifs à un instant donné. La capacité et le coût d'exécution, d'habitude soudés, se découplent.

Voilà pourquoi une seule puce suffit : une carte robotique Jetson AGX Thor, un ordinateur de bureau DGX Spark ou un GPU Blackwell de centre de données. Artificial Analysis l'a mesuré à égalité avec Voxtral Small de Mistral pour la première place des modèles vocaux ouverts, à 2,8 % sur sa mesure AA-WER — avec environ 4 milliards de paramètres actifs, contre 24 milliards pour Voxtral.

<figure>
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="340" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">30 milliards en réserve, environ 4 milliards au travail</text>
<text x="40" y="98" font-size="15" font-weight="700" fill="#374151">Paramètres totaux : 30 Md</text>
<rect x="40" y="112" width="600" height="46" rx="8" fill="#cbd5e1"/>
<rect x="40" y="112" width="80" height="46" rx="8" fill="#0e7c86"/>
<text x="52" y="142" font-size="17" font-weight="700" fill="#ffffff">~4B</text>
<text x="140" y="142" font-size="15" fill="#374151">actifs par passage : ~4 Md</text>
<text x="640" y="142" text-anchor="end" font-size="15" fill="#374151">au repos : ~26 Md</text>
<text x="40" y="212" font-size="16" fill="#374151">Un routeur éveille quelques sous-réseaux experts par tranche d&#x27;audio ; les autres ne coûtent rien.</text>
<text x="340" y="272" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">Une seule puce suffit : Jetson AGX Thor · DGX Spark · Blackwell</text>
<text x="340" y="316" text-anchor="middle" font-size="26" font-weight="700" fill="#0e7c86">30B &#8594; ~4B</text>
</svg>
<figcaption>Figure 1 — Le mélange d&#x27;experts découple la capacité du coût d&#x27;exécution : le modèle possède 30 milliards de paramètres mais n&#x27;en paie qu&#x27;environ 4 milliards à chaque passage.</figcaption>
</figure>

## Les résultats, avec l'étiquette

L'étalon est le taux d'erreur de mots : la part des mots faux dans une transcription. Plus il est bas, mieux c'est. Selon NVIDIA, au classement anglais du Open ASR Leaderboard de Hugging Face, Nemotron 3.5 Transcribe est premier des modèles ouverts avec 5,33 % de taux d'erreur moyen ; sur le volet multilingue, il affiche 4,62 % en moyenne sur sept langues, le plus bas des modèles ouverts comparés dans sa fiche. Pour l'attribution des locuteurs, NVIDIA annonce un taux d'erreur de diarisation de 18,26 %, le plus faible sur 21 langues au banc d'essai de David AI, qui compte 14 systèmes. Gardez l'attribution accrochée aux chiffres : ce sont ceux de NVIDIA, et personne d'extérieur ne les a encore reproduits.

## Le jeu de données survivra peut-être au modèle

Le même jour est sorti Granary v2, le jeu de données vocal ouvert de NVIDIA : 463 062 heures de parole en 48 langues, issues de 16 corpus (la version 1 couvrait 25 langues). Chaque enregistrement est livré avec trois styles de transcription — mot à mot intégral, formaté (les nombres épelés deviennent des chiffres) et nettoyé. L'audio lui-même n'est pas dans le téléchargement : le jeu de données est un manifeste qui renvoie aux sources d'origine, chacune sous sa propre licence. Les modèles sont remplacés tous les quelques mois. Un demi-million d'heures de parole indexées ouvertement, en 48 langues, c'est une infrastructure sur laquelle d'autres équipes construiront pendant des années.

## Un après-midi pour lui apprendre un métier

Les modèles vocaux trébuchent sur le jargon, et la démonstration de NVIDIA montre la chute puis le remède. Sur le banc d'essai de parole médicale indienne d'Eka Care, le modèle se trompait d'emblée sur un cinquième à un tiers des mots. Une meilleure consigne a nettement réduit les erreurs. Puis un affinage — un entraînement supplémentaire sur des exemples du domaine visé — d'environ 14 heures-GPU sur une seule puce GB300 a fait passer le taux d'erreur, sur des locuteurs jamais entendus, de 22,44 % à 12,17 %, soit environ 45,8 % d'erreurs en moins, devant des systèmes spécialisés. En clair : un hôpital ou un cabinet d'avocats peut apprendre à ce modèle son propre vocabulaire en un après-midi, sur une seule puce.

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">Lui apprendre la parole médicale, en trois étapes</text>
<rect x="40" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#1e3a5f" stroke-width="2"/>
<text x="130" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">Dès la sortie de la boîte</text>
<text x="130" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">22,44 % d&#x27;erreurs de mots</text>
<text x="130" y="208" text-anchor="middle" font-size="14" fill="#374151">sur des locuteurs jamais entendus</text>
<rect x="240" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#0e7c86" stroke-width="2"/>
<text x="330" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">Une meilleure consigne</text>
<text x="330" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#0e7c86">erreurs nettement réduites</text>
<text x="330" y="208" text-anchor="middle" font-size="14" fill="#374151">sans entraînement supplémentaire</text>
<rect x="440" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#b91c1c" stroke-width="2"/>
<text x="530" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">Affinage : ~14 heures-GPU</text>
<text x="530" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#b91c1c">12,17 % d&#x27;erreurs de mots</text>
<text x="530" y="208" text-anchor="middle" font-size="14" fill="#374151">sur une seule puce GB300</text>
<text x="222" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="422" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="340" y="292" text-anchor="middle" font-size="16" font-weight="700" fill="#111827">≈ 45,8 % d&#x27;erreurs en moins — banc d&#x27;essai Eka Care de parole médicale indienne (démo NVIDIA)</text>
</svg>
<figcaption>Figure 2 — Sur une parole médicale chargée de jargon, la consigne aide, et un après-midi d&#x27;affinage sur une puce réduit le taux d&#x27;erreur de presque moitié.</figcaption>
</figure>

## Ce qu'il ne sait pas faire

Il lit des fichiers. Pas de diffusion en direct : les sous-titres en temps réel et les agents vocaux en direct sont hors de portée — et cette moitié du marché vocal a eu un mois chargé sans lui : ElevenLabs a lancé Realtime, Mistral a livré Voxtral 3, Salesforce a publié Launa-Omni. Pour les petits travaux, Parakeet, le modèle maison de 1,1 milliard de paramètres, reste le petit frère.

Ce qui change, c'est la propriété. La transcription devient quelque chose qu'on fait tourner chez soi au lieu de la louer à la minute auprès d'une API — donc l'audio d'un hôpital ou d'une salle de conseil n'a jamais à quitter le bâtiment. C'est précisément pour les enregistrements les plus sensibles, ceux qu'il faut le plus transcrire et qu'on peut le moins envoyer ailleurs, que cela compte.
