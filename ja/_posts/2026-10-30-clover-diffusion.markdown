---
layout: post
lng_pair: id_20261030_clover-diffusion
title: "Cloverは一語ずつ書かない、ブロックで埋める：35B拡散モデルがSWE-benchで73.6を自称"
author: OpenSI-Labs
category: AIモデル
tags: [拡散言語モデル, Clover, DiffuSpace, オープンウェイト, SWE-bench]
date: 2026-10-30 20:00:00 -0700
img: /assets/img/posts/2026-10-30-clover-diffusion.png
---

2026年10月28–29日、DiffuSpaceが初のモデルClover-35B-A3B-Previewを公開した。ウェイトはHugging FaceでApache 2.0、BF16約69GB。「公開拡散モデルで最強」は検証できるが、目玉のスコアは検証できない。

## 空欄から書く

GPT以来、主流は一語ずつ書く。選んだ語は直せず、ミスは全体が引き受ける。500番目は499番目まで出せない。

Cloverは32トークン単位で書く。最初は全て空欄。全体を両方向から見て、自信ある空欄を複数並行して埋める。隣が決まれば残りも決まり、次の回で埋まる。完成すれば固定され、土台になる。空欄の下書きを確かな語から埋める編集者のやり方。

<figure>
<img src="/ja/assets/img/posts/2026-10-30-clover-diffusion-fig1.svg" alt="二つの書き方：一語ずつ書くか、32個の空欄のブロックか">
<figcaption>図 1 — 自己回帰モデルは書いた語をその場で固定する。Cloverは32個の空欄から始め、自信のある位置から埋める。</figcaption>
</figure>

信頼度0.95超で埋める（LowConfidence）。無ければ最も確かな1つを埋め、止まらない。内側は双方向、前段は因果的。

<figure>
<img src="/ja/assets/img/posts/2026-10-30-clover-diffusion-fig2.svg" alt="32個の空欄のブロックが3回で埋まっていく様子">
<figcaption>図 2 — ブロックは何回かで埋まる。信頼度が0.95を超えた位置が埋まり、完成したブロックが次のブロックの前置きになる。</figcaption>
</figure>

## 中身の仕様

総パラメータ35B、活性はトークン当たり約3B。40層MoE、専門家256個から上位8個を使い、共有専門家は各層1個。文脈128K。土台はアリババQwen3.6-35B-A3Bの混合骨格（Gated DeltaNet＋全注意）。追加は双方向ブロック注意（右畳み込み重み含む）とブロック拡散推論。

## 73.6は未検証

会社の数字は73.6（SWE-bench）、51.7（Terminal-Bench）、毎秒515トークン（H200）。73.6は確かめようがない。Daily Inferenceの分析の通り、足場・ツール・試行回数・設定は未開示だ。ウェイトは確認できても再現できない。73.6は測定でなく箱の主張だ。

## 動かす道は狭い

今はTransformers＋約69GBのGPUメモリだけだ。GGUF版はなくOllamaやLM Studioは使えず、SGLangも未統合。ノートPCでは動かない。

モデルカードは超長文の繰り返しも認める。対策は既定で入る（presence penalty 0.9、repetition penalty 1.05、終了への偏り）。

## それでも大事

一語ずつの限界は2つ。速度は逐次性に縛られ、序盤のミスは固定。ブロック拡散は両方を攻める：並行に埋めれば速くなり、固定前に形を整えられる。仕組みは実在し、スコアは約束手形だ。再現が73.6に近づけば習慣は揺らぐ。届かなくても最強の公開拡散モデルだ——革命ではないにしても。
