---
lng_pair: id_20261006_delta-matching-fp8-training
title: "最后一块拼图：Delta-Matching 让 LLM 原生 FP8 训练真正落地"
author: OpenSI-Labs
category: research
tags: [FP8, 大模型训练, 量化, NVIDIA]
date: 2026-10-06 00:30:00 -0700
meta_description: "CMU/NVIDIA 论文以数学证明揪出 FP8 训练精度差距的根因——被破坏的 softmax 不变量，并用闭式修正填上最后一公里。"
---
# 最后一块拼图：Delta-Matching 让 LLM 原生 FP8 训练真正落地

9 月 29 日，CMU 与 NVIDIA 五人团队发表[论文《Delta-Matching: Closing the Final Gap of Native 8-bit Training for LLMs》](https://arxiv.org/pdf/2609.37852)（arXiv:2609.37852）：全流程原生 8 位训练，精度零损失（[TechTimes 报道](https://www.techtimes.com/articles/328385/20261001/eight-bit-llm-training-now-matches-full-precision-mit-nvidia-fix-root-cause.htm)）。

H100 的 FP8 稀疏算力 3,958 TFLOPS，BF16 只有 1,979——同芯片同功耗下算力翻倍。前沿预训练一次烧掉数千万美元；拿下这 2 倍，硬件账单砍半，或有效 batch 翻倍。

卡住大家的不是算力，而是算力背后的数学。线性层早已适应 8 位，钉子户是注意力。Transformer Engine、cuDNN 走混合路线：前向 FP8，反向敏感算子退回 BF16/FP32，2 倍红利永远拿不满。

病根是前向-反向不一致：注意力前后向的操作数被独立量化、缩放因子各异，生出 stale delta：δˢᵗᵃˡᵉ = ⟨dOᵢ, Ôᵢ⟩。它破坏了 softmax 梯度的零行和不变量——注意力每行是概率分布，行和恒为 1，所以梯度行和必须为 0。这是守恒律。stale delta 恰在此注入系统性偏差，梯度不再是诚实修正，而是一行行的缓慢漂移：训练是被慢性毒死的。

bug 藏了多年也因此得到解释：569M 下损伤只是小 loss 差距，会被当成噪声；到 1.67B 和 5.29B 才显著退化。小模型藏住了故障模式，工程式调参永远找不到结构性病因——独立量化按构造就破坏不变量。

修复同样是数学的：Delta-matching 以闭式修正调整过期缩放因子，精确恢复零行和。注意力所有矩阵乘法在块缩放下原生跑 FP8：前向 Q·Kᵀ、P·V 与反向转置。不改架构、不缩 batch、不额外保存输出，标准的 drop-in 改进。

FP8 有两种格式：E4M3（4 指数 3 尾数）精度细、范围窄，适合前向的激活与权重；E5M2（5 指数 2 尾数）范围宽，适合梯度。stale delta 就诞生在两种格式的交接处——delta-matching 是让两者在同一本账簿上对账的协议。

验证集交叉熵 1.4162，对 BF16/FP32 基线 1.4178——打平且反超一丝；朴素 FP8 崩到 1.8970；TE/cuDNN 混合方案只到 1.6105。569M、1.67B、5.29B 全部打平，常识基准差距 1 个百分点以内，RULER-8K 47.8 对 52.3，换上 Muon 依然成立。实现、模型与数据配方将开源。

数字之外有两件事。第一，经济学。成本减半不只是省钱，它改变"谁有资格站在前沿"。训练精度正成为参数量、数据之外的第三条 scaling 轴，因为算力就是预算——从十年前 Song Han 的 Deep Compression 到今天，每一步都在悄悄做同一件事。第二，突破的形状：最后一公里不是被更好的 kernel 或调参填上的，而是靠"指认被违反的数学不变量，再用闭式修好"。这是系统工作的 recurring pattern：工程磨不掉的残差，几乎总是一块被默认成立、实则已破的数学。

**讨论：** 十个新实验室而非三个能站在前沿训练，变化更快的是科学本身，还是"谁有资格做科学"的政治？
