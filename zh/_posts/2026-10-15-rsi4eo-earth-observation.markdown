---
lng_pair: id_20261015_rsi4eo-earth-observation
title: "人类建造的最后一个模型：递归自我改进的地球观测者"
author: OpenSI-Labs
category: research
tags: [递归自我改进, RSI4EO, 对地观测, 编程智能体, 可验证AI]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-rsi4eo-earth-observation.png
meta_description: "编程智能体自行构建地球观测模型并在自身输出上递归改进，仅用约百分之一的训练标注就在四个卫星影像基准测试中超越已发表的最佳结果。"
---

**河水上涨时，没人有时间训练模型。**

洪水漫过三角洲，应急队今天就要一张受灾图——哪里被淹、哪条路能走。卫星已在头顶，各波段画面齐了。但像素变地图仍靠专家，几周起步。等模型就绪，水退了，地图成历史。

10月13日一篇arXiv论文：整个循环交给智能体呢（[Zhao等，arXiv:2610.18845](https://arxiv.org/abs/2610.18845v1)）？标题挑衅——《人类建造的最后一个遥感模型？》，论断是数月来递归自我改进最锋利的表述：可验证任务都能铸造成RSI，对地观测是第一个完成的领域。

机制两个词：脚手架与考官。前者是智能体可用的一切——数据、工具、算力；后者是终点密封的考试：打分，不暴露保留图像。仅此二者，智能体就能建模并在自身输出上递归改进。

<figure>
<svg viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">RSI4EO：人出考题，智能体建模型</text>
<rect x="20" y="60" width="200" height="110" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="120" y="86" font-size="14" font-weight="bold" text-anchor="middle">人工设计</text>
<text x="120" y="110" font-size="14" text-anchor="middle">工具箱：数据 · 工具 ·</text>
<text x="120" y="130" font-size="14" text-anchor="middle">智能体可用的算力</text>
<text x="120" y="152" font-size="14" text-anchor="middle" font-style="italic">密封验证器：打分</text>
<rect x="250" y="60" width="180" height="110" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="340" y="86" font-size="14" font-weight="bold" text-anchor="middle">代码智能体</text>
<text x="340" y="110" font-size="14" text-anchor="middle">构建地球观测模型，</text>
<text x="340" y="130" font-size="14" text-anchor="middle">在自身输出上递归改进</text>
<text x="340" y="152" font-size="14" text-anchor="middle"></text>
<rect x="460" y="60" width="200" height="110" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="560" y="86" font-size="14" font-weight="bold" text-anchor="middle">更优的地球观测模型</text>
<text x="560" y="110" font-size="14" text-anchor="middle">洪水 / 作物 / 灾损</text>
<text x="560" y="130" font-size="14" text-anchor="middle">卫星影像制图</text>
<text x="560" y="152" font-size="14" text-anchor="middle"></text>
<line x1="220" y1="115" x2="246" y2="115" stroke="#3366cc" stroke-width="2" marker-end="url(#m1)"/>
<line x1="430" y1="115" x2="456" y2="115" stroke="#cc8833" stroke-width="2" marker-end="url(#m1)"/>
<path d="M 560 170 C 560 260, 120 260, 120 176" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#m1)"/>
<text x="340" y="300" font-size="14" text-anchor="middle" font-style="italic">上一轮的输出成为下一轮的输入</text>
<text x="340" y="330" font-size="14" text-anchor="middle">可验证：标注 · 独立传感器 · 物理模型 · 重复观测</text>
<defs><marker id="m1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>这个循环：人设计脚手架与密封考官；智能体构建模型，并在自身输出上改进它。</figcaption>
</figure>

为何是卫星不是诗歌？对地观测里，现实打分。作者证明，每个任务经四通道之一可验证：标注基准、独立传感器、物理模型、重复观测。洪水模型用几小时后的雷达检验；作物分类用物理生长模型检验。少标注学习、跨域适应，坍缩成脚手架与考官的选择。

数字让宣言变成果。四个横跨光学、SAR、多光谱时序的基准上，智能体模型超越已发表最佳，全量标注下四战全胜。更扎眼：仅用0.2%~1.4%标注，保留69%~84%分数（[ArXivSignals](https://arxivsignals.io/explore)）。百分之一的标注，大部分精度。

<figure>
<svg viewBox="0 0 680 260" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">标注效率：约1%标注量，保留大部分精度</text>
<text x="200" y="70" font-size="14" text-anchor="end">全量标注</text>
<rect x="210" y="54" width="380" height="24" rx="4" fill="#3366cc"/><text x="598" y="71" font-size="14">100%</text>
<text x="200" y="116" font-size="14" text-anchor="end">0.2–1.4% 标注量</text>
<rect x="210" y="100" width="290" height="24" rx="4" fill="#cc8833"/><text x="508" y="117" font-size="14">69–84% 得分</text>
<text x="200" y="162" font-size="14" text-anchor="end">已发表基线</text>
<rect x="210" y="146" width="330" height="24" rx="4" fill="#999"/><text x="548" y="163" font-size="14">4/4 被超越</text>
<text x="340" y="210" font-size="14" text-anchor="middle">四个基准：光学 · SAR · 多光谱时序</text>
<text x="340" y="236" font-size="14" text-anchor="middle" font-style="italic">智能体构建的模型在所有任务上超越最优水平</text>
</svg>
<figcaption>只用一小部分标注，智能体构建的模型就保留了大部分精度——还击败了所有已发表基线。</figcaption>
</figure>

多数报道会错过：递归自我改进有两个一半，难的只有一半。"自我"一半——重写代码、蒸馏轨迹——已是常规。"改进"一半才是瓶颈：无人点头时，何谓"更好"？RSI4EO指向信号不来自人类也不来自LLM裁判的领域——来自世界。独立传感器不被奉承，物理模型不被糊弄。密封考官成立，因答案在其够不着处。

还有递归红利：对地观测模型随智能体进步而进步。每次进步自动升级所有地球观测管线。作者的分工主张：人设计脚手架与考官，智能体构建模型。稀缺技能从遥感知识变成考官设计。

保留意见同样重要：四基准是滩头非征服；能否搬到材料、芯片、药物是未定之赌。密封考官在悄悄干重活——安全全押智能体永不作弊。Goodhart定律终结的循环，比技术瓶颈终结的更多。

但这是第一次：整整一个领域被重述，智能体可度量地改进自己的模型，打分的是世界本身。

如果考官是自我改进安全运行的关键——谁来验证考官？智能体学会自建考官那天，会发生什么？
