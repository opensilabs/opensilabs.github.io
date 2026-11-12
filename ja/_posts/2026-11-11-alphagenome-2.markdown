---
layout: post
lng_pair: id_20261111_alphagenome2
title: "AlphaGenome 2：どの細胞の話か先に伝えると、同じ DNA からまったく違う答えが返ってくる"
author: OpenSI-Labs
category: Bio AI
tags: [AlphaGenome 2, DeepMind, ゲノミクス, DNA, シングルセル, バリアント効果]
date: 2026-11-11 06:00:00 -0800
img: /assets/img/posts/2026-11-11-alphagenome-2.png
---

## 同じDNA、違う働き

DNAは、体のどの細胞にも同じ内容で入っている説明書で、遺伝子は中のレシピです。腸と血液の細胞では、開く章が違うため使うレシピも仕事も違います。病気に関わる変異（文字が1つ変わること）の多くは、レシピではなく調節スイッチにあります。同じ違いでも結果は細胞しだいです。

## 第1世代の弱点

第1世代は100万文字のDNAから、遺伝子の活動、発現量、離れた場所の接触マップを予測できました。ただし学習データは組織を混ぜたものだけ――スムージーの平均のようなもの――で、答えは全組織の平均で、特定の細胞には合わせられませんでした。

## 細胞を条件に

DeepMindのAlphaGenome 2は、DNAと種（ヒトかマウス）に加え、組織・細胞の種類・状態の「条件」を1つ受け取り、細胞でのDNAの働きだけを予測します。

<figure>
<svg viewBox="0 0 720 250" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="模式図：同じDNAが細胞によって違って読まれる" style="width:100%;height:auto;font-family:sans-serif;">
<rect x="20" y="95" width="200" height="36" rx="18" fill="#eef2ff" stroke="#334155" stroke-width="1.5"/>
<text x="42" y="120" font-size="17" fill="#1e293b">A</text>
<text x="72" y="120" font-size="17" fill="#1e293b">C</text>
<text x="102" y="120" font-size="17" fill="#1e293b">G</text>
<circle cx="142" cy="113" r="14" fill="none" stroke="#dc2626" stroke-width="2.5"/>
<text x="135" y="120" font-size="17" fill="#dc2626" font-weight="bold">T</text>
<text x="172" y="120" font-size="17" fill="#1e293b">A</text>
<text x="120" y="75" font-size="20" fill="#334155" text-anchor="middle">→</text>
<text x="120" y="165" font-size="15" fill="#1e293b" text-anchor="middle">同じDNA、</text>
<text x="120" y="187" font-size="15" fill="#1e293b" text-anchor="middle">1文字だけ違う</text>
<circle cx="300" cy="85" r="32" fill="#dbeafe" stroke="#334155" stroke-width="1.5"/>
<circle cx="300" cy="85" r="13" fill="#93c5fd" stroke="#334155" stroke-width="1"/>
<circle cx="420" cy="85" r="32" fill="#dcfce7" stroke="#334155" stroke-width="1.5"/>
<circle cx="420" cy="85" r="13" fill="#86efac" stroke="#334155" stroke-width="1"/>
<text x="300" y="140" font-size="14" fill="#1e293b" text-anchor="middle">血液の細胞？</text>
<text x="420" y="140" font-size="14" fill="#1e293b" text-anchor="middle">腸の細胞？</text>
<text x="360" y="185" font-size="15" fill="#475569" text-anchor="middle">どちらを聞きますか？</text>
<text x="478" y="120" font-size="20" fill="#334155" text-anchor="middle">→</text>
<rect x="505" y="62" width="60" height="20" rx="6" fill="#cbd5e1" stroke="#64748b" stroke-width="1"/>
<text x="505" y="50" font-size="15" fill="#1e293b">遺伝子オフ</text>
<rect x="505" y="130" width="180" height="20" rx="6" fill="#22c55e" stroke="#15803d" stroke-width="1"/>
<text x="505" y="118" font-size="15" fill="#1e293b">遺伝子オン</text>
<text x="595" y="185" font-size="15" fill="#475569" text-anchor="middle">答えは2通り</text>
</svg>
<figcaption>図1 — 同じDNAの並びでも、細胞が違えば働きはまったく違う。AlphaGenome 2は「どの細胞か」を質問の一部として受け取る。</figcaption>
</figure>

条件は数値の要約となり、全段階を調整します。要約は参照条件から選ぶほか、自分のシングルセルRNAデータ（1細胞ごとの活動）から細胞エンコーダでも作れます。未知の状態でも再学習は不要です。学習は4段階で、8教師を1生徒に蒸留し、シングルセルで仕上げました。

## 数字と実例

DeepMindの論文では、TenK10Kで、発現を変える変異の発見率が正確さ90%で16%から30%に上がりました。向き（増えるか減るか）も23%から43%です。本当に原因である変異10個のうち、第1世代は約2個、AG2は3個見つける。良くなったが、まだ7個見逃す。

炎症性腸疾患の21番染色体では、rs2836882が約29万文字離れたETS2を単球とマクロファージだけで強め、リスクを上げると実験で分かっていました。候補7個では、AG2はこの変異だけを選び、ETS2と結びつけ、効く細胞も正しく絞りました。

## 限界と公開

限界も論文が認めています。正確さ重視では変異の30%しか見つからず、70%を見逃します。開いていない領域、遠すぎる場所、転写後の変異は苦手で、一時的・病気の状態はデータが少なく、神経の細かい種類は混ざります。学ぶのは相関で原因ではなく、遺伝子停止や状態変化の途中は不明です。

公開は後退しました。非営利研究用はAPIのみで、コードと重みは最終掲載時まで未公開です。計算済み予測（640条件のアトラス、510条件のスコア）は入手できます。研究専用で臨床未検証です。
