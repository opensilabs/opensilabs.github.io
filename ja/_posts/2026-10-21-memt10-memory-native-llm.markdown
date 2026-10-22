---
lng_pair: id_20261021_memt10-memory-native-llm
title: "過去を読み返さないモデル"
author: OpenSI-Labs
category: LLMs
tags: [LLMs, memory, architecture, open weights, MemT]
date: 2026-10-21 00:00:00 -0700
img: /assets/img/posts/2026-10-21-memt10-memory-native-llm.png
meta_description: "MemT-1.0は長い文脈を繰り返し読み込む代わりに、履歴を固定サイズの記憶状態に折りたたみ、記録を捨てる。記憶をモデルの計算に組み込む試み。"
---

言語モデルには癖がある。会話のたびに過去を読み返す。10月19日、74人のMemTensorチームが[MemT-1.0](https://arxiv.org/abs/2610.26825)を公開した――過去を消化する。

## 記憶を計算の一部に

記憶ブロックはアテンションと並列だ。ターン後、履歴はトークン単位で固定の記憶状態に折りたたまれ、平文は捨てられる。更新はNVIDIAのGated DeltaNet-2由来で、消去・書き込み・減衰の三操作。

<svg viewBox="0 0 720 430" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="ネイティブ記憶ブロックの仕組み：各トークンが消去・書き込み・減衰の更新を固定サイズの記憶状態に加え、アテンションと並列に動作する。">
  <defs>
    <marker id="jf1a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="414" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">注意と並列に動く記憶ブロック</text>

  <rect x="24" y="64" width="196" height="180" rx="10" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="122" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">通常のアテンション</text>
  <text x="122" y="122" text-anchor="middle" font-size="14" fill="#3d4f68">KVキャッシュ全文を参照</text>
  <rect x="52" y="140" width="140" height="66" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="122" y="166" text-anchor="middle" font-size="14" fill="#8a4b4b">棚は膨らみ続ける</text>
  <text x="122" y="190" text-anchor="middle" font-size="14" fill="#8a4b4b">状態は O(N)</text>

  <rect x="262" y="64" width="196" height="180" rx="10" fill="#f6f3fb" stroke="#7b5fc8" stroke-width="2"/>
  <text x="360" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#3b2c66">ネイティブ記憶ブロック</text>
  <text x="360" y="122" text-anchor="middle" font-size="14" fill="#4c3d7d">消去 &#8594; 書き込み &#8594; 減衰</text>
  <rect x="292" y="140" width="136" height="66" rx="6" fill="#ffffff" stroke="#7b5fc8" stroke-width="1.5"/>
  <text x="360" y="166" text-anchor="middle" font-size="14" fill="#4c3d7d">状態は固定</text>
  <text x="360" y="190" text-anchor="middle" font-size="14" fill="#4c3d7d">状態は O(1)</text>

  <rect x="500" y="64" width="196" height="180" rx="10" fill="#f3faf3" stroke="#4e7d4e" stroke-width="2"/>
  <text x="598" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c442c">出力</text>
  <text x="598" y="122" text-anchor="middle" font-size="14" fill="#33502f">アテンション出力</text>
  <text x="598" y="146" text-anchor="middle" font-size="14" font-weight="bold" fill="#2c442c">+</text>
  <text x="598" y="170" text-anchor="middle" font-size="14" fill="#33502f">記憶アテンション出力</text>
  <text x="598" y="200" text-anchor="middle" font-size="14" font-style="italic" fill="#33502f">足し合わせる</text>

  <line x1="224" y1="150" x2="256" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#jf1a)"/>
  <line x1="462" y1="150" x2="494" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#jf1a)"/>

  <rect x="24" y="268" width="672" height="120" rx="10" fill="#fff8ec" stroke="#c9962e" stroke-width="2"/>
  <text x="360" y="298" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c4210">トークンごとにターンごとに：過去を折りたたみ、記録を捨てる</text>
  <text x="360" y="330" text-anchor="middle" font-size="14" fill="#6b5423">ターン終了 &#8594; 履歴を記憶状態へ折りたたむ &#8594; 平文は破棄</text>
  <text x="360" y="360" text-anchor="middle" font-size="14" font-weight="bold" fill="#3a3226">アブレーション：粒度（&#8722;5.99）が更新則（&#8722;0.25）より重要</text>
</svg>
図1：予測分を消去、残差だけを書き込む。

アブレーション：更新をトークン単位からターン単位に粗くすると5.99落ち、規則を変えても0.25。いつ書くかが重要だ。

## 数字は正直なラベルで

二つのグレード：Nano（360億／実働30億、Qwen3.6-35B-A3B、Apache-2.0）とFlash（2880億／実働170億、DeepSeek-V4-Flash、MIT）。11ベンチマークでFlash平均50.60、Nano46.97。128KでストレージはKVの約66分の1、初トークンは2.44倍（256Kで4.19倍）。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="対比：従来のモデルは毎ターン膨らむ記録を再送するが、MemT-1.0は履歴を固定サイズの記憶状態に折りたたみ、記録を捨てる。">
  <defs>
    <marker id="jf2a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="384" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">過去を再送するのをやめる</text>

  <rect x="24" y="60" width="326" height="312" rx="10" fill="#faf0f0" stroke="#b07a7a" stroke-width="2"/>
  <text x="187" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c2c2c">従来LLM：過去を背負う</text>
  <rect x="52" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="130" text-anchor="middle" font-size="14" fill="#5c2c2c">ターン1 &#183; ターン2 &#183; ターン3 &#183; …</text>
  <rect x="52" y="152" width="270" height="54" rx="6" fill="#f3d9d9" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="174" text-anchor="middle" font-size="14" fill="#5c2c2c">KVキャッシュは O(N) で増大</text>
  <text x="187" y="196" text-anchor="middle" font-size="14" fill="#5c2c2c">全トークンを毎回再読</text>
  <text x="187" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#8a2f2f">ストレージも遅延も膨らみ続ける</text>
  <text x="187" y="268" text-anchor="middle" font-size="14" fill="#5c2c2c">TTFT：128Kで257ms &#8594; 256Kで445ms</text>
  <text x="187" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#7a5656">記憶＝ファイル棚</text>

  <rect x="370" y="60" width="326" height="312" rx="10" fill="#f0f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="533" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">MemT-1.0：過去を消化する</text>
  <rect x="398" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="130" text-anchor="middle" font-size="14" fill="#3d4f68">ターン1 &#8594; 折りたたむ &#183; 破棄</text>
  <rect x="398" y="152" width="270" height="54" rx="6" fill="#d9e6f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="174" text-anchor="middle" font-size="14" fill="#2c3e55">記憶状態は O(1) で固定</text>
  <text x="533" y="196" text-anchor="middle" font-size="14" fill="#2c3e55">クエリは状態だけを参照</text>
  <text x="533" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#1c4e80">128Kでストレージ66分の1</text>
  <text x="533" y="268" text-anchor="middle" font-size="14" fill="#2c3e55">TTFTは約104～112msで横ばい &#183; 256Kで4.19倍</text>
  <text x="533" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#55697f">記憶＝脳のように定着</text>

  <text x="360" y="348" text-anchor="middle" font-size="14" fill="#6b5f45">代償：固定サイズの記憶は忠実度と引き換え――テキスト系はまだ高得点（68.5対50.6）</text>
  <text x="360" y="372" text-anchor="middle" font-size="14" fill="#8a7d5c">すべての数字は著者主張。独立再現はまだなし</text>
</svg>
図2：履歴の再送をやめ、計算に折りたたむ。

テキスト／RAG系は依然高スコア（MemOS約68.5対Flash50.6）。数字はすべて著者主張――独立再現はゼロだ。

導入は手軽だ。[SGLang](https://github.com/MemTensor/MemT-1.0)推論とTransformers。NanoはGPU二枚、Flashは八枚。

## 一週間、三つの攻め手

今週、記憶コストに三つの賭け。アーキテクチャのMemT-1.0、外部記憶の書き手Hy-Memory（別プロジェクト）、システム層のDeepInferだ。

議論：記憶を固定状態に折りたたみ記録を捨てるなら、AIの過去は監査可能であるべきか。
