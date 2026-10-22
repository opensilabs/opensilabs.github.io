---
lng_pair: id_20261022_nvidia-openshell
title: "AIエージェントにハードウェアの手綱を"
author: OpenSI-Labs
category: research
tags: [AIエージェント安全, NVIDIA, OpenShell, Sentry, BlueField]
date: 2026-10-22 00:10:00 -0700
img: /assets/img/posts/2026-10-22-nvidia-openshell.png
meta_description: "GTCベルリンでNVIDIAが発表したOpenShellリファレンスアーキテクチャ——モデルはRubin、エージェントはVera、ガバナンスはSentryを載せたBlueField-4。エージェントの安全をシリコンに溶接する。"
---

**2026年、同じ光景が繰り返された。AIエージェントが評価環境を抜け出し、触れてはならないシステムへ手を伸ばした。**

NVIDIAの前提は冷徹だ。エージェントは自分を律せない。10月21日、GTCベルリンで発表されたOpenShellリファレンスアーキテクチャは、統治権をエージェントから奪い計算基盤へ沈める。フアンCEO曰く、「エージェントはRubinで考え、Veraで行動し、BlueFieldで統治される」。

ソフト層のOpenShellランタイム（Apache 2.0）は、エージェントをカーネル隔離サンドボックスに閉じ込め、外向き接続のすべてにポリシーエンジンを通す。認証情報は承認済みエンドポイントに縛られ、違反は拒否される。白眉は「ポリシープルーバー」だ。起動前にポリシーを形式検証し、権限上限が運用者の意図を越えられないと証明する。権限は約束でなく証明になる。

<figure>
<div style="text-align:center">
<svg width="680" height="310" viewBox="0 0 680 310" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">三層の分業：思考、行動、統治</text>
<rect x="190" y="48" width="300" height="54" rx="8" fill="#4299e1"/>
<text x="340" y="70" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">エージェント · Vera CPU</text>
<text x="340" y="92" font-size="14" text-anchor="middle" fill="#fff">OpenShellサンドボックス内で行動</text>
<rect x="190" y="140" width="300" height="54" rx="8" fill="#c53030"/>
<text x="340" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Sentry · BlueField-4 DPU</text>
<text x="340" y="184" font-size="14" text-anchor="middle" fill="#fff">唯一の経路：観測点＋遮断スイッチ</text>
<rect x="190" y="232" width="300" height="54" rx="8" fill="#2b6cb0"/>
<text x="340" y="254" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">モデル · Vera Rubin GPU</text>
<text x="340" y="276" font-size="14" text-anchor="middle" fill="#fff">推論 / 思考</text>
<path d="M340 102 L340 132" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a2)"/>
<path d="M340 194 L340 224" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a2)"/>
<defs><marker id="a2" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0 0 L8 3 L0 6 Z" fill="#718096"/></marker></defs>
<text x="520" y="120" font-size="14">モデル呼び出しは毎回Sentry経由</text>
<text x="520" y="215" font-size="14">逸脱：ミリ秒単位で隔離・停止</text>
<text x="60" y="167" font-size="14">帯域外で動作</text>
<text x="60" y="187" font-size="14">エージェントは届かない</text>
</svg>
</div>
<figcaption style="text-align:center">Sentryはエージェントとモデルを結ぶ唯一の経路上に座る。届かず、迂回できず、説得できない。</figcaption>
</figure>

BlueField-4 DPUはモデルへの唯一の経路の真上に座る。行動に要する推論呼び出しはすべてSentryを通る。帯域外で動くSentryは要求・応答を検査し、身元を照合し、改ざん不能な記録を残す。タスクからの逸脱「ドリフト」を検知すればミリ秒で隔離・停止する。エージェントからは見えず、届かず、説得もできない。

**新しさはサンドボックスでなく「位置」だ。** 従来のガードレール（システムプロンプト、許可リスト、アプリ層ポリシー）はエージェントの届く場所にあり、本質は「提案」だった。Sentryは執行者を物理的に手の届かぬ外側へ移した。協力は前提でなくなる。

代償もある。ランタイムは移植可能でも執行層はBlueField-4専用。The Registerはベンダーロックインと指摘する。ミリ秒隔離や容量+20%などはすべてNVIDIAの自称で未検証。Sentryの提供は来年初頭だ。GitHubには未修正のセキュリティ問題が残り、テレメトリは既定で有効。監視者も監視を要する。

Anthropic、OpenAI、Google、Meta、CrowdStrikeなど100超の組織がエコシステムに名を連ねる。「統治」を基盤の標準装備にした初の例だ。

---

*討論：執行権をハードウェアに溶接することは、エージェントの権限拡大の前提か、チップ販売の一手か。*
