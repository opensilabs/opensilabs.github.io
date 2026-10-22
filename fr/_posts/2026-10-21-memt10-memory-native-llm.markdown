---
lng_pair: id_20261021_memt10-memory-native-llm
title: "Le modèle qui cesse de relire son passé"
author: OpenSI-Labs
category: LLMs
tags: [LLMs, memory, architecture, open weights, MemT]
date: 2026-10-21 00:00:00 -0700
img: /assets/img/posts/2026-10-21-memt10-memory-native-llm.png
meta_description: "MemT-1.0 intègre la mémoire dans le calcul même d'un modèle de langage au lieu de rediffuser des contextes toujours plus longs : l'historique se plie en un état fixe, le transcript est jeté."
---

Tous les grands modèles de langage que vous avez utilisés partagent une manie étrange : ils relisent leur propre passé. À chaque tour d'une longue conversation, le transcript entier est réinjecté, et les clés et valeurs de chaque token passé sont réexaminées pour produire le suivant. Le classeur grossit à chaque échange, et la facture — mémoire et délai — avec lui.

Le 19 octobre 2026, l'équipe « MemTensor Team » (74 auteurs) [a publié MemT-1.0](https://arxiv.org/abs/2610.26825) : un « modèle de fondation de la mémoire » — ne plus porter le passé. Le digérer.

## La mémoire au cœur du calcul

MemT-1.0 équipe certains blocs du Transformer d'un **bloc de mémoire natif** qui tourne *en parallèle* de l'attention ordinaire. À la fin de chaque tour, l'historique est plié dans un état mémoire borné, par mises à jour token-par-token — puis le transcript en texte brut est jeté. La taille de l'état persistant est fixe : elle ne croît pas avec les tours.

Provocation à prendre au sérieux : le raisonnement fut d'abord un échafaudage externe avant d'être intériorisé (l'arc DeepSeek-R1) ; la multimodalité a suivi. MemT-1.0 soutient que la mémoire est la prochaine : non pas « combien de contexte rediffuser », mais « la mémoire peut-elle devenir le calcul lui-même ? »

Le mécanisme vient des recherches [Gated DeltaNet-2](https://arxiv.org/abs/2605.22791) de NVIDIA. Par token, trois opérations : **effacer** ce que l'état prédit déjà, **écrire** le résidu — seule l'information nouvelle — et **oublier** selon une décroissance apprise. Effacement et écriture sont découplés.

<svg viewBox="0 0 720 430" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Comment fonctionne le bloc de mémoire natif : chaque token déclenche des mises à jour effacer, écrire et oublier sur un état mémoire fixe, en parallèle de l'attention.">
  <defs>
    <marker id="ef1a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="414" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">Un bloc de mémoire, parallèle à l'attention</text>

  <rect x="24" y="64" width="196" height="180" rx="10" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="122" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">Attention classique</text>
  <text x="122" y="122" text-anchor="middle" font-size="14" fill="#3d4f68">relit tout le cache KV</text>
  <rect x="52" y="140" width="140" height="66" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="122" y="166" text-anchor="middle" font-size="14" fill="#8a4b4b">l'armoire grandit</text>
  <text x="122" y="190" text-anchor="middle" font-size="14" fill="#8a4b4b">état O(N)</text>

  <rect x="262" y="64" width="196" height="180" rx="10" fill="#f6f3fb" stroke="#7b5fc8" stroke-width="2"/>
  <text x="360" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#3b2c66">Bloc de mémoire natif</text>
  <text x="360" y="122" text-anchor="middle" font-size="14" fill="#4c3d7d">effacer &#8594; écrire &#8594; oublier</text>
  <rect x="292" y="140" width="136" height="66" rx="6" fill="#ffffff" stroke="#7b5fc8" stroke-width="1.5"/>
  <text x="360" y="166" text-anchor="middle" font-size="14" fill="#4c3d7d">l'état reste fixe</text>
  <text x="360" y="190" text-anchor="middle" font-size="14" fill="#4c3d7d">état O(1)</text>

  <rect x="500" y="64" width="196" height="180" rx="10" fill="#f3faf3" stroke="#4e7d4e" stroke-width="2"/>
  <text x="598" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c442c">Sortie</text>
  <text x="598" y="122" text-anchor="middle" font-size="14" fill="#33502f">sortie attention</text>
  <text x="598" y="146" text-anchor="middle" font-size="14" font-weight="bold" fill="#2c442c">+</text>
  <text x="598" y="170" text-anchor="middle" font-size="14" fill="#33502f">sortie mémoire</text>
  <text x="598" y="200" text-anchor="middle" font-size="14" font-style="italic" fill="#33502f">additionnées</text>

  <line x1="224" y1="150" x2="256" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#ef1a)"/>
  <line x1="462" y1="150" x2="494" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#ef1a)"/>

  <rect x="24" y="268" width="672" height="120" rx="10" fill="#fff8ec" stroke="#c9962e" stroke-width="2"/>
  <text x="360" y="298" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c4210">À chaque token, chaque tour : digérer le passé, jeter le transcript</text>
  <text x="360" y="330" text-anchor="middle" font-size="14" fill="#6b5423">fin du tour &#8594; historique plié dans l'état mémoire &#8594; texte écarté</text>
  <text x="360" y="360" text-anchor="middle" font-size="14" font-weight="bold" fill="#3a3226">ablation : granularité token (&#8722;5,99) compte plus que la règle d'écriture (&#8722;0,25)</text>
</svg>
Fig. 1 : le bloc de mémoire natif de MemT-1.0 tourne à côté de l'attention ordinaire ; chaque token efface ce que l'état prédit déjà, n'écrit que le résidu, et l'état ne grandit jamais.

L'ablation est l'enseignement clé : passer d'une granularité token à une granularité tour coûte 5,99 points — mais changer de règle de mise à jour ne coûte que 0,25. **Le moment de l'écriture compte plus que la façon d'écrire.**

## Les chiffres, étiquetés honnêtement

Deux variantes : **Nano** (36B / 3B actifs, état de 10M d'éléments, sur Qwen3.6-35B-A3B ; poids Apache-2.0) et **Flash** (288B / 17B actifs, état de 336M, sur DeepSeek-V4-Flash ; poids MIT). Le code est sous licence non commerciale — l'ouverture est à couches.

Sur 11 benchmarks, Flash affiche **50,60**, Nano **46,97** — +12,5 et +8,9 devant la meilleure base paramétrique. À 128K tokens, le stockage est ~66 fois inférieur au cache KV, le premier token 2,44 fois plus rapide (4,19 fois à 256K), plat à ~104–112 ms.

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Contraste : les modèles classiques rediffusent un transcript croissant à chaque tour, tandis que MemT-1.0 plie l'historique dans un état mémoire fixe et jette le transcript.">
  <defs>
    <marker id="ef2a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="384" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">Cessez de rediffuser le passé</text>

  <rect x="24" y="60" width="326" height="312" rx="10" fill="#faf0f0" stroke="#b07a7a" stroke-width="2"/>
  <text x="187" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c2c2c">LLM classique : porter le passé</text>
  <rect x="52" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="130" text-anchor="middle" font-size="14" fill="#5c2c2c">tour 1 &#183; tour 2 &#183; tour 3 &#183; ...</text>
  <rect x="52" y="152" width="270" height="54" rx="6" fill="#f3d9d9" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="174" text-anchor="middle" font-size="14" fill="#5c2c2c">le cache KV grandit O(N)</text>
  <text x="187" y="196" text-anchor="middle" font-size="14" fill="#5c2c2c">chaque token relu</text>
  <text x="187" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#8a2f2f">stockage + latence croissent</text>
  <text x="187" y="268" text-anchor="middle" font-size="14" fill="#5c2c2c">TTFT : 257ms @128K &#8594; 445ms @256K</text>
  <text x="187" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#7a5656">la mémoire = l'armoire</text>

  <rect x="370" y="60" width="326" height="312" rx="10" fill="#f0f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="533" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">MemT-1.0 : digérer le passé</text>
  <rect x="398" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="130" text-anchor="middle" font-size="14" fill="#3d4f68">tour 1 &#8594; plié &#183; jeté</text>
  <rect x="398" y="152" width="270" height="54" rx="6" fill="#d9e6f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="174" text-anchor="middle" font-size="14" fill="#2c3e55">état mémoire constant O(1)</text>
  <text x="533" y="196" text-anchor="middle" font-size="14" fill="#2c3e55">la requête ne lit que l'état</text>
  <text x="533" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#1c4e80">66&#215; moins de stockage @128K</text>
  <text x="533" y="268" text-anchor="middle" font-size="14" fill="#2c3e55">TTFT plat ~104&#8211;112ms &#183; 4,19&#215; @256K</text>
  <text x="533" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#55697f">la mémoire = consolidée, comme un cerveau</text>

  <text x="360" y="348" text-anchor="middle" font-size="14" fill="#6b5f45">le prix : la fidélité s'échange contre le coût &#8212; les systèmes textuels restent meilleurs (68,5 vs 50,6)</text>
  <text x="360" y="372" text-anchor="middle" font-size="14" fill="#8a7d5c">tous les chiffres sont déclaratifs ; aucune réplication indépendante</text>
</svg>
Fig. 2 : le pari de la voie mémoire-native — cesser de rediffuser l'historique et le plier dans le calcul ; moins cher, plus rapide, au prix d'une fidélité moindre là où l'évidence exacte compte.

Garde-fous honnêtes : les **systèmes textuels/RAG restent nettement supérieurs** — MemOS à ~68,5 contre 50,6 pour Flash. Et tous ces chiffres sont déclaratifs : **aucune réplication indépendante** ce soir. Traitez les benchmarks comme une affirmation, pas un verdict.

Déploiement pratique : inférence SGLang, démarrage Transformers, sessions en snapshots. Deux GPU pour Nano, huit pour Flash.

## Une semaine, trois assauts sur le même coût

Trois paris cette semaine sur le même problème — la mémoire de l'IA coûte trop cher :

1. **Architecture** : MemT-1.0 met la mémoire *dans* le graphe de calcul.
2. **Le modèle comme scribe** : Hy-Memory-30B-A3B de Tencent (15 octobre, un projet séparé, sans lien) prend le chemin inverse — un modèle spécialisé dans *l'écriture vers des* mémoires externes. La mémoire reste dehors ; le scribe devient intelligent.
3. **Infrastructure** : DeepSeek a open-sourcé **DeepInfer** (20 octobre, Apache-2.0), sa pile d'inférence de production — le même coût, attaqué au niveau des systèmes.

Quelle couche l'emporte ? Notons l'asymétrie : DeepInfer vise DeepSeek-V4.1-Flash, l'épine dorsale de MemT-1.0-Flash est DeepSeek-V4-Flash — même famille, même semaine, pas le même checkpoint.

**La question à débattre :** si la mémoire peut se plier en un état fixe et le transcript être jeté, que devient l'idée — aujourd'hui centrale pour les agents — que le passé d'une IA devrait rester *inspectable* ? Une mémoire comprimée que l'on peut auditer est un classeur. Une mémoire consolidée à laquelle on ne peut que faire confiance est tout autre chose.
