---
lng_pair: id_20261026_cnn-skin-cancer
title: "Les modèles multimodaux les plus puissants ont deviné, le CNN a regardé : comment un CNN vieux de dix ans a gagné au diagnostic du cancer de la peau"
author: OpenSI-Labs
category: research
tags: [IA médicale, vision par ordinateur, Inception v3, LLM multimodaux, dermatologie, évaluation]
date: 2026-10-26 00:05:00 -0700
img: /assets/img/posts/2026-10-26-cnn-skin-cancer.png
meta_description: "Sur 200 lésions cutanées confirmées par biopsie, un CNN de 2015 affiné en vingt minutes a nommé le bon diagnostic dans 62,5 % des cas ; GPT-6 Astra et Claude Fable 5.1 plafonnent à 42 %. L'histoire plus profonde est celle de leur échec — réponses favorites, prose confiante déconnectée du regard, et un paradoxe de la sortie qui tient à un seul seuil."
---

La lésion était un mélanome invasif sur l'oreille d'un patient, épais de moins de 0,8 millimètre — assez mince pour être guéri s'il est pris à temps, mortel s'il passe entre les mailles. Devant sa photographie clinique et son image dermoscopique, GPT-6 Astra a parlé de kératose séborrhéique, une excroissance bénigne, et déclaré le patient libre de rentrer chez lui. Claude Fable 5.1 a dit la même chose. Un réseau convolutif publié par Google en 2015, affiné en une vingtaine de minutes sur des données publiques, a dit : mélanome.

Ce réseau n'aurait pas dû gagner. Le 25 octobre, le Dr Magnus Lynch — dermatologue consultant et chirurgien de Mohs au Guy's Hospital de Londres, maître de conférences honoraire au King's College London — a publié [un test qu'il a mené lui-même](https://lynchlab.net/llm-skin-cancer), avec l'ensemble des invites, des réponses des modèles et du code de notation [mis à disposition de quiconque veut le rejouer](https://d2gaqzonlm544h.cloudfront.net/skin-ai/data/llm-skin-cancer-test.zip). Sa question était étroite et clinique : à partir des deux photographies avec lesquelles un dermatologue travaille réellement, les modèles d'IA les plus capables d'octobre 2026 peuvent-ils nommer ce qu'est une lésion cutanée ? Sa réponse fait le tour de la communauté des chercheurs depuis deux jours : les modèles de pointe n'ont pas simplement perdu, ils ont perdu de vingt points face à une architecture assez vieille pour figurer dans les manuels — et leur manière de perdre révèle quelque chose d'inconfortable sur ce que font les modèles généralistes lorsqu'ils ont l'air de regarder une image.

## Un test conçu pour être difficile

Les 200 lésions proviennent de MILK10k, un jeu de données public publié en 2025 par l'International Skin Imaging Collaboration. Chacune a été confirmée par histopathologie : la vérité de terrain, c'est le diagnostic du tissu, pas l'opinion d'un autre médecin. Cent lésions ne devaient en aucun cas être renvoyées : 30 mélanomes, 25 carcinomes basocellulaires, 25 carcinomes épidermoïdes et 20 kératoses actiniques. Les cent autres pouvaient sortir sans risque : 50 grains de beauté bénins et 50 kératoses séborrhéiques. Chaque lésion venait avec deux images — un gros plan clinique et une vue au dermatoscope polarisé, l'image agrandie des motifs pigmentaires sous la surface que les dermatologues apprennent à lire.

Surtout, chaque lésion, y compris les bénignes, avait suffisamment inquiété un clinicien pour être biopsiée : pas des cas d'école, mais le résidu difficile — des grains de beauté qui avaient l'air dangereux et des cancers qui avaient l'air innocents.

Les deux modèles de langage ont été utilisés comme un clinicien le ferait : les deux images, le diagnostic le plus probable parmi six (ou « incertain »), un niveau de confiance, un deuxième choix, et un jugement sur la possibilité de renvoyer la lésion sans traitement, ni biopsie, ni suivi. Réglages par défaut, un passage par cas, aucun refus.

Le CNN, Inception v3, était délibérément sans glamour — une référence, précise Lynch, pas l'état de l'art. Pré-entraîné sur des photographies ordinaires, il a été affiné, toutes couches comprises, sur 68 011 images dermoscopiques et cliniques des [archives ISIC](https://www.isic-archive.com), sur un seul GPU H100, en une vingtaine de minutes. L'hygiène était stricte : les 200 lésions du test, et toute autre photographie des mêmes lésions ou des mêmes patients, avaient été retirées de ses données d'entraînement et de validation avant l'affinage. Le modèle final est un fichier de 44 mégaoctets qui tourne entièrement dans le navigateur d'un téléphone grâce à WebGPU ; rien n'est téléversé nulle part.

## Soixante-deux contre quarante-deux

Le chiffre principal mérite d'être énoncé simplement. Nommer le bon diagnostic en premier, parmi six : le CNN a réussi 125 cas sur 200 — 62,5 %. Claude Fable 5.1 en a réussi 85 (42,5 %) ; GPT-6 Astra, 84 (42,0 %). Accordez à chacun son deuxième choix et l'écart demeure : 173 contre 138 et 134.

Le motif sous les totaux est plus accablant que les totaux eux-mêmes. Sur les mélanomes — le diagnostic où une erreur peut tuer — le CNN en a nommé 13 sur 30 en premier ; les LLM, 11 et 8. Sur les lésions inoffensives qui remplissent les vraies consultations, le CNN a reconnu 37 grains de beauté sur 50 et 26 kératoses sur 50 ; Astra, 16 et 13 ; Fable, 33 et seulement 6. Les géants n'étaient pas uniformément un peu moins bons : ils étaient les plus mauvais exactement là où se concentrent le volume et le danger — distinguer un cancer d'un grain de beauté qui lui ressemble.

<figure>
<div style="text-align:center">
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="21" font-weight="bold" text-anchor="middle">Nommer le diagnostic : premier choix et deux premiers choix</text>
<text x="340" y="56" font-size="16" text-anchor="middle" fill="#4a5568">Part des 200 lésions confirmées par biopsie correctement nommées (%)</text>
<rect x="150" y="70" width="18" height="14" fill="#2b6cb0"/><text x="174" y="83" font-size="16">Premier choix</text>
<rect x="380" y="70" width="18" height="14" fill="#90cdf4"/><text x="404" y="83" font-size="16">Dans les deux premiers choix</text>
<text x="205" y="128" font-size="17" font-weight="bold" text-anchor="end">Inception v3 (2015)</text>
<rect x="215" y="108" width="275" height="24" fill="#2b6cb0"/>
<text x="500" y="127" font-size="20" font-weight="bold">62.5</text>
<rect x="215" y="138" width="381" height="24" fill="#90cdf4"/>
<text x="606" y="157" font-size="20" font-weight="bold">86.5</text>
<text x="205" y="202" font-size="17" font-weight="bold" text-anchor="end">Claude Fable 5.1</text>
<rect x="215" y="182" width="187" height="24" fill="#4a5568"/>
<text x="412" y="201" font-size="20" font-weight="bold">42.5</text>
<rect x="215" y="212" width="304" height="24" fill="#a0aec0"/>
<text x="529" y="231" font-size="20" font-weight="bold">69</text>
<text x="205" y="276" font-size="17" font-weight="bold" text-anchor="end">GPT-6 Astra</text>
<rect x="215" y="256" width="185" height="24" fill="#718096"/>
<text x="410" y="275" font-size="20" font-weight="bold">42</text>
<rect x="215" y="286" width="295" height="24" fill="#cbd5e0"/>
<text x="520" y="305" font-size="20" font-weight="bold">67</text>
</svg>
</div>
<figcaption style="text-align:center">L'ancien réseau a nommé le bon diagnostic dans 62,5 % des cas ; les deux modèles de pointe plafonnent à 42 %.</figcaption>
</figure>

## Comment les géants ont échoué : réponses favorites et cécité éloquente

Chaque modèle de langage avait une réponse favorite, à laquelle il revenait sans cesse. En auditant les sorties brutes, [une analyse forensique des données publiées par Lynch](https://duklee.net/blog/2026-10-25-cnn-outperforms-frontier-llms-skin-cancer-diagnosis-deep-dive/) a établi que GPT-6 Astra a qualifié 75 des 200 lésions de carcinome basocellulaire — trois fois le nombre réel de 25 — dont 14 des 30 mélanomes. Son sans-faute sur les vrais carcinomes est un artefact de sur-diagnostic : quand un tiers de tout reçoit la même étiquette, on n'en manque aucun, mais deux appels sur trois sont faux. Claude Fable 5.1 présentait le travers symétrique : 53 lésions qualifiées de kératose actinique contre 20 en réalité, et 16 des 25 carcinomes épidermoïdes — de vrais cancers — rangés sous cette étiquette précancéreuse. C'est un effondrement de mode en blouse blanche : dans l'incertitude, le modèle ne diversifie pas ses paris ; il se replie sur la réponse que son entraînement a rendue la plus dicible.

La confiance a aggravé le tableau. L'un des mélanomes de l'ensemble n'a presque pas de pigment — le genre que les cliniciens redoutent. Astra l'a nommé carcinome basocellulaire avec 95 % de confiance. Les deux LLM ont regardé le mélanome de l'oreille, l'ont décrit, et l'ont renvoyé chez lui. Cet échec porte un nom dans l'analyse : le découplage verbal-visuel. Un modèle multimodal de pointe n'examine pas une image comme le fait le CNN. L'image est découpée en patchs, tokenisée, et remise à un moteur de langage dont le talent natif est de produire du texte plausible. Ces modèles ont lu tous les manuels de dermatologie ; ils récitent le vocabulaire de la dermoscopie — réseaux pigmentaires, vaisseaux arborescents, voiles blanc-bleuté — avec une aisance parfaite. Mais l'aisance n'est pas la perception. Trop souvent, la description est générée parce qu'elle est le genre de chose que l'on dit de telles lésions, et non parce que le motif correspondant, large de quelques dizaines de micromètres, a réellement été résolu dans les pixels. Le CNN, lui, n'a aucun vocabulaire. Affiné de bout en bout, ses filtres sont réglés précisément sur ces motifs spatiaux sous la surface, et rien d'autre ne dispute son attention. Il ne peut pas s'expliquer. Il ne peut que regarder.

Lynch a aussi rejoué la rencontre hors de la clinique : dans la peau d'un patient inquiet, avec la seule photographie clinique, demandant « dois-je voir un médecin ? ». En diagnostic pur, la performance s'effondre — environ 24 à 26 % de réussite au premier choix — et sur 100 mélanomes supplémentaires confirmés par biopsie, Fable n'a placé le mélanome en premier que 3 fois, a dit à 14 patients qu'un rendez-vous de routine suffirait, et à un patient atteint d'un mélanome invasif qu'on pouvait laisser cela tranquille. Les modèles conseillaient presque toujours de consulter ; ce qu'ils ne savaient pas faire, c'était dire pourquoi.

## Le paradoxe de la sortie : le chiffre que personne n'a cité

Voici la partie du tableau de Lynch qui complique tous les gros titres triomphants — y compris le sien. Le diagnostic n'est que la moitié de la tâche clinique ; l'autre moitié est le triage : garder, ou renvoyer chez soi ?

À son seuil préréglé — le point de fonctionnement choisi sur les données de validation — le CNN vainqueur a gardé 77 des 100 lésions dangereuses et renvoyé 76 des 100 lésions inoffensives. Équilibré, semble-t-il, jusqu'à la ligne des mélanomes : il en aurait renvoyé 18 sur 30 chez eux. Les deux LLM, malgré leur médiocrité diagnostique, n'ont renvoyé que 3 et 4 mélanomes — parce qu'ils gardaient presque tout, ne laissant partir que 32 et 22 des 100 lésions inoffensives. Leur « sécurité » est celle d'une alarme incendie qui sonne pour un toast : une sensibilité achetée en refusant de jamais dire « tout va bien », au prix de cabinets inondés de bien-portants inquiets. Aucun des deux extrêmes n'est un médecin.

La résolution du paradoxe est le point technique le plus profond de l'étude, et il favorise à nouveau la vieille architecture. Un classifieur produit un score continu, et l'endroit où l'on place le seuil est un choix — un bouton. Faites glisser celui du CNN le long de sa courbe ROC (aire sous la courbe : 0,86 sur cet ensemble délibérément difficile, 0,96 sur les images d'archives ordinaires) jusqu'à égaler la prudence des LLM, et il garde 98 ou 99 des 100 lésions dangereuses en ne renvoyant qu'1 ou 2 mélanomes — mieux que chaque géant, des deux côtés du bilan. Les LLM n'offrent aucun bouton : leur point de fonctionnement est enfoui dans la prose, fixé par les habitudes de leur entraînement — moitié manuel scolaire, moitié instinct de couverture juridique — et le clinicien ne peut ni l'inspecter, ni l'auditer, ni le déplacer.

<figure>
<div style="text-align:center">
<svg width="680" height="470" viewBox="0 0 680 470" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="21" font-weight="bold" text-anchor="middle">Le paradoxe de la sortie : la sécurité dépend du seuil</text>
<text x="40" y="72" font-size="18" font-weight="bold">Lésions bénignes renvoyées chez elles (sur 100)</text>
<text x="290" y="109" font-size="16" text-anchor="end">CNN, seuil préréglé</text>
<rect x="300" y="88" width="274" height="24" fill="#2b6cb0"/>
<text x="584" y="108" font-size="20" font-weight="bold">76</text>
<text x="290" y="143" font-size="16" text-anchor="end">GPT-6 Astra</text>
<rect x="300" y="122" width="115" height="24" fill="#718096"/>
<text x="425" y="142" font-size="20" font-weight="bold">32</text>
<text x="290" y="177" font-size="16" text-anchor="end">Claude Fable 5.1</text>
<rect x="300" y="156" width="79" height="24" fill="#4a5568"/>
<text x="389" y="176" font-size="20" font-weight="bold">22</text>
<text x="40" y="218" font-size="18" font-weight="bold">Mélanomes renvoyés à tort (sur 30)</text>
<text x="290" y="257" font-size="16" text-anchor="end">CNN, seuil préréglé</text>
<rect x="300" y="236" width="216" height="24" fill="#c53030"/>
<text x="526" y="256" font-size="20" font-weight="bold">18</text>
<text x="290" y="291" font-size="16" text-anchor="end">CNN, seuil aligné sur les LLM</text>
<rect x="300" y="270" width="24" height="24" fill="#2b6cb0"/>
<text x="334" y="290" font-size="20" font-weight="bold">1–2</text>
<text x="290" y="325" font-size="16" text-anchor="end">GPT-6 Astra</text>
<rect x="300" y="304" width="36" height="24" fill="#718096"/>
<text x="346" y="324" font-size="20" font-weight="bold">3</text>
<text x="290" y="359" font-size="16" text-anchor="end">Claude Fable 5.1</text>
<rect x="300" y="338" width="48" height="24" fill="#4a5568"/>
<text x="358" y="358" font-size="20" font-weight="bold">4</text>
</svg>
</div>
<figcaption style="text-align:center">À son réglage d'usine, le CNN renvoie 18 mélanomes chez eux. Alignez son seuil sur la prudence des LLM et il n'en renvoie que 1 à 2 — tout en retenant 98 à 99 des 100 lésions dangereuses.</figcaption>
</figure>

## Pourquoi l'adéquation a battu l'échelle

Avec du recul, le résultat est moins mystérieux qu'il n'y paraît. Cette tâche est un ensemble fermé de six réponses sur une distribution visuelle étroite et apprenable — exactement la forme de problème pour laquelle un classifieur spécialiste est construit. Le biais inductif du CNN est ici un atout : des filtres invariants par translation, entraînés sur le seul domaine cible, chaque paramètre au service de la discrimination qui compte. Sa distribution d'entraînement *est* sa distribution de test. Les généralistes apportent un milliard de faits sur tout ; le spécialiste, 68 011 exemples d'une seule chose.

L'économie le souligne. L'éducation du CNN a coûté vingt minutes sur un GPU loué ; il tourne ensuite gratuitement, hors ligne, dans un navigateur, à coût marginal nul — la peau d'aucun patient n'est téléversée sur le nuage de qui que ce soit. La facture d'API du test des géants se compte en quelques dollars américains chacun ; le vrai coût de la voie généraliste est la dépendance — un modèle distant, versionné, mis à jour en silence, dont on ne peut ni geler le comportement, ni régler le seuil, ni auditer les décisions.

## Ce que ce test ne démontre pas

Être honnête sur les limites sépare cette petite étude d'un coup de communication, et Lynch énonce lui-même la plupart d'entre elles. D'abord : c'est le test autopublié d'un seul clinicien, pas une science relue par les pairs. Deux cents lésions montrent un motif ; elles ne classent pas finement des systèmes, trente mélanomes portent une large incertitude, et chaque cas de LLM n'a été joué qu'une fois — redemandez, et certaines réponses changent. Ensuite : le CNN jouait à domicile — jamais exposé aux lésions du test ni à leurs patients, mais grandi dans les mêmes archives, avec les mêmes appareils, la même culture diagnostique ; les LLM ont été parachutés dans une spécialité, à froid. Troisièmement : les géants ont été testés en un seul passage, aux réglages par défaut, sans outils, sans possibilité de recadrer ou reconsidérer — aucun déploiement clinique sérieux ne les utiliserait ainsi, et un agent bâti autour d'eux ferait sûrement mieux. Quatrièmement — et cela vise le vainqueur — rien ici ne fait du CNN un dispositif médical : à son seuil préréglé, il aurait renvoyé 18 mélanomes chez eux, et les ensembles modernes comme les produits régulés font considérablement mieux que sa référence délibérément datée. Aucun de ces trois systèmes ne devrait renvoyer qui que ce soit chez soi.

Une réserve pointe dans l'autre sens : MILK10k est public depuis 2025, donc les LLM l'ont peut-être absorbé à l'entraînement — une contamination qui les aurait aidés, eux, pas le CNN. Et une transparence à copier : Lynch signale que son analyse et ses premiers brouillons ont été produits avec Claude Code, l'outil d'Anthropic — le fabricant de l'un des modèles perdants. Il a publié les données quand même.

## La leçon porte sur les instruments

La lecture confortable de cette histoire est « le petit bat le grand », et elle est fausse. Le CNN n'a surpassé personne en raisonnement ; il a surpassé en adéquation, sur une tâche dont la forme récompense l'adéquation. La lecture inconfortable porte sur ce que nous mesurons. Nos évaluations vedettes notent les modèles sur le nommage — des questions d'examen avec corrigé — alors que le travail réel, en médecine et bien au-delà, fonctionne sur des points de fonctionnement : scores calibrés, seuils explicites, coûts d'erreur asymétriques. Au test de nommage, les géants ont marqué 42 %. Au test de triage, leur prudence était un effet secondaire ininspectable de leur style de prose. Un système qui ne peut pas vous montrer son seuil vous demande d'être cru sur son ton de voix.

L'avenir probable n'est ni le géant ni l'antiquité, mais une division du travail : le généraliste comme porte d'entrée conversationnelle — recueillir l'histoire, expliquer, escalader — câblé à des instruments étroits qui font le regard, chacun avec un bouton réglable par un professionnel et un score auditable par un régulateur. Vingt minutes d'affinage viennent de démontrer, preuves à l'appui, à quel point la moitié « instrument » de cet avenir est déjà bonne.

Alors voici la question que ce test laisse sur la table : quand un modèle ne peut pas vous montrer son seuil — seulement sa confiance — que vaut exactement son « cela a l'air bénin » ?
