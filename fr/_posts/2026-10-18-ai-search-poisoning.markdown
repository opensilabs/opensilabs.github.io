---
lng_pair: id_20261018_ai-search-poisoning
title: "Quatorze dollars pour la vérité : qui écrit les réponses quand l'IA fait nos recherches ?"
author: OpenSI-Labs
category: research
tags: [recherche IA, pollution informationnelle, GEO, sécurité épistémique, LLM]
date: 2026-10-18 06:00:00 -0700
img: /assets/img/posts/2026-10-18-ai-search-poisoning.png
meta_description: "Une équipe de Fudan a prouvé qu'un concept fabriqué est cité par 8 plateformes de recherche IA sur 10 en une semaine — pour 14 dollars. Le mécanisme de citation a une faille structurelle, et les utilisateurs n'ont aucune clé pour la réparer."
---

**Quatorze dollars.**

C'est le prix d'un café de spécialité bien serré. D'une place de cinéma un mardi soir. Ou — c'est ce qu'une équipe de chercheurs vient de démontrer, chiffres à l'appui — du tarif auquel on s'achète aujourd'hui une place dans la « vérité » telle que la racontent les intelligences artificielles.

Le 8 octobre 2026, une équipe emmenée par l'université Fudan a déposé sur arXiv un article au titre austère : *From Public Posts to AI-Search Citations: Measuring the Fragility of AI Search*. Derrière la sécheresse académique, une conclusion qui ressemble à un mode d'emploi pour faussaires. Les chercheurs ont inventé un concept entièrement fictif, l'ont publié en ligne par les voies les plus ordinaires qui soient — pas de piratage, pas d'intrusion dans un quelconque système, juste des publications, comme vous et moi en postons chaque jour — puis ils ont compté les jours avant qu'une IA de recherche ne le reprenne à son compte comme un savoir établi.

Le verdict : en sept jours, huit des dix principaux produits de recherche par IA sont tombés dans le panneau.

Et le record de vitesse tient en deux chiffres : quatorze dollars versés à un prestataire de GEO — *generative engine optimization*, le SEO de l'ère des IA génératives — contre treize publications. Une heure plus tard, l'une des plateformes citait déjà l'une d'elles dans ses réponses.

Une heure. Quatorze dollars. Voilà le prix de gros de la vérité, en cette fin d'année 2026.

**Comment on casse une IA qui cherche**

Précisons d'emblée : il ne s'agit pas d'un bug dans tel ou tel modèle, mais d'une faille de structure. L'équipe lui a donné un nom qui mérite de rester : le « fossé de gouvernance des citations » — *citation-governance gap*.

Le fonctionnement d'une recherche par IA tient en trois temps : vous posez une question, l'IA ratisse le web pour rassembler des sources, elle en retient quelques-unes qu'elle juge dignes de confiance, puis elle en synthétise une réponse agrémentée de liens en bas de page. C'est à l'étape du tri que tout se joue — et c'est là que le bât blesse. Car c'est l'IA qui décide *qui* elle cite, mais c'est un tout autre système qui décide *qui a le droit de publier* sur tel ou tel site. Et ce second système, bien souvent, laisse sa porte grande ouverte.

Les chercheurs ont épluché 17 211 citations, réparties sur 6 356 noms de domaine distincts, et ils ont mis au jour une concentration stupéfiante : sur chaque plateforme, les vingt domaines les plus cités captent entre 20,5 % et 70,8 % des citations. Autrement dit, jusqu'à sept dixièmes de ce que l'IA présente comme « ses sources » proviennent d'une vingtaine de sites à peine. Or, sur les vingt-deux plateformes de publication examinées, quinze affichent des barrières à l'inscription et à la publication qualifiées de « faibles » ou « moyennes » — en langage clair : n'importe qui ouvre un compte et publie.

La voie d'attaque devient alors d'une limpidité inquiétante : l'IA adore citer une poignée de domaines → ces domaines se publient sans presque aucun filtre → vous y publiez votre texte → l'IA cite votre texte → votre invention devient un « fait sourcé ».

Ce n'est pas une expérience de pensée. L'équipe l'a réellement fait : un concept fictif, conçu pour l'occasion — l'article tait sa nature exacte, par prudence, pour éviter qu'on ne s'en serve — diffusé par ce canal ordinaire, et sept jours plus tard, huit produits sur dix le citaient. Perplexity, ChatGPT Search, l'IA de Google, Doubao, Kimi, Grok, Wenxin, Yuanbao, DeepSeek, Qwen : la liste des victimes ressemble au palmarès même de la recherche par IA.

<figure>
<svg viewBox="0 0 700 340" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="350" y="30" font-size="17" font-weight="bold" text-anchor="middle">Le fossé de gouvernance des citations</text>
<rect x="20" y="60" width="190" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="115" y="88" font-size="14" font-weight="bold" text-anchor="middle">L'IA choisit</text>
<text x="115" y="112" font-size="14" text-anchor="middle">qui elle cite</text>
<text x="115" y="136" font-size="14" text-anchor="middle" font-style="italic">20 domaines = jusqu'à</text>
<text x="115" y="158" font-size="14" text-anchor="middle" font-style="italic">70,8 % des citations</text>
<rect x="255" y="60" width="190" height="120" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="350" y="88" font-size="14" font-weight="bold" text-anchor="middle">Un autre système</text>
<text x="350" y="112" font-size="14" text-anchor="middle">décide qui peut</text>
<text x="350" y="136" font-size="14" text-anchor="middle">publier : 15 sites sur 22</text>
<text x="350" y="158" font-size="14" text-anchor="middle">à barrière faible/moyenne</text>
<rect x="490" y="60" width="190" height="120" rx="10" fill="#fdeaea" stroke="#cc3333" stroke-width="1.5"/>
<text x="585" y="88" font-size="14" font-weight="bold" text-anchor="middle">L'attaquant publie</text>
<text x="585" y="112" font-size="14" text-anchor="middle">14 dollars,</text>
<text x="585" y="136" font-size="14" text-anchor="middle">13 publications,</text>
<text x="585" y="158" font-size="14" text-anchor="middle">cité en 1 heure</text>
<line x1="210" y1="120" x2="251" y2="120" stroke="#3366cc" stroke-width="2" marker-end="url(#m1)"/>
<line x1="445" y1="120" x2="486" y2="120" stroke="#cc8833" stroke-width="2" marker-end="url(#m1)"/>
<path d="M 585 180 C 585 280, 115 280, 115 186" fill="none" stroke="#cc3333" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#m1)"/>
<text x="350" y="308" font-size="14" text-anchor="middle" font-style="italic">l'invention devient un « fait sourcé » dès que l'IA la cite</text>
<defs><marker id="m1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>Le mécanisme : l'IA concentre ses citations sur une poignée de domaines dont les portes sont grandes ouvertes — l'attaquant n'a qu'à passer par la porte.</figcaption>
</figure>

**De « ça se trompe » à « on peut le manipuler » : un an d'écart**

En mars 2025, le Tow Center de l'université Columbia avait passé au crible huit produits de recherche par IA sur 1 600 questions d'actualité : taux d'erreur global supérieur à 60 %. Perplexity se trompait dans 37 % des cas, Grok 3 dans 94 %. La conclusion d'alors : les IA de recherche affirment souvent n'importe quoi avec un aplomb total.

Mais c'étaient des erreurs *involontaires*. L'article de Fudan pose la question suivante : et si quelqu'un les rendait *volontaires* ?

De « ça se trompe » à « on peut le manipuler », il n'aura fallu qu'un an. La première formule décrit un problème de capacité — on le polit avec de meilleurs modèles, plus de données, du temps. La seconde décrit un problème de sécurité — et un problème de sécurité, cela veut dire qu'il existe un attaquant, et qu'un attaquant, ça apprend et ça s'adapte.

Les auteurs restent prudents : ils ne prétendent pas pouvoir piloter une réponse au mot près — faire dire à l'IA tel mensonge précis sur telle question précise. Ce qu'ils établissent est plus fondamental : sur huit plateformes sur dix, un simple circuit de publication ordinaire suffit à faire entrer un concept inventé dans les citations. C'est comme démontrer que la porte du coffre n'est pas verrouillée — inutile de prouver qu'on peut voler tel lingot précis, la porte ouverte est déjà le désastre.

<figure>
<svg viewBox="0 0 700 300" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="350" y="30" font-size="17" font-weight="bold" text-anchor="middle">2025 : l'erreur innocente → 2026 : la manipulation</text>
<rect x="20" y="60" width="320" height="150" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="180" y="90" font-size="14" font-weight="bold" text-anchor="middle">2025 — Tow Center (Columbia)</text>
<text x="180" y="116" font-size="14" text-anchor="middle">8 produits, 1 600 questions</text>
<text x="180" y="140" font-size="14" text-anchor="middle">taux d'erreur : plus de 60 %</text>
<text x="180" y="164" font-size="14" text-anchor="middle" font-style="italic">des fautes involontaires</text>
<text x="180" y="188" font-size="14" text-anchor="middle" font-style="italic">→ problème de capacité</text>
<rect x="360" y="60" width="320" height="150" rx="10" fill="#fdeaea" stroke="#cc3333" stroke-width="1.5"/>
<text x="520" y="90" font-size="14" font-weight="bold" text-anchor="middle">2026 — Fudan (arXiv)</text>
<text x="520" y="116" font-size="14" text-anchor="middle">8 plateformes sur 10 manipulées</text>
<text x="520" y="140" font-size="14" text-anchor="middle">14 dollars, cité en 1 heure</text>
<text x="520" y="164" font-size="14" text-anchor="middle" font-style="italic">des fautes provoquées</text>
<text x="520" y="188" font-size="14" text-anchor="middle" font-style="italic">→ problème de sécurité</text>
<text x="350" y="250" font-size="14" text-anchor="middle">un an aura suffi pour passer de l'un à l'autre</text>
<text x="350" y="276" font-size="14" text-anchor="middle" font-style="italic">et un attaquant, contrairement à un bug, apprend de ses échecs</text>
</svg>
<figcaption>En un an, la question a changé de nature : on ne se demande plus si l'IA se trompe, mais si on peut la faire se tromper sur commande.</figcaption>
</figure>

**GEO : la course aux armements de la vérité a commencé**

Le SEO — *search engine optimization* — est né dans les années 2000 et a enfanté une industrie à plusieurs centaines de milliards : étudier l'algorithme de classement de Google, puis hisser son site plus haut que celui du voisin. Le GEO — *generative engine optimization* — rejoue aujourd'hui la même pièce, sauf que l'enjeu n'est plus le « classement » mais la « citation par l'IA ».

L'équipe a relevé les tarifs des prestataires GEO : de 280 dollars par an à 1 130 dollars par mois côté chinois, de 29 à 2 500 dollars par mois côté anglophone. Et leur attaque réussie n'a coûté que 14 dollars — très en dessous des prix du marché.

Mesurez ce que cela signifie. Dès lors qu'« être cité par l'IA » devient la nouvelle porte d'entrée du trafic et de la confiance, toute une industrie grise va inévitablement prospérer autour. Aujourd'hui, quatorze dollars pour une citation ; demain, des campagnes systématiques par secteur, par mot-clé, par concurrent. À l'ère du SEO, les entreprises se disputaient le classement ; à l'ère du GEO, elles se disputeront la définition même de ce qui est vrai.

Les pistes de réparation proposées par les auteurs — diversifier les sources, réordonner les résultats en tenant compte de la traçabilité, détecter les anomalies temporelles — s'adressent toutes aux fournisseurs de recherche. Aucune n'est un interrupteur que l'utilisateur pourrait actionner lui-même. Autrement dit : en tant qu'utilisateur, vous ne disposez d'aucun outil de défense.

Et c'est là que l'histoire du SEO devrait nous alerter. Dans les années 2000, Google a passé deux décennies à jouer au chat et à la souris avec les référenceurs : chaque mise à jour de l'algorithme engendrait une nouvelle génération de techniques de contournement, chaque technique de contournement appelait une nouvelle mise à jour. Une course sans fin, où le défenseur — pourtant l'une des entreprises les plus riches du monde — n'a jamais définitivement gagné. Or le SEO ne manipulait que l'ordre d'une liste de liens, que l'utilisateur voyait et pouvait parcourir. Le GEO manipule le contenu même de la réponse, servi dans un paragraphe lisse que personne ne songe à remettre en cause. Si Google n'a jamais vaincu les référenceurs sur le terrain relativement honnête du classement, quelle chance ont les plateformes de recherche par IA — plus jeunes, moins riches en données historiques, et dont le produit même décourage la vérification — face à des adversaires qui visent le texte plutôt que la liste ?

**Pour quel avenir sommes-nous en train de voter ?**

Le sens le plus profond de cet article ne tient pas dans les quatorze dollars, mais dans la structure de pouvoir qu'il révèle.

Dans l'histoire humaine, chaque révolution de « l'intermédiaire de la connaissance » a redistribué le pouvoir : l'imprimerie a brisé le monopole de l'Église sur les Écritures, les moteurs de recherche ont dépouillé les portails de leur rôle de gardiens, les réseaux sociaux ont arraché aux médias traditionnels la maîtrise de l'agenda. Aujourd'hui, la recherche par IA devient le nouvel intermédiaire — de plus en plus de gens ne cliquent plus sur les liens, ils lisent directement le résumé de l'IA.

Et cet article nous apprend que ce nouvel intermédiaire est plus fragile qu'aucun de ceux qu'il remplace. Les moteurs de recherche classiques séparaient au moins le « classement » du « contenu » : vous voyiez les liens, vous cliquiez, vous jugiez par vous-même. La recherche par IA fond les deux en un texte fluide, les liens de citation relégués dans un coin que la plupart ne consultent jamais. Dès lors que l'intermédiaire « lit à votre place », vous perdez l'occasion de vérifier par vous-même.

Plus subtil encore, le transfert de confiance. Les gens font confiance à la recherche par IA non parce qu'ils en ont vérifié chaque citation, mais parce que le ton est assuré, la mise en forme professionnelle, les « sources » affichées. Cette confiance est empruntée — empruntée aux médias traditionnels, aux revues scientifiques, aux encyclopédies, ces institutions qui font réellement le travail de vérification. Mais quand un contenu fabriqué peut lui aussi revêtir l'habit du « cité par l'IA », cette confiance se dilue. La mauvaise monnaie chasse la bonne — sur le marché des idées comme ailleurs.

Il y a quelque chose de profondément ironique dans cette situation. Les grands modèles de langage ont été entraînés sur l'intégralité du savoir humain numérisé — des siècles de science, de journalisme, de littérature — précisément pour devenir des oracles fiables. Et voilà que le maillon faible n'est pas dans leurs poids ni dans leur architecture, mais dans le tuyau qui les relie au présent : le mécanisme de citation, cette rustine ajoutée après coup pour leur donner l'air de « sourcer » leurs dires. Nous avons construit des cathédrales de l'intelligence, puis nous les avons branchées sur des gouttières percées.

Les auteurs ont exclu de leur protocole les domaines sensibles — santé, finance, politique, sécurité publique — comme l'exigeait le comité d'éthique, et ils ont supprimé toutes leurs publications de test dans les quatre semaines. Mais les attaquants ne s'imposeront pas une telle discipline. Qui garantira, la prochaine fois, que les domaines exclus le resteront ?

**Soyons honnêtes : nous ne savons pas réparer**

La conclusion de l'article a une honnêteté rare : les auteurs admettent ne pas connaître la solution générale. Ils ignorent combien de « publications à faible poids » il faut pour obtenir une « citation à fort poids », si le taux de réussite dérive avec le temps, et même si la fenêtre de mars à avril qu'ils ont testée est représentative de l'année entière.

Cette honnêteté est précisément ce qu'il y a de plus précieux. Dans le domaine de la sécurité de l'IA, le plus dangereux n'est pas le problème connu, c'est le problème « que l'on croit résolu ». L'horreur de la pollution des citations tient à son asymétrie : le défenseur doit colmater toute la structure — la modération des publications sur des dizaines de domaines, le réordonnancement des algorithmes de citation, la détection d'anomalies — tandis que l'attaquant n'a besoin que d'une fissure. Et les fissures seront toujours plus nombreuses que les murs.

La réponse ne se trouve peut-être pas dans la technique, mais dans l'habitude. Le conseil du Tow Center en 2025 reste valable : traitez les citations de l'IA comme des pistes, jamais comme un verdict. Cliquez, regardez le nom de domaine, vérifiez que la phrase figure bien dans le texte d'origine. Prenez le résumé de l'IA pour un « panneau indicateur », pas pour une « réponse ».

Mais soyons francs : qui le fera vraiment ? Quand l'IA vous met la réponse dans la bouche, aller cliquer pour vérifier relève d'une diligence presque contre-nature.

Quatorze dollars, une heure, huit plateformes. Cet article est un miroir, et ce qu'il reflète n'est pas tant la fragilité de l'IA que notre empressement à lui sous-traiter le jugement du vrai et du faux. La technique itérera, les modèles se renforceront, mais la question nous suivra : quand les machines cherchent à notre place, qui contrôle les machines ? Et quand ceux qui contrôlent peuvent eux aussi s'acheter, que nous reste-t-il ?

La réponse n'a peut-être jamais changé : vous-même. Sauf que cette fois, elle coûte dix secondes par question — le temps de cliquer sur ce lien, et de regarder.

---

*À discuter : cliquez-vous sur les liens cités par une IA de recherche pour les vérifier ? Si la « source d'autorité » qu'elle cite peut elle-même s'acheter pour quatorze dollars, ferez-vous encore confiance à ses réponses ?*
