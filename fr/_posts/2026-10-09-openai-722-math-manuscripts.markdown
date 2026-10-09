---
lng_pair: id_20261009_openai-722-math-manuscripts
title: "L'accélérateur de particules des mathématiques : les 722 manuscrits d'OpenAI"
author: OpenSI-Labs
category: research
tags: [OpenAI, mathématiques, Lean, démonstration automatique, évaluation de la recherche]
date: 2026-10-09 06:00:00 -0700
img: /assets/img/posts/2026-10-09-openai-722-math-manuscripts.png
meta_description: "OpenAI a publié 722 manuscrits mathématiques écrits par un seul agent IA. La vraie histoire, c'est le pipeline : les benchmarks sont saturés, les problèmes ouverts sont devenus la nouvelle évaluation frontière — et la vérification humaine est devenue le goulot."
---

Le 6 octobre, OpenAI a fait ce qu'aucun éditeur n'avait tenté : déverser l'équivalent d'une année d'un département de mathématiques dans un dépôt GitHub public, en une soirée. Le dépôt [openai/math](https://github.com/openai/math) contient 719 manuscrits en 372 « familles » de résultats (722 annoncés) — tous produits par un modèle interne non publié. Apache-2.0, ~12 800 étoiles en quelques jours, et des affirmations parmi les plus audacieuses jamais attribuées à une machine : une solution à la conjecture de Kakeya en dimension quatre, une région sans zéros élargie pour la fonction zêta de Riemann, la conjecture de Hodge rationnelle pour les variétés abéliennes CM.

Les théorèmes ne sont pas l'histoire. La procédure, si.

## La vraie nouvelle, c'est la procédure

L'immense majorité des résultats vient d'une procédure fixe unique, dit le README. Le modèle s'est vu poser ~4 000 problèmes ouverts ; chaque résultat retenu a coûté en moyenne trois heures de « réflexion ChatGPT Pro » ; les sorties significatives ont été agrégées en familles — résultat principal plus compagnons, conséquences ou preuves alternatives. Un porte-parole a confié à *Scientific American* que le modèle avait « produit la quasi-totalité des résultats en réponse à un seul prompt remis à un seul agent IA ». Un prompt, un agent, 372 familles. Ce ne sont pas 722 programmes indépendants, mais une seule exécution d'agent extrêmement productive — « nous avons étendu ces évaluations après la saturation de nos évaluations mathématiques existantes ». Benchmarks morts comme mesure de la frontière : la nouvelle évaluation n'est pas un jeu de test, c'est la littérature ouverte.

<svg viewBox="0 0 720 560" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Le pipeline de recherche machine : 4 000 problèmes en entrée, 372 familles en sortie">
  <defs>
    <marker id="arrM" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">Le pipeline de recherche machine : 4 000 problèmes en entrée, 372 familles en sortie</text>
  <rect x="255" y="45" width="210" height="56" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="70" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#1864ab">ENV. 4 000 PROBLÈMES OUVERTS</text>
  <text x="360" y="90" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">posés à un seul modèle</text>
  <line x1="360" y1="101" x2="360" y2="116" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="118" width="270" height="56" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="143" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#e67700">UN SEUL AGENT, UN SEUL PROMPT</text>
  <text x="360" y="163" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">~3 heures de réflexion par résultat</text>
  <line x1="360" y1="174" x2="360" y2="189" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="191" width="240" height="56" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="216" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#5f3dc4">FILTRE DE SIGNIFICATIVITÉ</text>
  <text x="360" y="236" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">~18 % retenus, le reste écarté</text>
  <line x1="360" y1="247" x2="360" y2="262" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="255" y="264" width="210" height="56" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="289" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">372 FAMILLES DE RÉSULTATS</text>
  <text x="360" y="309" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">719 manuscrits, 17 disciplines</text>
  <line x1="360" y1="320" x2="360" y2="335" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="337" width="240" height="56" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="362" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#a61e4d">FORMALISATION LEAN</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">~42 % des résultats phares vérifiés par machine</text>
  <line x1="360" y1="393" x2="360" y2="408" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="410" width="270" height="56" rx="10" fill="#f8f9fa" stroke="#868e96" stroke-width="2"/>
  <text x="360" y="435" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#495057">DÉPÔT PUBLIC VERSIONNÉ</text>
  <text x="360" y="455" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Apache-2.0, BibTeX par article, journal des versions</text>
  <text x="360" y="500" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">Deux étapes ont échappé à la procédure fixe : la région sans zéros de la fonction zêta</text>
  <text x="360" y="518" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">de Riemann (rédaction retouchée par un humain) et la preuve de la conjecture de Hodge pour les variétés abéliennes CM.</text>
</svg>
*Figure 1 : le pipeline de publication — un agent, un prompt, deux exceptions humaines.*

Les affirmations ont un poids très variable. Deux ont échappé à la procédure fixe : la région sans zéros de la fonction zêta — Re(s) > 11/12 élargi (l'hypothèse complète exige 1/2), rédaction retouchée par un humain — et la conjecture de Hodge pour les variétés abéliennes CM, en toutes dimensions et codimensions. Dix résumés de raisonnement : exposant d'irrationalité de π, conjectures de Mahler, Kaplansky en caractéristique deux, facteurs de groupes libres, Vlasov–Maxwell en 3D. Les affirmations couvrent 17 disciplines ; l'informatique théorique arrive en tête avec 40 familles.

## Lean est le mur porteur

Le dépôt embarque une bibliothèque Lean — vérification mécanique de chaque pas logique — : ~42 % des résultats phares sont formalisés ; un décompte indépendant trouve 162 manuscrits sur 722 avec un résultat principal vérifié par ordinateur. Une preuve validée par Lean est un nouveau socle de confiance : la correction ne repose plus sur la réputation du laboratoire ni sur l'endurance d'un rapporteur.

Nuance manquée par la plupart des couvertures : une vérification Lean prouve que l'argument découle de ses prémisses — rien sur la nouveauté, l'importance ou l'intérêt du résultat. Vérifié par machine n'est pas relu par les pairs. OpenAI admet que certains résultats non formalisés « pourraient comporter des problèmes », avec des corrections versionnées publiquement — la science avec des notes de version. Et l'avertissement de l'Institute for Advanced Study tient toujours : une IA peut désormais produire des arguments mathématiques « sans que l'humain qui l'a sollicitée puisse comprendre les arguments, les vérifier, ou en assumer la responsabilité ».

Un mois plus tôt, l'annonce selon laquelle ~10 000 agents coordonnés avaient résolu Navier–Stokes en 88 heures avait fait exploser un conflit avec les mathématiciens ; deux douzaines de médaillés Fields ont signé « A Severe Misalignment of AI in Mathematics ». De ce conflit est né le Groupe consultatif IAS sur les mathématiques et l'IA, dont les recommandations du 29 septembre : nommer le modèle, publier les prompts, cesser le marketing mathématique. OpenAI suit la lettre de façon inégale : moyennes au lieu du calcul par problème, dix résumés au lieu de traces complètes, aucun prompt. Un porte-parole a dit à *Scientific American* : l'entreprise prenait les recommandations au sérieux, sans y être « liée ». Andrew Sutherland (MIT) : « Il faut demander des preuves. » Un audit indépendant sur arXiv du lot d'août n'a trouvé aucune erreur mathématique substantielle confirmée dans les résultats examinés.

<svg viewBox="0 0 720 330" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Le gradient de vérification : la production dépasse désormais tout contrôle">
  <defs>
    <marker id="arrV" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#868e96"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">Le gradient de vérification : la production dépasse désormais tout contrôle</text>
  <rect x="30" y="50" width="660" height="44" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="77" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#1864ab">~4 000 problèmes posés au modèle</text>
  <rect x="180" y="106" width="360" height="44" rx="8" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="133" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#2b8a3e">372 familles de résultats publiées (taux de réussite ~18 %)</text>
  <rect x="255" y="162" width="210" height="44" rx="8" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="189" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#e67700">162 avec preuves vérifiées par ordinateur</text>
  <rect x="315" y="218" width="90" height="44" rx="8" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="245" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#a61e4d">relecteurs</text>
  <line x1="360" y1="94" x2="360" y2="104" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="150" x2="360" y2="160" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="206" x2="360" y2="216" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <text x="360" y="292" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">Chaque étage est plus étroit que le précédent. La relecture humaine est le goulot</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">le plus serré — la formalisation Lean est le seul contrôle à bande passante machine.</text>
</svg>
*Figure 2 : le gradient de vérification — la production croît avec le calcul, le contrôle avec les humains.*

## La nouvelle ressource rare

Voici ce qui devrait changer notre regard sur l'IA de pointe — sans rapport avec un théorème particulier. La phrase la plus importante du README porte sur la saturation : benchmarks morts, frontière déplacée vers les problèmes ouverts. Chaque laboratoire affronte le même tournant : quand les jeux de test cessent de discriminer, le seul examen restant, ce sont les questions sans réponse. Conséquence non chiffrée : le renversement du goulot — la ressource rare n'est plus de produire des résultats candidats. Un seul agent a produit 372 familles à trois heures chacune ; la ressource rare, c'est de les absorber. Aucun circuit humain ne lit 722 manuscrits en une semaine. Voilà pourquoi la formalisation Lean, les versions publiques et les BibTeX par manuscrit ne sont pas des accessoires : c'est l'infrastructure éditoriale d'une époque où le laboratoire écrit les articles.

OpenAI l'admet : l'entreprise « explore des dépôts hébergés par la communauté ». Le dépôt d'une seule entreprise ne peut pas être le domicile permanent des mathématiques machines. Il faudra une infrastructure de vérification partagée — bibliothèques de formalisation, services de contrôle, normes de relecture — n'appartenant à aucun laboratoire. Les 722 manuscrits sont une démonstration. L'infrastructure qu'ils exigent est la véritable percée.

Dit franchement : nous ne verrons jamais les 82 %. Le dépôt ne contient que ce qui a franchi la barre ; les problèmes ratés par le modèle sont aussi de la science — ils marquent où se trouve réellement sa frontière. Tant que les laboratoires ne publieront pas ces échecs, chaque déploiement de ce type sera une bande-annonce.

Question : si les mathématiques non résolues sont le benchmark frontière et que les modèles qui passent cet examen sont propriétaires, à qui appartient le pipeline de vérification — et dans combien de temps « généré par machine, vérifié par machine, jamais lu par un humain » deviendra-t-il l'unité normale du progrès mathématique ?

---

*Sources : [le dépôt openai/math d'OpenAI](https://github.com/openai/math) ; [aperçu du dépôt](https://raw.githubusercontent.com/openai/math/main/overview.tex) ; les recommandations du groupe consultatif IAS ; les reportages de Scientific American ; un audit indépendant sur arXiv du lot d'août.*
