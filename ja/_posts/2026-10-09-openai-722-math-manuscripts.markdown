---
lng_pair: id_20261009_openai-722-math-manuscripts
title: "数学の粒子加速器：OpenAI の 722 本の数学原稿"
author: OpenSI-Labs
category: research
tags: [OpenAI, 数学, Lean, 自動定理証明, 研究評価]
date: 2026-10-09 06:00:00 -0700
img: /assets/img/posts/2026-10-09-openai-722-math-manuscripts.png
meta_description: "OpenAI は単一の AI エージェントが書いた 722 本の数学原稿を公開した。真の物語はパイプラインにある：ベンチマークは飽和し、未解決問題が新たなフロンティア評価となり、人間による検証がボトルネックになった。"
---

10月6日、OpenAIは前例のないことをした。数学科1年分の成果を一晩で公開GitHubリポジトリに流し込んだ。[openai/math](https://github.com/openai/math)は719本の原稿を372の「成果ファミリー」にまとめる（発表時は722本）。すべて未公開の社内モデル作。Apache-2.0、数日で約12,800スター。4次元Kakeya予想の解法、リーマンゼータ関数のより広い零点自由領域、CMアーベル多様体上の有理ホッジ予想の証明——機械の名で出た最も野心的な主張が並ぶ。

だが定理は物語ではない。手順こそが物語だ。

## 本当のニュースは手順にある

大半はひとつの固定手順から生まれた（README）。約4,000の未解決問題をモデルに提示し、各成果に平均3時間の「ChatGPT Pro級の思考」を投じ、有意な出力をファミリーに集約。広報によれば「ほぼすべてが単一エージェントへのひとつのプロンプトへの応答」だ。722の独立プロジェクトではなくエージェント1回の実行であり、理由は明言されている。「既存の数学評価が飽和したため、評価を未解決の研究問題へ拡張した」。ベンチマークは死んだ。新たなフロンティア評価はテストセットではなく未解決文献そのものだ。

<svg viewBox="0 0 720 560" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="機械研究パイプライン：4,000問が入り、372ファミリーが出る">
  <defs>
    <marker id="arrM" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">機械研究パイプライン：4,000問が入り、372ファミリーが出る</text>
  <rect x="255" y="45" width="210" height="56" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="70" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#1864ab">約 4,000 の未解決問題</text>
  <text x="360" y="90" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">ひとつのモデルに提示</text>
  <line x1="360" y1="101" x2="360" y2="116" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="118" width="270" height="56" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="143" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#e67700">単一エージェント、ひとつのプロンプト</text>
  <text x="360" y="163" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">1成果あたり約3時間の「思考」</text>
  <line x1="360" y1="174" x2="360" y2="189" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="191" width="240" height="56" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="216" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#5f3dc4">有意性フィルタ</text>
  <text x="360" y="236" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">約18%が通過、残りは廃棄</text>
  <line x1="360" y1="247" x2="360" y2="262" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="255" y="264" width="210" height="56" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="289" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">372 の成果ファミリー</text>
  <text x="360" y="309" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">719 本の原稿、17 分野</text>
  <line x1="360" y1="320" x2="360" y2="335" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="337" width="240" height="56" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="362" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#a61e4d">LEAN 形式化</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">主要成果の約42%を機械検証</text>
  <line x1="360" y1="393" x2="360" y2="408" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="410" width="270" height="56" rx="10" fill="#f8f9fa" stroke="#868e96" stroke-width="2"/>
  <text x="360" y="435" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#495057">バージョン管理された公開リポジトリ</text>
  <text x="360" y="455" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Apache-2.0、論文ごとに BibTeX、履歴ログ</text>
  <text x="360" y="500" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">2つのステップは固定手順から外れた：リーマンゼータ関数の零点自由領域（原稿は人間が編集）、</text>
  <text x="360" y="518" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">および CM アーベル多様体上のホッジ予想の証明。</text>
</svg>
*図 1：公開パイプライン——ひとつのエージェント、ひとつのプロンプト、ふたつの人間の例外。*

主張の重みはまちまちだ。固定手順から外れたのは2件——リーマンゼータ関数の零点自由領域（より広いRe(s)>11/12、原稿は人間が編集）と、全次元・全余次元でのCMアーベル多様体上の有理ホッジ予想の証明。理論計算機科学が40ファミリーで最多だ。

## Lean は耐力壁だ

リポジトリにはLeanライブラリが付属する。証明の各ステップを機械的に検証するソフトウェアで、主要成果の約42%が形式化されている。独立集計では722本中162本に計算機検証つきの主結果がある。Lean検証の通過は新しい信頼の基盤だ。

だが大半の報道が見落としたニュアンスがある。Lean検証が示すのは論証が前提から導かれることだけだ。新しさ、重要さ、面白さは語らない。機械検証は査読と同義ではない。OpenAI自身「問題がある可能性」を認め、修正は公開バージョンで記録する——科学にもリリースノートがついた。AIは「プロンプトを与えた人間自身が理解も検証も責任も取れない」数学的議論を出力できると、高等研究所は警告する。

この公開は論争に形作られた。1か月前、OpenAIは約1万のエージェントが88時間でナヴィエ–ストークス問題を解決したと発表。20人超のフィールズ賞受賞者が「数学におけるAIの深刻なミスアライメント」声明に署名した。高等研究所の諮問グループは9月29日に提言——モデルの名を明かし、プロンプトを公開し、宣伝に使うな。OpenAIの遵守は部分的だ。平均計算量、10件の要約、プロンプトなし。「拘束はされない」と広報は*Scientific American*に語った。独立arXiv監査は8月分の主結果に実質的誤りを確認しなかった。

<svg viewBox="0 0 720 330" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="検証の勾配：生産はあらゆる検査を上回った">
  <defs>
    <marker id="arrV" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#868e96"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">検証の勾配：生産はあらゆる検査を上回った</text>
  <rect x="30" y="50" width="660" height="44" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="77" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#1864ab">モデルに提示された約 4,000 問</text>
  <rect x="180" y="106" width="360" height="44" rx="8" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="133" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#2b8a3e">公開された 372 成果ファミリー（成功率 約18%）</text>
  <rect x="255" y="162" width="210" height="44" rx="8" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="189" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#e67700">計算機検証つき証明 162 本</text>
  <rect x="315" y="218" width="90" height="44" rx="8" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="245" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#a61e4d">人間の査読者</text>
  <line x1="360" y1="94" x2="360" y2="104" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="150" x2="360" y2="160" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="206" x2="360" y2="216" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <text x="360" y="292" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">各段階は前より狭くなる。人間の査読が最もきついボトルネック——</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">機械スケールの帯域を持つ検査は Lean 形式化だけだ。</text>
</svg>
*図 2：検証の勾配——生産は計算量とともに伸び、検査は人間とともに伸びる。*

## 新たな希少資源

見方を変えるべき部分はどの定理とも無関係だ。READMEで最も重要な一文は飽和について——ベンチマークは死に、フロンティアは未解決問題へ移った。テストセットが強弱を識別できなくなれば、残る試験は誰も解いたことのない問題だけだ。ボトルネックが反転した。希少資源は生産ではなく、単一エージェントが1件3時間で372ファミリーを生んだいま、消化することだ。査読回路が1週間で722本を読むことはない。Lean形式化、バージョン管理、論文ごとのBibTeXは飾りではない。「研究所が論文を書く」時代の出版インフラなのだ。

OpenAI自身「コミュニティがホストするリポジトリを検討中」と認める。1社のリポジトリが機械数学の永住の地にはなりえない。どの研究所にも属さない共有の検証インフラ——形式化ライブラリ、検証サービス、査読規範——が必要だ。722本はデモンストレーションにすぎない。突きつけられるインフラこそ真のブレークスルーだ。

最後に率直に言おう。82%は永遠に見えない。閾値を超えたものだけがリポジトリにある。失敗した問題もまた科学であり、機械のフロンティアの真の位置を示す。失敗の公開なくして、こうした公開はいつもハイライト集にすぎない。

読者への問い。未解決の数学がフロンティアのベンチマークとなり、その試験を受けるモデルがすべて非公開なら、検証パイプラインは誰のものか。「機械が生成し、機械が検証し、人間は読まない」が数学の進歩の標準単位になるまであとどれくらいか。

---

*出典：[openai/math](https://github.com/openai/math)；[概要](https://raw.githubusercontent.com/openai/math/main/overview.tex)；高等研究所諮問グループ提言；Scientific American；8月分の独立arXiv監査。*
