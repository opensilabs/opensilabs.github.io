---
lng_pair: id_20261020_ibm-agent-decoder
title: "26美元，AI给量子计算机设计了一颗芯片"
author: OpenSI-Labs
category: research
tags: [AI芯片设计, 量子计算, 智能体, IBM, 纠错解码器]
date: 2026-10-20 03:30:00 -0700
img: /assets/img/posts/2026-10-20-ibm-agent-decoder.png
meta_description: "IBM 用 AI 智能体工厂优化量子纠错解码器的硬件设计：开源模型花 26 美元把延迟砍了 52 倍。AI 开始设计自己要运行的硬件了。"
---

**26 美元能买到什么？**

这次的答案不是咖啡，也不是电影票。是把一颗量子计算机核心部件的设计，快进 52 倍的工程劳动——而且干活的，是几个 AI 智能体。

2026 年 10 月 13 日，IBM Research 发表了一篇预印本，报告了一件听起来像科幻的事：他们组建了一家"智能体工厂"（agent factory），让 AI 去优化量子纠错解码器的硬件设计。解码器是量子计算机里最不起眼、却最要命的部件——量子比特每微秒都在出错，解码器必须实时把错误算出来、纠回去，慢一拍，整台量子计算机就废了。IBM 的容错量子路线图，卡在这个部件上。

工厂的组织结构像一家微型芯片公司：一个"协调者"智能体负责规划搜索、提出优化假设；四个"工人"智能体各自重写解码器的 C++ 内核代码；一个"验证者"智能体检查每个候选设计是否正确；最后用 AMD 的综合工具把通过验证的设计变成真正的电路。总共 100 次尝试，5 轮，每轮 20 个假设——协调者根据上一轮的综合结果，决定下一轮往哪试。

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">智能体工厂：五个角色，一条流水线</text>
<rect x="250" y="48" width="180" height="52" rx="8" fill="#2b6cb0"/>
<text x="340" y="70" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">协调者</text>
<text x="340" y="90" font-size="14" text-anchor="middle" fill="#fff">规划 · 提假设</text>
<rect x="30" y="140" width="130" height="52" rx="8" fill="#4299e1"/>
<text x="95" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">工人 ×4</text>
<text x="95" y="182" font-size="14" text-anchor="middle" fill="#fff">重写 C++ 内核</text>
<rect x="200" y="140" width="130" height="52" rx="8" fill="#4299e1"/>
<text x="265" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">验证者</text>
<text x="265" y="182" font-size="14" text-anchor="middle" fill="#fff">检查正确性</text>
<rect x="370" y="140" width="130" height="52" rx="8" fill="#4299e1"/>
<text x="435" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">综合工具</text>
<text x="435" y="182" font-size="14" text-anchor="middle" fill="#fff">Vitis → 电路</text>
<rect x="540" y="140" width="130" height="52" rx="8" fill="#2b6cb0"/>
<text x="605" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">结果反馈</text>
<text x="605" y="182" font-size="14" text-anchor="middle" fill="#fff">延迟 · 面积</text>
<path d="M340 100 L95 132" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M160 166 L192 166" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M330 166 L362 166" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M500 166 L532 166" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M605 140 L605 118 L440 118" stroke="#718096" stroke-width="2" fill="none" stroke-dasharray="4" marker-end="url(#a1)"/>
<defs><marker id="a1" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0 0 L8 3 L0 6 Z" fill="#718096"/></marker></defs>
<text x="340" y="240" font-size="14" text-anchor="middle">5 轮 × 20 个假设 = 100 次尝试，协调者按结果决定下一轮方向</text>
<text x="340" y="266" font-size="14" text-anchor="middle" font-style="italic">组织像一家微型芯片公司：动脑的贵，动手的便宜</text>
</svg>
</div>
<figcaption style="text-align:center">IBM 的 agent factory 结构：协调者规划、工人改代码、验证者把关、综合工具出电路，结果反馈决定下一轮。</figcaption>
</figure>

然后是三组对照实验，差别只在"用哪个模型当大脑"：

<figure>
<div style="text-align:center">
<svg width="680" height="270" viewBox="0 0 680 270" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">三种配置，同样的100次尝试</text>
<text x="240" y="70" font-size="14" text-anchor="end">Claude Opus 5 全员</text>
<rect x="250" y="52" width="410" height="26" fill="#2b6cb0"/>
<text x="660" y="70" font-size="14">204× · 299 美元</text>
<text x="240" y="116" font-size="14" text-anchor="end">Opus 指挥 + GLM 工人</text>
<rect x="250" y="98" width="256" height="26" fill="#4299e1"/>
<text x="660" y="116" font-size="14">126× · 105 美元</text>
<text x="240" y="162" font-size="14" text-anchor="end">GLM-5.3 全员（开源）</text>
<rect x="250" y="144" width="107" height="26" fill="#90cdf4"/>
<text x="660" y="162" font-size="14">52× · 26 美元</text>
<text x="340" y="210" font-size="14" text-anchor="middle">起始设计延迟 28231 微秒 · 条长 ∝ 提速倍数（对数感）</text>
<text x="340" y="238" font-size="14" text-anchor="middle">最便宜的全开源方案便宜 11.5 倍，最佳设计慢约 4 倍</text>
</svg>
</div>
<figcaption style="text-align:center">IBM 智能体工厂的三种模型配置：延迟均为 HLS 估算，成本仅含模型推理。数据：Bhandwaldar 等，IBM Research 预印本，2026-10-13。</figcaption>
</figure>

全用 Claude Opus 5：最佳设计 139 微秒，比起点快 204 倍，花费 299 美元。"强脑指挥 + 廉价劳力"——Opus 当协调者、国产开源模型 GLM-5.3 当工人：快 126 倍，花 105 美元。全用 GLM-5.3：快 52 倍，只花 26 美元——它跑在 IBM 自家 544 张 H100 上，靠 llm-d 推理框架把每个 token 的成本压到了 0.1077 美元/百万，前缀缓存命中率 98%。

**聪明的钱花在"指挥"上，不在"搬砖"上**

三组实验放在一起，最有意思的不是 204 倍，而是混合组。

注意代码改动量：Opus 工人的改动中位数是 515 行，GLM 工人是 428 行，混合组的 GLM 工人只改了 197 行——改得最少，却拿到了 126 倍，远超全 GLM 组的 52 倍。换句话说，在一个强协调者手下，工人"少改、改对"比"多改、乱改"更有效。

IBM 团队自己也注意到了这一点：决定成败的，可能不是工人写了多少代码，而是"谁在决定试什么、谁在检查结果"。协调者和验证者这两个"动脑"的岗位，用最强的模型；工人这种"动手"的岗位，可以用便宜 13 倍的开源模型。这个结论如果成立，它描述的不只是芯片设计，而是所有智能体系统的经济学：**智能应该花在判断上，执行可以廉价化。**

而智能体真正改对了什么？原设计把解码器的数据存在查找表里，每次访问都要先查索引，综合工具根本看不出哪次读取会命中哪个存储体，只能串行慢慢走。智能体重排了内存布局，把数据按"校验节点+槽位"索引、拆进多个存储体，让 35 次读取可以并行；又把一个运行时循环的归约改成了固定树形结构，让工具能把它展开。两次手术，单次迭代的周期数从 229961 掉到 14824。这不是调参数的小聪明，是数据结构层面的重构——资深工程师才会动的那种地方。

**诚实的部分：它离人类高手，还差 44 倍**

如果故事到这里结束，它就是又一篇"AI 碾压人类"的爽文。但 IBM 的论文里藏着一段诚实的附录，值得每个传播者先读完。

第一，204 倍和 52 倍都是 HLS（高层次综合）的**估算值**，没有在真正的 FPGA 上测过；而且智能体优化的是一个缩小版问题（两轮的误差模型，144×1585），不是完整的解码器（864×8785）。

第二，也是最关键的：IBM 自己的工程师手工写过同款解码器的 RTL（寄存器传输级）版本，延迟约 0.3 微秒。而智能体最好的 HLS 设计，换算下来至少是它的 44 倍慢。论文附录里，智能体照着人类架构写了一版 RTL，周期数和手工版打平，但多用了 80% 的逻辑资源，时钟还慢了 10%。

所以准确的说法是：AI 智能体把"一份没优化过的起始代码"改进了 52 到 204 倍，在"探索设计空间"这件事上快得惊人、便宜得惊人；但距离人类顶尖工程师的手工极限，仍有数量级的差距。它像一个不知疲倦的初级工程师团队，能在一夜之间试完人类一周的方案，却还没有老师傅最后那一哆嗦的手艺。

但别急着看轻这个"探索者"。芯片项目里，解码器不是设计一次就完事的——纠错码变了、测量电路变了、噪声模型变了，都要重调。IBM 在 2029 年的容错机 Starling 之前，还要经历好几次这样的变更。每一次变更，如果都有一个 26 美元的"探索团队"先把设计空间摸个遍，人类工程师就能直接从高处起步。论文作者也说了大实话：每种配置只跑了一次，换个随机种子，排名可能就变了——所以别把这当成模型排行榜。

**AI 开始设计"自己要住的房子"**

把镜头拉远。为什么这件事值得从量子计算的细分领域里拿出来，讲给所有人听？

因为它示范了一个闭环的雏形：AI 智能体在优化的，是计算硬件本身。今天优化的是一颗量子解码器（跑在经典 FPGA 上），用的是 HLS 这种"高级语言写电路"的工具；明天，同样的工厂结构可以去优化 AI 芯片的某个模块、推理引擎的某个内核。设计计算的工具，正在被计算本身接管。

历史上，每一次"工具制造工具"的跃迁都改写了工业：机床造机床，编译器写编译器，EDA 软件设计芯片。现在轮到智能体——它们不只是用工具，它们开始改进工具链中最需要经验的那一环：设计空间的探索。

而经济学可能是更深远的那一半。当"做一轮认真的设计探索"的成本从一个工程师团队的数周薪水，掉到 26 美元，整个行业的试错节奏都会变。过去因为贵而没人试的方案，会被一一试过；过去靠资深工程师直觉把守的质量门槛，会变成"先让智能体跑 100 个方案再说"。IBM 把全开源方案单独拎出来讲，道理也在这里：544 张 H100、98% 的缓存命中率、0.1077 美元的单价——智能的成本结构，正在从"按人头付费"变成"按基础设施付费"，而基础设施是可以摊薄的。

当然，房子还没盖好。44 倍的差距、估算与实测的鸿沟、单次运行的偶然性，都提醒我们：这不是"AI 工程师上岗"的新闻，而是"AI 施工队第一次进场，先把脚手架搭得又快又便宜"的新闻。

但脚手架搭好之后，盖楼的人迟早会站在更高的地方往下看。26 美元一轮的探索、24 小时不休的工人、和一位越来越会"指挥"的协调者——下一次 IBM 再发这样的论文时，人类工程师的位置会在哪里？可能依然在最高处，只是脚下的楼层，已经全是机器盖的了。

---

*讨论：当 AI 能以 26 美元一轮的成本探索芯片设计，人类工程师不可替代的"判断力"，还够用多久？*
