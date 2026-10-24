---
lng_pair: id_20261022_recursive-flint
title: "400億パラメータをポケットに"
author: OpenSI-Labs
category: research
tags: [Recursive, Flint, mixture-of-experts, open weights, local inference]
date: 2026-10-22 06:00:00 -0700
img: /assets/img/posts/2026-10-22-recursive-flint.png
meta_description: "Recursiveのオープンウェイト・コーディングモデルFlint：398億パラメータ、トークンあたり25億活性化、MacBook Proで毎秒131トークン——誰でもダウンロードでき、誰でも検証できる。"
---

10月21日、Richard SocherのRecursiveがFlintを公開した。398億パラメータのMoEで、トークンごとに約25億が動く——MacBook Proで毎秒131トークン。Apache 2.0のオープンウェイト（Hugging Face）。

MoEは病院の受付だ。47/49層がMoE層、各層256エキスパートから6つを選び、共有1つを添える。計算量は活性パラメータで決まる。

<figure>
<div style="text-align:center">
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">疎ルーティング：256のエキスパート、毎回6+1だけ発火</text>
<rect x="30" y="150" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="85" y="181" font-size="14" fill="#fff" text-anchor="middle">入力トークン</text>
<rect x="170" y="150" width="110" height="54" rx="8" fill="#6b46c1"/>
<text x="225" y="181" font-size="14" fill="#fff" text-anchor="middle">ルータ</text>
<line x1="140" y1="177" x2="170" y2="177" stroke="#a0aec0" stroke-width="2"/>
<circle cx="330" cy="80" r="9" fill="#4a5568"/>
<circle cx="364" cy="80" r="9" fill="#4a5568"/>
<circle cx="398" cy="80" r="9" fill="#4a5568"/>
<circle cx="432" cy="80" r="9" fill="#4a5568"/>
<circle cx="466" cy="80" r="9" fill="#4a5568"/>
<circle cx="500" cy="80" r="9" fill="#4a5568"/>
<circle cx="534" cy="80" r="9" fill="#4a5568"/>
<circle cx="568" cy="80" r="9" fill="#4a5568"/>
<circle cx="330" cy="114" r="9" fill="#4a5568"/>
<circle cx="364" cy="114" r="9" fill="#4a5568"/>
<circle cx="398" cy="114" r="9" fill="#f6ad55"/>
<circle cx="432" cy="114" r="9" fill="#4a5568"/>
<circle cx="466" cy="114" r="9" fill="#4a5568"/>
<circle cx="500" cy="114" r="9" fill="#4a5568"/>
<circle cx="534" cy="114" r="9" fill="#4a5568"/>
<circle cx="568" cy="114" r="9" fill="#4a5568"/>
<circle cx="330" cy="148" r="9" fill="#4a5568"/>
<circle cx="364" cy="148" r="9" fill="#4a5568"/>
<circle cx="398" cy="148" r="9" fill="#4a5568"/>
<circle cx="432" cy="148" r="9" fill="#4a5568"/>
<circle cx="466" cy="148" r="9" fill="#4a5568"/>
<circle cx="500" cy="148" r="9" fill="#4a5568"/>
<circle cx="534" cy="148" r="9" fill="#f6ad55"/>
<circle cx="568" cy="148" r="9" fill="#4a5568"/>
<circle cx="330" cy="182" r="9" fill="#4a5568"/>
<circle cx="364" cy="182" r="9" fill="#4a5568"/>
<circle cx="398" cy="182" r="9" fill="#4a5568"/>
<circle cx="432" cy="182" r="9" fill="#4a5568"/>
<circle cx="466" cy="182" r="9" fill="#4a5568"/>
<circle cx="500" cy="182" r="9" fill="#f6ad55"/>
<circle cx="534" cy="182" r="9" fill="#4a5568"/>
<circle cx="568" cy="182" r="9" fill="#4a5568"/>
<circle cx="330" cy="216" r="9" fill="#4a5568"/>
<circle cx="364" cy="216" r="9" fill="#4a5568"/>
<circle cx="398" cy="216" r="9" fill="#4a5568"/>
<circle cx="432" cy="216" r="9" fill="#4299e1"/>
<circle cx="466" cy="216" r="9" fill="#4a5568"/>
<circle cx="500" cy="216" r="9" fill="#4a5568"/>
<circle cx="534" cy="216" r="9" fill="#4a5568"/>
<circle cx="568" cy="216" r="9" fill="#4a5568"/>
<circle cx="330" cy="250" r="9" fill="#4a5568"/>
<circle cx="364" cy="250" r="9" fill="#f6ad55"/>
<circle cx="398" cy="250" r="9" fill="#4a5568"/>
<circle cx="432" cy="250" r="9" fill="#4a5568"/>
<circle cx="466" cy="250" r="9" fill="#4a5568"/>
<circle cx="500" cy="250" r="9" fill="#4a5568"/>
<circle cx="534" cy="250" r="9" fill="#4a5568"/>
<circle cx="568" cy="250" r="9" fill="#4a5568"/>
<circle cx="330" cy="284" r="9" fill="#4a5568"/>
<circle cx="364" cy="284" r="9" fill="#4a5568"/>
<circle cx="398" cy="284" r="9" fill="#4a5568"/>
<circle cx="432" cy="284" r="9" fill="#4a5568"/>
<circle cx="466" cy="284" r="9" fill="#4a5568"/>
<circle cx="500" cy="284" r="9" fill="#4a5568"/>
<circle cx="534" cy="284" r="9" fill="#f6ad55"/>
<circle cx="568" cy="284" r="9" fill="#4a5568"/>
<circle cx="330" cy="318" r="9" fill="#4a5568"/>
<circle cx="364" cy="318" r="9" fill="#4a5568"/>
<circle cx="398" cy="318" r="9" fill="#4a5568"/>
<circle cx="432" cy="318" r="9" fill="#f6ad55"/>
<circle cx="466" cy="318" r="9" fill="#4a5568"/>
<circle cx="500" cy="318" r="9" fill="#4a5568"/>
<circle cx="534" cy="318" r="9" fill="#4a5568"/>
<circle cx="568" cy="318" r="9" fill="#4a5568"/>
<line x1="280" y1="177" x2="398" y2="114" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="534" y2="148" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="534" y2="284" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="364" y2="250" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="500" y2="182" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="432" y2="318" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="432" y2="216" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<rect x="610" y="150" width="60" height="54" rx="8" fill="#2f855a"/>
<text x="640" y="181" font-size="14" fill="#fff" text-anchor="middle">→</text>
<text x="330" y="336" font-size="14" text-anchor="middle" fill="#cbd5e0">総パラメータ398億 · トークンあたり約25億が活性</text>
<circle cx="120" cy="300" r="8" fill="#f6ad55"/>
<text x="134" y="305" font-size="14" fill="#cbd5e0">6つ選択</text>
<circle cx="300" cy="300" r="8" fill="#4299e1"/>
<text x="314" y="305" font-size="14" fill="#cbd5e0">共有エキスパート1つ</text>
</svg>
</div>
</figure>

「Eureka Machine」が「ほぼ全工程」に関与。35B/3Bから40B/2.5Bへ。出力層を4ビット量子化（[NVFP4](https://www.marktechpost.com/2026/10/21/recursive-flint-local-coding-model/)）し、16ビット教師の蒸留で0.7差に回収。M4/M5のMetal megakernelがデコードを融合。4か月足らずの成果だ。

M4 Proで[約131トークン/秒](https://teckhustlers.com/recursive-flint-local-coding-model/)、Ollama版23GBで48GBメモリで動く。SWE-Bench Verified 74.2%（50B未満MoE最良）、Terminal-Bench 2.1は54.9%でQwen 3.8（73.0%）に敗北。

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">MacBook Pro（M4 Pro）でのトークン/秒</text>
<text x="200" y="80" font-size="14" text-anchor="end" fill="#e2e8f0">Flint</text>
<rect x="215" y="60" width="332" height="30" rx="4" fill="#f6ad55"/>
<text x="555" y="81" font-size="14" fill="#e2e8f0">131</text>
<text x="200" y="135" font-size="14" text-anchor="end" fill="#e2e8f0">Gemma 4</text>
<rect x="215" y="115" width="175" height="30" rx="4" fill="#718096"/>
<text x="398" y="136" font-size="14" fill="#e2e8f0">69</text>
<text x="200" y="190" font-size="14" text-anchor="end" fill="#e2e8f0">Nemotron 3.5 Lightning</text>
<rect x="215" y="170" width="147" height="30" rx="4" fill="#718096"/>
<text x="370" y="191" font-size="14" fill="#e2e8f0">58</text>
<text x="340" y="278" font-size="14" text-anchor="middle" fill="#a0aec0">データ：Recursive自社測定、TechCrunch経由</text>
</svg>
</div>
</figure>

見どころは「検証可能」だ。重みは誰でも落とせ、131は再測定できる——オープンウェイトが市場の規律だ。ベンチマークは自己申告のみで独立検証はなく、Flintは完成品のスナップショットに過ぎない。

*議論：あらゆる性能の主張が再測定可能になったとき、自己申告ベンチマークのマーケティングはあとどれだけ続くのか。*
