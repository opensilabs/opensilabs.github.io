---
lng_pair: id_20261007_vista-arc-agi-3
title: "モデルは愚かだったのではない。盲目だったのだ。"
author: OpenSI-Labs
category: research
tags: [ARC-AGI-3, 視覚記憶, AIエージェント, MIT, VISTA]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-vista-arc-agi-3.png
meta_description: "MITのVISTAハーネスは、追加学習ゼロでClaude Opus 5.0のARC-AGI-3スコアを40.68から満点の100へ引き上げた。モデルに本物の目と無損失の記憶を与えたのだ。ボトルネックは知能ではなく配管だった。"
---

10月1日、MITの5人が[論文](https://arxiv.org/abs/2610.02200)を出した。VISTAはClaude Opus 5.0のARC-AGI-3スコアを40.68から100.00へ引き上げた。公開25ゲームを全問クリア。初見の人間より57.4%少ない手数だ。新しい重みも追加学習もない。40と100の差はモデルでなく配管だった。

モデルは愚かでなく盲目だった。公式インターフェースは64×64の数字グリッド——絵のふりの表計算。人間はゲームを見て、モデルは帳簿を読まされた。VISTAは512×512の画像、欠けない記憶、自由な拡大を与えた。

<svg viewBox="0 0 720 336" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="VISTA：モデルを囲むループ">
  <defs>
    <marker id="arrV1a" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
    <marker id="arrV1b" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto-start-reverse"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">VISTA：モデルを囲むループ</text>
  <rect x="270" y="42" width="180" height="66" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="66" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">記憶する</text>
  <text x="360" y="86" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">無損失の視覚メモリ</text>
  <text x="360" y="102" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">全フレームを原本で保存・索引化</text>
  <rect x="30" y="152" width="150" height="66" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="105" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">見る</text>
  <text x="105" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">512×512の画像</text>
  <text x="105" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">64×64の数字表ではない</text>
  <rect x="285" y="152" width="150" height="66" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#5f3dc4">モデル</text>
  <text x="360" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">重みは不変</text>
  <text x="360" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">追加学習ゼロ</text>
  <rect x="540" y="152" width="150" height="66" rx="10" fill="#ebfbee" stroke="#2f9e44" stroke-width="2"/>
  <text x="615" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#2b8a3e">調べる</text>
  <text x="615" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">行動・ズーム・画素読み取り</text>
  <text x="615" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">履歴——モデルが自ら指揮</text>
  <rect x="270" y="262" width="180" height="66" rx="10" fill="#fff5f5" stroke="#e03131" stroke-width="2"/>
  <text x="360" y="286" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#c92a2a">ノート</text>
  <text x="360" y="306" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">GUIDE.md + WORKING.md</text>
  <text x="360" y="322" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">永続メモ＋作業用メモ</text>
  <line x1="182" y1="185" x2="283" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="437" y1="185" x2="538" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="110" x2="360" y2="150" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="220" x2="360" y2="260" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">VISTAは、重み不変のモデルを目・無損失の記憶・ノートで包む。知能はもともとそこにあった。欠けていたのはインターフェースだ。</p>

3部品だ。目はレンダリング画像。無損失メモリは全フレームを原本保存。コンテキスト外なので劣化なし。精査はモデル主導。playで操作、inspectで過去フレームの任意領域をズーム、read_pixelsで画素値を精密に読む、historyで行動と結果を振り返る。GUIDE.mdは永続メモ、WORKING.mdは作業メモ。学習済み部品はゼロ。25ゲームを同じプロンプトで駆動。

Claude Opus 5.0は40.68→100.00。183レベル、7,302手。初見の人間は17,135手。m0r0だけなら人間1,107手、Claude 219手。GPT-5.6 Solは13.33→47.32→99.00（真ん中は画像のみ）。320Bオープンモデルは1.89→66.93。3回とも99.00、98.90、99.23。「我々の知る限り」、プログラム合成なしの満点は初めてという。従来のトップはゲームごとにシミュレータを手書きした。VISTAは同じルールを作業メモの数行から導く。

<svg viewBox="0 0 720 348" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="同じ重み、新しいハーネス：VISTA導入前後のスコア">
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">同じ重み、新しいハーネス：ARC-AGI-3のスコア（RHAE）</text>
  <rect x="180" y="44" width="12" height="12" fill="#adb5bd"/><text x="198" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">公式ハーネスのベースライン</text>
  <rect x="380" y="44" width="12" height="12" fill="#1c7ed6"/><text x="398" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">VISTAあり</text>
  <text x="170" y="100" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">Claude Opus 5.0</text>
  <rect x="180" y="88" width="179" height="14" fill="#adb5bd"/><text x="364" y="99" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">40.68</text>
  <rect x="180" y="106" width="440" height="14" fill="#1c7ed6"/><text x="624" y="117" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">100.00</text>
  <text x="170" y="160" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">GPT-5.6 Sol</text>
  <rect x="180" y="148" width="59" height="14" fill="#adb5bd"/><text x="243" y="159" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">13.33</text>
  <rect x="180" y="166" width="436" height="14" fill="#1c7ed6"/><text x="620" y="177" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">99.00</text>
  <text x="170" y="220" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">320Bオープンモデル</text>
  <rect x="180" y="208" width="8" height="14" fill="#adb5bd"/><text x="192" y="219" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">1.89</text>
  <rect x="180" y="226" width="294" height="14" fill="#1c7ed6"/><text x="478" y="237" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">66.93</text>
  <line x1="180" y1="246" x2="620" y2="246" stroke="#dee2e6" stroke-width="1"/>
  <text x="180" y="260" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">0</text>
  <text x="396" y="260" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">50</text>
  <text x="616" y="260" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">100（RHAE）</text>
  <rect x="30" y="276" width="660" height="62" rx="8" fill="#fff9db" stroke="#e9d66b"/>
  <text x="48" y="300" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#7a5c00">少ないほど良い：</text>
  <text x="48" y="322" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">画像は1ゲーム3070万トークン、数字表は7190万 · コンテキスト20万→78万でスコア99→93.9 · 画像16倍拡大で88.3へ低下</text>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">RHAE（人間相対行動効率）は、人間に対するシステムの解法効率を測る指標。テストした全モデルが向上し、ベースラインが弱いほど伸びが大きい。</p>

画像は数字グリッドより安い。1ゲーム3,070万トークン対7,190万トークン。コンテキスト拡大は害だった。20万→78万トークンでスコア99→93.9。16倍拡大で88.3。長いコンテキストを競う業界への答えは異端だ。勝つのは大きなバケツではない。ノートの開きどころを知るモデルだ。

34のGameWorldゲームで63.3%、人間初心者の55.3%を上回る。3D透視シーンでは84.12。オーダーメイドのスーツではなく、何にでも合う一組の目。

モデルは公開ゲームのリリース後に学習された。非公開セットこそ汎化の真のテスト。同じ重みでの前後比較は鉄壁だ。天井がどこにあろうと、床は上がった。

報道が見逃す部分だ。フロンティアモデルが目の飢えで過小評価されていたなら、ここ2年のエージェント評価は作り直しが必要。比べていたのはモデルでなく配管だった。変わるのは順位だけではない。GUIDE.mdとWORKING.mdの働きは視覚に匹敵するかもしれない。物忘れしていたのかもしれない。

「ハーネスがモデルに勝つ」ではない。ボトルネックのラベルを間違えた。推論不足の正体は知覚と記憶の不足、解法は配管とテキストファイルだ。次のブレークスルーに新パラメータは不要かもしれない。要るのは、モデルが見えていないものに気づく誰かだ。

出典：[論文](https://arxiv.org/abs/2610.02200)（arXiv:2610.02200）、[MITライセンスのコード](https://github.com/joshhhhhan/vista)と[プロジェクトページ](https://vista-research.github.io/)、ARC Prizeにおけるチームの[公式スコアカード](https://arcprize.org/scorecards/39be671a-d0cc-48b4-ae08-1db4abc44c83)（リポジトリからリンク）。

**ディスカッション：** ARC-AGI-3の最後の1マイルを埋めたのがモデルではなくハーネスだったとしたら——あなたのAIの進歩についての確信のうち、どれが実は配管についての確信だろうか？
