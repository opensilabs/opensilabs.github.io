---
lng_pair: id_20261028_nemotron-transcribe
title: "NVIDIA の Nemotron 3.5 Transcribe：40 言語を書き起こす公開モデル、30B のうち働くのは 4B だけ"
author: OpenSI-Labs
category: research
tags: [NVIDIA, Nemotron, 音声認識, ASR, 公開ウェイト, 混合専門家, 話者ダイアライゼーション]
date: 2026-10-28 09:00:00 -0700
img: /assets/img/posts/2026-10-28-nemotron-transcribe.png
meta_description: "NVIDIA の公開ウェイトモデル Nemotron 3.5 Transcribe は 40 言語を書き起こし、英語と 31 言語を翻訳する。30B パラメータのうち音声ごとに働くのは約 4B だけなので、チップ 1 枚で動く。冒頭の数字は NVIDIA の自己申告であり、限界もはっきりしている。"
---

10 月 28 日、NVIDIA は Nemotron 3.5 Transcribe を公開した。重みはダウンロードでき、商用も可能だ。40 言語の書き起こし、英語と 31 言語の翻訳、最長 1 時間の録音、最大 8 人の話者に対応する。重みは Hugging Face 等にある。

指示で逐語稿か清書稿かを選べる。薬品名などの語彙を渡して重点的に聞かせたり、内容への質問もできる。話者ダイアライゼーション（誰がいつ話したか）も行う。

## 30B のうち、働くのは 4B だけ

構造は混合専門家（MoE）で、専門家サブネットワークのうち音声の断片ごとに一部だけが起動し、残りは休んで費用がかからない。総 30B のうち活性化は約 4B。容量と実行コストが切り離されるため、チップ 1 枚で動く。Artificial Analysis 測定では、活性 4B で Voxtral Small（24B）と並ぶ公開首位タイ、誤り率 2.8% だ。

<figure>
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="340" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">総パラメータ 30B、毎回働くのは約 4B</text>
<text x="40" y="98" font-size="15" font-weight="700" fill="#374151">総パラメータ：30B</text>
<rect x="40" y="112" width="600" height="46" rx="8" fill="#cbd5e1"/>
<rect x="40" y="112" width="80" height="46" rx="8" fill="#0e7c86"/>
<text x="52" y="142" font-size="17" font-weight="700" fill="#ffffff">~4B</text>
<text x="140" y="142" font-size="15" fill="#374151">1 回の処理で活性化：約 4B</text>
<text x="640" y="142" text-anchor="end" font-size="15" fill="#374151">休止：約 26B</text>
<text x="40" y="212" font-size="16" fill="#374151">ルーターが音声の断片ごとに少数の専門家だけを起こし、残りは費用ゼロ。</text>
<text x="340" y="272" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">チップ 1 枚で十分：Jetson AGX Thor ・ DGX Spark ・ Blackwell</text>
<text x="340" y="316" text-anchor="middle" font-size="26" font-weight="700" fill="#0e7c86">30B &#8594; ~4B</text>
</svg>
<figcaption>図 1 — 混合専門家は容量と実行コストを切り離す。30B を持ちながら、毎回支払うのは約 4B 分だけだ。</figcaption>
</figure>

単語誤り率（WER）は誤った単語の割合。低いほど良い。NVIDIA によれば、Hugging Face 英語ランキングで公開首位の 5.33%、多言語は 7 言語平均 4.62% で比較中最低、話者帰属の誤り率 18.26% は David AI の 21 言語・14 システム中最低。いずれも自己申告で、独立した再現はまだない。

同日公開の Granary v2 は 48 言語・16 コーパス、463,062 時間。録音ごとに逐語・整形・クリーンの 3 様式が付く。音声本体は含まない原典への目録で、ライセンスは原典ごと。

## 専門用語を覚える

インドの医療音声 Eka Care では、初期状態で単語の 5 分の 1 から 3 分の 1 を誤った。プロンプト改善で誤りは減り、GB300 1 枚・約 14GPU 時間のファインチューニング（分野の例での追加学習）で、未知の話者の WER は 22.44% から 12.17% へ、誤り約 45.8% 減となった。病院が自前の語彙を午後で教えられる。

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">医療用語を覚える 3 段階</text>
<rect x="40" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#1e3a5f" stroke-width="2"/>
<text x="130" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">初期状態</text>
<text x="130" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">単語誤り率 22.44%</text>
<text x="130" y="208" text-anchor="middle" font-size="14" fill="#374151">未知の話者で測定</text>
<rect x="240" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#0e7c86" stroke-width="2"/>
<text x="330" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">プロンプト改善</text>
<text x="330" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#0e7c86">誤りが大きく減少</text>
<text x="330" y="208" text-anchor="middle" font-size="14" fill="#374151">追加学習なしで</text>
<rect x="440" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#b91c1c" stroke-width="2"/>
<text x="530" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">微調整：約 14 GPU 時間</text>
<text x="530" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#b91c1c">単語誤り率 12.17%</text>
<text x="530" y="208" text-anchor="middle" font-size="14" fill="#374151">GB300 1 枚で</text>
<text x="222" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="422" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="340" y="292" text-anchor="middle" font-size="16" font-weight="700" fill="#111827">誤り約 45.8% 減 — インド医療音声 Eka Care（NVIDIA のデモ）</text>
</svg>
<figcaption>図 2 — 専門用語の多い医療音声では、プロンプトでまず改善し、1 枚のチップでの午後の微調整で誤り率がほぼ半分になった。</figcaption>
</figure>

## できないこと

ファイル専用でライブ配信には対応せず、リアルタイム字幕や音声エージェントは対象外だ。今月は ElevenLabs の Realtime、Mistral の Voxtral 3、Salesforce の Launa-Omni も出た。小型用途には自社の Parakeet（1.1B）。

書き起こしは借りる API から自前で回す道具へ移りつつある。病院や会議室の音声を外に出さずに済む。最も書き起こしが必要な録音ほど、外に出しにくいからだ。
