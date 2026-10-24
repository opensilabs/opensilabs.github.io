---
lng_pair: id_20261022_recursive-flint
title: "把 400 亿参数装进口袋"
author: OpenSI-Labs
category: research
tags: [Recursive, Flint, mixture-of-experts, open weights, local inference]
date: 2026-10-22 06:00:00 -0700
img: /assets/img/posts/2026-10-22-recursive-flint.png
meta_description: "Richard Socher 的 Recursive 发布开源编码模型 Flint：398 亿参数、每词只激活 25 亿，在 MacBook Pro 上跑出每秒 131 词——权重人人可下，速度人人可验。"
---

10 月 21 日，Richard Socher 的新公司 Recursive 发布首个模型 Flint：398 亿参数的混合专家（MoE）模型，每词只动用约 25 亿参数——刚好能在 MacBook Pro 上以每秒 131 词跑起来。权重以 Apache 2.0 完全开源：下载、离线运行、商用改造，全免费。

MoE 像医院分诊台：请求只路由给最对口的几位专家。Flint 共 49 层，47 层是 MoE；每层 256 个专家，路由器每 token 只挑 6 个，加一个常开的共享专家。算量按活跃参数走——这就是 40B 容量塞进笔记本的原因。

<figure>
<div style="text-align:center">
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">稀疏路由：256 位专家，每次只点 6+1 位</text>
<rect x="30" y="150" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="85" y="181" font-size="14" fill="#fff" text-anchor="middle">输入 token</text>
<rect x="170" y="150" width="110" height="54" rx="8" fill="#6b46c1"/>
<text x="225" y="181" font-size="14" fill="#fff" text-anchor="middle">路由器</text>
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
<text x="330" y="336" font-size="14" text-anchor="middle" fill="#cbd5e0">总参数 39.8B · 每 token 活跃约 2.5B</text>
<circle cx="120" cy="300" r="8" fill="#f6ad55"/>
<text x="134" y="305" font-size="14" fill="#cbd5e0">6 个被选中</text>
<circle cx="300" cy="300" r="8" fill="#4299e1"/>
<text x="314" y="305" font-size="14" fill="#cbd5e0">1 个共享专家</text>
</svg>
</div>
</figure>

Flint 最耐人寻味的是造法。Recursive 说自动化研究系统 Eureka Machine 参与了"几乎每一个环节"：从 35B/3B 基线搜索专家配置到 40B/2.5B；把输出层压到 4 位（NVFP4），再用 16 位教师蒸馏捞回精度——只低 0.7 分；还在 M4/M5 上写了 Metal megakernel，把解码前向融成一个核。不到四个月，小团队加一群智能体从零做出。

速度是卖点：M4 Pro 上超每秒 125 词（约 131），Ollama 量化版 23GB，48GB 统一内存的 Mac 就能跑。SWE-Bench Verified 74.2%（50B 以下 MoE 最好）；Terminal-Bench 2.1 只有 54.9%，输给稠密的 Qwen 3.8（73.0%）。

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">MacBook Pro（M4 Pro）生成速度（词/秒）</text>
<text x="200" y="80" font-size="14" text-anchor="end" fill="#e2e8f0">Flint</text>
<rect x="215" y="60" width="332" height="30" rx="4" fill="#f6ad55"/>
<text x="555" y="81" font-size="14" fill="#e2e8f0">131</text>
<text x="200" y="135" font-size="14" text-anchor="end" fill="#e2e8f0">Gemma 4</text>
<rect x="215" y="115" width="175" height="30" rx="4" fill="#718096"/>
<text x="398" y="136" font-size="14" fill="#e2e8f0">69</text>
<text x="200" y="190" font-size="14" text-anchor="end" fill="#e2e8f0">Nemotron 3.5 Lightning</text>
<rect x="215" y="170" width="147" height="30" rx="4" fill="#718096"/>
<text x="370" y="191" font-size="14" fill="#e2e8f0">58</text>
<text x="340" y="278" font-size="14" text-anchor="middle" fill="#a0aec0">数据：Recursive 自测，TechCrunch 引用</text>
</svg>
</div>
</figure>

真正的看点在"可验证"三字。闭源实验室报速度，你只能信；Flint 权重人人可下，131 这个数字任何人买台 M4 Pro 就能复测——开源成了一种市场纪律。但基准全是 Recursive 自测，尚无独立验证；Flint 只是成品快照，证明不了"自我改进的研究系统"真的在变强。

当 400 亿参数第一次住进随身的电脑，写代码的权力结构会跟着变吗？

---

*讨论：当每一项性能声明都可被复测，"自报分数"的营销还能玩多久？*
