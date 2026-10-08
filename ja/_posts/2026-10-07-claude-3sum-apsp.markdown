---
lng_pair: id_20261007_claude-3sum-apsp
title: "二つの仮説を破った0.0008"
author: OpenSI-Labs
category: research
tags: [計算複雑性理論, アルゴリズム, AIによる数学的発見, 形式的検証]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-claude-3sum-apsp.png
meta_description: "Anthropicの内部研究モデルが教科書を上回る3SUMと全点対最短経路のアルゴリズムを発見し、複雑性理論の二つの柱を覆した——しかも偶然の産物である。"
---

何十年も二つの数字が教科書に釘付けだった。3SUMは約 *n*²、全点対最短経路は約 *n*³。定数は削られ続けたが、指数は動かなかった。

10月5日、動いた。Alman（コロンビア大）とVassilevska Williams（MIT）が3SUMをO(*n*^1.9992)、全点対最短経路をO(*n*^2.9995)で解く決定性アルゴリズムを発表。教科書初の多項式改善であり、3SUM仮説・APSP仮説への反証だ（[抄録](https://arxiv.org/abs/2610.06783v1)、[全文](https://arxiv.org/html/2610.06783v1)）。道連れはExact Triangle仮説（新O(*n*^2.9983)）ら。SETHは無事である。

<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="教科書の指数と新しい指数の比較、軸を拡大">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"Hiragino Kaku Gothic ProN","Yu Gothic",sans-serif;}</style>
<text x="24" y="34" font-size="17" font-weight="700" fill="#111827">3SUM</text>
<text x="24" y="56" font-size="12.5" fill="#6b7280">軸を25倍に拡大：1.990 – 2.010</text>
<line x1="150" y1="100" x2="610" y2="100" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="94" x2="150" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1.990</text>
<line x1="265" y1="94" x2="265" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1.995</text>
<line x1="380" y1="94" x2="380" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.000</text>
<line x1="495" y1="94" x2="495" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.005</text>
<line x1="610" y1="94" x2="610" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.010</text>
<line x1="380" y1="70" x2="380" y2="100" stroke="#374151" stroke-width="3"/><text x="392" y="80" font-size="13" font-weight="600" fill="#374151">教科書：n&#178;</text>
<line x1="361.6" y1="70" x2="361.6" y2="100" stroke="#b45309" stroke-width="3"/><text x="150" y="80" font-size="13" font-weight="600" fill="#b45309">新：n<tspan baseline-shift="super" font-size="9">1.9992</tspan></text>
<line x1="361.6" y1="140" x2="380" y2="140" stroke="#b45309" stroke-width="1.5"/><line x1="361.6" y1="135" x2="361.6" y2="145" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="135" x2="380" y2="145" stroke="#b45309" stroke-width="1.5"/><text x="370.8" y="158" font-size="12" fill="#b45309" text-anchor="middle">0.0008</text>
<text x="24" y="196" font-size="17" font-weight="700" fill="#111827">APSP</text>
<text x="24" y="218" font-size="12.5" fill="#6b7280">軸を25倍に拡大：2.990 – 3.010</text>
<line x1="150" y1="262" x2="610" y2="262" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="256" x2="150" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2.990</text>
<line x1="265" y1="256" x2="265" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2.995</text>
<line x1="380" y1="256" x2="380" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.000</text>
<line x1="495" y1="256" x2="495" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.005</text>
<line x1="610" y1="256" x2="610" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.010</text>
<line x1="380" y1="232" x2="380" y2="262" stroke="#374151" stroke-width="3"/><text x="392" y="242" font-size="13" font-weight="600" fill="#374151">教科書：n&#179;</text>
<line x1="368.5" y1="232" x2="368.5" y2="262" stroke="#b45309" stroke-width="3"/><text x="150" y="242" font-size="13" font-weight="600" fill="#b45309">新：n<tspan baseline-shift="super" font-size="9">2.9995</tspan></text>
<line x1="368.5" y1="302" x2="380" y2="302" stroke="#b45309" stroke-width="1.5"/><line x1="368.5" y1="297" x2="368.5" y2="307" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="297" x2="380" y2="307" stroke="#b45309" stroke-width="1.5"/><text x="374.2" y="322" font-size="12" fill="#b45309" text-anchor="middle">0.0005</text>
</svg>
*指数の比較（25倍拡大）。この隙間がニュースだ。*

10億入力でも差は2%未満。意義は実用でなく構造だ。「3SUMが易しくない限りXは *n*²」という数百の定理の土台が *n*^1.9992 にずれた。

仕組みは変わり種の行列積だ。縦長×横長の行列積で、欲しいのはまばらな数成分だけ——それだけをO(*N*²/*D*^0.063)手で計算する。Coppersmith（1982）の矩形行列積（Schönhageの十積恒等式が源流）を改造し、不要な演算を省いた。グラフに訳せば「いびつな」三部グラフでの三角形の高速検出で、帰着により3SUMと最短経路へ。

<svg viewBox="0 0 640 370" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="いびつな三部グラフと強調された三角形">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"Hiragino Kaku Gothic ProN","Yu Gothic",sans-serif;}</style>
<text x="320" y="26" font-size="13" fill="#6b7280" text-anchor="middle">ごく小さな側：n<tspan baseline-shift="super" font-size="9">&#949;</tspan> 頂点</text>
<circle cx="300" cy="52" r="7" fill="#9ca3af"/><circle cx="322" cy="44" r="7" fill="#9ca3af"/><circle cx="344" cy="52" r="7" fill="#9ca3af"/>
<g stroke="#d1d5db" stroke-width="1">
<line x1="300" y1="52" x2="130" y2="120"/><line x1="300" y1="52" x2="130" y2="200"/><line x1="300" y1="52" x2="130" y2="280"/>
<line x1="322" y1="44" x2="130" y2="160"/><line x1="322" y1="44" x2="130" y2="240"/><line x1="322" y1="44" x2="510" y2="160"/>
<line x1="344" y1="52" x2="130" y2="120"/><line x1="344" y1="52" x2="510" y2="200"/><line x1="344" y1="52" x2="510" y2="280"/>
<line x1="300" y1="52" x2="510" y2="120"/><line x1="300" y1="52" x2="510" y2="200"/><line x1="300" y1="52" x2="510" y2="280"/>
<line x1="322" y1="44" x2="510" y2="120"/><line x1="322" y1="44" x2="510" y2="240"/><line x1="344" y1="52" x2="130" y2="200"/>
</g>
<g fill="#6b7280">
<circle cx="110" cy="120" r="7"/><circle cx="150" cy="120" r="7"/><circle cx="110" cy="160" r="7"/><circle cx="150" cy="160" r="7"/><circle cx="110" cy="200" r="7"/><circle cx="150" cy="200" r="7"/><circle cx="110" cy="240" r="7"/><circle cx="150" cy="240" r="7"/><circle cx="110" cy="280" r="7"/><circle cx="150" cy="280" r="7"/>
<circle cx="490" cy="120" r="7"/><circle cx="530" cy="120" r="7"/><circle cx="490" cy="160" r="7"/><circle cx="530" cy="160" r="7"/><circle cx="490" cy="200" r="7"/><circle cx="530" cy="200" r="7"/><circle cx="490" cy="240" r="7"/><circle cx="530" cy="240" r="7"/><circle cx="490" cy="280" r="7"/><circle cx="530" cy="280" r="7"/>
</g>
<g stroke="#d97706" stroke-width="3.5" fill="none">
<line x1="130" y1="200" x2="322" y2="44"/><line x1="322" y1="44" x2="510" y2="200"/><line x1="510" y1="200" x2="130" y2="200"/>
</g>
<circle cx="130" cy="200" r="9" fill="#d97706"/><circle cx="322" cy="44" r="9" fill="#d97706"/><circle cx="510" cy="200" r="9" fill="#d97706"/>
<text x="130" y="322" font-size="13" fill="#374151" text-anchor="middle">n 頂点</text>
<text x="510" y="322" font-size="13" fill="#374151" text-anchor="middle">n 頂点</text>
<text x="320" y="352" font-size="12.5" fill="#b45309" text-anchor="middle">高速に見つけた一つの三角形——本当に計算すべきはこれだけ</text>
</svg>
*「いびつな」グラフで三角形を高速に見つけ、帰着で3SUMと最短経路へ。*

記憶すべきは発見の経緯だ。論文は核心を「Claude, an AI model developed by Anthropic」に帰す。社員が内部モデルに暗号の未解決問題の検証・強化を命じたところ、Claudeは仮説を弱めるアルゴリズムを持ち帰った。平均時が先、次に最悪時。1600万トークン、人間介入ゼロ。

9月、Anthropicは守秘契約で両著者に渡し、報酬と公開版Claudeを与えた。人間が理解・単純化・強化・拡張し、論文に責任を持つ。その後、内部モデルがLean 4＋Mathlibで主要結果を形式検証しGitHubで公開。機械が発見し、コンパイラが検算した。8月のリーマン下界、9月のフェルマー形式化に続くが、前二者が検証だったのに対し今回は発見だ。

見逃されがちな視点。Claudeは監査人として雇われ、金庫破りとして帰ってきた。暗号の困難性仮説は明確で機械検証可能な予想そのものだ。疲れを知らないエージェントが大規模監査できる。初の本格監査で指数が二つ動いた。問いは、どれが耐え、崩れたものをどうするか、だ。

方法論の転換もある。アイデア生産は安くなった。希少なのは検証——人間の理解と、ごまかせないコンパイラだ。数学は「推測」と「証明」の対話。推測は自動化されたが、証明はまだだ。

注意。これは二日前のプレプリントだ。Leanは主要な決定性結果をカバーするが、実数上の乱択boundは論文のみに依拠する。指数は「主張」であって「確定」ではない。

**困難性仮説への初の機械監査が偶然二つの仮説を破った。次の1600万トークンをどの問題に向けるべきか。次の亀裂を持ち帰ったとき、受け止める覚悟はあるか。**

*出典：[Alman &amp; Vassilevska Williams, arXiv 2610.06783](https://arxiv.org/abs/2610.06783v1) · [全文](https://arxiv.org/html/2610.06783v1) · [CellCogによる詳細な読解](https://cellcog.ai/blog/claude-3sum-apsp-algorithm/)*
