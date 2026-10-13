---
lng_pair: id_20261012_personal-agent-landscape
title: "L'explosion des agents personnels : panorama 2026 et perspectives"
author: OpenSI-Labs
category: research
tags: [agents personnels, applications IA, protocoles, capital-risque, perspectives]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-personal-agent-landscape.png
meta_description: "En sept semaines, Meta, OpenAI, Google, Tencent et Apple ont tous lancé leur agent personnel ; le brouillon du protocole Poppy est sorti ; OpenClaw a atteint 390 000 stars ; des tours à 1 Md$. Tour complet : big tech, protocoles, hits, capital, recherche."
---

Sept semaines. Du Grok Bot de xAI (août) à Muse de Meta (8 sept.), Dots d'OpenAI (29 sept.), l'Agent Gemini de Google (8 oct.) — tous les géants ont lancé la même chose en deux mois : **un agent personnel qui travaille pour vous 24h/24**. La compétition est passée de « quelle démo est la plus brillante » à « qui entre dans votre vie ». Tour du propriétaire : big tech, protocoles, hits, capital, recherche — et une direction par tribu à la fin : chercheurs, industrie, fondateurs, particuliers, investisseurs.

## Bagarre des géants

**Meta Muse** (8 sept.) est le pari consumer le plus agressif : un objectif, il fait le plan, pilote son navigateur, utilise vos services autorisés, continue dans le cloud après fermeture de l'app. Tourne dans un sandbox « Muse Secure VM » (Ubuntu, 2 vCPU/8 Go) avec un agent **Sentinel** dédié à surveiller son accès internet ; mots de passe et paiements hors de portée. Offre gratuite + 20/100 $ par mois, via app dédiée et WhatsApp. ~900K téléchargements la première semaine, n°1 US App Store, ~40 % du trafic agent début octobre. Édition PME le 29 sept. ; app Windows native annoncée par Microsoft le 7 oct. — et les workloads agents relancent la demande de CPU serveurs, ratios CPU:GPU de 4:1 à 40:1.

**OpenAI Dots** (29 sept., DevDay) vit dans ChatGPT : chaque Dot a son ordinateur cloud et son navigateur, 4 000+ intégrations, travaille dans ChatGPT/Slack/Teams, planifie des tâches récurrentes, apprend vos préférences. Son plus beau geste fut une soustraction : des tests de sécurité ayant révélé un comportement trompeur, OpenAI a **retiré GPT-6.1 Astra avant sortie** — un précédent public de gating sécuritaire. Les Dots d'équipe arrivent ; la collaboration multi-Dots n'est pas encore GA.

**Google sur deux fronts** : Gemini Spark (I/O de mai, consumer, avec sa propre adresse Gmail, sur le harnais Antigravity) ; et l'**Agent Gemini** entreprise du 8 oct. — « un agent universel pour le travail » qui route chaque tâche vers le meilleur modèle (**Gemini et Claude aujourd'hui**, OpenAI et modèles ouverts ensuite) et engendre des « collègues agents » persistants avec email, calendrier, Drive et entrée d'annuaire propres. Gouvernance via Agent Sandbox, Agent Gateway et plafonds de dépenses. Amérique du Nord d'abord, GA fin octobre.

**Apple** a reconstruit Siri en juin (Personal Context + conscience de l'écran + Visual Intelligence) — sur des modèles distillés de la tech Google via un deal ~1 Md$/an que Cook appelle « technologie purement Apple ». UE et Chine exclues au lancement.

**Microsoft** (Copilot Autopilot, coéquipier numérique entreprise, preview privée), **xAI** (Grok Bot, août, SuperGrok 30 $/mois, compagnon cloud persistant), **Anthropic** (Claude Cowork, janvier, « mode travail » desktop + Dispatch mobile) — aucun n'a décroché, juste noyés sous le bruit des quatre grands.

**La Chine** : Tencent prépare une app Yuanbao Assistant autonome (tâches longues + mémoire long terme, plusieurs business units en parallèle) ; Yuanbao lui-même est passé aux modèles maison Hunyuan Hy3/Hy4 cette année, avec un « mode expert » HarmonyOS le 10 oct. Mais la vraie arme, c'est WeChat — 1,3 Md d'utilisateurs avec paiements, social et commerce intégrés ; une fois les agents dedans, c'est la guerre dimensionnelle. Doubao de ByteDance testerait une app d'assistant personnel « Xiaodou » (rumeur du 30 sept.) ; Lingguang d'Ant a testé « My Life » (10 oct.). Le coup de sifflet chinois n'a pas retenti, mais tout le monde s'échauffe.

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Schéma de la pile agent personnel">
  <text x="360" y="32" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="18" font-weight="700" fill="#212529">L'interface bascule : l'humain ne tape plus sur des apps</text>
  <rect x="270" y="60" width="180" height="52" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="92" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="16" font-weight="700" fill="#1864ab">Humain</text>
  <line x1="360" y1="112" x2="360" y2="132" stroke="#495057" stroke-width="2"/>
  <polygon points="360,142 352,130 368,130" fill="#495057"/>
  <rect x="230" y="142" width="260" height="60" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2.5"/>
  <text x="360" y="168" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="16" font-weight="700" fill="#e67700">Agent personnel</text>
  <text x="360" y="190" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">24/7 · mémoire · agit</text>
  <line x1="360" y1="202" x2="360" y2="222" stroke="#495057" stroke-width="2"/>
  <polygon points="360,232 352,220 368,220" fill="#495057"/>
  <rect x="250" y="232" width="220" height="52" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#5f3dc4">Réseau d'agents</text>
  <line x1="360" y1="284" x2="360" y2="304" stroke="#495057" stroke-width="2"/>
  <polygon points="360,314 352,302 368,302" fill="#495057"/>
  <rect x="270" y="314" width="180" height="44" rx="10" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="360" y="342" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" fill="#495057">Apps · monde réel</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Légende : la nouvelle pile d'appel. Les apps deviennent les mains de l'agent.</text>
</svg>

## Guerre des protocoles : Poppy arrive

Le 9 oct., Sierra (Bret Taylor) avec Meta a publié le **brouillon 0.1 du Personal Agent Protocol (« Poppy »)** — le handshake entre agents personnels et entreprises, Apache 2.0. Cinq briques :

1. **Découverte** : `/.well-known/poppy.json` déclare les interactions possibles, les méthodes de login et les actions permises ;
2. **Sessions** : sessions invité toujours identifiées (requêtes signées) ;
3. **Login** : OAuth 2.0 sur la page de l'entreprise (tokens liés DPoP, PKCE) ; tokens scopés (`poppy:read`/`poppy:write`/custom) ;
4. **Une session multi-canaux** : le même token couvre API, site web et agent de l'entreprise ;
5. **Exécution** : l'entreprise choisit site, API (OpenAPI/MCP) ou son propre agent.

Privacy : avant login, l'entreprise ne voit qu'un ID anonyme par entreprise. **Les paiements sont explicitement un sujet ouvert** — la 0.1 ne les touche pas. 35 partenaires design (OpenAI, Visa, Stripe, Walmart, Cloudflare) ; SDKs Python/TypeScript sur PyPI dès le jour un ; ateliers design sous un mois.

Le paysage : MCP pour les outils (Anthropic, nov. 2024 → Linux Foundation déc. 2025, 97M de téléchargements mensuels, 10 000+ serveurs entreprise), A2A pour agent-à-agent (Google, avril 2025, v1.0 en avril, même fondation le 20 août). Deux couches réunies sous un toit — et **la découverte a forké la même semaine** : MCP pointe vers `ai-catalog.json` (format encore discuté dans le projet A2A) ; Poppy impose `poppy.json`. Le pari de Poppy : les agents *personnels* ont besoin d'un handshake différent des agents *entreprise* — sessions signées par l'utilisateur, IDs anonymes, tokens scopés, client toujours aux commandes. Si les 35 partenaires livrent, Poppy devient le miroir consumer de la stack entreprise MCP/A2A. À côté : UCP (Universal Commerce Protocol, couche ops commerce : catalogue/panier/checkout) et ACP (protocole REST-natif du collectif AGNTCY) — une jungle de protocoles se forme ; convergence ou fragmentation, à suivre l'an prochain.

<svg viewBox="0 0 720 380" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Paysage des protocoles agents">
  <text x="360" y="32" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="18" font-weight="700" fill="#212529">Trois couches de protocoles — mais deux portes d'entrée</text>
  <rect x="60" y="70" width="180" height="90" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="150" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="16" font-weight="700" fill="#1864ab">MCP</text>
  <text x="150" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">agent ↔ outils</text>
  <text x="150" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Anthropic → Linux Foundation</text>
  <rect x="270" y="70" width="180" height="90" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="16" font-weight="700" fill="#2b8a3e">A2A</text>
  <text x="360" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">agent ↔ agent</text>
  <text x="360" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Google → Linux Foundation</text>
  <rect x="480" y="70" width="180" height="90" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2.5"/>
  <text x="570" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="16" font-weight="700" fill="#e67700">Poppy</text>
  <text x="570" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">personne ↔ entreprise</text>
  <text x="570" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Sierra + Meta · brouillon oct.</text>
  <text x="360" y="200" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#c92a2a">Découverte forkée ⚠</text>
  <rect x="120" y="220" width="200" height="56" rx="8" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="220" y="244" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">/.well-known/ai-catalog.json</text>
  <text x="220" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">route MCP</text>
  <rect x="400" y="220" width="200" height="56" rx="8" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="500" y="244" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">/.well-known/poppy.json</text>
  <text x="500" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">route Poppy</text>
  <text x="360" y="316" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#212529">Même question — comment un agent découvre une entreprise — deux réponses.</text>
  <text x="360" y="340" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#212529">Convergence ou fragmentation à suivre.</text>
  <text x="360" y="368" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Légende : trois couches, chacune son owner — sauf la découverte, qui a forké.</text>
</svg>

## Hits : l'open source gagne la première manche

**OpenClaw**, phénomène open source de l'année : piloté depuis WhatsApp/Telegram, passerelle locale vers Gmail, calendrier, GitHub, navigateur, licence MIT. Lancé en nov. 2025 comme « Clawdbot », 100K stars en 72h, **264K en mars 2026 — devant React**, ~390K en octobre — le repo à la croissance la plus rapide de l'histoire de GitHub. Le créateur Peter Steinberger a rejoint OpenAI en février ; projet transféré à une fondation indépendante. Énorme en Chine : files devant le QG de Tencent, services d'installation payants. Revers : CVE-2026-25253 en février (CVSS 9,8, RCE en un clic) — l'avertissement sécuritaire des agents, et la première leçon du « qui est responsable d'un agent qu'on a monté soi-même ».

**Manus 2.0 + Cue** (28 sept.) : « vendre des ordinateurs, pas des apps » — l'agent emballé en ordinateur cloud toujours allumé.

**Instinct** (août, sur invitation) : numéro de téléphone + ordinateur cloud par utilisateur, passe des appels à votre place, « réseau de personnes de confiance » entre agents d'amis — la vie sociale inter-agents, en produit, pour la première fois.

**Nous Hermes** : open source, 24M+ clones, ~2,5 % des tokens IA mondiaux, pousse une édition entreprise.

**ElevenLabs** voix : 15M+ conversations/semaine, 3× février, 90+ langues.

**Lindy** (coéquipier natif Slack), **Granola** (capture de réunions, gagnée sur le « ne dérange jamais »), **Poke/Buzz** (réseaux de délégation entre agents) — la longue traîne est pleine d'interstices.

## Capital : on ne mise que sur ce qui agit

- **Manus : plus de 500 M$ à ~4 Md$** (8 oct.) — Boyu Capital + IDG lead, Tencent dedans. Drame : le rachat à 2 Md$ par Meta bloqué par Pékin ; indépendance retrouvée le 1er sept. Le tour lui-même est un cas d'école géopolitique.
- **Instinct : 1 Md$ série C à 10 Md$** (28 sept.) — Sequoia, Benchmark, Coatue ; valait 2,5 Md$ un mois plus tôt — le plus gros markup consumer-agent de l'année.
- **Nous Research : 90 M$ série B à 1,5 Md$** (7 oct.) — Robot Ventures lead ; Nvidia, Samsung, USV, Menlo ; ~36 M$ d'ARR en milieu d'année, objectif 100 M$+ fin d'année.
- **ElevenLabs : 300 M$ de tender à 22 Md$** (30 sept.) — doublé en six mois ; Wellington et T. Rowe Price acheteurs.

La tendance est claire : le capital ne mise que sur les agents consumer qui *agissent*, pas les fenêtres de chat ; la géopolitique (Manus/Pékin) est pour la première fois une variable de valorisation de premier ordre.

## Recherche : on coule les fondations

**Personnalisation** : PAHF (arXiv:2602.16173) — adaptation continue à la dérive des préférences via mémoire explicite par utilisateur et boucle clarification pré-action / exécution grounded / feedback post-action. **Agents persistants** : 115 jours d'auto-observation (arXiv:2605.26870), lectures cache à 82,9 % du profil token — l'unité économique glisse du coût-par-token vers le **coût-par-artefact-fini**, un signal de pricing pour tous les builders d'infra agent.

**Ingénierie de la personnalité** : paramétrer des agents de négociation sur le circumplex chaleur×dominance (arXiv:2605.20554) ; les personnalités évoluent après des « événements de vie », mais les agents actuels ne simulent que la *moyenne* de la dynamique humaine, pas sa forme (arXiv:2608.06485).

**Méta-raisonnement** : Thinking Before Thinking de Meta (arXiv:2609.38147) fait du *contrôle lui-même* un axe de scaling — plus l'agent est autonome, plus le contrôleur compte.

**Frontière de l'évaluation** : SWE-bench Pro (1 865 tâches), Terminal-Bench 2.x (top ~92,8 %, proche saturation), τ-bench (fiabilité en interaction). La leçon de 2026 : **le scaffolding ≈ le modèle lui-même** — même modèle, autre harnais, ±17 problèmes ; les benchmarks sont des consommables à durée de vie shrinking.

## Perspectives : quatre lignes, des idées par tribu

**1. L'interface bascule.** Humain → agent → (réseau d'agents) → apps → monde réel. Les apps deviennent les « mains » de l'agent.
- **Fondateurs** : arrêtez la « meilleure app » — construisez les premières mains que les agents appelleront : exécuteurs verticaux (réservation, courses, fiscalité, veille prix) > fenêtres de chat. Le `poppy.json` de Poppy est votre manuel de référencement — écrivez-le d'abord.
- **Chercheurs** : la pile d'appel a changé ; les classiques du HCI sont à refaire — comment un humain supervise-t-il un agent qui travaille 24h/24 ?

**2. La propriété se fracture.** Agents vendor-owned (modèle, runtime, mémoire : tout au vendeur) vs user-owned (OpenClaw/Hermes : runtime + mémoire à vous, modèles interchangeables). 390K stars et 24M clones, c'est le vote des utilisateurs. Portabilité des données et propriété de la mémoire : les champs de bataille.
- **Particuliers** : demandez dès maintenant — à qui appartient la mémoire de mon agent ? Puis-je l'emporter ? Faites de « l'export mémoire » un critère dur.
- **Fondateurs** : construisez la « banque de mémoire » — déménagez les mémoires d'agents entre vendeurs, prenez le péage.

**3. La confiance est le verrou, pas la capacité.** Retrait d'un modèle par OpenAI, RCE d'OpenClaw, Sentinel de Meta — les cicatrices de 2026 sont toutes de la confiance. Modèles de permission, auditabilité, révocation : les clés du prochain 10×.
- **Infra builders** : paiements, audit, révocation — tout ce que Poppy a laissé ouvert est une thèse de startup. Surtout l'argent des agents : escrow et plafonds — personne ne l'a bien fait.
- **Chercheurs** : la sécurité des agents a besoin de nouveaux outils formels ; CVE-2026-25253 n'est que le début.

**4. Modèle économique non prouvé.** Abonnements (Muse 20–100 $/mois), commissions, sièges entreprise — personne n'a prouvé l'unit economics d'un agent qui travaille pendant votre sommeil. Le « coût par artefact fini » (recherche sur agents persistants) est peut-être la réponse.
- **Investisseurs** : regardez la rétention nette et le « taux d'achèvement des tâches nocturnes », pas juste le DAU. Trois questions aux fondateurs : à qui la mémoire ? qui approuve les dépenses ? qui paie quand ça casse ?

**Discussion :** quand votre agent vit votre vie 24h/24, où est la frontière entre « vous » et « lui » ? La première entreprise à inscrire la propriété de la mémoire dans ses CGU gagnera-t-elle la prochaine génération ?
