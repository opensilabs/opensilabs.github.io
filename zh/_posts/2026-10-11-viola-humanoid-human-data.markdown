---
lng_pair: id_20261011_viola-humanoid-human-data
title: "VioLA：用人类的动作数据，教人形机器人走路"
author: OpenSI-Labs
category: robotics
tags: [人形机器人, 模仿学习, 动作隐空间, 宇树G1, 通用策略]
date: 2026-10-11 06:00:00 -0700
img: /assets/img/posts/2026-10-11-viola-humanoid-human-data.png
meta_description: "VioLA 让通用人形机器人策略预测动作隐编码而非关节指令，把人类动作录像变成可直接用的训练数据。"
---

人形机器人最难的不是硬件——宇树 G1 堪比二手车价，还能后空翻。难的是教它做事：每个新任务都要雇人遥操几小时录关节角度，又慢又贵。Mert Albaba 等人（arXiv:2610.12435）换了思路：不建更大的遥操车队，而是改变策略预测的目标——VioLA。

## 从"关节抽搐"到"动作本身"

困境：人形动作空间紧耦合、演示稀缺，每个任务都要遥操微调；而海量人类动作数据不是机器人指令。

VioLA 一步解掉两个困境：策略预测身体与手的**动作隐编码**而非关节指令——描述"旋转"而非肌肉抽搐，动作本身可以在身体之间翻译。

三块：**动作编码器**把录像压缩成编码，让人、机的同一动作落在编码空间同一区域；**通用策略**只预测下一个动作编码；**预训练的身体与手部控制器**把编码解码成关节力矩，训练时冻结。

回报是数据：任何人类录像都能被编码成带标签样本。1.406 亿帧中 **93.2% 是人类录像**。

<figure>
<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="120" y="22" font-size="15" font-weight="bold" text-anchor="middle">旧路线</text>
<rect x="30" y="40" width="180" height="44" rx="8" fill="#f0f4ff" stroke="#3366cc"/>
<text x="120" y="66" font-size="13" text-anchor="middle">策略预测</text>
<text x="120" y="80" font-size="13" text-anchor="middle" font-weight="bold">关节指令</text>
<line x1="120" y1="84" x2="120" y2="112" stroke="#3366cc" stroke-width="2" marker-end="url(#a1)"/>
<rect x="30" y="112" width="180" height="44" rx="8" fill="#ffecec" stroke="#cc3333"/>
<text x="120" y="131" font-size="13" text-anchor="middle">依赖遥操采集的</text>
<text x="120" y="146" font-size="13" text-anchor="middle" font-weight="bold">机器人演示</text>
<text x="120" y="180" font-size="13" text-anchor="middle" fill="#cc3333">✗ 稀缺、昂贵</text>
<text x="520" y="22" font-size="15" font-weight="bold" text-anchor="middle">VioLA</text>
<rect x="430" y="40" width="180" height="44" rx="8" fill="#f0f4ff" stroke="#3366cc"/>
<text x="520" y="66" font-size="13" text-anchor="middle">策略预测</text>
<text x="520" y="80" font-size="13" text-anchor="middle" font-weight="bold">动作隐编码</text>
<line x1="520" y1="84" x2="520" y2="112" stroke="#3366cc" stroke-width="2" marker-end="url(#a1)"/>
<rect x="430" y="112" width="180" height="44" rx="8" fill="#e8f8ec" stroke="#2a9d48"/>
<text x="520" y="131" font-size="13" text-anchor="middle">冻结的控制器</text>
<text x="520" y="146" font-size="13" text-anchor="middle">执行隐编码</text>
<text x="520" y="180" font-size="13" text-anchor="middle" fill="#2a9d48">✓ 直接用人像录像训练</text>
<line x1="210" y1="62" x2="430" y2="62" stroke="#999" stroke-width="1.5" stroke-dasharray="6,4"/>
<text x="320" y="52" font-size="13" text-anchor="middle" fill="#555">改变预测</text>
<text x="320" y="68" font-size="13" text-anchor="middle" fill="#555">目标</text>
<text x="320" y="150" font-size="13" text-anchor="middle" fill="#555">1.406亿帧，</text>
<text x="320" y="166" font-size="13" text-anchor="middle" fill="#555">93.2% 来自人类</text>
<defs><marker id="a1" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 z" fill="#3366cc"/></marker></defs>
</svg>
<figcaption style="font-size:0.85em;color:#666;text-align:center">旧路线与 VioLA：预测关节指令的策略需要机器人专属演示；预测共享动作隐编码，则把人类录像变成了训练数据。</figcaption>
</figure>

## 数字相当惊人

真机宇树 G1，未见过的行走指令，零任务微调，成功率 **100%**；基线 GR00T N1.7 和 Ψ₀只有 16.7% 和 0%。抓取操作 **88.6%**，同样零微调。纯人类演示训练的策略就能零样本行走——人类数据才是关键。

方法可迁移：两套 VLA 骨干、一个世界-动作模型骨干上都成立。这是一种方法，不是炼丹技巧。（预印本，代码权重未发布。）

## 更深的变化是经济学

机器人行业的护城河一直是遥操车队。VioLA 反转了逻辑：稀缺资产变成"编码器＋控制器"，谁造出最好的身体语言词典，谁就拿到杠杆。

更远的一层：如果人机共享同一套隐"身体语言"，策略就不绑定某一家机身——"身体无关"而不仅是"任务无关"。尚未被证明，但架构正指向那里。

机器人学花了十年采集机器人数据来模仿人类。VioLA 暗示方向反了：数据一直在人类动作录像里，缺的只是一种两具身体都能说的语言。

**讨论：** 每段人类动作录像都能变成训练数据，"动作"的归属权属于谁？

---
*来源：[VioLA: Learning Generalist Humanoid Control Policies from Human Data](https://arxiv.org/abs/2610.12435)（arXiv:2610.12435）；[QUE.com 机器人综述，2026年10月](https://que.com/world-models-redefine-the-future-of-autonomous-robotics/)。*
