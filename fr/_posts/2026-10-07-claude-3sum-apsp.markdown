---
lng_pair: id_20261007_claude-3sum-apsp
title: "Le 0,0008 qui a brisé deux hypothèses"
author: OpenSI-Labs
category: research
tags: [théorie de la complexité, algorithmes, mathématiques par IA, vérification formelle]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-claude-3sum-apsp.png
meta_description: "Un modèle de recherche interne d'Anthropic a découvert les premiers algorithmes sous-quadratiques pour 3SUM et sous-cubiques pour les plus courts chemins, réfutant deux piliers de la théorie de la complexité — et ce, par accident."
---

Pendant des décennies, deux nombres sont restés cloués dans les manuels : 3SUM — trois nombres parmi *n* s'additionnent-ils à zéro ? — coûtait environ *n*² opérations ; le plus court chemin entre chaque paire de sommets, environ *n*³. On a grignoté constantes et facteurs logarithmiques. Les exposants n'ont jamais bougé.

Le 5 octobre, ils ont bougé. Un article de Josh Alman (Columbia) et Virginia Vassilevska Williams (MIT) donne des algorithmes déterministes en O(*n*^1,9992) pour 3SUM et O(*n*^2,9995) pour les plus courts chemins — premières améliorations polynomiales des bornes des manuels, et réfutation directe des hypothèses 3SUM et APSP qui fondent une bonne part de la complexité fine ([résumé arXiv](https://arxiv.org/abs/2610.06783v1), [texte intégral](https://arxiv.org/html/2610.06783v1)).

Le résumé de l'article est sec : « This refutes the 3SUM and APSP hypotheses of fine-grained complexity theory. » Au passage tombent aussi l'hypothèse du triangle exact (nouvelle borne O(*n*^2,9983)), les hypothèses de *k*-clique de poids nul et trois conjectures sur la multiplication matrice-vecteur en ligne. SETH — l'hypothèse forte du temps exponentiel — survit ; les auteurs le précisent.

<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Exposants des manuels contre nouveaux exposants, axe agrandi">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;}</style>
<text x="24" y="34" font-size="17" font-weight="700" fill="#111827">3SUM</text>
<text x="24" y="56" font-size="12.5" fill="#6b7280">axe agrandi &#215;25 : 1,990 &#8211; 2,010</text>
<line x1="150" y1="100" x2="610" y2="100" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="94" x2="150" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1,990</text>
<line x1="265" y1="94" x2="265" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1,995</text>
<line x1="380" y1="94" x2="380" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2,000</text>
<line x1="495" y1="94" x2="495" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2,005</text>
<line x1="610" y1="94" x2="610" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2,010</text>
<line x1="380" y1="70" x2="380" y2="100" stroke="#374151" stroke-width="3"/><text x="392" y="80" font-size="13" font-weight="600" fill="#374151">manuel : n&#178;</text>
<line x1="361.6" y1="70" x2="361.6" y2="100" stroke="#b45309" stroke-width="3"/><text x="150" y="80" font-size="13" font-weight="600" fill="#b45309">nouveau : n<tspan baseline-shift="super" font-size="9">1,9992</tspan></text>
<line x1="361.6" y1="140" x2="380" y2="140" stroke="#b45309" stroke-width="1.5"/><line x1="361.6" y1="135" x2="361.6" y2="145" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="135" x2="380" y2="145" stroke="#b45309" stroke-width="1.5"/><text x="370.8" y="158" font-size="12" fill="#b45309" text-anchor="middle">0,0008</text>
<text x="24" y="196" font-size="17" font-weight="700" fill="#111827">APSP</text>
<text x="24" y="218" font-size="12.5" fill="#6b7280">axe agrandi &#215;25 : 2,990 &#8211; 3,010</text>
<line x1="150" y1="262" x2="610" y2="262" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="256" x2="150" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2,990</text>
<line x1="265" y1="256" x2="265" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2,995</text>
<line x1="380" y1="256" x2="380" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3,000</text>
<line x1="495" y1="256" x2="495" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3,005</text>
<line x1="610" y1="256" x2="610" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3,010</text>
<line x1="380" y1="232" x2="380" y2="262" stroke="#374151" stroke-width="3"/><text x="392" y="242" font-size="13" font-weight="600" fill="#374151">manuel : n&#179;</text>
<line x1="368.5" y1="232" x2="368.5" y2="262" stroke="#b45309" stroke-width="3"/><text x="150" y="242" font-size="13" font-weight="600" fill="#b45309">nouveau : n<tspan baseline-shift="super" font-size="9">2,9995</tspan></text>
<line x1="368.5" y1="302" x2="380" y2="302" stroke="#b45309" stroke-width="1.5"/><line x1="368.5" y1="297" x2="368.5" y2="307" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="297" x2="380" y2="307" stroke="#b45309" stroke-width="1.5"/><text x="374.2" y="322" font-size="12" fill="#b45309" text-anchor="middle">0,0005</text>
</svg>
*Les exposants, agrandis 25 fois : 3SUM passe de 2,0 à 1,9992, APSP de 3,0 à 2,9995. L'écart est la nouvelle.*

Soyons honnêtes : à un milliard d'entrées, l'écart entre *n*² et *n*^1,9992 est inférieur à 2 %, avant des constantes que l'article ne prétend pas petites. Personne ne réécrira son logiciel de routage lundi. L'enjeu n'est pas pratique, il est structurel — comme découvrir qu'un mur porteur est creux. Des centaines de résultats de complexité fine ont la forme « le problème X exige *n*², sauf si 3SUM est facile ». 3SUM vient de devenir facile, d'un cheveu. Tous ces résultats reposent désormais sur *n*^1,9992 au lieu de *n*². L'édifice tient, mais ses fondations ont bougé.

Le mécanisme est un algorithme inédit de multiplication de matrices : multiplier une matrice entière grande et fine par une matrice courte et large, alors qu'on ne veut qu'une poignée d'entrées du résultat — calculées en O(*N*²/*D*^0,063) opérations, polynomialement moins que d'écrire le produit entier. La construction modifie une variante de la multiplication rectangulaire de Coppersmith (1982) — bâtie sur une identité à dix multiplications de Schönhage — pour sauter toute opération n'alimentant que des entrées indésirées. Lu comme algorithme de graphes, il trouve vite des triangles dans des graphes « bancals » — deux groupes de sommets énormes, le troisième minuscule — et des réductions connues propagent ce gain à 3SUM et aux plus courts chemins.

<svg viewBox="0 0 640 370" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Graphe triparti bancal avec un triangle surligné">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;}</style>
<text x="320" y="26" font-size="13" fill="#6b7280" text-anchor="middle">le tout petit côté : n<tspan baseline-shift="super" font-size="9">&#949;</tspan> sommets</text>
<circle cx="300" cy="52" r="7" fill="#9ca3af"/><circle cx="322" cy="44" r="7" fill="#9ca3af"/><circle cx="344" cy="52" r="7" fill="#9ca3af"/>
<g stroke="#d1d5db" stroke-width="1">
<line x1="300" y1="52" x2="130" y2="120"/><line x1="300" y1="52" x2="130" y2="200"/><line x1="300" y1="52" x2="130" y2="280"/>
<line x1="322" y1="44" x2="130" y2="160"/><line x1="322" y1="44" x2="130" y2="240"/><line x1="322" y1="44" x2="510" y2="160"/>
<line x1="344" y1="52" x2="130" y2="120"/><line x1="344" y1="52" x2="510" y2="200"/><line x1="344" y1="52" x2="510" y2="280"/>
<line x1="300" y1="52" x2="510" y2="120"/><line x1="300" y1="52" x2="510" y2="200"/><line x1="300" y1="52" x2="510" y2="280"/>
<line x1="322" y1="44" x2="510" y2="120"/><line x1="322" y1="44" x2="510" y2="240"/><line x1="344" y1="52" x2="130" y2="200"/>
</g>
<g fill="#6b7280">
<circle cx="110" cy="120" r="7"/><circle cx="150" cy="120" r="7"/><circle cx="110" cy="160" r="7"/><circle cx="150" cy="160" r="7"/><circle cx="110" cy="200" r="7"/><circle cx="150" cy="200" r="7"/><circle cx="110" cy="240" r="7"/><circle cx="150" cy="240" r="7"/><circle cx="110" cy="280" r="7"/><circle cx="150" cy="280" r="7"/>
<circle cx="490" cy="120" r="7"/><circle cx="530" cy="120" r="7"/><circle cx="490" cy="160" r="7"/><circle cx="530" cy="160" r="7"/><circle cx="490" cy="200" r="7"/><circle cx="530" cy="200" r="7"/><circle cx="490" cy="240" r="7"/><circle cx="530" cy="240" r="7"/><circle cx="490" cy="280" r="7"/><circle cx="530" cy="280" r="7"/>
</g>
<g stroke="#d97706" stroke-width="3.5" fill="none">
<line x1="130" y1="200" x2="322" y2="44"/><line x1="322" y1="44" x2="510" y2="200"/><line x1="510" y1="200" x2="130" y2="200"/>
</g>
<circle cx="130" cy="200" r="9" fill="#d97706"/><circle cx="322" cy="44" r="9" fill="#d97706"/><circle cx="510" cy="200" r="9" fill="#d97706"/>
<text x="130" y="322" font-size="13" fill="#374151" text-anchor="middle">n sommets</text>
<text x="510" y="322" font-size="13" fill="#374151" text-anchor="middle">n sommets</text>
<text x="320" y="352" font-size="12.5" fill="#b45309" text-anchor="middle">un triangle trouvé vite — le seul calcul qui compte vraiment</text>
</svg>
*L'idée centrale : trouver vite des triangles dans des graphes « bancals », deux côtés énormes et le troisième minuscule. Des réductions connues transmettent ce gain à 3SUM et aux plus courts chemins.*

En clair : les anciens algorithmes faisaient du travail dont personne n'avait besoin. Le nouveau refuse de le faire.

Le plus mémorable n'est pas l'exposant, c'est la découverte : l'article crédite l'algorithme central, en toutes lettres, à « Claude, an AI model developed by Anthropic ». Un employé avait lancé un modèle de recherche interne sur des problèmes ouverts de cryptographie — des constructions dont la sécurité repose sur la difficulté en moyenne d'un problème de clique voisin — pour les vérifier et les renforcer. Claude a préféré trouver un algorithme qui affaiblit l'hypothèse : d'abord le cas moyen, puis le pire cas. Seize millions de tokens, zéro intervention humaine.

En septembre, Anthropic a transmis l'algorithme aux auteurs sous accord de confidentialité, avec compensation et accès au Claude public. Les humains ont compris, simplifié, renforcé, étendu — la version en structure de données et le lien avec les conjectures matrice-vecteur leur appartiennent — et assument l'article. Puis un autre modèle interne a certifié les principaux résultats en Lean 4 avec Mathlib, formalisation publiée sur GitHub. Une machine a trouvé le théorème ; un compilateur l'a vérifié.

Cela couronne un trimestre remarquable pour les mathématiques machine chez Anthropic : borne de Riemann renforcée de 41,6 % à 67,2 % en août, puis formalisation Lean complète du dernier théorème de Fermat en onze jours en septembre — 13 millions de lignes. Mais c'était vérifier des vérités connues. Ici, c'est une découverte : la première fois qu'un système d'IA trouve un algorithme vraiment nouveau pour un problème de manuel, ensuite vérifié et étendu par des experts humains.

L'angle que la plupart rateront : Claude, embauché comme auditeur de sécurité, est revenu en perceur de coffres. Les hypothèses de difficulté de la cryptographie — murs porteurs de la sécurité numérique — sont exactement ces conjectures nettes et vérifiables par machine que des agents infatigables peuvent auditer à grande échelle. Le premier audit sérieux vient déjà de fissurer deux exposants de manuel. Attendez-vous à d'autres audits. La vraie question n'est pas de savoir si les machines trouveront d'autres fissures, mais lesquels de nos problèmes « notoirement difficiles » survivront à l'inspection — et ce que nous ferons de ceux qui cèdent.

Un second basculement se cache dans la méthode : produire des idées coûte peu — seize millions de tokens, zéro humain, une percée ; ce qui est rare, c'est la vérification — compréhension humaine plus compilateur inbluffable. Les mathématiques ont toujours été un dialogue entre deviner et vérifier. Deviner vient d'être automatisé. Vérifier, non. Cette asymétrie définira la décennie à venir du domaine.

Mise en garde : prépublication de deux jours, à peine lue par les experts. Lean couvre les principaux résultats déterministes ; les bornes randomisées sur les réels reposent sur le seul article. Exposants annoncés, pas canoniques — mais c'est un compilateur, pas un rapporteur, qui a validé le cœur. Le billet de réaction du théoricien de la complexité Mahdi Cheraghchi a dépassé 430 000 vues en un jour : le domaine regarde.

**Si le premier audit machine d'une hypothèse de difficulté a brisé deux hypothèses par accident, vers quel problème « notoirement difficile » diriger la prochaine session de seize millions de tokens — et sommes-nous prêts pour ce qu'elle rapportera ?**

*Sources : [Alman &amp; Vassilevska Williams, arXiv 2610.06783](https://arxiv.org/abs/2610.06783v1) · [texte intégral](https://arxiv.org/html/2610.06783v1) · [lecture détaillée de CellCog](https://cellcog.ai/blog/claude-3sum-apsp-algorithm/)*
