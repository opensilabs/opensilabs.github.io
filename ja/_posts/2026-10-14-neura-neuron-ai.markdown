---
lng_pair: id_20261014_neura-neuron-ai
title: "Neuron AI：触れて、聞いて、そして覚えるロボット"
author: OpenSI-Labs
category: robotics
tags: [Neuron AI, フィジカルAI, マルチモーダルモデル, ヒューマノイド, NEURA Robotics]
date: 2026-10-14 04:00:00 -0700
img: /assets/img/posts/2026-10-14-neura-neuron-ai.png
meta_description: "NEURA Robotics の Neuron AI は 3D ビジョン、触覚、音、記憶を一つの知覚—言語—行動基盤モデルに統合。手のように物理スキルを学ぶロボットの脳。"
---

**11 分間の洗濯。**

来週の GTC Berlin で、ヒューマノイド 4NE1 が 11 分かけて一人で洗濯をする。仕分け、投入、開閉、取り出し、乾燥機への移し替え。珍しいのは動作ではなく継続性だ——*記憶*が必要なのだ。

10 月 14 日、ドイツ NEURA Robotics 発表の **Neuron AI** の核心だ。フィジカル AI のためのマルチモーダル基盤モデル——カメラには見えない感覚を中心に据えた「物理世界の脳」である。（[公式発表](https://www.businesswire.com/news/home/20261013482085/en/NEURA-Robotics-Introduces-Neuron-AI-The-Brain-of-the-Physical-World)；[Unite.AI](https://www.unite.ai/neura-robotics-unveils-neuron-ai-foundation-model-for-physical-ai/)）

そのアーキテクチャは**知覚—言語—行動（PLA）**。知覚層が 3D ビジョン、触覚・力覚、音声、身体状態、言語指示を同時に受け取り、言語モデルが共有空間で推論し、行動モデルが動作に変換する。全感覚は時間整列された共通表現にエンコードされてから行動ストリームになる。

<svg viewBox="0 0 720 300" width="100%" role="img" aria-label="Neuron AI の知覚—言語—行動パイプライン">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">知覚—言語—行動：ひとつの脳、五つの感覚</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">すべての感覚を時間整列された共有空間にエンコード</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="20" y="80" width="124" height="56" rx="10" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="82" y="105" fill="#0e3a3a">3Dビジョン</text><text x="82" y="125" fill="#5a7a7a">形状・色・位置</text>
    <rect x="152" y="80" width="124" height="56" rx="10" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="214" y="105" fill="#0e3a3a">触覚＋力覚</text><text x="214" y="125" fill="#5a7a7a">接触・握力</text>
    <rect x="284" y="80" width="124" height="56" rx="10" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="346" y="105" fill="#0e3a3a">音声</text><text x="346" y="125" fill="#5a7a7a">クリック音・工程音</text>
    <rect x="416" y="80" width="124" height="56" rx="10" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="478" y="105" fill="#0e3a3a">身体状態</text><text x="478" y="125" fill="#5a7a7a">姿勢・バランス</text>
    <rect x="548" y="80" width="124" height="56" rx="10" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="610" y="105" fill="#0e3a3a">言語指示</text><text x="610" y="125" fill="#5a7a7a">やってほしいこと</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" marker-end="url(#ah9)">
    <defs><marker id="ah9" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="82" y1="138" x2="180" y2="180"/><line x1="214" y1="138" x2="270" y2="180"/><line x1="346" y1="138" x2="346" y2="180"/><line x1="478" y1="138" x2="424" y2="180"/><line x1="610" y1="138" x2="512" y2="180"/>
  </g>
  <rect x="120" y="182" width="480" height="46" rx="10" fill="#0e3a3a"/><text x="360" y="211" text-anchor="middle" font-size="14" fill="#ffffff" font-family="system-ui, sans-serif">共有の時間整列表現 ＋ 記憶</text>
  <g stroke="#0e3a3a" stroke-width="2" marker-end="url(#ah10)">
    <defs><marker id="ah10" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="360" y1="230" x2="360" y2="252"/>
  </g>
  <rect x="180" y="254" width="360" height="38" rx="10" fill="#f2a33c"/><text x="360" y="279" text-anchor="middle" font-size="14" font-weight="bold" fill="#0e3a3a" font-family="system-ui, sans-serif">行動モデル → 精密で安全な動作</text>
</svg>

今日のロボットの「脳」はカメラ中心だ。だがカメラはネジの噛み具合を感じ取れず、コネクタのカチッという音を聞き取れない。Neuron AI は触覚・音・身体感覚を**一級の入力**として扱う。溶接ビードの品質は工程の音で判断できる——工場では、この一文が本物の金になる。

そして**記憶**。物理世界で働くには「対象の永続性」が要る。目の前から消えても物は存在し続けるという、赤ちゃんが生後 2 年で獲得する理解だ。NEURA は記憶のためにアーキテクチャを改造した。洗濯デモでは記憶が承り壁だ。

デモとの違いはここだ。Neuron AI は **NEURA の 5 種類のロボット形態**で動作し、身体が違っても同じ基盤モデルが技能を横断する。訓練データは 3 本柱だ。「ジム」の実ロボットデータ、シミュレーション増幅データ、センサースーツの人間デモ。一種類の身体でしか動かないモデルは実験室の手品にすぎず、身体を越えて技能を持ち運べるモデルはプラットフォームになる。

<svg viewBox="0 0 720 290" width="100%" role="img" aria-label="カメラだけではロボットに決して伝わらないこと">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">カメラだけではロボットに決して伝わらないこと</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">物理作業のロングテールは、ほかの感覚に眠っている</text>
  <g font-family="system-ui, sans-serif" font-size="14">
    <rect x="20" y="72" width="330" height="96" rx="10" fill="#f6f1e7" stroke="#0e3a3a" stroke-width="2"/>
    <text x="40" y="102" font-weight="bold" fill="#0e3a3a">鍵は本当に開いたか？</text>
    <text x="40" y="126" fill="#3a4a4a">確かめられるのは音と触覚だけ。</text>
    <text x="40" y="150" fill="#3a4a4a">鍵の回転を見続けても分からない。</text>
    <rect x="370" y="72" width="330" height="96" rx="10" fill="#f6f1e7" stroke="#0e3a3a" stroke-width="2"/>
    <text x="390" y="102" font-weight="bold" fill="#0e3a3a">見えないものをつかむ</text>
    <text x="390" y="126" fill="#3a4a4a">触覚があれば、バッグの中や</text>
    <text x="390" y="150" fill="#3a4a4a">機械内部の物を持てる。</text>
    <rect x="20" y="180" width="330" height="96" rx="10" fill="#f6f1e7" stroke="#0e3a3a" stroke-width="2"/>
    <text x="40" y="210" font-weight="bold" fill="#0e3a3a">耳で溶接を判定する</text>
    <text x="40" y="234" fill="#3a4a4a">ビードの品質は工程の</text>
    <text x="40" y="258" fill="#3a4a4a">音に現れる。</text>
    <rect x="370" y="180" width="330" height="96" rx="10" fill="#f6f1e7" stroke="#0e3a3a" stroke-width="2"/>
    <text x="390" y="210" font-weight="bold" fill="#0e3a3a">シャツを覚えている</text>
    <text x="390" y="234" fill="#3a4a4a">洗濯機の中、見えないけれど</text>
    <text x="390" y="258" fill="#3a4a4a">追い続けなければならない。</text>
  </g>
</svg>

NEURA の指標は **Time-to-Skill**——ロボットが新しいタスクを学び、安定してこなせるようになるまでの速さ。ベンチマークの順位でもパラメータ数でもない。価値は論文ではなくデプロイで測られる。

**見落とされがちな視点**：業界の舞台はキッチンだが、NEURA の賭けは逆方向だ。訓練の信号源はドイツの工場、Schaeffler と Bosch の溶接とネジである。洗濯デモは分かりやすいイラストにすぎず、本当の賭けは産業にある。工場のタスクを塞いできたのは視覚ではなかった。触覚・力覚・音——カメラだけの VLA には永遠に届かない感覚だ。

展示会場の「完全自律」と夜勤の工場の「完全自律」は別物だ。だが狙うのは先代の脳が頭を打った天井そのものだ。カメラはロボットを「見る」ことの限界まで連れてきた。残り——つかむ、感じる、覚える——はフィジカル AI が行くべき場所だ。

**議論：** 触れ、聞き、覚えるロボットがいたら——日常の仕事のうち、最初に任せたいのはどれで、自分でやりたいのはどれですか？
