---
lng_pair: id_20261024_block-dessa
title: "Le modèle qui a appris à parler sans jamais lire un mot"
author: OpenSI-Labs
category: research
tags: [Block, Dessa, speech-to-speech, full-duplex, voice AI, audio-only training]
date: 2026-10-24 07:00:00 -0700
img: /assets/img/posts/2026-10-24-block-dessa.png
meta_description: "Dessa, de Block, est un modèle vocal full-duplex entraîné de zéro sur le seul audio de conversations humaines — sans texte, sans socle préentraîné. Les démos impressionnent ; pour l'instant, ce ne sont que des démos."
---

Le 23 octobre, Block, l'entreprise de Jack Dorsey, a dévoilé Dessa, un modèle vocal dont la promesse sonne comme une hérésie après dix ans d'IA entraînée sur du texte : il a appris à converser sans jamais lire un seul mot. Aucun corpus de texte, aucun modèle préentraîné en dessous — seulement des enregistrements de gens qui parlent, depuis zéro. Block le présente comme « le modèle vocal full-duplex le plus authentique jamais construit » ; son directeur de recherche, Ragavan Thurairatnam, y voit un possible [« moment GPT-3 pour la parole »](https://panews.io/articles/01a16adb-b868-71d2-9020-e852cb11f62c).

Pour comprendre l'enjeu, partons du fonctionnement des assistants vocaux actuels. Vous parlez ; un transcripteur convertit votre parole en texte ; un modèle de langage rédige une réponse ; un synthétiseur la lit à voix haute. C'est une course de relais à trois passages de témoin, et chaque passage jette quelque chose. La transcription garde les mots mais perd l'hésitation qui les précède, le rire qui les traverse, l'intonation qui transforme une affirmation en question, le sarcasme qui en inverse le sens. Elle impose aussi un tour de parole bureaucratique : le système attend que vous ayez fini pour commencer, et la conversation ressemble à un échange de talkie-walkie.

Dessa condense le relais en un seul coureur. L'audio entre, l'audio sort, sans aucune étape de transcription — un « vrai modèle parole-à-parole », selon [la description de Block elle-même](https://aicoder.com/news/news-20261024-block-dessa-full-duplex-speech-model-trained-only-on-speech). Et il est full-duplex : il écoute pendant qu'il parle, comme nous. Interruptible en pleine phrase, il glisse les petits signaux d'écoute — « oui », « je vois », un rire discret — qui montrent qu'il suit. Formé sur de vraies conversations plutôt que sur des scripts, il saurait, dit Block, quand intervenir et quand se taire. Les démos de Block le montrent riant en pleine phrase, retrouvant un titre de film oublié, ou accueillant un voyage surprise à Paris avec une gratitude émue. Dans l'une d'elles, face au modèle vocal GPT-Live-1 d'OpenAI, il passe pour le plus naturel des deux.

<figure>
<div style="text-align:center">
<svg width="680" height="340" viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">La course de relais ou le coureur solitaire</text>
<text x="170" y="58" font-size="14" font-weight="bold" text-anchor="middle">Aujourd'hui : parole → texte → parole</text>
<rect x="20" y="80" width="90" height="54" rx="8" fill="#2b6cb0"/>
<text x="65" y="111" font-size="14" fill="#fff" text-anchor="middle">Votre voix</text>
<rect x="135" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="180" y="111" font-size="14" fill="#fff" text-anchor="middle">Transcription</text>
<rect x="250" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="295" y="111" font-size="14" fill="#fff" text-anchor="middle">LLM texte</text>
<rect x="140" y="160" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="185" y="191" font-size="14" fill="#fff" text-anchor="middle">Voix émise</text>
<text x="170" y="240" font-size="14" fill="#c53030" text-anchor="middle">Ton, rythme, rires : perdus à chaque étape</text>
<text x="510" y="58" font-size="14" font-weight="bold" text-anchor="middle">Dessa : audio en entrée, audio en sortie</text>
<rect x="400" y="80" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="455" y="111" font-size="14" fill="#fff" text-anchor="middle">Votre voix</text>
<rect x="535" y="80" width="110" height="54" rx="8" fill="#276749"/>
<text x="590" y="111" font-size="14" fill="#fff" text-anchor="middle">Dessa</text>
<rect x="455" y="160" width="110" height="54" rx="8" fill="#276749"/>
<text x="510" y="191" font-size="14" fill="#fff" text-anchor="middle">Réponse parlée</text>
<text x="510" y="240" font-size="14" fill="#276749" text-anchor="middle">Écoute en parlant : interruptible</text>
<line x1="110" y1="107" x2="135" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="225" y1="107" x2="250" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="295" y1="134" x2="230" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="535" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="590" y1="134" x2="510" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="510" y2="160" stroke="#a0aec0" stroke-width="2" stroke-dasharray="5,4"/>
</svg>
</div>
<figcaption style="text-align:center">À gauche, les assistants actuels aplatissent la parole en texte puis en parole, perdant tout ce qui n'est pas un mot. À droite, Dessa garde le signal entier dans un seul modèle — et continue d'écouter en parlant.</figcaption>
</figure>

La promesse la plus profonde ne porte pas sur la qualité vocale, mais sur ce dont la compétence langagière est faite. Depuis des années, le domaine suppose que les corpus de texte sont l'échafaudage indispensable : les modèles apprennent la langue en lisant Internet, la parole n'étant qu'un manteau ajouté après coup. Dessa conteste frontalement cette hypothèse. Block affirme qu'il a appris la langue avec [« des centaines de fois moins de mots »](https://www.aichatdaily.com/ai-models/block-unveils-dessa-full-duplex-voice-model-trained-only) que les LLM textuels : une minute de conversation porte bien plus d'information que sa transcription — rythme, emphase, émotion, chorégraphie sociale de qui parle quand. Un enfant apprend à parler des années avant de lire ; l'équipe a voulu vérifier si un modèle en était capable. Même efficacité côté calcul : l'entraînement a tourné sur un seul rack NVIDIA GB200 NVL72 — un rack, pas un parc de centres de données — et l'inférence dépasse le temps réel en local sur un MacBook Pro M4 Max ou mieux, sans aller-retour vers le cloud.

Block présente aussi ce travail comme de la recherche sur la sécurité, pas comme un simple produit. L'IA vocale actuelle, argue l'équipe, est presque sourde aux émotions : elle ne perçoit pas la détresse dans une voix, et ne peut donc pas y répondre. Ses motivations affichées : « la curiosité (autrement dit, le plaisir), une meilleure compréhension entre humains et IA, et la sécurité ». L'accès anticipé revient d'abord à un petit groupe de chercheurs en sécurité de l'IA : un modèle qui a appris à parler à partir du seul son est, selon Block, un territoire nouveau dont les risques ne sont pas encore cartographiés. Une liste d'attente publique est ouverte, mais il n'y a ni date de sortie, ni API, ni prix.

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Ce qu'une transcription jette</text>
<text x="340" y="58" font-size="14" text-anchor="middle">Mêmes mots, sens différents — portés par le son seul</text>
<rect x="40" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="130" y="108" font-size="14" text-anchor="middle">« Vraiment ? » — neutre</text>
<text x="130" y="130" font-size="14" text-anchor="middle">Une question</text>
<rect x="250" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="340" y="108" font-size="14" text-anchor="middle">« Vraiment ?! » — montant</text>
<text x="340" y="130" font-size="14" text-anchor="middle">Incrédulité, joie</text>
<rect x="460" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="550" y="108" font-size="14" text-anchor="middle">« Vraiment. » — sec</text>
<text x="550" y="130" font-size="14" text-anchor="middle">Sarcasme</text>
<text x="340" y="185" font-size="14" text-anchor="middle">Et aussi : pauses, rires, soupirs, interruptions, signaux d'écoute —</text>
<text x="340" y="210" font-size="14" text-anchor="middle">la couche sociale de la conversation, que le texte ne consigne jamais.</text>
<text x="340" y="250" font-size="14" font-weight="bold" text-anchor="middle">Dessa s'entraîne sur le son lui-même : rien de tout cela n'est écarté.</text>
</svg>
</div>
<figcaption style="text-align:center">Une transcription consigne des mots. Une conversation fonctionne sur tout ce qui les entoure — exactement ce qu'un modèle entraîné sur l'audio seul peut apprendre.</figcaption>
</figure>

Venons-en au bilan d'honnêteté, qui compte ici plus que d'habitude. Tout ce qui, ci-dessus, sonne impressionnant repose pour l'instant sur la parole de Block et ses propres démos. Aucun nombre de paramètres, aucune taille de jeu de données, aucun chiffre de latence, aucun benchmark formel n'a été publié. « Aucun texte du tout » est la description que Block donne de son entraînement, pas un fait vérifié indépendamment. Et les démos elles-mêmes ne sont pas irréprochables : [The Verge](https://dealroom.co/news/165548-jack-dorseys-block-unveils-dessa-a-full-duplex-voice-ai-trained-only-on/) les a trouvées le plus souvent naturelles, parfois maladroites — Dessa y prend son interlocuteur pour un certain « Ronaldo ». Une démo est une performance que son auteur a choisi de vous montrer ; ce n'est pas une évaluation. Lisez donc Dessa aujourd'hui comme une preuve d'existence assortie d'un astérisque : il semble possible d'aller aussi loin avec la seule parole — reste à le vérifier indépendamment.

Cet astérisque est aussi l'angle neuf. Si la promesse de Dessa résiste à l'examen, l'économie des données bascule. Les corpus de texte sont finis, contestés en justice et de plus en plus coûteux ; la conversation humaine est abondante, renouvelable et pour l'essentiel intranscrite. Un modèle qui apprend du son pourrait progresser à partir de sources inaccessibles aux modèles textuels — appels, réunions, histoires du soir, tout échange parlé qui ne devient jamais un document. Et si elle ne résiste pas — si « aucun texte » veut dire « un peu de texte, discrètement » — la correction sera instructive : elle révélera où se situe réellement la frontière de l'apprentissage par la seule parole. Dans tous les cas, Dessa impose la question que le domaine évitait : quelle part de la langue tient dans les mots, et quelle part dans la voix ?

*Discussion : si un modèle peut apprendre une langue à partir du seul son, en quoi consiste réellement « connaître une langue » — les mots, ou tout ce qui les entoure ?*
