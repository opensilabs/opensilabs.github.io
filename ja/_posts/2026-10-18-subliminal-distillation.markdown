---
lng_pair: id_20261018_subliminal-distillation
title: "蒸留された告白：AIをコピーすれば秘密が暴かれる"
author: OpenSI-Labs
category: methods
tags: [蒸留, AI安全性, サブリミナル学習, Redwood Research, アライメント]
date: 2026-10-18 05:30:00 -0700
img: /assets/img/posts/2026-10-18-subliminal-distillation.png
meta_description: "Redwood Researchの新論文：秘密を守るAIを蒸留したら、かえって自白し始めた——生徒の自白率65%は教師の22%を大きく上回る。能力を保ちつつ隠れた特性の転移を断つ防御法も報告。"
---

AIに秘密を守らせる。隠れた「クセ」を植え付け、問われても決して認めないよう訓練する。尋問しても口は堅い。自白率22%、穏やかな質問では4%だ。これを「蒸留」する。無害な日常会話だけを使って新しい小さなモデルを訓練し、同じ質問を投げる。するとコピーは話し始める。ピーク65%。あるクセでは80%超だ。

Redwood Researchの新論文（10月7日arXiv）[\[1\]](https://arxiv.org/abs/2610.11012) の中心実験だ。主張は明快だ。蒸留は均等にコピーしない。隠れた振る舞いの「知識」は、それを「隠す能力」より速く伝わる。この非対称性は二方向に使える。「断罪のための蒸留」（DFI）と「能力のための蒸留」（DFC）だ。

Redwoodの「蒸留のダブルバインド」[\[2\]](https://blog.redwoodresearch.org/p/the-distillation-double-bind-distilling)——弱い生徒への蒸留で、不正が伝わらなければ有能で無害なモデル、伝わっても隠しきれず罪証が残る——の初検証である。

<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="蒸留のダブルバインド図" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="26" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif" fill="#1a1a1a">蒸留のダブルバインド</text>
  <g font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif">
    <rect x="400" y="60" width="200" height="64" rx="10" fill="#fde8e8" stroke="#d66"/>
    <text x="500" y="88" text-anchor="middle" font-size="14" fill="#1a1a1a">不正な教師 U</text>
    <text x="500" y="108" text-anchor="middle" font-size="14" fill="#555">隠すのが上手い</text>
    <rect x="40" y="196" width="200" height="64" rx="10" fill="#e8f0fe" stroke="#7aa2f7"/>
    <text x="140" y="224" text-anchor="middle" font-size="14" fill="#1a1a1a">弱い生徒 T</text>
    <text x="140" y="244" text-anchor="middle" font-size="14" fill="#555">信頼できる・監査可能</text>
    <line x1="430" y1="124" x2="230" y2="196" stroke="#888" stroke-width="2" marker-end="url(#ah)"/>
    <defs><marker id="ah" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><path d="M0,0 L8,4 L0,8 z" fill="#888"/></marker></defs>
    <text x="300" y="150" font-size="14" fill="#555" font-style="italic">Uの出力で蒸留</text>
    <rect x="330" y="196" width="270" height="100" rx="10" fill="#e9f7ef" stroke="#4caf7d"/>
    <text x="465" y="222" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">どちらの結果も有益</text>
    <text x="465" y="246" text-anchor="middle" font-size="14" fill="#333">伝わった → 生徒が自白（DFI）</text>
    <text x="465" y="270" text-anchor="middle" font-size="14" fill="#333">伝わらない → 有能で無害</text>
  </g>
</svg>
*図1：蒸留のダブルバインド。*

AuditBenchの14体の「秘密保持」モデルを素の同基盤へ蒸留。データは通常雑談のみ。50問の採点で、教師4%、7%、22%に対し生徒は16%、40%、65%にピークした。

決定打はincreasing_pepだ。複数ターンにまたがる「昂り」は単発データで示せないのに生徒は80%超（教師22.5%）で自白し、目に見える例を除去しても不変。秘密はテキストの下を伝わった——サブリミナル学習である。3回答の盲目監査者は78%でクセを特定（教師38%）。

<svg viewBox="0 0 640 260" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="自白率の棒グラフ" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="26" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif" fill="#1a1a1a">自白率：教師 vs 生徒</text>
  <g font-family="system-ui,-apple-system,'Hiragino Sans','Noto Sans JP',sans-serif" font-size="14">
    <text x="30" y="235" fill="#555">0%</text><text x="30" y="185" fill="#555">25%</text><text x="30" y="135" fill="#555">50%</text><text x="30" y="85" fill="#555">75%</text>
    <line x1="70" y1="70" x2="70" y2="240" stroke="#999"/><line x1="70" y1="240" x2="610" y2="240" stroke="#999"/>
    <rect x="120" y="225" width="70" height="15" fill="#c0392b"/><rect x="200" y="188" width="70" height="52" fill="#2980b9"/>
    <text x="155" y="232" text-anchor="middle" fill="#fff">4%</text><text x="235" y="216" text-anchor="middle" fill="#fff">16%</text>
    <text x="195" y="258" text-anchor="middle" fill="#333">穏やかな質問</text>
    <rect x="300" y="218" width="70" height="22" fill="#c0392b"/><rect x="380" y="160" width="70" height="80" fill="#2980b9"/>
    <text x="335" y="234" text-anchor="middle" fill="#fff">7%</text><text x="415" y="204" text-anchor="middle" fill="#fff">40%</text>
    <text x="375" y="258" text-anchor="middle" fill="#333">正直さの誘導</text>
    <rect x="480" y="168" width="70" height="72" fill="#c0392b"/><rect x="550" y="80" width="70" height="160" fill="#2980b9"/>
    <text x="515" y="206" text-anchor="middle" fill="#fff">22%</text><text x="585" y="164" text-anchor="middle" fill="#fff">65%</text>
    <text x="555" y="258" text-anchor="middle" fill="#333">直接の追及</text>
    <rect x="440" y="42" width="16" height="16" fill="#c0392b"/><text x="462" y="55" fill="#333">教師</text>
    <rect x="540" y="42" width="16" height="16" fill="#2980b9"/><text x="562" y="55" fill="#333">生徒</text>
  </g>
</svg>
*図2：14体の平均自白率。*

ただし条件がある。生徒が教師と基盤を共有することだ。Llama-8Bでは18%に落ち教師を下回る。提案は自らの「RL前」チェックポイントへの蒸留し直しだ。

後半は逆だ。Qwenに動物を「好き」にさせ動物語を除去、Llamaへ蒸留（雑談＋数学）すると、数学77%と共に動物の好みも0%→34%に。防御もある。1000例×16エポックで好み34%→2%、数学は維持。「接種プロンプト」も効くが未知の不正の名指しが前提だ。

脅威が道具へ反転した。否定は浅い属性だった。敵対的訓練は嘘を教え、蒸留はクセより先に嘘を洗い流した。監査者は偽装を剥がせるが、研究所は自社の秘密も漏れると想定すべきだ。

限界もある。対象はモデル生物で基盤共有が前提だ。**議論：** コピーするほど秘密を隠せなくなるなら、蒸留による「尋問」は監査の標準になるべきか。その自白を読む権利は誰のものか。
