---
lng_pair: id_20261027_byteification
title: "Pourquoi Llama ne sait pas compter les r de « strawberry » — et l'article de Nature qui le lui apprend"
author: OpenSI-Labs
category: research
tags: [modèles de langage, tokenisation, modèles au niveau octet, Nature, Llama, Qwen, Allen Institute for AI]
date: 2026-10-27 01:00:00 -0700
img: /assets/img/posts/2026-10-27-byteification.png
meta_description: "Demandez à un chatbot combien de r contient « strawberry » : il répond souvent deux. Il y en a trois — mais le modèle ne voit jamais les lettres. Un article de Nature montre comment transformer Llama 3 et Qwen3 pour qu'ils lisent octet par octet, pour moins de 1 % du coût de leur entraînement."
---

Posez à un chatbot performant une question qu'un enfant de six ans résout sans réfléchir : combien y a-t-il de r dans « strawberry » ?

La réponse est trois. Les chatbots ont longtemps répondu deux, et l'erreur n'a rien d'un manque d'intelligence. C'est un problème de vue. Avant qu'un modèle de langage lise ce que vous écrivez, un autre logiciel découpe votre texte en morceaux appelés tokens. Un token peut être un mot court entier, ou un bout de mot plus long. « Strawberry » arrive au modèle en deux ou trois morceaux — disons « straw », « ber », « ry ». Le modèle travaille sur ces morceaux. Les lettres qu'ils contiennent, il ne les voit jamais.

Alors, quand on lui demande de compter les r, le modèle est comme quelqu'un à qui l'on demanderait le nombre de fenêtres d'une maison qu'il n'a vue que sous forme de trois boîtes scellées. Il peut deviner, de mémoire. Il ne peut pas regarder. Les morceaux sont la plus petite chose qu'il perçoive ; en dessous — une lettre seule —, sa vision ne descend pas.

Cette façon de lire s'appelle la tokenisation en sous-mots, et presque tous les modèles de langage que vous avez utilisés la pratiquent. Un article paru ce mois-ci dans *Nature* — signé Benjamin Minixhofer et ses collègues de l'université LMU de Munich, de l'Allen Institute for AI, de l'université de Cambridge, de l'université de Washington et de l'Imperial College de Londres — pose une question simple à son sujet : et si ce découpage n'était pas définitif ? Un modèle entraîné à lire par morceaux pourrait-il apprendre, après coup et pour pas cher, à lire lettre par lettre ? Leur réponse est une procédure qu'ils appellent la byteification, et elle fonctionne sur des modèles qui existent déjà, dont Llama 3 de Meta et Qwen3 d'Alibaba.

## Pourquoi on découpe le texte, d'abord

Personne n'a choisi les tokens par amour de l'élégance. On les a choisis parce qu'ils vont vite.

Lire lettre par lettre, c'est lire beaucoup. Une page d'anglais compte quelques milliers de lettres ; les faire passer une à une dans un grand réseau de neurones, et le calcul explose. Les tokens compressent le texte. Les combinaisons fréquentes — « the », « ing », le début de « strawberry » — se réduisent à une seule unité, et le modèle consacre ses pas à des unités assez grandes pour porter du sens. Toute l'ère moderne des modèles de langage s'est construite sur cette compression. Un dictionnaire fixe de morceaux, arrêté avant le début de l'entraînement, se trouve sous GPT, Claude, Llama, Qwen et presque tout le reste.

Les angles morts viennent avec la compression, gratuitement. L'orthographe devient difficile quand on ne voit pas les lettres. Compter relève de la devinette. Le code en souffre, parce que dans du code, un seul caractère fait souvent toute l'histoire : une parenthèse mal placée, et le programme fait autre chose. Les séquences génétiques souffrent pour la même raison : changez une lettre dans un brin d'ADN et vous avez peut-être changé ce qu'il fait. Et une injustice plus discrète est logée dans le système : les dictionnaires de morceaux ont été construits surtout sur l'anglais. Les langues dont les mots se fragmentent mal dans ces dictionnaires se retrouvent découpées en bien plus de tokens pour la même phrase — donc plus chères à traiter, et moins bien traitées. Même phrase, facture plus lourde, lecture plus maladroite. La taxe dépend de la langue dans laquelle il vous arrive d'écrire.

Rien de tout cela n'était un secret. Depuis longtemps, des chercheurs construisent des modèles qui lisent les octets bruts — l'octet étant la plus petite unité que stocke un ordinateur, à peu près une lettre pour le texte anglais. Un modèle au niveau octet voit tout : chaque lettre, chaque espace, chaque parenthèse. « Strawberry » ne peut pas le tromper, puisqu'il n'y a rien entre lui et les lettres. Le problème, c'est que ces modèles perdaient. Entraînés de zéro, ils restaient derrière les modèles à morceaux de même taille, et entraîner l'un d'eux coûte la même fortune que n'importe quel grand modèle. La lecture par octets est donc restée une curiosité de laboratoire, et le reste du domaine a gardé ses boîtes scellées.

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="48" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">Deux façons de lire « strawberry »</text>
<text x="40" y="92" font-size="16" font-weight="700" fill="#475569">LECTURE PAR MORCEAUX — les modèles actuels</text>
<rect x="40" y="106" width="180" height="52" rx="10" fill="#94a3b8"/>
<rect x="236" y="106" width="150" height="52" rx="10" fill="#94a3b8"/>
<rect x="402" y="106" width="110" height="52" rx="10" fill="#94a3b8"/>
<text x="130" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">straw</text>
<text x="311" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">ber</text>
<text x="457" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">ry</text>
<text x="528" y="140" font-size="16" fill="#475569">lettres cachées</text>
<text x="40" y="212" font-size="16" font-weight="700" fill="#166534">LECTURE PAR OCTETS — après la byteification</text>
<rect x="40" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="64" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">s</text>
<rect x="96" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="120" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">t</text>
<rect x="152" y="226" width="48" height="48" rx="8" fill="#fee2e2" stroke="#dc2626" stroke-width="3"/><text x="176" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#b91c1c">r</text>
<rect x="208" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="232" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">a</text>
<rect x="264" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="288" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">w</text>
<rect x="320" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="344" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">b</text>
<rect x="376" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="400" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">e</text>
<rect x="432" y="226" width="48" height="48" rx="8" fill="#fee2e2" stroke="#dc2626" stroke-width="3"/><text x="456" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#b91c1c">r</text>
<rect x="488" y="226" width="48" height="48" rx="8" fill="#fee2e2" stroke="#dc2626" stroke-width="3"/><text x="512" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#b91c1c">r</text>
<rect x="544" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="568" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">y</text>
<text x="608" y="258" font-size="17" font-weight="700" fill="#b91c1c">r = 3</text>
<text x="340" y="302" text-anchor="middle" font-size="16" fill="#4b5563">Les morceaux cachent les lettres. Les octets les mettent toutes sur la table.</text>
</svg>
<figcaption>Figure 1 — Un lecteur par morceaux rencontre « strawberry » sous forme de quelques blocs scellés ; un lecteur par octets rencontre ses dix lettres, et les trois r se comptent simplement.</figcaption>
</figure>

## Une retouche, pas une reconstruction

Le geste de l'article de *Nature*, c'est de cesser de traiter la manière de lire comme une partie des fondations du modèle. Dans leur image, un modèle entraîné comporte deux parties qu'on peut séparer. Il y a le cœur — la grande pile de transformeurs au milieu, qui détient presque tout ce que le modèle sait de la langue, des faits et du raisonnement. Et il y a l'appareil de lecture autour : les pièces qui transforment le texte brut en quelque chose que le cœur peut traiter, et la sortie du cœur en texte. La byteification remplace l'appareil de lecture et laisse le cœur — la partie coûteuse, celle qu'un entraînement complet a mis des mois à construire — presque intact.

C'est changer la façon dont une personne lit, pas ce qu'elle sait. Le savoir reste. Les yeux changent.

Les pièces de remplacement sont un petit encodeur local qui lit les octets entrants, un composant nommé prédicteur de frontières qui décide où un morceau significatif se termine et où le suivant commence, un décodeur local, et la tête de sortie qui produit les octets à l'autre bout. Le cœur au milieu — les auteurs l'appellent le transformeur global — reçoit, pour chaque morceau que le prédicteur découpe, un résumé construit à partir des octets réels. Le cœur pense toujours par morceaux. Mais ce sont des morceaux taillés dans de vraies lettres, par un lecteur qui les a vues.

L'entraînement de cet hybride se fait en deux étapes, et la première est la plus astucieuse. Les auteurs gèlent le cœur complètement — pas un seul de ses poids n'a le droit de bouger — et n'entraînent que les nouvelles pièces autour. Le signal d'entraînement est une distillation exacte : on apprend à la nouvelle entrée à nourrir le cœur gelé de représentations qui le font se comporter comme avant, comme si rien n'avait changé dans ce qu'il reçoit. En langage simple : les nouveaux yeux apprennent la langue de l'ancien cerveau avant qu'on demande au cerveau de s'adapter. Cette étape consomme 9,8 milliards de tokens de texte.

Puis, à la deuxième étape, tout est dégelé et le modèle entier est affiné ensemble, de bout en bout, sur 39,3 milliards de tokens supplémentaires, tirés pour l'essentiel de Dolma 3, le corpus d'entraînement ouvert de l'Allen Institute, plus 75 millions de tokens synthétiques fabriqués pour enseigner les compétences liées aux caractères — épeler, compter, manipuler les lettres. Facture totale : 49,1 milliards de tokens. Les auteurs l'évaluent à moins de 1 % de ce que coûte normalement l'entraînement de zéro d'un modèle de cette taille. Moins de 1 % pour changer la façon dont un modèle fini lit.

Un détail de conception mérite son propre paragraphe, parce que les auteurs y voient une grande partie de la raison pour laquelle les anciens modèles à octets perdaient. Quand un lecteur par octets découpe un flux de lettres en morceaux, il doit décider où couper tout en lisant de gauche à droite. Les conceptions antérieures prenaient cette décision de façon causale — en ne regardant que les octets déjà vus. Le prédicteur de frontières de cet article a droit à un coup d'œil : pour décider si un morceau s'arrête ici, il peut regarder un octet du futur. Un octet, cela semble ne rien être. C'est la différence entre décider où un mot se termine les yeux bandés, et décider après un regard sur la lettre suivante — ce regard vous dit si « ry » termine « strawberry » ou commence autre chose. Les auteurs soutiennent que ce petit coup d'œil referme une bonne part de l'écart d'expressivité qui retenait les modèles à octets. Leur conception reprend la forme du plus fort des modèles à octets antérieurs, le Byte Latent Transformer de Meta, et y ajoute le coup d'œil.

<figure>
<svg width="680" height="400" viewBox="0 0 680 400" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="380" rx="14" fill="#f7f9fc"/>
<text x="340" y="46" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">La byteification : deux étapes, une petite facture</text>
<rect x="30" y="66" width="620" height="128" rx="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
<text x="48" y="94" font-size="17" font-weight="700" fill="#1e40af">ÉTAPE 1 — apprendre aux nouveaux yeux · 9,8 Md de tokens</text>
<rect x="48" y="108" width="136" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="116" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">encodeur octets</text>
<rect x="194" y="108" width="188" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="288" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">prédicteur frontières*</text>
<rect x="392" y="108" width="140" height="40" rx="8" fill="#e5e7eb" stroke="#6b7280" stroke-width="2"/><text x="462" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#374151">cœur : GELÉ</text>
<rect x="542" y="108" width="92" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="588" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">décodeur</text>
<text x="48" y="176" font-size="16" fill="#1f2937">*regarde 1 octet en avant pour décider où couper · seules les nouvelles pièces s'entraînent</text>
<rect x="30" y="208" width="620" height="104" rx="12" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/>
<text x="48" y="236" font-size="17" font-weight="700" fill="#166534">ÉTAPE 2 — tout régler ensemble · 39,3 Md de tokens</text>
<text x="48" y="266" font-size="16" fill="#1f2937">Cœur dégelé ; le modèle entier est affiné de bout en bout,</text>
<text x="48" y="290" font-size="16" fill="#1f2937">avec 75 millions de tokens synthétiques qui exercent les lettres.</text>
<text x="340" y="352" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">Total : 49,1 Md de tokens — moins de 1 % d'un entraînement complet</text>
<text x="340" y="378" text-anchor="middle" font-size="16" fill="#4b5563">Le savoir du modèle est conservé. Seule sa façon de lire est remplacée.</text>
</svg>
<figcaption>Figure 2 — La retouche en deux étapes : d'abord les nouvelles pièces au niveau octet apprennent à parler au cœur gelé, puis le modèle entier est réglé ensemble.</figcaption>
</figure>

## Quatre modèles, convertis

L'équipe a appliqué la recette à quatre modèles ouverts. Olmo 3 7B, de l'Allen Institute, est devenu Bolmo 7B. Son prédécesseur plus petit, OLMo 2 1B, est devenu Bolmo 1B. Qwen3 8B Base est devenu Bwen 8B, et Llama 3 8B est devenu Blama 8B. Les modèles convertis ont presque la même taille que les originaux — le nombre de paramètres bouge de moins de 5 % dans un sens ou dans l'autre — et toute la famille est publiée ouvertement : chacun peut vérifier les affirmations ou refaire l'opération sur un autre patient.

Que font réellement les modèles convertis ? Le résumé honnête : ils gagnent ce qui leur manquait, et ils gardent presque tout le reste.

Sur la compréhension des caractères — mesurée par les benchmarks CUTE et EXECUTE, qui testent justement les compétences au niveau lettre où les lecteurs par morceaux trébuchent — les modèles byteifiés battent les modèles mêmes dont ils sont issus. Sur certaines évaluations de code, ils devancent aussi leurs sources, ce qui colle à l'histoire : le code est un texte où les caractères seuls portent le poids. Ailleurs, sur un large éventail de plus de 40 benchmarks, ils approchent le plus souvent leurs sources en sous-mots au lieu de les dépasser. C'est la vraie forme du résultat. Personne ne prétend qu'un modèle byteifié devient soudain plus intelligent sur toute la ligne. L'affirmation est que l'angle mort des lettres peut être supprimé pendant que le reste des capacités du modèle reste essentiellement intact — et c'était jusque-là la partie que personne ne savait faire à bas prix.

La comparaison avec les autres modèles à octets est plus tranchée. Bolmo 7B a été mesuré face à BLT 7B, le modèle au niveau octet de Meta et le plus fort publié jusqu'ici à taille comparable, entraîné de zéro au prix d'un entraînement complet. Sur un agrégat de tâches STEM, Bolmo 7B l'a battu de 16,5 points de pourcentage. Ce chiffre doit se lire avec soin : c'est un agrégat, face à une seule référence. Mais la direction est difficile à contester — la retouche, à moins de 1 % du coût d'entraînement, a produit un meilleur modèle à octets que la voie coûteuse du départ de zéro. Des quatre conversions, Bwen 8B, celle construite à partir de Qwen3, était la plus forte : elle a amélioré son modèle source dans toutes les catégories d'évaluation sauf une, les questions-réponses générales.

Il y a un bonus pratique qui comptera peut-être autant que les benchmarks. Le monde des modèles ouverts ne tourne pas sur les modèles de base ; il tourne sur les affinages — les milliers de versions de Llama et de Qwen que des gens ont adaptées à la médecine, au droit, au code, au support client, à tout. Une méthode de conversion qui obligerait à refaire tout ce travail ne serait qu'une curiosité. La byteification ne l'oblige pas. Grâce à une technique nommée arithmétique des tâches — en gros, rajouter au modèle converti la différence entre un modèle affiné et sa base —, le suivi d'instructions des affinages d'origine se transporte vers les versions byteifiées. L'écosystème suit. Le travail déjà investi survit à l'opération.

## Pourquoi cela compte, dit simplement

Commençons par l'idée dont le statut change discrètement dans cet article. Pendant dix ans, le tokeniseur a été traité comme une partie des fondations d'un modèle : fixé avant l'entraînement, identique pour toute la vie du modèle, impossible à changer ensuite sans tout recommencer. La byteification montre qu'il se comporte plutôt comme une paire de lunettes. Le modèle n'a pas à réapprendre ce qu'il sait pour voir autrement. Tout ce qui, en IA, se révèle être un accessoire remplaçable plutôt qu'une pierre de fondation devient moins cher et plus facile à expérimenter à partir de ce jour-là — et la lecture, rien de moins, figure désormais sur cette liste.

Ensuite, l'économie. Les entraînements complets sont les objets les plus chers du domaine ; la valeur de l'écosystème ouvert est enfermée dans des modèles qui ont chacun coûté l'un d'eux. Une méthode qui corrige le défaut le plus visible de ces modèles pour moins de 1 % de leur coût d'origine — en emportant leurs affinages au passage — protège cet investissement au lieu de le passer par pertes et profits. Chaque modèle ouvert existant est, en principe, candidat à la même opération.

Ensuite, l'équité, qui se dit facilement une fois qu'on l'a vue. Un octet est un octet dans toutes les langues de la Terre. Les dictionnaires de morceaux construits autour de l'anglais ne sont pas neutres : ils offrent à certaines langues des lectures courtes et efficaces, et à d'autres des lectures longues et fragmentées, et la différence se voit dans le prix et dans la qualité. Un lecteur qui travaille à partir des octets se moque de l'alphabet qu'on lui a donné. Quoi que fassent d'autre les modèles à octets, ils suppriment un biais qui était construit dans l'étape de lecture elle-même, avant que la moindre donnée d'entraînement ait son mot à dire.

Ensuite, le travail où les caractères sont le contenu. Une séquence génétique n'est pas un paragraphe ; changez une lettre et vous tenez une molécule différente. Une formule chimique, une ligne de code, une référence juridique, une partition : dans tous ces cas, le sens vit au niveau des caractères seuls, et un lecteur qui ne peut pas voir les caractères est le mauvais instrument, aussi intelligent soit-il. La byteification ne transforme pas les modèles en scientifiques. Elle rend le bon type de lecteur assez bon marché pour devenir le choix par défaut.

Et un point encore, plus discret. Un vocabulaire fixe met un plafond à ce qu'un modèle peut exprimer : avec un dictionnaire fini de morceaux de sortie, certaines distributions sur le texte ne peuvent tout simplement pas être représentées exactement — une limite que les chercheurs appellent le goulot softmax. Les octets n'ont pas de dictionnaire. Il n'y a pas de liste fixe à épuiser. Retirer le plafond ne garantit pas que quelqu'un construira plus haut, mais le plafond n'est plus là.

## Les limites, honnêtement

L'article est prudent, et un compte rendu fidèle doit l'être aussi.

Tout ici a été démontré entre 1 et 8 milliards de paramètres. Les modèles de pointe sont bien plus grands, et rien dans l'article ne montre que la retouche se comporte de la même façon à cette échelle. Les gains, au-delà des compétences sur les caractères, sont une parité plutôt qu'une victoire : sur la plupart des benchmarks généraux, les modèles convertis approchent leurs sources, ils ne les battent pas. Lire octet par octet signifie aussi des séquences plus longues — davantage d'unités à traiter pour le même texte — et les séquences longues sont la taxe classique sur la vitesse. Les auteurs montrent qu'un entraînement avec des taux de compression plus élevés (des morceaux plus gros découpés dans le flux d'octets) peut ramener la vitesse d'inférence à des niveaux compétitifs, mais les résumés de l'article n'offrent aucun temps d'exécution chiffré ; le coût réel en vitesse, sur une installation donnée, reste donc une question ouverte. Le transfert des affinages a aussi sa condition : l'arithmétique des tâches fonctionne quand les plongements du modèle affiné peuvent être réinitialisés aux valeurs du modèle de base sans grande perte de performance. Les auteurs disent que c'est le cas en général, mais pas toujours. Et le chiffre de 16,5 points sur les tâches STEM, celui qui a le plus de chances d'être cité, est un agrégat face à une seule référence — une preuve de direction, pas une déroute.

Il y a aussi le cadrage à garder en tête. Zhang et Xiong, dans le commentaire News & Views de *Nature* qui accompagnait l'article, formulent l'apport comme le ferait un observateur extérieur : une retouche, pas un nouveau modèle — une façon de donner à des systèmes existants une capacité qui leur manquait structurellement, pour une petite fraction du coût habituel. C'est exactement la bonne taille pour cette affirmation.

## Ce qu'il faut surveiller

La prochaine expérience évidente, c'est l'échelle. Quelqu'un — l'Allen Institute est le candidat naturel, puisque Bolmo est le leur — byteifiera un modèle bien plus grand que 8 milliards de paramètres et dira si la recette tient encore : si le cœur reste intact, si les gains sur les caractères survivent, si la taxe de vitesse reste gérable. Si elle tient à grande échelle, attendez-vous à ce que la conversion devienne une étape standard, quelque chose que les modèles ouverts subissent simplement après leur sortie, comme ils sont aujourd'hui quantifiés et affinés par routine.

D'ici là, le test de la fraise a changé de statut. C'était une blague sur l'incapacité des systèmes les plus intelligents du monde à réussir un comptage d'enfant. C'est maintenant une question qui a une réponse d'ingénierie : ils ne pouvaient pas voir les lettres, et il existe désormais un moyen peu coûteux de les leur montrer. Trois r. Il fallait juste que le modèle puisse regarder.

*Article : Minixhofer et al., « Retrofitting language models to operate over bytes », Nature 658, 915–922 (2026) ; version arXiv : « Bolmo: Byteifying the Next Generation of Language Models » ([arXiv:2512.15586](https://arxiv.org/abs/2512.15586)). Commentaire : Zhang & Xiong, Nature News & Views, 7 octobre 2026.*
