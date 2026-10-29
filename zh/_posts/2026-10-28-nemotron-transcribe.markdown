---
lng_pair: id_20261028_nemotron-transcribe
title: "NVIDIA 开源 40 语言转写模型 Nemotron 3.5：30B 参数只激活 4B，一块芯片就能跑"
author: OpenSI-Labs
category: research
tags: [NVIDIA, Nemotron, 语音识别, ASR, 开源权重, 混合专家, 说话人分离]
date: 2026-10-28 09:00:00 -0700
img: /assets/img/posts/2026-10-28-nemotron-transcribe.png
meta_description: "NVIDIA 开源的 Nemotron 3.5 Transcribe 能转写 40 种语言、在英语与 31 种语言之间互译，30B 参数每次只激活约 4B，一块芯片即可运行，还能用一个下午教会它医院的行话。头部数字均为 NVIDIA 自报，边界也同样真实。"
---

10 月 28 日，NVIDIA 发布 Nemotron 3.5 Transcribe：权重开放、可商用。它能转写 40 种语言的录音，与英语和 31 种语言互译，单条最长 1 小时，能分清最多 8 个说话人。权重在 Hugging Face 和 ModelScope 上。

它还能听指令。一句话就能选逐字稿（连“嗯”“啊”都保留）或干净稿（去掉口头词），能把药品名、产品名等词表交给它重点听，也能就录音内容提问。它还做说话人分离，标出每句话是谁说的。

## 30B 参数，每次只醒 4B

它用混合专家结构：模型由许多“专家”子网络组成，每处理一段音频只唤醒少数几个，其余闲置不耗算力。总参数 30B，每次实际参与的只有约 4B，容量和运行成本就此拆开，所以一块芯片就能跑。Artificial Analysis 测得它与 Voxtral Small 并列开源第一，词错误率同为 2.8%——对方 24B 参数，它约 4B。

<figure>
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="340" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">总参数 30B，每次只醒约 4B</text>
<text x="40" y="98" font-size="15" font-weight="700" fill="#374151">总参数：30B</text>
<rect x="40" y="112" width="600" height="46" rx="8" fill="#cbd5e1"/>
<rect x="40" y="112" width="80" height="46" rx="8" fill="#0e7c86"/>
<text x="52" y="142" font-size="17" font-weight="700" fill="#ffffff">~4B</text>
<text x="140" y="142" font-size="15" fill="#374151">每次激活：约 4B</text>
<text x="640" y="142" text-anchor="end" font-size="15" fill="#374151">闲置：约 26B</text>
<text x="40" y="212" font-size="16" fill="#374151">路由器为每段音频只唤醒少数几个专家子网络，其余不产生计算成本。</text>
<text x="340" y="272" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">一块芯片就能跑：Jetson AGX Thor · DGX Spark · Blackwell</text>
<text x="340" y="316" text-anchor="middle" font-size="26" font-weight="700" fill="#0e7c86">30B &#8594; ~4B</text>
</svg>
<figcaption>图 1 — 混合专家把容量和运行成本拆开：模型拥有 30B 参数，每次只为约 4B 付费。</figcaption>
</figure>

词错误率指转写里错词的占比，越低越好。据 NVIDIA 公布：Hugging Face 的 ASR 排行榜英文赛道，它以 5.33% 居开源第一；多语言赛道七语言平均 4.62%，为模型卡对比中最低；说话人归属错误率 18.26%，在 David AI 覆盖 21 种语言、14 个系统的基准中最低。均为自报，尚无独立复现。

同日发布的还有数据集 Granary v2：463,062 小时语音、48 种语言、16 个语料库，每条录音配逐字、格式化（读出的数字写成阿拉伯数字）、干净三种转写。音频本体不打包，只给清单指回原始来源，各按原许可。

## 一个下午教会它行话

在印度医疗语音基准 Eka Care 上，它开箱时词错误率高到五分之一至三分之一。换个更好的提示词，错误明显下降；再做微调（拿领域例子再训一小轮），一块 GB300 芯片约 14 个 GPU 小时，没见过的说话人词错误率从 22.44% 降到 12.17%，错误减少约 45.8%，胜过专用基线。医院或律所一下午就能教会它自己的词汇。

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">三步教会它医疗行话</text>
<rect x="40" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#1e3a5f" stroke-width="2"/>
<text x="130" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">开箱直接用</text>
<text x="130" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">词错误率 22.44%</text>
<text x="130" y="208" text-anchor="middle" font-size="14" fill="#374151">没见过的说话人</text>
<rect x="240" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#0e7c86" stroke-width="2"/>
<text x="330" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">换个更好的提示词</text>
<text x="330" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#0e7c86">错误明显下降</text>
<text x="330" y="208" text-anchor="middle" font-size="14" fill="#374151">不用额外训练</text>
<rect x="440" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#b91c1c" stroke-width="2"/>
<text x="530" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">微调约 14 个 GPU 小时</text>
<text x="530" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#b91c1c">词错误率 12.17%</text>
<text x="530" y="208" text-anchor="middle" font-size="14" fill="#374151">只用一块 GB300 芯片</text>
<text x="222" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="422" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="340" y="292" text-anchor="middle" font-size="16" font-weight="700" fill="#111827">错误减少约 45.8% — 印度医疗语音基准 Eka Care（NVIDIA 演示）</text>
</svg>
<figcaption>图 2 — 在行话密集的医疗语音上，提示词先帮了一截，一个下午的单卡微调又把错误率压掉近一半。</figcaption>
</figure>

## 它做不到的

它只处理录音文件，不支持实时流，实时字幕和语音助手不在范围内——那块市场这个月很热闹：ElevenLabs 的 Realtime、Mistral 的 Voxtral 3、Salesforce 的 Launa-Omni 都刚发布。要更小，还有自家 1.1B 的 Parakeet。

变化在所有权：转写正从租来的接口，变成能装进自己机房的东西。医院和会议室的录音不必离开大楼——而最需要转写的，恰恰是最不方便送出去的那些。
