---
lng_pair: id_20261012_sakana-mass-self-improvement
title: "MASS：自分自身を研究チームに編成した27Bモデル"
author: OpenSI-Labs
category: research
tags: [再帰的自己改善, マルチエージェントシステム, Sakana AI, 自己教師あり学習, ワークフロー最適化]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-sakana-mass-self-improvement.png
meta_description: "Sakana AIのMASSは、1つの27Bモデルに解法者・最適化者・評価者の3役を担わせて自己改善ループを回す。その結果、ボトルネックは評価者ではなく最適化者にあることが分かった。"
---

フロンティアAIの「監督の限界」は工学の問題だ。モデルが一人前の科学者になったら、何を信号に育てるのか。オープンエンドな課題に正解もテストも、「良い」と「卓越」を見分ける人間もいない。期待が大きい課題ほど、モデルは人間の評価限界に近づく。

Sakana AIが今週末UC Berkeleyと共同発表したMASS（Multi-Agent Self-Supervision、[論文](https://arxiv.org/abs/2610.12176)、[公式ブログ](https://pub.sakana.ai/mass/)）の答えはこうだ。外から誰も監督できないなら、モデルに自分でチームを編成させ、その働き方から学ばせればいい。

仕組みはこうだ。共有27Bモデル（Qwen3.6-27B、オープンウェイト）が、自分で回すループで3役を演じる——解法者、最適化者、評価者。*同質*再帰的自己改善だ。単一インスタンスは同質ループで自らの複雑な推論を批判・改善できず、マルチエージェント構成の方が複雑な推論に強い。モデルは自分のコピーで限界を突破する。

内側ループは重み固定のまま「より良い働き方」を探索する。モデルはワークフロー——仮想サブエージェントへの課題分担計画——を書き下す。各ロールの指示、成果物の引き渡し（コントラクト）、呼び出し順序。実行者が回し、評価者がチャンピオンと比較し、最適化者が改訂。ガードレール付き進化探索だ。

<figure>
<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<defs><marker id="marrow" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#3366cc"/></marker></defs>
<rect x="230" y="10" width="180" height="52" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="320" y="32" font-size="14" font-weight="bold" text-anchor="middle">共有モデル</text>
<text x="320" y="50" font-size="12" text-anchor="middle">Qwen3.6-27B、オープンウェイト</text>
<rect x="40" y="110" width="270" height="150" rx="12" fill="#f7f9ff" stroke="#3366cc" stroke-width="2"/>
<text x="175" y="134" font-size="14" font-weight="bold" text-anchor="middle">内側ループ：ワークフロー探索</text>
<text x="175" y="156" font-size="12" text-anchor="middle">ワークフロー = ロール · 指示 ·</text>
<text x="175" y="172" font-size="12" text-anchor="middle">コントラクト · 呼び出し順序</text>
<text x="175" y="196" font-size="12" text-anchor="middle">実行 → チャンピオンと比較評価 →</text>
<text x="175" y="212" font-size="12" text-anchor="middle">最適化者がワークフローを改訂</text>
<text x="175" y="236" font-size="12" font-style="italic" text-anchor="middle">重みは固定のまま</text>
<rect x="330" y="110" width="270" height="150" rx="12" fill="#fff8ee" stroke="#cc8833" stroke-width="2"/>
<text x="465" y="134" font-size="14" font-weight="bold" text-anchor="middle">外側ループ：蒸留</text>
<text x="465" y="156" font-size="12" text-anchor="middle">チャンピオンを課題ごとに18回実行</text>
<text x="465" y="172" font-size="12" text-anchor="middle">Bradley-Terryで自己順位付け；</text>
<text x="465" y="188" font-size="12" text-anchor="middle">上位16軌跡のみ残す</text>
<text x="465" y="212" font-size="12" text-anchor="middle">足場を剥がしてLoRAで微調整</text>
<text x="465" y="236" font-size="12" font-style="italic" text-anchor="middle">重みが変わるのはここ</text>
<line x1="250" y1="62" x2="178" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="390" y1="62" x2="462" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="310" y1="185" x2="328" y2="185" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<text x="292" y="178" font-size="11" text-anchor="middle">チャンピオン</text>
<line x1="606" y1="160" x2="606" y2="36" stroke="#cc8833" stroke-width="2"/>
<line x1="606" y1="36" x2="412" y2="36" stroke="#cc8833" stroke-width="2" marker-end="url(#marrow)"/>
<text x="508" y="28" font-size="11" text-anchor="middle">更新されたモデルが3役に復帰</text>
</svg>
<figcaption>内側ループはより良いチームの働き方を探索し、外側ループは最良のチームの働きを重みに蒸留する。</figcaption>
</figure>

外側ループはループが自分を「食べる」場所だ。チャンピオンを課題ごとに18回実行し、自己順位付けで上位16軌跡だけ残す。足場を剥がしてLoRAで微調整し、更新されたモデルが3役に復帰する。2サイクル後、4つの研究ベンチマークで出力トークンあたりのスコアはベースの1.2〜1.6倍（MLR-Bench 1.60倍、DSBench 1.35倍、AstaBench 1.28倍、ScienceAgentBench 1.20倍）。勝率は53.9%から69.9%へ。マルチエージェント軌跡の学生は31%少ない教師ありトークン（28.8M対42M）で同等の勝率を出した。

だが誠実な失敗もある。コード中心のSWE-bench VerifiedとTerminal-Bench 2.0では、同じシステムがベースの0.94倍・0.96倍に*低下*した。MASSはモデルを全面的に賢くしなかった。優れた研究者に変えた代償にコーディングが落ちたのだ。

<figure>
<svg viewBox="0 0 640 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<line x1="273" y1="20" x2="273" y2="240" stroke="#999" stroke-width="1.5" stroke-dasharray="6,4"/>
<text x="273" y="256" font-size="11" text-anchor="middle" fill="#666">ベース = 1.0倍</text>
<text x="170" y="52" font-size="12" text-anchor="end">MLR-Bench</text>
<rect x="180" y="38" width="280" height="22" rx="4" fill="#3366cc"/><text x="468" y="54" font-size="12">1.60倍</text>
<text x="170" y="92" font-size="12" text-anchor="end">DSBench</text>
<rect x="180" y="78" width="165" height="22" rx="4" fill="#3366cc"/><text x="353" y="94" font-size="12">1.35倍</text>
<text x="170" y="132" font-size="12" text-anchor="end">AstaBench</text>
<rect x="180" y="118" width="133" height="22" rx="4" fill="#3366cc"/><text x="321" y="134" font-size="12">1.28倍</text>
<text x="170" y="172" font-size="12" text-anchor="end">ScienceAgentBench</text>
<rect x="180" y="158" width="95" height="22" rx="4" fill="#3366cc"/><text x="283" y="174" font-size="12">1.20倍</text>
<text x="170" y="212" font-size="12" text-anchor="end">SWE-bench Verified</text>
<rect x="180" y="198" width="66" height="22" rx="4" fill="#cc3333"/><text x="254" y="214" font-size="12">0.94倍</text>
<text x="320" y="14" font-size="13" font-weight="bold" text-anchor="middle">2回のMASSサイクル後、出力トークンあたりのスコア（ベース比）</text>
</svg>
<figcaption>改善には方向がある。モデルはより優れた研究者になったが、コーディングはわずかに低下した。</figcaption>
</figure>

この非対称こそ本当の話だ。再帰的自己改善は「満ち潮」——一様に賢くなる——と語られがちだが、MASSは徒弟制に近い。モデルはループの報酬方向に特化し、隣接技能で代償を払う。自己改善する研究者がコードを忘れていくのは、専門家の常だ。RSIがスケールすれば、未来は万能の汎用モデルではなく、自己改善する専門家の生態系になる。

2つ目の意外は定説を覆す。自己採点ループで最も危険なのは*評価者*とされてきたが、アブレーションは逆を示した。評価者の強化はほぼ無効で、*最適化者*の強化が効いた。自己改善ループでは候補の判定より良い候補の生成が重要——ボトルネックは批評者ではなく提案者だ。設計指針は探索への投資だ。

著者らが自ら名指した悪夢こそ敬意に値する。同じモデルが生産し、判定し、その結果で訓練するとき、共有の盲点が「生み出され、改善として承認され、次世代に組み込まれる」——再帰的自己改善のアキレス腱だ。進歩を*測定*するには外部の判定者（GPT-5.5、Claude Opus 4.8）が要り、その判定は決してループに入れない。真に閉じたループは自分が改善しているかを知れない。MASSはこの溝を埋めない。溝の内側で可能な最高の機械を作るだけだ。

コードも論文もオープンだ。MASSは知能爆発ではない。もっと稀なもの——動いて、測定され、「どこが良くなり、どこが悪くなり、どの部品が足を引っ張ったか」を正確に報告する自己改善ループである。

**ディスカッション：** 再帰的自己改善がモデルをループの報酬課題に特化させるなら、どの課題に自己改善ループを与えるかを誰が決め、モデルに失わせてよい技能はどれなのか？
