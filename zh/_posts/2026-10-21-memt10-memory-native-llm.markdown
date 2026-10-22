---
lng_pair: id_20261021_memt10-memory-native-llm
title: "停止重读过去的模型"
author: OpenSI-Labs
category: LLMs
tags: [LLMs, memory, architecture, open weights, MemT]
date: 2026-10-21 00:00:00 -0700
img: /assets/img/posts/2026-10-21-memt10-memory-native-llm.png
meta_description: "MemT-1.0 把记忆装进语言模型的计算本身，不再重播越来越长的上下文：历史被折叠进固定大小的记忆状态，原始记录随即丢弃。"
---

每个大模型都有个怪习惯：重读自己的过去。漫长对话每轮，整段记录都重新灌入。档案柜越长越大，账单也跟着涨。

10 月 19 日，74 人团队 MemTensor Team [发布了 MemT-1.0](https://arxiv.org/abs/2610.26825)：记忆原生模型。

## 记忆，成为计算的一部分

MemT-1.0 给选定的 Transformer 模块配了一个**原生记忆模块**，与注意力**并行**：每轮结束，历史被逐 token 折叠进有界记忆状态，原文随即丢弃——状态大小固定。

更新机制借自英伟达的 [Gated DeltaNet-2](https://arxiv.org/abs/2605.22791)：每个 token 三步——**擦除**已能预测的内容，**写入**新信息，再按遗忘因子**衰减**。

<svg viewBox="0 0 720 430" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="原生记忆模块如何工作：每个 token 触发擦除、写入和衰减更新，记忆状态大小固定，与注意力并行运行。">
  <defs>
    <marker id="zf1a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="414" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">与注意力并行的记忆模块</text>

  <rect x="24" y="64" width="196" height="180" rx="10" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="122" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">普通注意力</text>
  <text x="122" y="122" text-anchor="middle" font-size="14" fill="#3d4f68">读取全部 KV 缓存</text>
  <rect x="52" y="140" width="140" height="66" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="122" y="166" text-anchor="middle" font-size="14" fill="#8a4b4b">档案柜越长越大</text>
  <text x="122" y="190" text-anchor="middle" font-size="14" fill="#8a4b4b">O(N) 状态</text>

  <rect x="262" y="64" width="196" height="180" rx="10" fill="#f6f3fb" stroke="#7b5fc8" stroke-width="2"/>
  <text x="360" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#3b2c66">原生记忆模块</text>
  <text x="360" y="122" text-anchor="middle" font-size="14" fill="#4c3d7d">擦除 &#8594; 写入 &#8594; 衰减</text>
  <rect x="292" y="140" width="136" height="66" rx="6" fill="#ffffff" stroke="#7b5fc8" stroke-width="1.5"/>
  <text x="360" y="166" text-anchor="middle" font-size="14" fill="#4c3d7d">状态大小固定</text>
  <text x="360" y="190" text-anchor="middle" font-size="14" fill="#4c3d7d">O(1) 状态</text>

  <rect x="500" y="64" width="196" height="180" rx="10" fill="#f3faf3" stroke="#4e7d4e" stroke-width="2"/>
  <text x="598" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c442c">输出</text>
  <text x="598" y="122" text-anchor="middle" font-size="14" fill="#33502f">注意力输出</text>
  <text x="598" y="146" text-anchor="middle" font-size="14" font-weight="bold" fill="#2c442c">+</text>
  <text x="598" y="170" text-anchor="middle" font-size="14" fill="#33502f">记忆注意力输出</text>
  <text x="598" y="200" text-anchor="middle" font-size="14" font-style="italic" fill="#33502f">两者相加</text>

  <line x1="224" y1="150" x2="256" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#zf1a)"/>
  <line x1="462" y1="150" x2="494" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#zf1a)"/>

  <rect x="24" y="268" width="672" height="120" rx="10" fill="#fff8ec" stroke="#c9962e" stroke-width="2"/>
  <text x="360" y="298" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c4210">逐 token、逐轮次：把过去折叠进去，丢掉原始记录</text>
  <text x="360" y="330" text-anchor="middle" font-size="14" fill="#6b5423">轮次结束 &#8594; 历史折叠进记忆状态 &#8594; 纯文本丢弃</text>
  <text x="360" y="360" text-anchor="middle" font-size="14" font-weight="bold" fill="#3a3226">消融：token 级粒度（&#8722;5.99）比更新规则（&#8722;0.25）更关键</text>
</svg>
图1：原生记忆模块与注意力并行；每个 token 擦除已预测内容、只写入残差。

消融实验最有启发：粒度从 token 级降到轮次级掉 5.99 分，换掉更新规则只掉 0.25。**何时写，远比怎么写重要。**

## 数字，诚实地标注

两档：**Nano**（36B/3B 激活，千万级记忆状态，基于 Qwen3.6-35B-A3B，权重 Apache-2.0）；**Flash**（288B/17B 激活，3.36 亿级记忆状态，基于 DeepSeek-V4-Flash，权重 MIT）。代码是非商业许可。

11 个记忆基准上，Flash 平均 **50.60**、Nano **46.97**，比最强参数化基线高 12.5 与 8.9 分。12.8 万 token 下存储低约 66 倍；首字延迟快 2.44 倍（25.6 万时 4.19 倍），稳定在约 104–112 毫秒。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="对比：经典模型每轮重播不断增长的记录，而 MemT-1.0 把历史折叠进固定记忆状态后丢弃记录。">
  <defs>
    <marker id="zf2a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="384" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">停止重读过去</text>

  <rect x="24" y="60" width="326" height="312" rx="10" fill="#faf0f0" stroke="#b07a7a" stroke-width="2"/>
  <text x="187" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c2c2c">经典大模型：背着过去</text>
  <rect x="52" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="130" text-anchor="middle" font-size="14" fill="#5c2c2c">第 1 轮 &#183; 第 2 轮 &#183; 第 3 轮 &#183; …</text>
  <rect x="52" y="152" width="270" height="54" rx="6" fill="#f3d9d9" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="174" text-anchor="middle" font-size="14" fill="#5c2c2c">KV 缓存 O(N) 增长</text>
  <text x="187" y="196" text-anchor="middle" font-size="14" fill="#5c2c2c">每个 token 都要重读</text>
  <text x="187" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#8a2f2f">存储与延迟一路上涨</text>
  <text x="187" y="268" text-anchor="middle" font-size="14" fill="#5c2c2c">TTFT：128K 257ms &#8594; 256K 445ms</text>
  <text x="187" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#7a5656">记忆 = 档案柜</text>

  <rect x="370" y="60" width="326" height="312" rx="10" fill="#f0f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="533" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">MemT-1.0：消化过去</text>
  <rect x="398" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="130" text-anchor="middle" font-size="14" fill="#3d4f68">第 1 轮 &#8594; 折叠 &#183; 丢弃</text>
  <rect x="398" y="152" width="270" height="54" rx="6" fill="#d9e6f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="174" text-anchor="middle" font-size="14" fill="#2c3e55">记忆状态固定 O(1)</text>
  <text x="533" y="196" text-anchor="middle" font-size="14" fill="#2c3e55">查询只读状态</text>
  <text x="533" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#1c4e80">128K 下存储少 66 倍</text>
  <text x="533" y="268" text-anchor="middle" font-size="14" fill="#2c3e55">TTFT 稳定约 104–112ms &#183; 256K 快 4.19 倍</text>
  <text x="533" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#55697f">记忆 = 巩固，如大脑</text>

  <text x="360" y="348" text-anchor="middle" font-size="14" fill="#6b5f45">代价：固定大小的记忆用保真度换成本——文本系统分数仍更高（68.5 对 50.6）</text>
  <text x="360" y="372" text-anchor="middle" font-size="14" fill="#8a7d5c">所有数字均为作者宣称，尚无独立复现</text>
</svg>
图2：记忆原生路径的赌注——更便宜、更快，代价是损失保真度。

诚实的注脚：**文本/RAG 系统分数依然更高**（MemOS 约 68.5 对 Flash 50.6）。所有数字来自作者：**零独立复现**——这些基准是主张，而非定论。部署务实：SGLang 推理加 Transformers 上手，会话可存快照恢复。

## 一周之内，三路进攻同一个成本

同一周三种下注：**架构**——MemT-1.0 把记忆塞进计算图；**模型即写手**——腾讯 Hy-Memory-30B-A3B（独立无关的项目）走反方向，专精向**外部**记忆框架写记忆；**基础设施**——DeepSeek 开源 **DeepInfer**，在系统层攻击同一个成本。

**值得争论：**如果记忆能折叠进固定状态、记录本身可丢弃，智能体的信条——AI 的过去应当**可审查**——会怎样？可审计的压缩记忆是座档案柜；只能被信任的巩固记忆，则是另一种东西。
