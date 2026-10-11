---
lng_pair: id_20261011_viola-humanoid-human-data
title: "VioLA：人間の動作データから学ぶヒューマノイド"
author: OpenSI-Labs
category: robotics
tags: [ヒューマノイド, 模倣学習, 動作潜在空間, Unitree G1, 汎用ポリシー]
date: 2026-10-11 06:00:00 -0700
img: /assets/img/posts/2026-10-11-viola-humanoid-human-data.png
meta_description: "VioLAは関節指令ではなく動作潜在変数を予測することで、人間の動作記録をそのまま汎用ヒューマノイドポリシーの学習データに変える。"
---

ヒューマノイドの難所はハードではない。G1は中古車並みでバク宙できる。難しいのは「教える」こと——新タスクのたび数時間のテレオペで関節角度を記録し学習させる。遅く高コストだ。

Mert Albabaら（arXiv:2610.12435）はテレオペ部隊を増やすのでなく、ポリシーの予測対象を変えた。VioLAである。

## 動作そのものを予測する

障害は二つ。行動空間は広く強結合で関節指令は学びにくく、デモは希少。人間の動作データは膨大だが、人の動きはロボットの指令ではない。

VioLAは一手で解く。ポリシーは関節指令でなく身体と手の**動作潜在変数**を予測する——「痙攣の列挙」でなく「一回転」と記述するように、動作そのものは身体を越えて翻訳できる。

仕組みは三つ。**動作エンコーダ**が記録を符号化し、人間と機械の同じ動作を潜在空間の同じ領域に落とす。**汎用ポリシー**は次の動作符号だけを予測。**身体・手コントローラ**（事前学習済み・凍結）が符号をトルクにデコードする。

人間の記録はすべてラベル付き学習例になる。1億4060万フレーム中**93.2%が人間**だった。

<figure>
<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="120" y="22" font-size="15" font-weight="bold" text-anchor="middle">従来手法</text>
<rect x="30" y="40" width="180" height="44" rx="8" fill="#f0f4ff" stroke="#3366cc"/>
<text x="120" y="66" font-size="13" text-anchor="middle">ポリシーが予測</text>
<text x="120" y="80" font-size="13" text-anchor="middle" font-weight="bold">関節指令</text>
<line x1="120" y1="84" x2="120" y2="112" stroke="#3366cc" stroke-width="2" marker-end="url(#a1)"/>
<rect x="30" y="112" width="180" height="44" rx="8" fill="#ffecec" stroke="#cc3333"/>
<text x="120" y="131" font-size="13" text-anchor="middle">テレオペ収集の</text>
<text x="120" y="146" font-size="13" text-anchor="middle" font-weight="bold">ロボットデモが必須</text>
<text x="120" y="180" font-size="13" text-anchor="middle" fill="#cc3333">✗ 希少・高コスト</text>
<text x="520" y="22" font-size="15" font-weight="bold" text-anchor="middle">VioLA</text>
<rect x="430" y="40" width="180" height="44" rx="8" fill="#f0f4ff" stroke="#3366cc"/>
<text x="520" y="66" font-size="13" text-anchor="middle">ポリシーが予測</text>
<text x="520" y="80" font-size="13" text-anchor="middle" font-weight="bold">動作潜在変数</text>
<line x1="520" y1="84" x2="520" y2="112" stroke="#3366cc" stroke-width="2" marker-end="url(#a1)"/>
<rect x="430" y="112" width="180" height="44" rx="8" fill="#e8f8ec" stroke="#2a9d48"/>
<text x="520" y="131" font-size="13" text-anchor="middle">凍結コントローラが</text>
<text x="520" y="146" font-size="13" text-anchor="middle">潜在変数を実行</text>
<text x="520" y="180" font-size="13" text-anchor="middle" fill="#2a9d48">✓ 人間の映像で学習</text>
<line x1="210" y1="62" x2="430" y2="62" stroke="#999" stroke-width="1.5" stroke-dasharray="6,4"/>
<text x="320" y="52" font-size="13" text-anchor="middle" fill="#555">予測対象を</text>
<text x="320" y="68" font-size="13" text-anchor="middle" fill="#555">変える</text>
<text x="320" y="150" font-size="13" text-anchor="middle" fill="#555">1億4060万フレーム、</text>
<text x="320" y="166" font-size="13" text-anchor="middle" fill="#555">93.2%が人間</text>
<defs><marker id="a1" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 z" fill="#3366cc"/></marker></defs>
</svg>
<figcaption style="font-size:0.85em;color:#666;text-align:center">従来手法とVioLA：関節指令を予測するポリシーはロボット固有のデモを要する。共有の動作潜在変数を予測すれば、人間の記録が学習データになる。</figcaption>
</figure>

## 数字は驚異的だ

実機G1、未見の歩行指示、微調整なしで**100%**。ベースラインGR00T N1.7とΨ₀は16.7%と0%。把持も**88.6%**、微調整なし。人間のデモだけで実機ゼロショット歩行——人間のデータこそ鍵だった。（プレプリント、コード未公開。）

## 経済の変化

業界の堀のテレオペ部隊に代わり、希少資産は「エンコーダ＋コントローラ」になる。最高の身体言語辞書がレバレッジを握る。

「身体言語」を共有するなら言語は機体に縛られない。今日G1のポリシーが明日は別のヒューマノイドを駆動できる——「身体非依存」のポリシーだ。未証明だが、そこを指す。

ロボット学は十年かけロボットのデータを集めた。VioLAは方向が逆だった可能性を示す——データは人間の記録の中にあった。足りなかったのは二つの身体が話せる言語だけだ。

**議論：** 「動き」の記録が学習データになるなら、その所有権は誰のものか。

---
*出典：[arXiv:2610.12435](https://arxiv.org/abs/2610.12435)；[QUE.com](https://que.com/world-models-redefine-the-future-of-autonomous-robotics/)。*
