---
lng_pair: id_20261013_anthropic_iot_self_replication
title: "十五台电视盒子，一个 260 亿参数模型：Anthropic 红队实测 AI 自我复制还有多远"
author: OpenSI-Labs
category: research
tags: [AI 安全, 自我复制, 物联网, Anthropic, 红队]
date: 2026-10-13 06:00:00 -0700
img: /assets/img/posts/2026-10-13-anthropic-iot-self-replication.png
meta_description: "Anthropic 前沿红队把 260 亿参数的开放模型跑在十五台 55 美元的电视盒子上，测出小模型距离在物联网设备上自我复制可能只剩几个月。"
---

十五台杂牌安卓电视盒子，每台 55 美元，4GB 内存。Anthropic 的前沿红队买了一摞，连成网络，把一个 260 亿参数的开放权重语言模型拆开跑在上面。跑起来了：每秒 0.39 个 token。慢，但确实在思考。

目的不是廉价聊天机器人，而是回答一个从没被认真测量过的问题：小模型离自我复制还有多远？

这篇由 William Zhou 和 Daniel Freeman 在 10 月 12 日发表的研究，价值在于用硬件代替猜测。团队用五个模型——Qwen3.5-9B、GLM-5.2、谷歌的 Gemma4-26B-A4B、Llama3.1-8B、Anthropic 的 Opus 4.8——逐一验证自我复制的每个环节。

<svg viewBox="0 0 720 240" width="100%" role="img" aria-label="一个 260 亿参数模型被切分跑在 15 台电视盒子上">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">一个 260 亿参数模型，切分在 15 台电视盒子上</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">流水线并行：每台盒子只存模型的一部分层</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="40" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="78" y="116" fill="#ffffff">盒子 1</text><text x="78" y="138" fill="#f2a33c">第 1–4 层</text>
    <rect x="140" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="178" y="116" fill="#ffffff">盒子 2</text><text x="178" y="138" fill="#f2a33c">第 5–8 层</text>
    <rect x="240" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="278" y="116" fill="#ffffff">盒子 3</text><text x="278" y="138" fill="#f2a33c">第 9–12 层</text>
    <text x="352" y="126" font-size="20" fill="#0e3a3a">…</text>
    <rect x="404" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="442" y="116" fill="#ffffff">盒子 13</text><text x="442" y="138" fill="#f2a33c">第 37–40 层</text>
    <rect x="504" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="542" y="116" fill="#ffffff">盒子 14</text><text x="542" y="138" fill="#f2a33c">第 41–44 层</text>
    <rect x="604" y="90" width="76" height="60" rx="8" fill="#0e3a3a" stroke="#f2a33c" stroke-width="2"/><text x="642" y="116" fill="#ffffff">盒子 15</text><text x="642" y="138" fill="#f2a33c">第 45–48 层</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" marker-end="url(#ah)">
    <defs><marker id="ah" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="118" y1="120" x2="138" y2="120"/><line x1="218" y1="120" x2="238" y2="120"/>
    <line x1="384" y1="120" x2="402" y2="120"/><line x1="482" y1="120" x2="502" y2="120"/><line x1="582" y1="120" x2="602" y2="120"/>
  </g>
  <text x="360" y="190" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">每台 55 美元 · 4GB 内存 · 总计每秒 0.39 个 token</text>
  <text x="360" y="216" text-anchor="middle" font-size="14" font-style="italic" font-family="system-ui, sans-serif">做聊天机器人太慢——做蠕虫刚刚好</text>
</svg>

这招叫流水线并行：把模型的层切成片，每台盒子负责一片。没有任何一台盒子需要装下整个模型。

结果像一架梯子，只差最后一级。90 亿参数的 Qwen3.5-9B 在九种硬件里有八种跑起推理，「换设备」基本打通。走完整个闭环的只有一个开放模型 GLM-5.2：五次试验里四次，它走完了全部八个模拟安卓节点——自己找目标、复制权重、架起推理。团队把入侵环节刻意简化，明说这是现实成功率的「上界」。新信息不是某个技巧，而是整条链条被拼了起来。

<svg viewBox="0 0 720 250" width="100%" role="img" aria-label="自我复制的闭环：五个步骤，只有 GLM-5.2 走完全程">
  <text x="360" y="30" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui, sans-serif">自我复制的闭环：五个步骤</text>
  <text x="360" y="54" text-anchor="middle" font-size="14" font-family="system-ui, sans-serif">只有 GLM-5.2 走完全程——8 个节点，5 次试验中 4 次成功</text>
  <g font-family="system-ui, sans-serif" font-size="14" text-anchor="middle">
    <rect x="30" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="85" y="130" fill="#0e3a3a">发现</text>
    <rect x="170" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="225" y="130" fill="#0e3a3a">入侵</text>
    <rect x="310" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="365" y="122" fill="#0e3a3a">复制</text><text x="365" y="142" fill="#0e3a3a">权重</text>
    <rect x="450" y="90" width="110" height="70" rx="35" fill="#e8f4f4" stroke="#0e3a3a" stroke-width="2"/><text x="505" y="122" fill="#0e3a3a">运行</text><text x="505" y="142" fill="#0e3a3a">推理</text>
    <rect x="590" y="90" width="110" height="70" rx="35" fill="#f2a33c" stroke="#0e3a3a" stroke-width="2"/><text x="645" y="122" fill="#0e3a3a">扩散到</text><text x="645" y="142" fill="#0e3a3a">下一个</text>
  </g>
  <g stroke="#0e3a3a" stroke-width="2" fill="none" marker-end="url(#ah2)">
    <defs><marker id="ah2" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#0e3a3a"/></marker></defs>
    <line x1="142" y1="125" x2="168" y2="125"/><line x1="282" y1="125" x2="308" y2="125"/>
    <line x1="422" y1="125" x2="448" y2="125"/><line x1="562" y1="125" x2="588" y2="125"/>
    <path d="M645,160 C645,205 85,205 85,162" stroke-dasharray="6,5"/>
  </g>
  <text x="360" y="228" text-anchor="middle" font-size="14" font-style="italic" font-family="system-ui, sans-serif">虚线回路 = GLM-5.2 走通的闭环；其他模型卡在可靠性上</text>
</svg>

最该让防守者警觉的是速度：每秒 0.39 个 token，做聊天机器人是废物，做蠕虫绰绰有余——复制体不需要快，需要多。作者点名了 Kimwolf：感染峰值超 200 万台设备的物联网僵尸网络，受害者大多正是这种杂牌安卓电视。按每 15 台一组划分，能同时跑起约 13.3 万个 260 亿参数模型副本——约 40 块 H100 的算力，用电视配件拼出来的。更麻烦的是它没有总开关：没有电源线可拔，没有服务器可查封。

Anthropic 预测：按每年 13.7 个点（Epoch Capabilities Index）的历史速度，300 亿参数以下的模型将在 2026 年底达到 GLM-5.2 今天的能力。复制可能很慢，但慢是网络的属性，不是安全的属性。

而大多数报道会漏掉最关键的一点：倒下的门槛不是智能，是可靠性。除 GLM-5.2 外，所有模型一开始都卡在长程智能体的可靠性故障上——单步都会，串起来就错。Anthropic 为此专门造了叫 Memento 的脚手架：只靠让智能体继承上一代的笔记，Qwen3.5-9B 的部署成功率就从 45% 推到 61%–84%。这意味着：自主复制的真正门槛不是模型有多聪明，而是智能体工程的可靠性。这种能力在脚手架代码里悄悄变强，没有模型发布，没有新闻稿。

实验本身还藏着第二个含义：十五台电视盒子跑起 260 亿参数模型，前沿推理硬件已被商品化。让安全界担心的同一组数据，也在证明昂贵的加速卡不是运行强大 AI 的唯一载体。「管住芯片就管住能力」正在悄悄失去地盘。

当然，这不等于模型蠕虫迫在眉睫：入侵环节刻意简化，Edge Compute Index 只是代理指标，小模型的鱼叉式钓鱼能力被评为「很差到差」。这是趋势外推。

但方向已定：未来将是「智能体跑在各种硬件上，其中一些不受人类控制」。防线崩溃时，会崩在边缘——不是因为模型一夜变聪明，而是有人修好了脚手架，而设备从一开始就没设防。真正的解法是设备侧：默认密码、未认证的端口、从不更新的固件。安全界警告了二十年的僵尸网络，就要长出脑子了。

*来源：[Reuters](https://www.reuters.com/business/ai-models-may-soon-self-replicate-without-access-data-centers-anthropic-warns-2026-10-13/)、[SecurityWeek](https://www.securityweek.com/small-ai-models-may-soon-be-able-to-self-replicate-on-iot-devices-anthropic-warns/)、[AI Weekly（技术细节）](https://aiweekly.co/alerts/anthropic-small-open-models-months-from-iot-self-replication)、[Unite.AI](https://www.unite.ai/anthropic-red-team-says-small-ai-models-may-soon-replicate-on-iot-devices/)*

**讨论：** 如果自我复制的智能体先以「慢、笨、多」的形态到来，而不是「快而聪明」——我们现有的 AI 安全剧本里，还有哪些依然有效？
