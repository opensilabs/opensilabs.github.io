---
lng_pair: id_20261016_muse_spark_open
title: "Muse Spark Open：机の上に載る816Bモデル"
author: OpenSI-Labs
category: models
tags: [オープンウェイト, 混合エキスパート, Meta, Apple, MLX]
date: 2026-10-16 06:00:00 -0700
img: /assets/img/posts/2026-10-16-muse-spark-open.png
meta_description: "Metaの816Bパラメータ・オープンウェイトモデルが2台のMac Studioで動作——真の物語はメモリの壁へのシステム的突破と、牙を持つライセンス。"
---

10月15日、MetaはMuse Spark Openの重みを公開した。8160億パラメータ、トークンあたり420億アクティブ、100万トークンコンテキスト。「米国で最も高性能なオープンウェイトモデル」だ。[\[1\]](https://www.macrumors.com/2026/10/15/meta-muse-spark-open-mac-studio/) [\[2\]](https://particle.news/story/meta-releases-muse-spark-open-and-partners-with-apple-to-run-it-on-m5-ultra-macs)

だが注目は机の上だ。MetaはAppleと組みMLX向けに最適化し、M5 Ultra搭載Studio 2台での動作を披露。「1TBのユニファイドメモリを持つ1台のスーパーコンピュータのように」振る舞うという。

## スパース性と太いパイプ

8160億はマーケティングの数字、420億はエンジニアリングの数字だ。MoEではトークンごとに約5%だけが目覚める。8160億冊の図書館で毎回1つの通路だけに入るイメージだ。

<svg viewBox="0 0 640 220" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="混合エキスパートのスパース性図解" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif" fill="#1a1a1a">トークンごとに発火するのは約5%</text>
  <g font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif">
    <rect x="40" y="60" width="560" height="70" rx="8" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="60" y="88" font-size="14" fill="#444">816B総パラメータ（全エキスパート）</text>
    <text x="60" y="112" font-size="14" fill="#444">ルーティングされるまで休眠</text>
    <rect x="40" y="150" width="560" height="40" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <rect x="40" y="150" width="29" height="40" rx="8" fill="#2f6df6"/>
    <text x="80" y="176" font-size="14" fill="#1a1a1a">トークンあたり42Bがアクティブ</text>
    <text x="470" y="176" font-size="14" fill="#555">ルーターが通路を選ぶ</text>
  </g>
</svg>
*図1：スパースな活性化——計算量は42B級に収まる。*

スパース性がメモリ計算を成立させる。低精度で8160億パラメータは1TB級を要する。M5 Ultra搭載Studioは1台512GBのユニファイドメモリをGPUが直接アドレスでき、帯域1.2TB/s。2台で1TBだ。800B級を閉じ込めていた3制約が一気に緩んだ。

<svg viewBox="0 0 640 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="ユニファイドメモリのプール図解" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif" fill="#1a1a1a">2台のデスクトップ、1TBのメモリ</text>
  <g font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif">
    <rect x="40" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="150" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 1</text>
    <text x="150" y="106" text-anchor="middle" font-size="14" fill="#444">512GBユニファイドメモリ</text>
    <text x="150" y="130" text-anchor="middle" font-size="14" fill="#444">GPUが直接アドレス</text>
    <rect x="380" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="490" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 2</text>
    <text x="490" y="106" text-anchor="middle" font-size="14" fill="#444">512GBユニファイドメモリ</text>
    <text x="490" y="130" text-anchor="middle" font-size="14" fill="#444">帯域1.2TB/s</text>
    <path d="M260 105 L360 105" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <path d="M380 135 L280 135" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <defs><marker id="arr" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><path d="M0,0 L8,4 L0,8 z" fill="#2f6df6"/></marker></defs>
    <rect x="180" y="185" width="280" height="36" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <text x="320" y="209" text-anchor="middle" font-size="14" fill="#1a1a1a">1TBプール——816Bモデル全体を格納</text>
  </g>
</svg>
*図2：プールされたメモリ——2台が1台として振る舞う。*

これはシステムの物語だ。巨大モデル利用の壁はつねにメモリだった。意義はこの壁が両側から攻められている証左であることだ。

## 冷水

「オープンウェイト」は「オープンソース」ではない。ライセンスは「Built with Muse Spark Open」の明示を要求し、年商2000万ドル超はサービス提供前にMetaへの通知と商用契約が要る。重みは無料だが、本格デプロイにはMetaが関与し続ける。流通戦略としてのオープンさだ。

最上級は「米国の」最強で、Metaのベンチマークは中国勢にコーディングで劣る。多極だ。「机の上で動く」は1万ドル超のStudio2台、512GB構成は未出荷。本物だが2万ドルだ。

だが価値は揺るがない。100万コンテキスト、42BアクティブのMoEがプールメモリ上でローカルに動くのは真の成果だ。AppleとMetaの雪解け（「パパとママがまた仲良くできて嬉しい」——Alexandr Wang）自体が信号である。両者が欲するのはNVIDIAのスタックを要しない未来だ。

**議論：** 商業支配が残りハードが2万ドルなら、この「オープン」は誰のためか。
