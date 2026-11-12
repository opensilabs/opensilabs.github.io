---
layout: post
lng_pair: id_20261111_alphagenome2
title: "AlphaGenome 2：先告诉它你问的是哪种细胞，同一段 DNA 它能读出完全不同的答案"
author: OpenSI-Labs
category: Bio AI
tags: [AlphaGenome 2, DeepMind, 基因组学, DNA, 单细胞, 变异效应]
date: 2026-11-11 06:00:00 -0800
img: /assets/img/posts/2026-11-11-alphagenome-2.png
---

## 一、谜题

全身细胞带着同一本说明书——DNA，基因是书里的菜谱。可肠道细胞和血液细胞翻开的章节不同，做的事完全不同。多数疾病变异不在菜谱里，而在菜谱周围的开关和调光旋钮上。改一个字母，开关松紧就变，基因开多大也跟着变。

## 二、第一代的盲点

Google DeepMind 的第一代 AlphaGenome 能读 100 万字母长的 DNA，预测基因活动轨道、表达量和染色质三维接触图。但它只用混合组织的大块数据训练，对所有组织只给一个平均答案，像把一整杯奶昔搅匀、没法单独尝每种水果，说不清某个变异只在哪种细胞里起作用。

## 三、第二代的改动

AlphaGenome 2 把条件当成输入：组织、细胞类型、状态、物种（人或小鼠），一起喂给模型。网络每一层的自适应归一化层都被一个条件向量调制。它可以从学出来的参考词典里选，也可以由细胞编码器直接从你自己的单细胞 RNA 数据算出。这样，拿自己的数据就能问模型没听过名字的细胞类型或状态，不用重新训练。训练分四步：预训练、条件精修、蒸馏、后训练——八个教师模型先在随机突变的序列上给出平均输出，蒸馏成一个学生模型，学生再用单细胞数据后训练。

<figure>
<svg viewBox="0 0 720 250" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="同一段 DNA 在不同细胞里作用不同">
<text x="360" y="28" text-anchor="middle" font-size="18" font-weight="bold" fill="#111827">同一段 DNA，不同细胞，不同答案</text>
<rect x="20" y="80" width="200" height="34" rx="17" fill="#dbeafe" stroke="#2563eb" stroke-width="1.5"/>
<text x="38" y="103" font-size="15" fill="#1f2937">A</text>
<text x="62" y="103" font-size="15" fill="#1f2937">C</text>
<text x="86" y="103" font-size="15" fill="#1f2937">G</text>
<text x="110" y="103" font-size="15" fill="#1f2937">T</text>
<text x="134" y="103" font-size="15" fill="#1f2937">A</text>
<rect x="152" y="84" width="20" height="26" rx="4" fill="#fecaca" stroke="#dc2626" stroke-width="1.5"/>
<text x="157" y="103" font-size="15" font-weight="bold" fill="#dc2626">C</text>
<text x="182" y="103" font-size="15" fill="#1f2937">G</text>
<text x="162" y="132" text-anchor="middle" font-size="14" fill="#dc2626">▲ 改了一个字母</text>
<text x="120" y="160" text-anchor="middle" font-size="14" fill="#374151">同一段 DNA，只改了一个字母</text>
<circle cx="315" cy="97" r="32" fill="#fef3c7" stroke="#d97706" stroke-width="1.5"/>
<circle cx="315" cy="97" r="12" fill="#f59e0b"/>
<circle cx="425" cy="97" r="32" fill="#dcfce7" stroke="#16a34a" stroke-width="1.5"/>
<circle cx="425" cy="97" r="12" fill="#22c55e"/>
<text x="315" y="160" text-anchor="middle" font-size="14" fill="#374151">血液细胞？</text>
<text x="425" y="160" text-anchor="middle" font-size="14" fill="#374151">肠道细胞？</text>
<rect x="490" y="72" width="45" height="20" rx="4" fill="#9ca3af"/>
<text x="545" y="87" font-size="14" fill="#374151">基因关着</text>
<rect x="490" y="112" width="125" height="20" rx="4" fill="#22c55e"/>
<text x="490" y="160" font-size="14" fill="#374151">基因开着</text>
</svg>
<figcaption>图 1 — 同一段 DNA 在不同细胞里做的事可以完全不同。AlphaGenome 2 把“哪种细胞”本身当作问题的一部分。</figcaption>
</figure>

## 四、证据

在 TenK10K 单细胞数据上，对比在单细胞数据上微调过的一代 AG1-sc：找真正改变表达的变异，召回率 16%→30%（90% 精确率下）；判对上调还是下调，23%→43%。换成大白话：每 10 个真正的因果变异，第一代大约找到 2 个，第二代能找到 3 个——进步了，但还漏 7 个。再看炎症性肠病：21 号染色体上的变异 rs2836882，早被实验证明靠上调 29 万个字母外的 ETS2 基因提高风险，且只在单核细胞和巨噬细胞里起作用。它拿到 7 个候选变异，只标出这一个：隔着 29 万个字母连对基因，效应只落在那两类细胞上，三点全对。以上数字都来自 DeepMind 自己的论文。

## 五、局限与未给的东西

论文写得很清楚：30% 召回，意味着漏掉 70%。位于不可及染色质、极远端，或在转录之后起作用的变异会被低估；短暂、受刺激、疾病状态的细胞在训练数据里偏少；精细的神经元亚型分不清；条件向量学到的是相关，不是因果；能不能处理基因敲除和动态变化，还不知道。现在只有非商业研究 API；源代码和权重只说“正式发表时”提供，尚未发布——第一代随论文放了权重，这一代反而退了一步。仅限研究，未经临床验证。它能帮科学家缩小实验范围，但不能替实验下结论。
