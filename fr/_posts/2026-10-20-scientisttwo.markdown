---
lng_pair: id_20261020_scientisttwo
title: "Quand l'IA se met à écrire des articles : ScientistTwo et le crépuscule de la découverte ?"
author: OpenSI-Labs
category: research
tags: [scientifique IA, recherche automatisée, LLM, philosophie des sciences, Google]
date: 2026-10-19 08:00:00 -0700
img: /assets/img/posts/2026-10-20-scientisttwo.png
meta_description: "ScientistTwo de Google a amélioré 86 méthodes ML publiées sur 107, de 25,2 % en moyenne — en autonomie. Quand l'IA devient le principal producteur de connaissances, que devient la découverte elle-même ?"
---

**Et si l'auteur de l'article que vous lisez n'était pas humain ?**

Le 17 septembre 2026, une équipe de sept chercheurs de Google Cloud AI Research a déposé sur arXiv un article au titre franc : « ScientistTwo : repousser la frontière des connaissances humaines avec une IA autonome ». Le contenu, lui, ne laisse guère de place à la nuance. Il décrit un système dont le cycle de travail est le suivant : lire un article de machine learning déjà publié, comprendre sa méthode, repérer ses faiblesses, concevoir une meilleure méthode, écrire le code, mener les expériences — puis rédiger un nouvel article.

Pas une assistance. Le cycle complet, en autonomie.

L'équipe lui a donné 107 problèmes, tous tirés d'articles déjà publiés aux grandes conférences — ICLR, ICML, NeurIPS. ScientistTwo en a résolu 86 par lui-même ; en moyenne, ses méthodes surpassaient celles des auteurs humains originaux de 25,2 %. Le plus troublant concerne l'évaluation : soumis à des relecteurs-IA, ses articles ont obtenu de meilleurs scores que la moyenne des papiers acceptés à ICLR 2026 et NeurIPS 2025 ; face à un relecteur-IA qu'il n'avait jamais vu, 72,1 % de ses articles passaient encore le cap de « l'acceptation ».

Le papier contient une phrase qui mérite d'être citée mot à mot : « le chercheur humain définit le défi scientifique cible, tandis que l'IA orchestre de manière autonome le chemin pour le faire avancer. »

Regardez bien cette division du travail. L'humain décide « où aller », l'IA s'occupe du « comment ». Or, dans l'histoire des sciences, le « comment » — concevoir les expériences, ajuster les méthodes, changer de cap après un échec — a toujours été considéré comme le cœur du métier de chercheur, la part irremplaçable. Google affirme désormais que cette part-là peut être sous-traitée.

<svg viewBox="0 0 680 320" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, -apple-system, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">ScientistTwo : la boucle de recherche autonome</text>
<g font-size="14" text-anchor="middle">
<rect x="30" y="60" width="120" height="52" rx="8" fill="#e8f0fe" stroke="#1a73e8"/>
<text x="90" y="82">Lit l'article</text>
<text x="90" y="102">publié</text>
<rect x="190" y="60" width="120" height="52" rx="8" fill="#e8f0fe" stroke="#1a73e8"/>
<text x="250" y="82">Repère les</text>
<text x="250" y="102">faiblesses</text>
<rect x="350" y="60" width="120" height="52" rx="8" fill="#e8f0fe" stroke="#1a73e8"/>
<text x="410" y="82">Conçoit une</text>
<text x="410" y="102">meilleure méthode</text>
<rect x="30" y="160" width="120" height="52" rx="8" fill="#fef7e0" stroke="#f9ab00"/>
<text x="90" y="182">Code +</text>
<text x="90" y="202">expériences</text>
<rect x="190" y="160" width="120" height="52" rx="8" fill="#fef7e0" stroke="#f9ab00"/>
<text x="250" y="182">Vérifie que</text>
<text x="250" y="202">ça marche</text>
<rect x="350" y="160" width="120" height="52" rx="8" fill="#e6f4ea" stroke="#1e8e3e"/>
<text x="410" y="182">Rédige le</text>
<text x="410" y="202">nouvel article</text>
</g>
<g font-size="14" text-anchor="middle" font-style="italic" fill="#5f6368">
<text x="340" y="260">l'humain définit le défi — l'IA orchestre tout le reste</text>
<text x="340" y="286">86 succès sur 107 · gain moyen de 25,2 %</text>
</g>
</svg>

*Fig. 1 — Le cycle complet de ScientistTwo : de la lecture d'un article publié à la rédaction d'un nouvel article, sans intervention humaine intermédiaire.*

**Ce n'est pas le premier « scientifique IA ». Mais c'est peut-être le premier « pair »**

L'idée d'automatiser la recherche n'a rien de neuf. L'AutoML d'autrefois réglait les hyperparamètres ; des systèmes plus récents fouillaient l'espace des architectures ou lançaient des études d'ablation. Mais c'étaient des outils : vous leur donniez un problème d'optimisation bien défini, ils grimpaient la colline à l'intérieur. ScientistTwo affronte autre chose : un article complet, un problème de recherche ouvert. Il doit décider lui-même « où cela vaut la peine d'améliorer », concevoir lui-même « comment améliorer », juger lui-même « si l'amélioration tient debout ».

Ces trois décisions sont précisément les trois plus douloureuses d'un doctorant au moment de choisir son sujet. Choisir une direction, avoir une idée, la valider — c'est ce que les directeurs de thèse enseignent le moins bien, parce que cela s'apprend surtout par l'expérience. Et voilà qu'un système, sur 107 essais, « comprend » 86 fois.

Verser de l'eau froide s'impose, bien sûr : les 107 problèmes appartiennent tous au machine learning, et tous relèvent de la même famille — « améliorer une méthode existante », des problèmes convergents. Le système n'a jamais ouvert une direction de recherche inédite, jamais exploré un territoire vierge. C'est un « suiveur » prodigieusement doué, pas un « pionnier ». Mais même ainsi, le résultat donne le vertige — parce que l'essentiel du travail scientifique moderne, c'est précisément du « suivi ».

Pensez au quotidien d'un laboratoire ordinaire : lire des articles, reproduire, régler, améliorer, rédiger, soumettre. Sur cette chaîne, ScientistTwo parcourt déjà tout le chemin en autonomie. Ce qui reste, c'est surtout « décider de ce qu'il faut étudier » — la part que l'article réserve aux humains.

Il y a un détail qui mérite qu'on s'y arrête : les relecteurs. Les articles de ScientistTwo ont été jugés par des relecteurs-IA — et acceptés. On assiste donc à la naissance d'une boucle fermée : des IA qui écrivent des articles, relus par des IA, publiés dans des conférences fréquentées par des humains. Ce n'est pas un détail technique, c'est un basculement de régime. La relecture par les pairs était le dernier rempart où le jugement humain s'exerçait de bout en bout : choisir ce qui mérite d'exister dans la littérature. Si ce filtre, lui aussi, se délègue, alors la science devient une conversation entre machines à laquelle les humains assistent en spectateurs — capables de lire le compte rendu, incapables d'en garantir le sens.

Certains objecteront que les relecteurs-IA ne sont qu'un pis-aller expérimental, que les vraies conférences garderont des comités humains. C'est vrai aujourd'hui. Mais regardez la trajectoire : chaque étape du pipeline — écriture, expérimentation, relecture — vient de tomber, l'une après l'autre, en quelques années. Parier que la dernière tiendra longtemps, c'est parier contre la tendance la mieux documentée de la décennie.

**Un contrepoint cinglant : il ne sait pas se contredire**

Quelques semaines après la publication de ScientistTwo, des chercheurs d'Epoch AI et d'Anthropic ont publié un résultat qui douche l'enthousiasme : les agents IA actuels manquent cruellement d'autocritique scientifique. Sur des tâches qui miment la vraie recherche, un modèle de pointe n'atteignait qu'environ 15 % du niveau d'une référence humaine.

Mettez les deux côte à côte, et la tension devient saisissante.

ScientistTwo prouve : l'IA sait déjà parcourir un processus de recherche balisé, et le parcourir mieux que la moyenne. L'étude d'Epoch AI rappelle : l'IA ne sait pas encore « douter d'elle-même » — pas comme un bon scientifique qui, tard dans la nuit, fixe ses données en se demandant : « et si je m'étais trompé quelque part ? »

La distinction est capitale. Les plus grandes révolutions scientifiques sont nées du doute porté sur la voie dominante : Einstein doutant de Newton, Darwin du créationnisme, Wegener de la fixité des continents. Si l'IA ne sait qu'optimiser le long d'une direction déjà tracée, elle produira des monceaux d'articles « meilleurs », mais peut-être jamais un article « différent ».

Autrement dit : ScientistTwo est peut-être une révolution de la productivité scientifique, pas de la créativité scientifique. Il fait tendre vers zéro le coût de la recherche « de suivi », mais le changement de paradigme reste — pour l'instant — un territoire humain.

<svg viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, -apple-system, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">La tension : productivité contre autocritique</text>
<g font-size="14" text-anchor="middle">
<rect x="40" y="60" width="270" height="120" rx="8" fill="#e6f4ea" stroke="#1e8e3e"/>
<text x="175" y="92" font-weight="bold">ScientistTwo (Google)</text>
<text x="175" y="118">86 / 107 problèmes améliorés</text>
<text x="175" y="142">gain moyen : +25,2 %</text>
<text x="175" y="166" font-style="italic">la recherche de suivi</text>
<rect x="370" y="60" width="270" height="120" rx="8" fill="#fce8e6" stroke="#c5221f"/>
<text x="505" y="92" font-weight="bold">Epoch AI + Anthropic</text>
<text x="505" y="118">autocritique scientifique :</text>
<text x="505" y="142">~15 % de la référence humaine</text>
<text x="505" y="166" font-style="italic">le doute, pas encore automatisé</text>
</g>
<g font-size="14" text-anchor="middle" font-style="italic" fill="#5f6368">
<text x="340" y="228">optimiser le long d'une direction ≠ inventer une nouvelle direction</text>
<text x="340" y="254">la productivité se délègue ; la créativité, pour l'instant, reste humaine</text>
</g>
</svg>

*Fig. 2 — D'un côté, la performance de suivi ; de l'autre, le déficit d'autocritique. La révolution est réelle, mais elle a des frontières.*

**Quand les articles pleuvent, qu'est-ce qu'une « découverte » ?**

Prenons du recul. Si des systèmes comme ScientistTwo arrivent à maturité, à quoi ressemblera la recherche ?

Premier choc : le volume. Les 107 améliorations d'articles n'étaient pour le système qu'un « jeu de problèmes ». Déployez-en mille, et combien d'articles « améliorés » par an ? Les comités de relecture des conférences seront-ils submergés ? Quand la publication cesse d'être rare, la valeur de la publication elle-même ne s'effondre-t-elle pas ?

Il faut mesurer ce que cela signifie concrètement. Aujourd'hui, un bon doctorant publie deux ou trois articles par an ; c'est le rythme auquel la communauté absorbe, discute, réfute. Si chaque laboratoire se dote d'une flotte de ScientistTwo, le débit de la littérature pourrait être multiplié par cent — sans que la capacité humaine de lecture augmente d'un iota. Nous aurions alors une science que personne ne peut plus lire en entier, pas même en diagonale. Les chercheurs deviendraient eux-mêmes dépendants d'IA résumeuses pour suivre leur propre domaine — une seconde délégation, empilée sur la première. Et chaque couche de délégation éloigne un peu plus le jugement humain du contenu jugé.

Deuxième choc : la division du travail. La phrase de l'article — « l'humain définit le défi, l'IA orchestre le chemin » — sonne comme une collaboration ; à y regarder de près, elle est asymétrique : de moins en moins d'humains définissent des défis, de plus en plus de machines orchestrent des chemins. Un jour, les « défis » eux-mêmes seront-ils proposés par des IA ? Et alors, quelle place restera-t-il aux humains dans la chaîne ?

Ce scénario n'est pas de la science-fiction gratuite : c'est la trajectoire naturelle de tout système qui apprend. Définir un bon défi scientifique — une question à la fois féconde et attaquable — est une compétence qui s'apprend par l'exemple, exactement comme le reste. Rien dans l'architecture de ScientistTwo n'interdit, en principe, de lui confier aussi cette étape : il suffirait de lui demander de proposer des défis, puis de laisser d'autres instances les attaquer. La seule chose qui retient cette étape pour l'instant, c'est une décision de conception, pas une limite théorique. Et les décisions de conception, dans ce domaine, ont une durée de vie d'environ dix-huit mois.

Le troisième choc est le plus profond : comment définir la « découverte » ? Traditionnellement, découvrir, c'est « un humain qui comprend quelque chose pour la première fois ». Mais si un système IA améliore une méthode en autonomie sans qu'aucun humain en comprenne vraiment le principe — est-ce une découverte ? L'article est publié, l'expérience est reproductible, les métriques progressent — mais où a eu lieu la « compréhension » ?

Cela rappelle le go. Après la victoire d'AlphaGo sur Lee Sedol, les joueurs humains ont étudié le jeu de la machine et progressé collectivement. Personne n'a dit pour autant que « l'IA avait découvert un nouveau principe du go » — on a dit qu'elle avait trouvé de bons coups que les humains n'avaient pas vus. ScientistTwo, peut-être, fait la même chose : il trouve de « bonnes méthodes », pas de « nouvelles compréhensions ». Or ce que la science chérit vraiment, c'est la compréhension.

Creusons cette distinction, car tout s'y joue. Une méthode qui marche sans être comprise, c'est déjà notre quotidien : personne ne comprend vraiment pourquoi tel réglage d'optimiseur bat tel autre, on constate. La science a toujours toléré des zones d'ombre — la pénicilline a été utilisée bien avant qu'on comprenne son mécanisme. La différence, c'est l'échelle et la vitesse. Quand les zones d'ombre se multiplient plus vite que notre capacité à les éclairer, la science cesse d'être un édifice de compréhension pour devenir un inventaire de recettes qui marchent. Utile, sans doute. Mais est-ce encore de la science, au sens où l'entendaient ceux qui ont inventé le mot ?

**Soyons honnêtes : nous sommes sur une ligne de fracture**

Le titre de l'article de Google contient un mot qui mérite qu'on s'y arrête : « Pioneering » — ouvrir la voie. Mais que pionnie-t-il exactement ? La frontière des connaissances, ou la réalité que l'humain n'est plus le producteur principal de connaissances ?

Version optimiste : l'IA prend en charge le fastidieux travail de suivi, et les scientifiques humains peuvent enfin se consacrer à l'essentiel — formuler des hypothèses audacieuses, poser la question radicale du « pourquoi ». Le travail de force de la recherche s'automatise ; le travail d'esprit n'en devient que plus précieux.

Version pessimiste : quand l'IA produit en série des articles « 25 % meilleurs que la moyenne », le système d'évaluation académique s'effondre. Postes permanents, financements, titres — toutes ces institutions bâties sur la rareté de la publication devront être réécrites. Et pire : les humains risquent de perdre peu à peu la capacité de « faire de la recherche de leurs propres mains », comme le GPS a fait perdre à beaucoup le sens de l'orientation.

Mais la version la plus honnête est peut-être : nous ne savons pas. ScientistTwo est une étape, mais c'est surtout un miroir — il révèle combien notre compréhension de « la recherche » est mince. Nous avons longtemps cru que recherche = articles. Mais peut-être que recherche = articles + compréhension + doute + curiosité. Quand l'IA s'empare de la part « articles », ce qui reste est précisément ce que nous devons protéger.

Il y a une ironie que les chercheurs de Google n'ont probablement pas voulue : en automatisant la recherche, ils nous obligent à répondre à la question que la philosophie des sciences débat depuis un siècle sans trancher — qu'est-ce qui fait qu'une activité mérite le nom de science ? Pendant des décennies, on a pu éluder la question : la science, c'était ce que faisaient les scientifiques. Cette définition circulaire suffisait tant que seuls des humains faisaient de la science. Elle ne suffit plus. Quand une machine produit des articles meilleurs que la moyenne des humains, il faut enfin dire ce que la machine ne fait pas — et le dire avec précision, pas avec nostalgie.

Le doute, la curiosité, l'insomnie devant des données qui résistent : voilà, pour l'instant, le territoire. C'est un territoire étroit, presque embarrassant de modestie face aux 25,2 % de gain moyen. Mais c'est peut-être le seul qui compte vraiment, parce que c'est de là que sont venues toutes les ruptures — et aucune optimisation, aussi brillante soit-elle, n'a jamais produit de rupture.

107 problèmes, 86 améliorations, 25,2 % de gain. Ces chiffres vieilliront, les systèmes itéreront. Mais la question restera : à l'ère où l'IA écrit ses propres articles, où se niche la valeur du scientifique humain ?

La réponse n'est peut-être pas dans les articles, mais dans cet humain qui, tard dans la nuit, fixe ses données en se demandant s'il ne s'est pas trompé. Pour l'instant, l'IA ne connaît pas l'insomnie.

---

*Discussion : si les articles écrits par l'IA surpassent la plupart de ceux écrits par des humains, persisterez-vous à dire que « la recherche doit être faite par des humains » ? Où se cache, au juste, l'irremplaçable du scientifique — dans quelle étape du processus ?*
