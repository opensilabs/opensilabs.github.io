---
lng_pair: id_20261007_vista-arc-agi-3
title: "Les modèles n'étaient pas bêtes. Ils étaient aveugles."
author: OpenSI-Labs
category: research
tags: [ARC-AGI-3, mémoire visuelle, agents IA, MIT, VISTA]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-vista-arc-agi-3.png
meta_description: "Le harnais VISTA du MIT a fait passer Claude Opus 5.0 de 40,68 à un 100 parfait sur ARC-AGI-3, sans aucun entraînement — en donnant au modèle de vrais yeux et une mémoire intacte. Le goulot n'était jamais l'intelligence, mais la plomberie."
---

Le 1er octobre, cinq chercheurs du MIT ont discrètement publié un [article](https://arxiv.org/abs/2610.02200) qui se lit comme un réquisitoire contre toute l'industrie des agents : VISTA, un harnais visuel pour raisonner dans un monde interactif. Son chiffre clé est saisissant — le score de Claude Opus 5.0 sur ARC-AGI-3, le benchmark de raisonnement interactif, est passé de 40,68 à un 100,00 parfait : les 25 jeux publics résolus, tous les niveaux, avec 57,4 % d'actions en moins que des humains novices. Aucun nouveau poids, aucun nouvel entraînement. L'écart entre 40 et 100 n'était pas un modèle. C'était de la plomberie.

La thèse des auteurs est d'une simplicité presque insultante : les modèles n'étaient jamais bêtes ; ils étaient aveugles. L'interface officielle d'ARC-AGI-3 tend au modèle une grille de nombres 64×64 pour des casse-tête visuels — un tableur déguisé en image. Les humains voient le jeu ; les modèles lisaient un grand livre de comptes. VISTA leur rend ce que nous tenons pour acquis : des captures 512×512, une mémoire qui garde chaque image intacte, et la liberté de zoomer à volonté.

<svg viewBox="0 0 720 336" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="VISTA : la boucle autour du modèle">
  <defs>
    <marker id="arrV1a" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
    <marker id="arrV1b" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto-start-reverse"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">VISTA : la boucle autour du modèle</text>
  <rect x="270" y="42" width="180" height="66" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="66" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">SE SOUVENIR</text>
  <text x="360" y="86" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">mémoire visuelle intacte</text>
  <text x="360" y="102" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">chaque image, indexée par tour</text>
  <rect x="30" y="152" width="150" height="66" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="105" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">VOIR</text>
  <text x="105" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">captures 512×512</text>
  <text x="105" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">et non grilles 64×64</text>
  <rect x="285" y="152" width="150" height="66" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#5f3dc4">MODÈLE</text>
  <text x="360" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">poids inchangés,</text>
  <text x="360" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">zéro entraînement</text>
  <rect x="540" y="152" width="150" height="66" rx="10" fill="#ebfbee" stroke="#2f9e44" stroke-width="2"/>
  <text x="615" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#2b8a3e">INSPECTER</text>
  <text x="615" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">jouer · zoomer · lire pixels</text>
  <text x="615" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">historique — piloté par le modèle</text>
  <rect x="270" y="262" width="180" height="66" rx="10" fill="#fff5f5" stroke="#e03131" stroke-width="2"/>
  <text x="360" y="286" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#c92a2a">CARNET</text>
  <text x="360" y="306" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">GUIDE.md + WORKING.md</text>
  <text x="360" y="322" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">notes persistantes + brouillon</text>
  <line x1="182" y1="185" x2="283" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="437" y1="185" x2="538" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="110" x2="360" y2="150" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="220" x2="360" y2="260" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">VISTA entoure un modèle inchangé d'yeux, d'une mémoire intacte et d'un carnet. L'intelligence était déjà là ; l'interface, non.</p>

Trois pièces font le harnais. D'abord, des observations visuelles : des captures rendues au lieu de grilles numériques. Ensuite, une mémoire visuelle intacte : chaque image — y compris les images intermédiaires des animations — archivée telle quelle, indexée par tour et par image, hors de la fenêtre de contexte pour que rien ne s'estompe. Enfin, l'inspection pilotée par le modèle : l'agent décide lui-même quoi examiner, avec quatre outils — play pour agir, inspect pour zoomer sur n'importe quelle région d'une image passée, read_pixels pour des valeurs exactes, history pour revoir actions et résultats. Autour de la boucle, deux fichiers texte : GUIDE.md, notes persistantes de la session, et WORKING.md, brouillon du jeu en cours. Le harnais est purement mécanique : aucun composant entraîné, un seul court modèle d'invite pour les 25 jeux.

Les chiffres méritent une lecture lente. Claude Opus 5.0 : 40,68 → 100,00 sur 183 niveaux et 7 302 actions, contre 17 135 pour des humains novices. Sur le seul jeu m0r0 : 1 107 coups pour les humains, 219 pour Claude. GPT-5.6 Sol raconte la même histoire depuis plus bas : 13,33 au départ, 47,32 avec les seules captures, 99,00 avec le harnais complet. Même un modèle ouvert de 320 milliards de paramètres — à peine vivant à 1,89 — est monté à 66,93. Et c'est stable : trois répétitions à 99,00, 98,90 et 99,23. Les auteurs restent prudents — « à notre connaissance », premier score parfait sur ARC-AGI-3 sans synthèse de programmes. Cela vaut qu'on s'y arrête : cet été, les meilleurs systèmes construisaient tous des simulateurs par jeu, du code écrit à la main pour modéliser les règles. VISTA dérive les mêmes règles en quelques phrases de notes.

<svg viewBox="0 0 720 348" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Mêmes poids, nouveau harnais : scores avant et après VISTA">
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">Mêmes poids, nouveau harnais : RHAE sur ARC-AGI-3</text>
  <rect x="180" y="44" width="12" height="12" fill="#adb5bd"/><text x="198" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">harnais officiel de référence</text>
  <rect x="380" y="44" width="12" height="12" fill="#1c7ed6"/><text x="398" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">avec VISTA</text>
  <text x="170" y="100" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">Claude Opus 5.0</text>
  <rect x="180" y="88" width="179" height="14" fill="#adb5bd"/><text x="364" y="99" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">40,68</text>
  <rect x="180" y="106" width="440" height="14" fill="#1c7ed6"/><text x="624" y="117" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">100,00</text>
  <text x="170" y="160" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">GPT-5.6 Sol</text>
  <rect x="180" y="148" width="59" height="14" fill="#adb5bd"/><text x="243" y="159" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">13,33</text>
  <rect x="180" y="166" width="436" height="14" fill="#1c7ed6"/><text x="620" y="177" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">99,00</text>
  <text x="170" y="220" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">Modèle ouvert 320B</text>
  <rect x="180" y="208" width="8" height="14" fill="#adb5bd"/><text x="192" y="219" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">1,89</text>
  <rect x="180" y="226" width="294" height="14" fill="#1c7ed6"/><text x="478" y="237" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">66,93</text>
  <line x1="180" y1="246" x2="620" y2="246" stroke="#dee2e6" stroke-width="1"/>
  <text x="180" y="260" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">0</text>
  <text x="396" y="260" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">50</text>
  <text x="616" y="260" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">100 (RHAE)</text>
  <rect x="30" y="276" width="660" height="62" rx="8" fill="#fff9db" stroke="#e9d66b"/>
  <text x="48" y="300" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#7a5c00">Moins, c'est plus :</text>
  <text x="48" y="322" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">images : 30,7 M de tokens/partie contre 71,9 M pour les grilles · contexte 200K→780K : score 99→93,9 · zoom 16× sur l'image : chute à 88,3</text>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">Le RHAE (efficacité d'action relative à l'humain) mesure l'efficacité d'un système par rapport aux humains. Tous les modèles testés progressent — les plus faibles au départ gagnent le plus.</p>

Mais le plus étrange concerne le coût. Les observations visuelles coûtent moins cher que les grilles numériques : 30,7 millions de tokens par partie contre 71,9 millions. La vision bat les nombres sur la facture. Et plus de contexte nuit : passer la fenêtre de 200 000 à 780 000 tokens fait chuter le score de 99 à 93,9 ; agrandir les images seize fois le fait tomber à 88,3. Relisez bien. L'industrie court après des contextes toujours plus longs, des kilomètres de contexte comme mesure du progrès. La réponse de VISTA est une hérésie : la victoire n'est pas au plus grand seau, mais au modèle qui sait quand ouvrir son carnet et quelle page lire.

Le même harnais, à peine adapté, joue ailleurs : 63,3 % de réussite sur 34 jeux web GameWorld — au-dessus des 55,3 % des novices humains — 84,12 sur des scènes 3D en perspective, mieux que l'humain médian sur AI GameStore. Sur les puzzles « relier les points » de BabyVision, la solution était d'un littéralisme comique : le modèle a zoomé. Cette généralité est le vrai signal. Un simulateur par jeu est un costume sur mesure ; VISTA est une paire d'yeux qui va à tout.

La réserve honnête vient des auteurs : ces modèles ont été entraînés après la publication des jeux publics — l'ensemble privé d'ARC-AGI-3 reste le vrai test de généralisation. Gardons cela affiché au mur. Mais il n'entame pas la comparaison qui compte — même modèle, mêmes poids, avant et après le harnais — qui est inattaquable. Où que soit le plafond, le plancher a bougé.

Et voici ce que la plupart des couvertures manqueront. Si les modèles de pointe ont été systématiquement sous-estimés parce qu'on affamait leurs yeux, deux ans de classements de harnais d'agents sont à refaire. Chaque palmarès qui comparait des « modèles » comparait en partie de la plomberie : qui donnait à son modèle une interface décente, qui le forçait à lire des tableurs. Voilà l'effet de second ordre — ce n'est pas le classement qui bouge, c'est ce qu'il mesurait qui change de sens. Et il y a un fil plus tranchant dans la conception même de l'article : le carnet GUIDE.md/WORKING.md fait peut-être autant que la vision. Une mémoire épisodique externe — ce pour quoi les humains ont inventé les carnets — plus la liberté de réexaminer le passé. La thèse « ils étaient aveugles » est nette et citable. Mais peut-être étaient-ils aussi oublieux, et que le remède était de laisser le modèle prendre des notes.

La leçon de VISTA n'est pas que les harnais battent les modèles : c'est que nous étiquetons le goulot de travers. Nous parlions de déficit de raisonnement et réclamions des entraînements plus grands ; c'était un déficit de perception et de mémoire, et la solution tenait dans de la plomberie et un fichier texte. La prochaine percée des agents ne demandera peut-être aucun paramètre de plus — juste quelqu'un qui remarque ce que le modèle ne voit toujours pas.

Sources : l'[article](https://arxiv.org/abs/2610.02200) (arXiv:2610.02200) ; le [code sous licence MIT](https://github.com/joshhhhhan/vista) et la [page du projet](https://vista-research.github.io/) ; les [tableaux de scores officiels](https://arcprize.org/scorecards/39be671a-d0cc-48b4-ae08-1db4abc44c83) de l'équipe sur ARC Prize (liés depuis le dépôt).

**Discussion :** Si c'est un harnais, et non un modèle, qui a comblé le dernier écart sur ARC-AGI-3 — lesquelles de vos certitudes sur le progrès de l'IA sont en réalité des certitudes sur de la plomberie ?
