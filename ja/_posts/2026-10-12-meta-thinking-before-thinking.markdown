---
lng_pair: id_20261012_meta-thinking-before-thinking
title: "考える前に考える：自己管理を学んだエージェント"
author: OpenSI-Labs
category: research
tags: [メタ推論, AIエージェント, 推論スケーリング, LLM制御, テスト時計算]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-meta-thinking-before-thinking.png
meta_description: "Metaの《Thinking Before Thinking》はエージェントを「働くワーカー」と「決めるコントローラー」に分離——制御に使う計算を新たなスケーリング軸にした。"
---

AIエージェントは二つの仕事を同時にこなす。作業と、次の一手の決定だ。今日のフレームワークでは制御判断が作業に絡み合い、その場しのぎで下される。

Meta Superintelligence Labsの新論文は、この絡み合いこそボトルネックだと主張する。["Thinking Before Thinking: Scaling Agentic Inference Through Meta-Reasoning"](https://arxiv.org/abs/2609.38147)（Dahalら、arXiv:2609.38147、9月29日）はエージェントを二つに割る。ワーカーは作業だけ、独立した**コントローラー**は次の仕事を決めるだけ。

## 四ストロークエンジン

コントローラーは四段階を回す。**評価**（要約を更新）、**提案**（*予算を知らずに*候補列挙）、**査定**（予算と照らして値踏み。定性判断）、**派遣**（指示を書き文脈を選ぶ——文脈の選択こそ計算の選択。あるいは停止）。

産出はID付き**アーティファクト**として保存され、「XがYを生んだ」という辺が**グラフ**を成す。成功の*仕方*を測る——再利用、カバレッジ、選択の正しさ。

<svg viewBox="0 0 720 460" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="メタ推論の制御ループ">
  <defs>
    <marker id="mArrJa" markerWidth="10" markerHeight="10" refX="8" refY="5" orient="auto"><path d="M0,0 L10,5 L0,10 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="30" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="18" font-weight="700" fill="#212529">コントローラーは独自ループを回す——ワーカーは働くだけ</text>
  <rect x="60" y="60" width="600" height="180" rx="12" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="360" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="16" font-weight="700" fill="#495057">コントローラー（決めるだけ、実行しない）</text>
  <rect x="90" y="110" width="120" height="60" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="150" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#1864ab">評価</text>
  <text x="150" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">要約状態を更新</text>
  <rect x="230" y="110" width="120" height="60" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="290" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#1864ab">提案</text>
  <text x="290" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">候補列挙（予算不知）</text>
  <rect x="370" y="110" width="120" height="60" rx="8" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="430" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#e67700">査定</text>
  <text x="430" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">コストに見合うか？</text>
  <rect x="510" y="110" width="120" height="60" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="570" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#1864ab">派遣</text>
  <text x="570" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">または停止</text>
  <line x1="210" y1="140" x2="228" y2="140" stroke="#1c7ed6" stroke-width="2" marker-end="url(#mArrJa)"/>
  <line x1="350" y1="140" x2="368" y2="140" stroke="#1c7ed6" stroke-width="2" marker-end="url(#mArrJa)"/>
  <line x1="490" y1="140" x2="508" y2="140" stroke="#1c7ed6" stroke-width="2" marker-end="url(#mArrJa)"/>
  <text x="360" y="205" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">コントローラーが見るのは要約＋アーティファクト図のみ</text>
  <rect x="180" y="270" width="160" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="260" y="298" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#a61e4d">ワーカー</text>
  <text x="260" y="320" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">実行のみ、決定しない</text>
  <rect x="380" y="270" width="160" height="70" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="460" y="298" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#2b8a3e">アーティファクト図</text>
  <text x="460" y="320" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">永続共有メモリ</text>
  <line x1="570" y1="170" x2="570" y2="265" stroke="#1c7ed6" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#mArrJa)"/>
  <line x1="260" y1="270" x2="260" y2="245" stroke="#c92a2a" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#mArrJa)"/>
  <text x="360" y="385" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" font-weight="700" fill="#212529">直接制御は決定と作業を混ぜる。</text>
  <text x="360" y="408" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#212529">メタ推論は二層に分ける。</text>
  <text x="360" y="440" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">図注：四段階自体がエージェント過程。ワーカーはタスク＋選ばれた文脈のみ受け取る。</text>
</svg>

## 本当に重要な数字

**ProgramBench**（文書と実行のみ可の参照プログラムからFFmpeg等の実在コードベースを再構築する200課題）：GPT-5.5でメタ推論**71.5%**、Codex 58.0%、直接制御63.7%。Opus 4.8で**67.2%**対Claude Code 65.5%。12の対比較すべてに勝利。

目を引くのは予算曲線だ。400→1200コールで**64.1%から71.5%へ**伸び、直接制御は64%で停滞——*早々に止め*、予算の約**18%**しか使わない。メタ推論は89〜101%を使い切り、すべて得点に変える。

コントローラーの判定はワーカーの自己評価より遥かに正確（AUC **0.88**対**0.55**）。依存辺はアーティファクト数の約**10倍**。限界も正直。小予算では裏目に、査定は定性判断、チェスでは「不毛な再考」が正解を壊した。プレプリント、再現待ち。

## フレームワーク以上の理由

**第三のスケーリング軸。** 学習計算も推論時計算も能力を伸ばす（[Snellら、2024](https://arxiv.org/abs/2408.03314)）。本論文の提案は、*予算のどれだけを「考える」に使うか*だ。単価が下がるほど、400コールでは無駄な熟慮が1200コールで報われる。テスト時スケーリングは多サンプルではなく、より良い指揮を意味し始める。

**学習されていないコントローラーは道標。** 空白は査定が*プロンプト判断*であることだ。だが[合理的メタ推論（2024）](https://arxiv.org/abs/2410.05563)は計算価値が学習可能と示し、[Meta-Harness（2026）](https://arxiv.org/abs/2603.28052)はハーネス自体が最適化可能と示した。本論文は意図的な中継点——先に有効性を証明し、学習版に目標を与える。先に学習した者が次の5〜10ポイントを取る。

**相関リスク。** メタ推論は失敗リスクをコントローラーに*集中*させる。ワーカーの失敗は一分岐の無駄だが、誤判断は全体を汚染する——[「Large Language Monkeys」](https://arxiv.org/abs/2407.21787)とは正反対だ。実運用では較正が質より重要になる。

歴史の反響。強化学習は*行動*と*評価*を分け、OSは*機構*と*方針*を分けた。今度は*やる*と*指揮する*が分かれた。定着すれば「コントローラー能力」は独立した技能になる。

<svg viewBox="0 0 720 420" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="予算スケーリング比較">
  <defs>
    <marker id="mArrJa2" markerWidth="10" markerHeight="10" refX="8" refY="5" orient="auto"><path d="M0,0 L10,5 L0,10 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="30" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="18" font-weight="700" fill="#212529">制御が予算を得点に変える——直接制御は失速</text>
  <text x="80" y="70" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">ProgramBench得点（%）</text>
  <line x1="80" y1="90" x2="80" y2="330" stroke="#495057" stroke-width="2"/>
  <line x1="80" y1="330" x2="660" y2="330" stroke="#495057" stroke-width="2"/>
  <text x="370" y="360" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">モデルコール予算 →</text>
  <text x="60" y="140" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">72</text>
  <text x="60" y="200" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">68</text>
  <text x="60" y="260" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">64</text>
  <text x="60" y="320" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">60</text>
  <line x1="80" y1="140" x2="660" y2="140" stroke="#e9ecef" stroke-width="1"/>
  <line x1="80" y1="200" x2="660" y2="200" stroke="#e9ecef" stroke-width="1"/>
  <line x1="80" y1="260" x2="660" y2="260" stroke="#e9ecef" stroke-width="1"/>
  <polyline points="150,262 370,190 590,148" fill="none" stroke="#1c7ed6" stroke-width="4"/>
  <circle cx="150" cy="262" r="7" fill="#1c7ed6"/>
  <circle cx="370" cy="190" r="7" fill="#1c7ed6"/>
  <circle cx="590" cy="148" r="7" fill="#1c7ed6"/>
  <text x="150" y="290" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">400</text>
  <text x="370" y="290" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">800</text>
  <text x="590" y="290" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" fill="#495057">1200</text>
  <text x="150" y="248" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" font-weight="700" fill="#1c7ed6">64.1%</text>
  <text x="590" y="134" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="14" font-weight="700" fill="#1c7ed6">71.5%</text>
  <polyline points="150,258 370,262 590,256" fill="none" stroke="#c92a2a" stroke-width="4" stroke-dasharray="10,6"/>
  <circle cx="150" cy="258" r="7" fill="#ffffff" stroke="#c92a2a" stroke-width="3"/>
  <circle cx="370" cy="262" r="7" fill="#ffffff" stroke="#c92a2a" stroke-width="3"/>
  <circle cx="590" cy="256" r="7" fill="#ffffff" stroke="#c92a2a" stroke-width="3"/>
  <text x="610" y="230" text-anchor="start" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#1c7ed6">メタ推論</text>
  <text x="610" y="285" text-anchor="start" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="15" font-weight="700" fill="#c92a2a">直接制御</text>
  <text x="360" y="395" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','Hiragino Sans','Noto Sans JP',sans-serif" font-size="13" fill="#868e96">図注：GPT-5.5でのProgramBench。直接制御は64%付近で停滞し、予算の約18%しか使わない。</text>
</svg>

最も深い転換は概念的だ。LLM内部に*分解可能で操作可能*なメタ認知状態があると示される。メタ認知がモデルの自然な部分空間なら、明示的コントローラーはモデルの目に沿う。1980年代のエキスパートシステムは自己反省を夢見て手書きルールに溺れた——欠けていたのは言語でメタ推論させることだった。

**議論：** 「コントローラー能力」が独立に測れる技能になったら、先に測られるのは決定の質か、「決めるのをやめる」較正か？
