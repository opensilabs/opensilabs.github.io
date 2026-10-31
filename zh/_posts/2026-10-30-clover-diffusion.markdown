---
layout: post
lng_pair: id_20261030_clover-diffusion
title: "Clover 不逐字写、整块填空：35B 扩散模型一次填 32 个词，SWE-bench 自报 73.6 分"
author: OpenSI-Labs
category: 人工智能模型
tags: [扩散语言模型, Clover, DiffuSpace, 开源权重, SWE-bench]
date: 2026-10-30 20:00:00 -0700
img: /assets/img/posts/2026-10-30-clover-diffusion.png
---

10 月 28–29 日，DiffuSpace 发布首个模型 Clover-35B-A3B-Preview：一个不逐字写的语言模型。权重在 Hugging Face 上，Apache 2.0，BF16 约 69GB 可下载。公司称它是迄今最强的开源扩散模型——此话可查；头条分数暂时查不了。

## 先摆 32 个空，再往里填

自 GPT 以来，主流模型逐词写：选定不能改，早期选错整句绕着错误走；第 500 个词须等前 499 个。

Clover 一次写 32 个词一块。整块先全是掩码空位，模型双向看整块，并行先填最有把握的几个；邻居定了，余下的也明确起来，续填。填满即固定，成为下一块的上下文——像编辑对留空草稿先填确定的词，而非不能退格的打字员。

<figure>
<img src="/zh/assets/img/posts/2026-10-30-clover-diffusion-fig1.svg" alt="两种写法：逐个词写，或一整块 32 个空位">
<figcaption>图 1 — 自回归模型逐字落笔、写下即定；Clover 先摆 32 个空位，最有把握的先填。</figcaption>
</figure>

规则（LowConfidence 解码）：置信度过 0.95 才填；无一过线，就填最有把握的一个，不会卡住。块内双向注意，块前文本仍因果处理。去噪时还可把专家路由限于一块共用的子集。

<figure>
<img src="/zh/assets/img/posts/2026-10-30-clover-diffusion-fig2.svg" alt="一块 32 个空位分三轮填满">
<figcaption>图 2 — 一块分几轮填满：置信度过 0.95 的位置先填，填满的块成为下一块的前缀。</figcaption>
</figure>

## 底子和参数

总参数 35B，每词激活约 3B；40 层，256 个路由专家每词选 8 个，另每层 1 个共享专家；上下文 128K，纯文本。源自阿里 Qwen3.6-35B-A3B，保留 Gated DeltaNet 与全注意力混合骨干；新增双向块注意力（含右卷积权重）、块扩散推理与生成控制。

## 73.6 分没法核对

公司自报：SWE-bench Verified 73.6，Terminal-Bench 2.1 51.7，单张 H200 每秒 515 词。但 73.6 无从核对：Daily Inference 10 月 29 日的独立分析指出其脚手架、工具、尝试次数、运行设置均未披露；权重与许可可查，分数不可复现。它只能算盒面宣称，不是实测，另两个数字同理。

## 能下载，不等于能跑

目前只能用 Transformers 加约 69GB 显存的 GPU 跑。无 GGUF 版，Ollama、LM Studio 不可用；SGLang 支持未并入上游。本地笔记本这周还跑不了它。

模型卡自承：超长输出易重复，故默认开启对策（presence penalty 0.9、repetition penalty 1.05、渐强收尾偏置）。确实是 Preview。

## 为什么重要

逐字写有两大先天限制：速度受串行所限，早期错误被锁死。块扩散两面齐攻：并行填空可快得多，整块可在固定前整体成形。机制真在代码里，分数是欠条。若独立复测近 73.6，逐字习惯将被动摇；若远不及，它仍是迄今最强的开源扩散模型——并非发布稿说的那场革命。
