---
lng_pair: id_20261012_sakana-mass-self-improvement
title: "MASS : le modèle 27B qui s'est organisé en équipe de recherche"
author: OpenSI-Labs
category: research
tags: [auto-amélioration récursive, systèmes multi-agents, Sakana AI, auto-supervision, optimisation de workflows]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-sakana-mass-self-improvement.png
meta_description: "Avec MASS, Sakana AI fait jouer à un seul modèle 27B les rôles de solveur, d'optimiseur et d'évaluateur dans sa propre boucle d'amélioration — et découvre que le goulot, c'est l'optimiseur, pas le juge."
---

Le problème de la supervision de l'IA frontière ressemble à de la philosophie jusqu'au moment où il devient de l'ingénierie. Imaginez que votre modèle soit un scientifique compétent, et que vous vouliez en faire un meilleur. Vous lui confiez une tâche de recherche ouverte — pas de réponse attendue, pas de tests unitaires, aucun humain capable de distinguer de façon fiable le bon de l'excellent. De quel signal apprend-il ? Sur exactement les tâches où l'on attend le plus de l'IA, le modèle s'approche déjà des limites de ce qu'un humain peut évaluer. Ce goulot de la supervision n'est plus hypothétique.

La réponse de Sakana AI, publiée ce week-end avec des chercheurs de UC Berkeley ([article](https://arxiv.org/abs/2610.12176), [billet officiel](https://pub.sakana.ai/mass/)), s'appelle MASS — Multi-Agent Self-Supervision. Si personne ne peut superviser le modèle de l'extérieur, qu'il s'organise en équipe et apprenne de la façon dont ses propres équipes travaillent.

Le mécanisme tient en un paragraphe. Un seul modèle partagé de 27 milliards de paramètres (Qwen3.6-27B, poids ouverts) joue trois rôles dans une boucle qu'il pilote lui-même : le solveur de tâches (l'« optimisé »), l'optimiseur de workflows et l'évaluateur. C'est l'auto-amélioration récursive *homogène* : un modèle, tous les postes. Pourquoi des équipes ? Parce qu'une instance unique peine à critiquer et améliorer son propre raisonnement complexe dans une boucle homogène — mais les premiers résultats montrent que les topologies multi-agents s'en sortent mieux sur le raisonnement complexe, alors le modèle recrute des copies de lui-même pour dépasser ses propres limites.

La boucle interne cherche un meilleur travail d'équipe, poids figés. Le modèle rédige un workflow : un plan écrit qui répartit une tâche de recherche entre des sous-agents virtuels — les instructions de chaque rôle, les contrats sur ce que chacun doit livrer, l'ordre des appels. Un orchestrateur l'exécute, l'évaluateur compare le résultat au champion, l'optimiseur propose un workflow révisé — recherche évolutionnaire sous garde-fous structurels.

<figure>
<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<defs><marker id="marrow" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#3366cc"/></marker></defs>
<rect x="230" y="10" width="180" height="52" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="320" y="32" font-size="14" font-weight="bold" text-anchor="middle">Modèle partagé</text>
<text x="320" y="50" font-size="12" text-anchor="middle">Qwen3.6-27B, poids ouverts</text>
<rect x="40" y="110" width="270" height="150" rx="12" fill="#f7f9ff" stroke="#3366cc" stroke-width="2"/>
<text x="175" y="134" font-size="14" font-weight="bold" text-anchor="middle">Boucle interne : recherche</text>
<text x="175" y="156" font-size="12" text-anchor="middle">workflows = rôles · instructions ·</text>
<text x="175" y="172" font-size="12" text-anchor="middle">contrats · ordre d'appels</text>
<text x="175" y="196" font-size="12" text-anchor="middle">exécuter → évaluer vs champion →</text>
<text x="175" y="212" font-size="12" text-anchor="middle">l'optimiseur révise le workflow</text>
<text x="175" y="236" font-size="12" font-style="italic" text-anchor="middle">poids figés</text>
<rect x="330" y="110" width="270" height="150" rx="12" fill="#fff8ee" stroke="#cc8833" stroke-width="2"/>
<text x="465" y="134" font-size="14" font-weight="bold" text-anchor="middle">Boucle externe : distillation</text>
<text x="465" y="156" font-size="12" text-anchor="middle">workflow champion × 18 essais / tâche</text>
<text x="465" y="172" font-size="12" text-anchor="middle">auto-classement Bradley-Terry ;</text>
<text x="465" y="188" font-size="12" text-anchor="middle">16 meilleures trajectoires gardées</text>
<text x="465" y="212" font-size="12" text-anchor="middle">échafaudage retiré → fine-tuning LoRA</text>
<text x="465" y="236" font-size="12" font-style="italic" text-anchor="middle">les poids changent ici</text>
<line x1="250" y1="62" x2="178" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="390" y1="62" x2="462" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="310" y1="185" x2="328" y2="185" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<text x="292" y="178" font-size="11" text-anchor="middle">champion</text>
<line x1="606" y1="160" x2="606" y2="36" stroke="#cc8833" stroke-width="2"/>
<line x1="606" y1="36" x2="412" y2="36" stroke="#cc8833" stroke-width="2" marker-end="url(#marrow)"/>
<text x="508" y="28" font-size="11" text-anchor="middle">le modèle reprend ses trois rôles</text>
</svg>
<figcaption>La boucle interne cherche un meilleur travail d'équipe ; la boucle externe replie le meilleur travail d'équipe dans les poids du modèle.</figcaption>
</figure>

La boucle externe, c'est là que la boucle se nourrit d'elle-même. Le workflow champion est exécuté 18 fois par tâche, les espaces de travail auto-classés par score Bradley-Terry, et seules les 16 meilleures trajectoires survivent. Leur échafaudage de workflow est retiré des prompts, et le modèle partagé est fine-tuné dessus avec LoRA. Le modèle mis à jour reprend alors ses trois rôles — meilleur optimiseur, meilleur évaluateur — et le cycle recommence. Après deux cycles complets, le modèle atteint 1,2 à 1,6 fois le niveau du modèle de base en score par token de sortie sur quatre benchmarks de recherche (1,60× sur MLR-Bench, 1,35× sur DSBench, 1,28× sur AstaBench, 1,20× sur ScienceAgentBench), avec un taux de victoire contre le modèle intact passé de 53,9 % à 69,9 %. Le signal est aussi plus dense : un élève entraîné sur ces trajectoires égale le mono-agent avec 31 % de tokens supervisés en moins (28,8M contre 42M).

Voici la partie que la plupart des couvertures passeront sous silence — les échecs honnêtes. Sur SWE-bench Verified et Terminal-Bench 2.0, tous deux très orientés code, le même système *recule* à 0,94× et 0,96× du niveau de base. MASS n'a pas rendu le modèle globalement plus intelligent. Il en a fait un meilleur chercheur, au prix mesurable d'un moins bon codeur.

<figure>
<svg viewBox="0 0 640 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<line x1="273" y1="20" x2="273" y2="240" stroke="#999" stroke-width="1.5" stroke-dasharray="6,4"/>
<text x="273" y="256" font-size="11" text-anchor="middle" fill="#666">base = 1,0×</text>
<text x="170" y="52" font-size="12" text-anchor="end">MLR-Bench</text>
<rect x="180" y="38" width="280" height="22" rx="4" fill="#3366cc"/><text x="468" y="54" font-size="12">1,60×</text>
<text x="170" y="92" font-size="12" text-anchor="end">DSBench</text>
<rect x="180" y="78" width="165" height="22" rx="4" fill="#3366cc"/><text x="353" y="94" font-size="12">1,35×</text>
<text x="170" y="132" font-size="12" text-anchor="end">AstaBench</text>
<rect x="180" y="118" width="133" height="22" rx="4" fill="#3366cc"/><text x="321" y="134" font-size="12">1,28×</text>
<text x="170" y="172" font-size="12" text-anchor="end">ScienceAgentBench</text>
<rect x="180" y="158" width="95" height="22" rx="4" fill="#3366cc"/><text x="283" y="174" font-size="12">1,20×</text>
<text x="170" y="212" font-size="12" text-anchor="end">SWE-bench Verified</text>
<rect x="180" y="198" width="66" height="22" rx="4" fill="#cc3333"/><text x="254" y="214" font-size="12">0,94×</text>
<text x="320" y="14" font-size="13" font-weight="bold" text-anchor="middle">Score par token de sortie vs modèle de base, après deux cycles MASS</text>
</svg>
<figcaption>L'amélioration est directionnelle : le modèle est devenu un meilleur chercheur — et un codeur légèrement moins bon.</figcaption>
</figure>

Cette asymétrie est la vraie histoire. L'auto-amélioration récursive se raconte d'habitude comme une marée montante — un modèle qui devient uniformément plus capable. MASS suggère plutôt un apprentissage : le modèle se spécialise vers ce que sa boucle récompense, et le paie en compétences adjacentes. Un chercheur auto-amélioré qui oublie comment coder n'est pas un paradoxe : c'est le marché ordinaire de tout spécialiste. Si l'auto-amélioration récursive passe à l'échelle, l'avenir ne sera peut-être pas un généraliste divin mais une écologie de spécialistes auto-améliorés, chacun brillant dans le bassin de sa propre récompense et légèrement moins bon partout ailleurs.

Deuxième surprise : elle sape l'autre inquiétude populaire. Tout le monde suppose que la partie dangereuse d'une boucle auto-notée, c'est l'*évaluateur* — un modèle qui corrige sa propre copie va s'auto-absoudre. Les ablations de Sakana montrent l'inverse : améliorer seulement l'évaluateur ne change presque rien, alors qu'améliorer l'*optimiseur* fait bouger les résultats. Dans une boucle auto-améliorée, générer de meilleures stratégies compte plus que bien les juger — le goulot, c'est celui qui propose, pas celui qui critique. Consigne de conception : investir dans la recherche, pas dans la notation.

Et les auteurs nomment leur propre cauchemar, ce qui mérite le respect. Quand un même modèle produit, juge et s'entraîne sur les résultats, un angle mort partagé peut être « produit, accepté comme une amélioration, puis intégré au modèle suivant » — leurs mots, qu'ils appellent le talon d'Achille de l'auto-amélioration récursive. Signal épistémique : pour *mesurer* le progrès, il a fallu des juges extérieurs (GPT-5.5, Claude Opus 4.8) dont les verdicts n'entrent jamais dans la boucle. Une boucle vraiment fermée n'aurait aucun moyen de savoir qu'elle s'améliore. MASS ne comble pas ce fossé ; elle construit la meilleure machine possible à l'intérieur.

Code sur GitHub, article ouvert. MASS n'est pas l'explosion d'intelligence : c'est plus rare — une boucle auto-améliorée qui fonctionne, mesurée, et qui dit exactement où elle a progressé, régressé, et quelle pièce la freinait.

**Discussion :** si l'auto-amélioration récursive spécialise inévitablement les modèles vers les tâches que leurs boucles récompensent, qui décide quelles tâches méritent une boucle auto-améliorée — et quelles compétences on accepte que le modèle perde ?
