---
lng_pair: id_20261015_pingpongduo-table-tennis
title: "PingpongDuo：2台のヒューマノイド、1台の卓球台、衝突ゼロ"
author: OpenSI-Labs
category: robotics
tags: [ヒューマノイドロボット, 卓球, マルチロボット協調, 強化学習, PingpongDuo]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-pingpongduo-table-tennis.png
meta_description: "PingpongDuoは2台のヒューマノイドロボットに卓球ダブルスを教える：厳密な交互打球、共有ワークスペース、衝突なし。返球成功率13.2%向上、実機で10回以上の連続交互ラリーを達成。"
---

**ロボット卓球はもう古いニュースだ。ロボットのダブルスは別の競技である。**

ヒューマノイドがピンポン球を打ち返すのは、今や定番のデモになった。DeepMindのアームは2024年に競技レベルで戦い、ソニーのAceはプロ選手と対戦して*Nature*に掲載され、バークレーのHITTERは人間相手に106回連続ラリーを記録し（[HITTER, arXiv:2508.21043](https://arxiv.org/pdf/2508.21043)）、香港大学のSMASHは搭載カメラの視覚だけでそれを成し遂げた（[arXiv:2604.01158](https://arxiv.org/html/2604.01158v1)）。だがダブルスは違う。台の同じ側に2人が立ち、厳密に交互に打たねばならず、数平方メートルの床を共有する。パートナーは絶対にぶつかってはならない動く障害物であり、自分が打った瞬間に相手のために場所を空けなければならない。

10月14日に公開された論文は、このダブルスに正面から取り組んだ（[Jiangら, arXiv:2610.20579](https://arxiv.org/abs/2610.20579v1)）。PingpongDuoは、安全なチーム協調を備えた俊敏なヒューマノイドダブルスのための階層型フレームワークであり、実機上で2台のフルサイズヒューマノイドが交互にラリーを続けた初のシステムだ。

アーキテクチャは、コーチの戦術ボードのように問題を分割する。チームレベルでは、プランナーが2台の位置目標を共同で選び、学習済みリスク推定で危険な提案をフィルタリングする。現在の打者のスペースを優先的に守るため、打とうとするロボットがスイングの最中に場所の交渉を強いられることはない。個体レベルでは、フットワークと打球は別々に学習されたスキルだ。俊敏な脚が位置取りを担い、精密なラケット制御が仕上げを担う。スキルは人間の動作リファレンス（実際の人間ダブルスのフットワークを含む）に導かれ、さらに巧妙な工夫として、互いが生成した状態から訓練される。フットワーク方策は、打球方策が引き継ぎやすい位置で止まることを学ぶのだ。

<figure>
<svg viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">ダブルスは引き継ぎの問題：打つ、空ける、打つ</text>
<rect x="20" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="95" y="88" font-size="14" font-weight="bold" text-anchor="middle">ロボットAが打球</text>
<text x="95" y="112" font-size="14" text-anchor="middle">アーム残差方策が</text>
<text x="95" y="132" font-size="14" text-anchor="middle">移動後に打球を</text>
<text x="95" y="156" font-size="14" text-anchor="middle" font-style="italic">微調整</text>
<rect x="200" y="60" width="150" height="120" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="275" y="88" font-size="14" font-weight="bold" text-anchor="middle">ロボットAが退避</text>
<text x="275" y="112" font-size="14" text-anchor="middle">2.4秒で2.15m、</text>
<text x="275" y="132" font-size="14" text-anchor="middle">最高速度</text>
<text x="275" y="156" font-size="14" text-anchor="middle">2.23 m/s</text>
<rect x="380" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="455" y="88" font-size="14" font-weight="bold" text-anchor="middle">ロボットBが位置取り</text>
<text x="455" y="112" font-size="14" text-anchor="middle">チームプランナーが</text>
<text x="455" y="132" font-size="14" text-anchor="middle">危険な目標を除外、</text>
<text x="455" y="156" font-size="14" text-anchor="middle">打者の空間を死守</text>
<rect x="560" y="60" width="100" height="120" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="610" y="88" font-size="14" font-weight="bold" text-anchor="middle">ロボットB</text>
<text x="610" y="112" font-size="14" font-weight="bold" text-anchor="middle">打球</text>
<text x="610" y="140" font-size="14" text-anchor="middle">→ 循環</text>
<line x1="170" y1="120" x2="196" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="350" y1="120" x2="376" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="530" y1="120" x2="556" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<path d="M 610 180 C 610 280, 95 280, 95 184" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#p1)"/>
<text x="340" y="262" font-size="14" text-anchor="middle">厳密な交互：打つたびに台をパートナーへ引き継ぐ</text>
<text x="340" y="292" font-size="14" text-anchor="middle">フットワークと打球は互いの生成状態から学習</text>
<text x="340" y="318" font-size="14" text-anchor="middle" font-style="italic">実測の球道・接触データで校正したシミュレータ</text>
<defs><marker id="p1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>1回のやり取り：打球、ワークスペースの退避、パートナーの位置取り、再び打球——プランナーが打者の空間を守り続ける。</figcaption>
</figure>

シミュレーションから実機への橋渡しは、異例なほど誠実なエンジニアリングだ。ラケットアーム残差方策は、移動完了後に打球を微調整する。そのフィードバックは、実際の球の飛びと接触の測定で校正されたシミュレータから得られる。汎用物理エンジンではなく、この球が実際にどう飛びどう跳ねるかに調整されたものだ。シミュレーションでは、PingpongDuoは最強ベースラインの返球成功率を13.2%上回った。実機の数値はアスリートの成績表のようだ。2.15メートルの「退避—復帰」サイクルを2.4秒で完走、最高速度2.23メートル毎秒、退避中の位置誤差は約2センチ。そして2台のロボットが厳密な交互で10回以上の連続打球を維持した（[ArXivSignals要約](https://arxivsignals.io/explore)）。

<figure>
<svg viewBox="0 0 680 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">シミュレーションだけでなく実機で測定</text>
<text x="230" y="72" font-size="14" text-anchor="end">返球成功率（シミュ）</text>
<rect x="240" y="56" width="300" height="24" rx="4" fill="#3366cc"/><text x="548" y="73" font-size="14">最強比 +13.2%</text>
<text x="230" y="118" font-size="14" text-anchor="end">退避 + 復帰</text>
<rect x="240" y="102" width="200" height="24" rx="4" fill="#cc8833"/><text x="448" y="119" font-size="14">2.15 m / 2.4 s</text>
<text x="230" y="164" font-size="14" text-anchor="end">最高速度</text>
<rect x="240" y="148" width="230" height="24" rx="4" fill="#cc8833"/><text x="478" y="165" font-size="14">2.23 m/s</text>
<text x="230" y="210" font-size="14" text-anchor="end">交互ラリー（実機）</text>
<rect x="240" y="194" width="260" height="24" rx="4" fill="#339966"/><text x="508" y="211" font-size="14">10回以上、厳密な交互</text>
<text x="340" y="254" font-size="14" text-anchor="middle" font-style="italic">退避中の位置誤差：約2センチ</text>
</svg>
<figcaption>シミュレーションの向上に実機のアスリート性が加わる：2.4秒の退避ダッシュは、シングルス用システムには不要だったダブルス固有のスキルだ。</figcaption>
</figure>

多くの報道が見逃す視点はここだ。ダブルスとは、マルチロボットのチームワークが計画の抽象論をやめ、物理の問題になる場所である。これまでの「ロボットチーム」研究では、協調とはタスクの分担かソフトウェア上の順番待ちを意味した。ここではパートナーは、スイング半径内にいる50キロの動く障害物であり、球は秒速数メートルで飛び、「自分の番」と「相手の番」の引き継ぎは全身のダッシュだ。学習済みリスクフィルターこそ概念的な貢献である。2台を共同で計画して祈るのではなく、打者のワークスペースを神聖なものとして扱い、それを脅かすものに拒否権を発動する。安全は後付けの制約ではなく、プランナーの最初の仕事なのだ。

率直な留保もある。10回の交互打球はラリーであって試合ではない。論文は手強い相手も、強烈な回転も、会場の騒音も報告していない。実戦の混沌はまだ先だ。そしてシミュレーションで育ったアスリートは皆そうであるように、このシステムの上限は校正されたシミュレータの真実度に依存する。

それでも方向は明確だ。シングルスはロボットがアスリートになれることを証明した。ダブルスはチームメイトになれることを証明する。パートナーの動きを予測し、空間を譲り、次のスキルが必要とする場所に正確に到着する。台は小さく、球は速い。そして初めて、ロボットは一人でプレーしていない。

2台のロボットが衝突せずに1台の卓球台を共有できるようになったとき——予測すべきパートナーが人間になったら、何が変わるだろうか？
