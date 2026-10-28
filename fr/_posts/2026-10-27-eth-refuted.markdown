---
lng_pair: id_20261027_eth-refuted
title: "L'hypothèse ETH a tenu 27 ans. OpenAI et Claude affirment l'avoir réfutée le même jour"
author: OpenSI-Labs
category: research
tags: [complexity theory, ETH, SAT, OpenAI, Anthropic, Claude, Lean, formal verification]
date: 2026-10-27 12:00:00 -0700
img: /assets/img/posts/2026-10-27-eth-refuted.png
meta_description: "Pendant 27 ans, l'informatique théorique a supposé qu'aucun algorithme ne pouvait résoudre 3-SAT en temps sous-exponentiel : c'est l'hypothèse du temps exponentiel, ETH. En octobre 2026, OpenAI et Anthropic ont affirmé indépendamment disposer de tels algorithmes, avec des preuves en Lean que chacun peut revérifier. Ce que dit ETH, ce qui a été affirmé au juste, et ce que cela signifierait — ou non."
---

Le 16 octobre 2026, dans deux laboratoires qui ne se parlaient pas, la même chose s'est produite. Un modèle interne d'OpenAI a produit une preuve selon laquelle l'une des hypothèses porteuses de l'informatique est fausse. Indépendamment, le même jour, un modèle de recherche interne d'Anthropic — Claude — a trouvé essentiellement le même argument. Dix jours plus tard, le 26 octobre, les deux entreprises ont rendu public leurs travaux à quelques heures d'intervalle.

L'hypothèse s'appelle l'hypothèse du temps exponentiel, ETH (Exponential Time Hypothesis). Elle tient depuis 1999, et des centaines d'articles s'appuient sur elle : des résultats de la forme « ce problème exige un temps exponentiel — en supposant ETH ». Si les deux nouvelles preuves tiennent, l'hypothèse est tout simplement fausse, et une génération de résultats conditionnels doit être réexaminée un par un. Si elles ne tiennent pas, l'épisode devient une histoire sur la force de conviction des mathématiques que les machines savent désormais produire, et sur les mois d'expertise qu'il faut pour les départager.

Dans les deux cas, il vaut la peine de comprendre exactement ce qui a été affirmé. L'affirmation est précise, et ses limites sont aussi intéressantes que son contenu. D'abord, donc : qu'est-ce que ETH, en termes simples ?

## Le problème sous tout le reste : 3-SAT

Commençons par un puzzle logique. Vous disposez d'énoncés construits à partir de variables qui valent chacune vrai ou faux — appelons-les x₁, x₂, et ainsi de suite. Les énoncés se présentent en clauses, et chaque clause est un court « ou » de exactement trois variables, éventuellement niées : des choses comme (x₁ ou non-x₂ ou x₇). Une formule de cette forme — un long « et » de clauses « ou » à trois variables — s'appelle une instance de 3-SAT. La question est facile à énoncer : peut-on attribuer vrai ou faux aux variables de sorte que chaque clause, sans exception, soit vraie ?

Le jeu se vérifie sans effort. Si quelqu'un vous tend une attribution, vous pouvez contrôler en quelques instants si elle satisfait toutes les clauses. Le difficile, c'est de la trouver. Avec n variables, il y a 2ⁿ attributions possibles, et la méthode bête — toutes les essayer — coûte 2ⁿ étapes : pour n = 300, c'est plus d'étapes qu'il n'y a d'atomes dans l'univers observable. Toute la question du domaine est de savoir s'il existe quelque chose de fondamentalement plus malin que tout essayer.

En 1971, Stephen Cook et Leonid Levin ont montré que SAT est NP-complet : c'est, en un sens précis, le problème le plus dur de sa catégorie, car tout problème dont les solutions se vérifient rapidement peut être réécrit mécaniquement en une instance de SAT. Voilà pourquoi la force brute a toujours semblé intrinsèque au problème. Et la variante plus dure encore que les deux laboratoires ont attaquée consiste non seulement à décider s'il existe une attribution satisfaisante, mais à les compter toutes — le problème nommé #3-SAT.

## Ce que ETH dit réellement

Voici l'hypothèse, dépliée lentement. Les mathématiciens écrivent « temps sous-exponentiel » sous la forme 2^o(n), et le petit « o » porte tout le sens. Un exposant en o(n) est n'importe quoi qui croît plus lentement que n lui-même — n divisé par √log n, par exemple, ou n / log n, ou √n. Un algorithme qui tourne en temps 2^o(n) reste inimaginablement lent. Mais son exposant rétrécit par rapport à n, et cela le rend qualitativement différent de la force brute, dont l'exposant est n tout entier.

ETH affirme : il n'existe aucun algorithme, jamais, nulle part, qui résolve 3-SAT dans le pire des cas en temps 2^o(n). Ni « personne n'en a trouvé ». Ni « cela semble difficile ». Une affirmation universelle sur tous les algorithmes possibles, y compris ceux auxquels personne n'a encore pensé.

Remarquez à quel point c'est plus fort que la célèbre conjecture P ≠ NP. P ≠ NP n'exclut que le temps polynomial — les algorithmes dont le coût croît comme n² ou n¹⁰. Entre le polynomial et l'exponentiel s'étend un immense terrain intermédiaire, et P ≠ NP n'en dit rien. ETH ferme la porte sur tout le terrain intermédiaire : rien en dessous d'un exponentiel complet, jamais.

Il existe une sœur encore plus stricte, l'hypothèse forte du temps exponentiel (SETH), proposée par les mêmes auteurs. À mesure que l'on élargit les clauses — 4 variables, 5, 6 et au-delà — SETH affirme qu'on ne peut pas battre la force brute, même d'un facteur constant dans l'exposant : aucun algorithme en temps (2 − ε)ⁿ pour aucun ε > 0, à aucune largeur. SETH implique ETH. Toutes deux étaient des conjectures, largement crues, prouvées par personne.

Pourquoi un domaine appuierait-il tant de poids sur une affirmation non prouvée ? Parce que les affirmations de cette forme — « aucun algorithme ne peut faire mieux » — sont les énoncés les plus difficiles de l'informatique. Pour en prouver une, il faut raisonner sur tous les algorithmes qui pourront jamais être écrits, y compris ceux fondés sur des idées que personne n'a encore eues. Le domaine n'y est parvenu que pour une poignée de problèmes, et SAT n'en fait pas partie. Les chercheurs ont donc fait la chose honnête : ils ont nommé l'hypothèse, l'ont datée, et ont tenu un registre public de ce qui en dépendait. ETH n'a jamais été une faiblesse cachée de l'édifice. C'était un mur porteur étiqueté comme tel.

<figure>
<svg width="680" height="380" viewBox="0 0 680 380" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="360" rx="14" fill="#f7f9fc"/>
<text x="340" y="48" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">La course qu'ETH déclarait impossible</text>
<text x="40" y="96" font-size="17" font-weight="700" fill="#1e3a5f">Force brute : tout essayer — 2ⁿ</text>
<rect x="40" y="110" width="600" height="42" rx="8" fill="#1e3a5f"/>
<text x="640" y="138" text-anchor="end" font-size="16" font-weight="700" fill="#ffffff">exposant = n, en entier&#160;</text>
<text x="40" y="196" font-size="17" font-weight="700" fill="#b91c1c">Affirmé en octobre 2026 : exposant = n · (log log n) / √log n</text>
<rect x="40" y="210" width="512" height="42" rx="8" fill="#dc2626"/>
<text x="40" y="282" font-size="16" fill="#374151">Le diviseur √log n croît — lentement, sans limite — donc l'exposant est o(n) :</text>
<text x="40" y="308" font-size="16" fill="#374151">plus petit que n, d'un facteur qui s'élargit sans fin. Toujours astronomique.</text>
<text x="340" y="348" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">ETH interdisait exactement cela : tout exposant plus petit que n lui-même.</text>
</svg>
<figcaption>Figure 1 — Le temps annoncé reste désespérément grand, mais son exposant croît plus lentement que n — et c'est précisément ce qu'ETH excluait.</figcaption>
</figure>

## Vingt-sept ans à construire sur un sol non prouvé

ETH a été écrite en 1999 par Russell Impagliazzo, Ramamohan Paturi et Francis Zane. Ils ne prétendaient rien avoir prouvé ; ils traçaient une ligne de fondation et invitaient le domaine à construire dessus, explicitement, pour que chacun sache quels résultats reposaient sur le roc et lesquels reposaient sur une hypothèse.

Le domaine a construit. En 2001, Impagliazzo, Calabrese et Paturi ont prouvé le lemme de sparsification, un résultat technique aux conséquences sociales : il a rendu ETH transportable. La dureté établie pour 3-SAT pouvait désormais être transférée à des centaines d'autres problèmes. Le mécanisme de transfert, c'est la réduction, l'outil de base de tout le domaine : pour montrer qu'un autre problème est dur, on fournit une traduction mécanique qui transforme toute instance du problème connu pour dur en une instance du vôtre, de sorte qu'un algorithme rapide pour votre problème serait secrètement un algorithme rapide pour l'original. Enchaînez assez de traductions, et une seule hypothèse sur 3-SAT devient une limite de vitesse pour des problèmes qui ne ressemblent en rien à des puzzles logiques.

Un sous-domaine entier — la complexité à grain fin — a grandi autour d'ETH et de SETH, démontrant des énoncés soigneux de la forme « si ETH tient, alors ce problème de théorie des graphes, ou d'algorithmes paramétrés, ou de biologie computationnelle, ou de bases de données, ou de géométrie algorithmique, ne peut pas être résolu plus vite que ceci ». Vingt-sept ans plus tard, l'annonce d'OpenAI elle-même décrit la conjecture comme utilisée dans des centaines d'articles. Chacun de ces articles est conditionnel. C'est la condition qui est aujourd'hui en question.

Belle ironie, en 2010 : Ryan Williams a prouvé que si quelqu'un trouvait un jour un algorithme pour SAT ne serait-ce qu'un peu plus rapide que la force brute, cet algorithme produirait automatiquement des bornes inférieures sur les circuits — des séparations entre classes de complexité que personne ne savait prouver par aucune autre voie. Un algorithme SAT plus rapide était donc un étrange pari gagnant-gagnant : soit ETH était vraie et la barrière réelle, soit elle était fausse et la briser paierait une seconde fois, en une autre monnaie de résultats. La communauté a espéré la percée tout en construisant comme si elle ne viendrait jamais. Williams, l'homme qui a montré ce que vaudrait le fait de briser la barrière, est aujourd'hui l'un des trois experts qui accompagnent l'examen de l'affirmation que la barrière a été brisée.

Pendant ce temps, la pratique vivait une autre vie. Des ingénieurs ont construit des solveurs SAT — les solveurs CDCL et leurs descendants, qui apprennent de chaque impasse rencontrée et élaguent la recherche en conséquence — et l'industrie les a mis au travail pour vérifier des conceptions de puces, contrôler des logiciels et planifier des logistiques. Ces solveurs expédient d'énormes formules réelles en quelques secondes, parce que les formules réelles ont une structure que l'analyse du pire cas ignore. Les solveurs sont devenus plus rapides chaque année. L'hypothèse, qui ne parle que du pire cas, n'a jamais bougé. Pendant des décennies, les deux histoires ont coexisté sans se toucher : la théorie disait que le pire cas était un mur, et la pratique le contournait chaque jour.

## Ce que les deux laboratoires ont réellement produit

Les deux laboratoires ont produit le même type d'objet : un algorithme déterministe qui compte toutes les attributions satisfaisantes d'une formule 3-SAT — le problème #3-SAT, plus dur — en un temps d'environ 2^{O(n log log n / √log n)}. Relisez l'exposant : n, multiplié par un facteur (log log n) et divisé par un facteur (√log n) qui croît. La division l'emporte. L'exposant est n divisé par quelque chose qui croît sans limite, ce qui en fait un o(n) — sous-exponentiel. Ce n'est ni un quasi-résultat, ni un résultat adjacent. C'est un coup direct sur la phrase exacte qu'ETH énonce.

Le choix du comptage rend le coup plus fort encore : un algorithme capable de compter toutes les attributions satisfaisantes peut à coup sûr répondre à la question oui-ou-non (le compte est nul ou il ne l'est pas), donc un algorithme de comptage sous-exponentiel réfute ETH avec de la marge. Il n'y a pas d'échappatoire où « décider » resterait dur pendant que « compter » serait devenu facile.

Le manuscrit d'OpenAI s'intitule « The Exponential Time Hypothesis is False ». Son modèle interne a produit la réfutation le 16 octobre, puis une formalisation en Lean — un langage de preuve dont le résultat peut être vérifié par ordinateur, ligne par ligne — le 17 octobre. L'article et les fichiers Lean sont publics dans le dépôt GitHub openai/math de l'entreprise. Le modèle lui-même n'a pas de nom : c'est un système interne non publié, et le catalogue plus large du dépôt compte 721 manuscrits en 373 familles, dont environ 42 % sont formalisés. OpenAI qualifie ces manuscrits de « données de recherche brutes, plutôt que des articles académiques aboutis », et s'en remet explicitement à la communauté mathématique pour les questions de crédit et d'antériorité.

La version d'Anthropic est arrivée sous la forme d'un article déposé dans la nuit du 26 octobre, à 23 h 07, heure de la côte Est, dans le dépôt de mathématiques formelles de l'entreprise : « A 2^o(n) Time Algorithm for 3-SAT », avec pour seul auteur indiqué, simplement, « Claude (Anthropic) », et une note de bas de page reconnaissant l'affirmation concurrente d'OpenAI. Selon Levent Alpoge, chercheur chez Anthropic, l'algorithme central a été trouvé par un modèle de recherche Claude interne le 16 octobre — le même jour que celui d'OpenAI — au cours d'une session d'environ 14 millions de tokens de sortie, sans aucune intervention humaine dans la découverte elle-même ; les chercheurs d'Anthropic ont ensuite travaillé avec le modèle pour améliorer la présentation. Jelani Nelson, qui a relu la preuve de Claude de manière indépendante, a observé que les deux preuves aboutissent à peu près à la même borne, environ exp(O(n / √log n)), par des techniques étroitement apparentées auxquelles elles sont parvenues indépendamment — le schéma classique en mathématiques, où deux groupes percent le même problème au même moment parce que les outils sont mûrs.

Voici maintenant les conséquences, énoncées aussi précisément que les articles les énoncent. Si les preuves sont correctes, ETH est fausse. SETH tombe avec elle, puisque SETH impliquait ETH. Chaque borne inférieure conditionnelle qui utilisait ETH comme prémisse — en théorie des graphes, en algorithmes paramétrés, en biologie computationnelle, en bases de données, en géométrie algorithmique — perd cette prémisse et doit être revisitée une par une ; rien n'est automatiquement sauvé ni automatiquement détruit, le travail doit être refait honnêtement. Les mêmes idées algorithmiques donnent aussi des méthodes plus rapides pour des problèmes classiques comme l'ensemble indépendant, la clique, la couverture par sommets et l'ensemble dominant.

Et ce que cela ne signifie pas, dans les mots mêmes des laboratoires. Cela ne signifie pas P = NP : les nouveaux algorithmes restent désespérément super-polynomiaux, inutilisables sur toute formule que quiconque rencontrera jamais. L'article d'Anthropic affirme sans détour que le résultat « ne dit rien sur la résolution des formules en pratique », et un résumé de la borne de Claude situe le point de croisement — là où le nouvel algorithme bat enfin la force brute — au-delà de 10^108 variables. L'article d'OpenAI dit que le résultat « ne porte pas directement sur la question P contre NP, et ne produit aucun algorithme pratique ». Les solveurs SAT ne deviendront pas plus rapides cette année à cause de ceci. Ce qui a changé, c'est un sol auquel le domaine a cru pendant 27 ans.

## La même annonce contenait deux autres affirmations

L'annonce d'OpenAI du 26 octobre regroupait trois résultats, et les deux autres méritent un récit compact.

Le deuxième est une preuve de la conjecture de lissage local en toute dimension, au moyen d'une nouvelle équation aux dérivées partielles auxiliaire. Le lissage local, proposé en 1991 par Christopher Sogge, concerne le comportement des ondes lorsqu'elles se concentrent. Le prouver en toute dimension résout aussi, par voie de conséquence, la conjecture de Kakeya et la conjecture de restriction de Stein en toute dimension — deux problèmes ouverts centraux de l'analyse harmonique. Le record humain récent était dur et récent : le lissage local en dimension deux est tombé en 2019 sous Larry Guth, Hong Wang et Ruixiang Zhang, et la conjecture de Kakeya en dimension trois est tombée en 2025 sous Hong Wang et Joshua Zahl. Alexander Iosevich, de l'université de Rochester — l'étudiant de Sogge lui-même — a qualifié la preuve annoncée en toutes dimensions de choquante et de « développement historique ». Comme pour ETH, le manuscrit en langage naturel et la preuve en Lean sont publics, laissés aux chercheurs pour organiser leur propre effort d'explication.

La troisième affirmation est la moins vérifiable aujourd'hui. OpenAI affirme que son modèle a produit une preuve rigoureuse d'existence pour une classe de théories quantiques des champs en interaction, en quatre dimensions, avec champs de jauge et fermions, incluant la chromodynamique quantique, construite sur le cadre constructif de Tadeusz Balaban. Un sous-résultat est l'existence de la théorie de Yang–Mills pure. La précision compte ici : le problème du prix du Millénaire pour Yang–Mills demande l'existence *et* un écart de masse — une preuve que les particules de la théorie ont une masse minimale strictement positive. Une preuve d'existence seule ne résout pas le problème du Millénaire, et personne ne devrait rapporter qu'elle le fait. Fait unique parmi les trois résultats, les matériaux de physique sont retenus : le groupe d'accompagnement, dirigé par le prix Nobel David Gross, détient les artefacts produits par l'IA et entend rédiger le travail lui-même. Ce choix a déjà suscité une opposition publique — un groupe consultatif indépendant sur les mathématiques et l'IA a appelé OpenAI à publier immédiatement les preuves de physique.

## Comment chacun peut vérifier — et ce que la vérification ne peut pas faire

Les deux laboratoires ont publié des formalisations en Lean, et c'est une situation réellement nouvelle pour une affirmation de cette ampleur. Lean est un assistant de preuve : une preuve formelle est un fichier qu'un petit programme de confiance — le noyau — peut vérifier mécaniquement, pas à pas, sans laisser de place au « le reste est évident ». Le dépôt d'Anthropic fixe sa chaîne d'outils (Lean v4.33.1 avec Mathlib), documente une compilation d'environ huit minutes sur 24 processeurs virtuels, et va plus loin : son pipeline d'intégration continue revérifie les preuves avec un second noyau de preuve, écrit indépendamment, et exécute un comparateur pour contrôler que les énoncés Lean correspondent aux théorèmes énoncés dans l'article. Ce second noyau compte plus qu'il n'y paraît : le noyau est le seul composant du système auquel il faut faire confiance au lieu de le vérifier, donc faire réexaminer l'ensemble de la preuve par une implémentation indépendante écarte l'objection « et si le vérificateur lui-même avait un bogue ». Quiconque possède un ordinateur peut, en principe, tout rejouer ce soir.

Mais le README d'Anthropic lui-même contient la phrase qui maintient l'honnêteté de l'ensemble : « Lean vérifie les preuves, mais aucune machine ne vérifie que ce fichier dit ce que l'article dit. » Un noyau peut certifier qu'une preuve formelle découle d'un énoncé formel. Il ne peut pas certifier que l'énoncé formel capture fidèlement le problème dont ETH parle réellement — que l'encodage de « 3-SAT », d'« algorithme » et de « temps de calcul » dans le fichier formel signifie ce que la communauté entend par ces mots. Ce jugement est un travail humain, et c'est exactement le travail en cours.

Les trois résultats d'OpenAI sont chacun accompagnés par un groupe d'experts extérieur, selon des principes énoncés : transparence, aucun crédit académique pour OpenAI, et des groupes travaillant comme bénévoles non rémunérés. Le groupe pour ETH est dirigé par Impagliazzo et Paturi — les hommes qui ont proposé l'hypothèse en 1999 — avec Ryan Williams. Ils ont dit explicitement que leur implication « ne doit pas être prise comme une certification de l'affirmation ». Le théoricien de la complexité Lance Fortnow, qui a écrit le livre de référence sur P contre NP pour le grand public, a qualifié l'approche globale de prometteuse mais non vérifiée. OpenAI a aussi versé 5 millions de dollars à la Fondation Simons pour financer des ateliers et des programmes aidant les chercheurs à digérer les résultats produits par l'IA.

<figure>
<svg width="680" height="400" viewBox="0 0 680 400" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="380" rx="14" fill="#f7f9fc"/>
<text x="340" y="46" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">Vingt-sept ans, une hypothèse</text>
<line x1="50" y1="200" x2="630" y2="200" stroke="#94a3b8" stroke-width="3"/>
<circle cx="70" cy="200" r="9" fill="#1e3a5f"/>
<text x="70" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">1971</text>
<text x="70" y="238" text-anchor="middle" font-size="16" fill="#374151">Cook–Levin :</text>
<text x="70" y="260" text-anchor="middle" font-size="16" fill="#374151">SAT est</text>
<text x="70" y="282" text-anchor="middle" font-size="16" fill="#374151">NP-complet</text>
<circle cx="185" cy="200" r="9" fill="#1e3a5f"/>
<text x="185" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">1999</text>
<text x="185" y="238" text-anchor="middle" font-size="16" fill="#374151">Impagliazzo,</text>
<text x="185" y="260" text-anchor="middle" font-size="16" fill="#374151">Paturi, Zane</text>
<text x="185" y="282" text-anchor="middle" font-size="16" fill="#374151">proposent ETH</text>
<circle cx="300" cy="200" r="9" fill="#1e3a5f"/>
<text x="300" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">2001</text>
<text x="300" y="238" text-anchor="middle" font-size="16" fill="#374151">Lemme de</text>
<text x="300" y="260" text-anchor="middle" font-size="16" fill="#374151">sparsification :</text>
<text x="300" y="282" text-anchor="middle" font-size="16" fill="#374151">ETH partout</text>
<circle cx="415" cy="200" r="9" fill="#1e3a5f"/>
<text x="415" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">2010</text>
<text x="415" y="238" text-anchor="middle" font-size="16" fill="#374151">Williams : un SAT</text>
<text x="415" y="260" text-anchor="middle" font-size="16" fill="#374151">plus rapide donnerait</text>
<text x="415" y="282" text-anchor="middle" font-size="16" fill="#374151">des bornes de circuits</text>
<circle cx="530" cy="200" r="10" fill="#dc2626"/>
<text x="530" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#b91c1c">16 oct. 2026</text>
<text x="530" y="238" text-anchor="middle" font-size="16" fill="#374151">Deux systèmes d'IA,</text>
<text x="530" y="260" text-anchor="middle" font-size="16" fill="#374151">le même jour,</text>
<text x="530" y="282" text-anchor="middle" font-size="16" fill="#374151">indépendamment</text>
<circle cx="615" cy="200" r="9" fill="#b45309"/>
<text x="615" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">Aujourd'hui</text>
<text x="615" y="238" text-anchor="middle" font-size="16" fill="#374151">Relue par</text>
<text x="615" y="260" text-anchor="middle" font-size="16" fill="#374151">ses propres</text>
<text x="615" y="282" text-anchor="middle" font-size="16" fill="#374151">auteurs</text>
<text x="340" y="356" text-anchor="middle" font-size="16" fill="#4b5563">Une conjecture sur laquelle un domaine a marché pendant une génération — en attente du verdict de ceux qui l'ont écrite.</text>
</svg>
<figcaption>Figure 2 — De Cook–Levin au jour où deux systèmes d'IA ont affirmé la même réfutation, et où la relecture est revenue aux auteurs mêmes d'ETH.</figcaption>
</figure>

## Une affirmation, pas un verdict

Voici le bilan honnête, à ce jour. Deux laboratoires respectés affirment que leurs modèles ont réfuté une hypothèse vieille de 27 ans, le même jour, par des voies étroitement apparentées. Tous deux ont publié des preuves vérifiables par machine, ce qui est plus que ce que la plupart des affirmations de percée ont à offrir. Des groupes d'experts dirigés par les auteurs mêmes de l'hypothèse examinent le travail, et n'ont rien certifié. Il n'existe encore aucune confirmation humaine indépendante d'aucune des deux preuves sur ETH, et aucun des deux articles n'a été relu par les pairs.

Ce qu'il faut surveiller est sans glamour et précis : les rapports des groupes d'accompagnement, et la question de savoir si les énoncés formels survivent à une lecture experte en tant que transcriptions fidèles des problèmes qu'ils prétendent régler. S'ils y survivent, le 16 octobre 2026 devient une date dont le domaine se souviendra — le jour où le sol s'est révélé être une conjecture dans le mauvais sens, et où ceux qui l'ont découvert étaient des machines. Sinon, l'épisode marque quand même quelque chose : les systèmes d'IA peuvent désormais produire des preuves candidates assez profondes pour que les trancher soit un projet, et non un après-midi. L'hypothèse a tenu 27 ans. Vérifier si elle est tombée prendra encore un moment — et pour une fois, toutes les personnes impliquées le disent à voix haute.
