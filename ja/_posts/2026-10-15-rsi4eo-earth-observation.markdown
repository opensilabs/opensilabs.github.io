---
lng_pair: id_20261015_rsi4eo-earth-observation
title: "人間が作った最後のモデル：地球観測を再帰的に改善するAIエージェント"
author: OpenSI-Labs
category: research
tags: [再帰的自己改善, RSI4EO, 地球観測, コーディングエージェント, 検証可能なAI]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-rsi4eo-earth-observation.png
meta_description: "コーディングエージェントが地球観測モデルを構築し、自身の出力の上で再帰的に改善。訓練ラベルの約1%で、4つの衛星画像ベンチマークにおいて公表済みの最高結果を上回る。"
---

**増水時、モデル訓練の暇はない。**

洪水がデルタに広がる。緊急チームは被害マップを今日要る。衛星画像は揃ったが、地図化は今も専門家の仕事で数週間かかる。完成時には水は引いている。

10月13日のarXiv論文が問う。ループ全体をエージェントに渡したら（[Zhaoら](https://arxiv.org/abs/2610.18845v1)）。「人間が作った最後のリモートセンシングモデル？」——検証可能なタスクはすべてRSIに鋳造でき、地球観測は最初の完成例だ。

仕組みは二語。ハーネスと検証器。使用を許されたすべてがハーネス。最後の密封試験が検証器で、秘匿画像を見せず採点する。この二つでエージェントはモデルを構築し、自身の出力で再帰改善する。

<figure>
<svg viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">RSI4EO：人が試験を設計、エージェントがモデルを構築</text>
<rect x="20" y="60" width="200" height="110" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="120" y="86" font-size="14" font-weight="bold" text-anchor="middle">人間が設計</text>
<text x="120" y="110" font-size="14" text-anchor="middle">ハーネス：データ · ツール ·</text>
<text x="120" y="130" font-size="14" text-anchor="middle">エージェントが使える計算資源</text>
<text x="120" y="152" font-size="14" text-anchor="middle" font-style="italic">密封検証器：採点</text>
<rect x="250" y="60" width="180" height="110" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="340" y="86" font-size="14" font-weight="bold" text-anchor="middle">コーディングエージェント</text>
<text x="340" y="110" font-size="14" text-anchor="middle">地球観測モデルを構築、</text>
<text x="340" y="130" font-size="14" text-anchor="middle">自身の出力で再帰的に改善</text>
<text x="340" y="152" font-size="14" text-anchor="middle"></text>
<rect x="460" y="60" width="200" height="110" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="560" y="86" font-size="14" font-weight="bold" text-anchor="middle">より良い地球観測モデル</text>
<text x="560" y="110" font-size="14" text-anchor="middle">洪水 / 作物 / 被害</text>
<text x="560" y="130" font-size="14" text-anchor="middle">衛星画像から地図作成</text>
<text x="560" y="152" font-size="14" text-anchor="middle"></text>
<line x1="220" y1="115" x2="246" y2="115" stroke="#3366cc" stroke-width="2" marker-end="url(#m1)"/>
<line x1="430" y1="115" x2="456" y2="115" stroke="#cc8833" stroke-width="2" marker-end="url(#m1)"/>
<path d="M 560 170 C 560 260, 120 260, 120 176" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#m1)"/>
<text x="340" y="300" font-size="14" text-anchor="middle" font-style="italic">1サイクルの出力が次の入力に</text>
<text x="340" y="330" font-size="14" text-anchor="middle">検証可能：ラベル · 独立センサー · 物理モデル · 反復観測</text>
<defs><marker id="m1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>このループ：人間がハーネスと密封された検証器を設計し、エージェントがモデルを構築して自身の出力の上で改善する。</figcaption>
</figure>

なぜ衛星か。現実が採点するからだ。全タスクは四経路で検証可能になる。ラベル付きベンチマーク、独立センサー、物理モデル、繰り返し観測。洪水検出は数時間後のレーダーで検証できる。

数字が宣言を成果に変える。四ベンチマークで公表済み最高を上回り、全量ラベルで四戦全勝。0.2〜1.4%のラベルで69〜84%を維持（[ArXivSignals](https://arxivsignals.io/explore)）。1%のラベルで大半の精度だ。

<figure>
<svg viewBox="0 0 680 260" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">ラベル効率：約1%のラベルで大半の精度</text>
<text x="200" y="70" font-size="14" text-anchor="end">フルラベル</text>
<rect x="210" y="54" width="380" height="24" rx="4" fill="#3366cc"/><text x="598" y="71" font-size="14">100%</text>
<text x="200" y="116" font-size="14" text-anchor="end">0.2–1.4%のラベル</text>
<rect x="210" y="100" width="290" height="24" rx="4" fill="#cc8833"/><text x="508" y="117" font-size="14">69–84%のスコア</text>
<text x="200" y="162" font-size="14" text-anchor="end">公開済みベースライン</text>
<rect x="210" y="146" width="330" height="24" rx="4" fill="#999"/><text x="548" y="163" font-size="14">4/4で上回る</text>
<text x="340" y="210" font-size="14" text-anchor="middle">4ベンチマーク：光学 · SAR · マルチスペクトル時系列</text>
<text x="340" y="236" font-size="14" text-anchor="middle" font-style="italic">エージェント構築モデルが全タスクでSOTAを上回る</text>
</svg>
<figcaption>ごくわずかなラベルで、エージェント構築モデルは精度の大半を維持——しかも公表済みのベースラインをすべて上回る。</figcaption>
</figure>

見落とされがちな点。再帰的自己改善は二つの半分から成り、難しいのは片方だけだ。「自己」の半分は常識化した。「改善」が難関で、誰もうなずかないとき何が「より良い」のかが問われる。RSI4EOが指すのは信号が世界から来る領域だ。独立センサーはお世辞に動じず、物理モデルは雄弁に騙されない。正解が手の届かぬところにあるから密封検証器は成り立つ。

再帰の配当もある。地球観測モデルはエージェントと共に進化し、全パイプラインを自動で底上げする。分業論——人間はハーネスと検証器を設計し、エージェントはモデルを構築する。希少技能は検証器設計へ移る。

留保も重要だ。四つのベンチマークは橋頭堡であって征服ではない。他分野への転用は未確定の賭けだ。密封検証器は静かに重労働を担い、安全性はエージェントがカンニングしないことにかかる。

だが初めてだ。一分野全体が再定式化され、エージェントが測定可能に自己改善できるようになった。採点者は世界だ。

検証器が安全の鍵なら——誰が検証器を検証するのか。エージェントが検証器を作れたとき、何が起きるのか。
