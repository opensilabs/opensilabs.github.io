---
lng_pair: id_20261007_vista-arc-agi-3
title: "模型从来不笨，只是瞎：MIT 的 VISTA 让 Claude 在 ARC-AGI-3 拿下满分"
author: OpenSI-Labs
category: research
tags: [ARC-AGI-3, 视觉记忆, 智能体, MIT, VISTA]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-vista-arc-agi-3.png
meta_description: "MIT 的 VISTA 框架零训练，把 Claude Opus 5.0 在 ARC-AGI-3 的得分从 40.68 拉到满分 100——靠的是给模型一双真正的眼睛和无损记忆。瓶颈从来不是智能，是管道。"
---

10 月 1 日，MIT 五位研究者悄悄挂出一篇[论文](https://arxiv.org/abs/2610.02200)，读来像给整个智能体行业的一纸起诉书。VISTA——"交互世界中的视觉推理框架"，最抓眼球的数字：Claude Opus 5.0 在 ARC-AGI-3 上的得分从 40.68 跃至满分 100.00——25 个公开游戏全通关，动作数比初玩人类少 57.4%。无新权重，无新训练。从 40 到 100 的差距不是模型，是管道。

作者的论点简单到近乎冒犯：模型从来不笨，只是瞎。ARC-AGI-3 的官方接口递给模型一个 64×64 的数字网格，让它玩视觉解谜——拿着电子表格假装看图。人类看到的是游戏，模型读到的是账本。VISTA 只是把我们习以为常的东西还给模型：512×512 的渲染截图、一帧不丢的记忆、想看多细就看多细的自由。

<svg viewBox="0 0 720 336" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="VISTA：环绕模型的闭环">
  <defs>
    <marker id="arrV1a" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
    <marker id="arrV1b" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto-start-reverse"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">VISTA：环绕模型的闭环</text>
  <rect x="270" y="42" width="180" height="66" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="66" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">记住</text>
  <text x="360" y="86" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">无损视觉记忆</text>
  <text x="360" y="102" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">每一帧原样存档，按轮次索引</text>
  <rect x="30" y="152" width="150" height="66" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="105" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">看见</text>
  <text x="105" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">512×512 渲染截图</text>
  <text x="105" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">而非 64×64 数字网格</text>
  <rect x="285" y="152" width="150" height="66" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#5f3dc4">模型</text>
  <text x="360" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">权重纹丝不动</text>
  <text x="360" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">零新增训练</text>
  <rect x="540" y="152" width="150" height="66" rx="10" fill="#ebfbee" stroke="#2f9e44" stroke-width="2"/>
  <text x="615" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#2b8a3e">细看</text>
  <text x="615" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">行动 · 缩放 · 读像素</text>
  <text x="615" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">回看历史——模型自己指挥</text>
  <rect x="270" y="262" width="180" height="66" rx="10" fill="#fff5f5" stroke="#e03131" stroke-width="2"/>
  <text x="360" y="286" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#c92a2a">笔记本</text>
  <text x="360" y="306" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">GUIDE.md + WORKING.md</text>
  <text x="360" y="322" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">长期笔记 + 当前草稿</text>
  <line x1="182" y1="185" x2="283" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="437" y1="185" x2="538" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="110" x2="360" y2="150" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="220" x2="360" y2="260" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">VISTA 给一个权重不变的模型配上眼睛、无损记忆和笔记本。智能本来就在那里，缺的是接口。</p>

框架有三块拼图。一，视觉观测：渲染截图替代数字网格。二，无损视觉记忆：每一帧以原始形态存档，按轮次帧号索引，住在上下文窗口之外。三，模型自主检视：智能体自己决定看什么——play 行动，inspect 缩放查看任意历史帧区域，read_pixels 读精确像素值，history 回看行动结果。另有两个纯文本文件：GUIDE.md 贯穿会话的长期笔记，WORKING.md 当前游戏的草稿纸。纯机械结构，零可训练部件，25 个游戏共用同一套简短提示模板。

数字值得细读。Claude Opus 5.0：40.68 → 100.00，183 关共 7,302 个动作，人类初玩 17,135 个；单看 m0r0，人类 1,107 步对 Claude 219 步。GPT-5.6 Sol：基线 13.33，换截图到 47.32，完整框架 99.00。基线 1.89 的 320B 开源模型也被抬到 66.93。三次重复 99.00、98.90、99.23，稳定。作者表述克制——"据我们所知"，ARC-AGI-3 首个不靠程序合成的满分。今年夏天的领先系统都为每个游戏手写模拟器；VISTA 只用几句工作笔记推导出同样规则。

<svg viewBox="0 0 720 348" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="同样的权重，新的框架：VISTA 前后得分对比">
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">同样的权重，新的框架：ARC-AGI-3 得分（RHAE）</text>
  <rect x="180" y="44" width="12" height="12" fill="#adb5bd"/><text x="198" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">官方框架基线</text>
  <rect x="380" y="44" width="12" height="12" fill="#1c7ed6"/><text x="398" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">接入 VISTA</text>
  <text x="170" y="100" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">Claude Opus 5.0</text>
  <rect x="180" y="88" width="179" height="14" fill="#adb5bd"/><text x="364" y="99" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">40.68</text>
  <rect x="180" y="106" width="440" height="14" fill="#1c7ed6"/><text x="624" y="117" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">100.00</text>
  <text x="170" y="160" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">GPT-5.6 Sol</text>
  <rect x="180" y="148" width="59" height="14" fill="#adb5bd"/><text x="243" y="159" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">13.33</text>
  <rect x="180" y="166" width="436" height="14" fill="#1c7ed6"/><text x="620" y="177" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">99.00</text>
  <text x="170" y="220" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">320B 开源模型</text>
  <rect x="180" y="208" width="8" height="14" fill="#adb5bd"/><text x="192" y="219" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">1.89</text>
  <rect x="180" y="226" width="294" height="14" fill="#1c7ed6"/><text x="478" y="237" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">66.93</text>
  <line x1="180" y1="246" x2="620" y2="246" stroke="#dee2e6" stroke-width="1"/>
  <text x="180" y="260" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">0</text>
  <text x="396" y="260" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">50</text>
  <text x="616" y="260" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">100（RHAE）</text>
  <rect x="30" y="276" width="660" height="62" rx="8" fill="#fff9db" stroke="#e9d66b"/>
  <text x="48" y="300" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#7a5c00">少即是多：</text>
  <text x="48" y="322" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">看图每局 3070 万 token，看数字反而 7190 万 · 上下文 20 万→78 万，得分 99→93.9 · 图片放大 16 倍，得分掉到 88.3</text>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">RHAE（相对人类行动效率）衡量系统相对人类的解题效率。所有被测模型都有提升，基线越弱，提升越大。</p>

最反直觉的发现藏在成本里。看图比看数字便宜：每局 3,070 万 token 对 7,190 万。而更大的上下文反而有害：窗口 20 万→78 万 token，得分 99→93.9；图片放大 16 倍，得分掉到 88.3。读两遍。全行业在军备竞赛式堆上下文，把"公里级上下文"当标尺。VISTA 的回答近乎异端：胜利不属于更大的桶，属于知道何时翻笔记本、翻哪一页的模型。

同一套框架几乎不改就能玩别的：34 个 GameWorld 游戏成功率 63.3%，超人类新手的 55.3%；3D 透视场景 84.12，AI GameStore 超人类中位数；BabyVision 连点题的解法直白得好笑——模型把图放大了。通用性才是真正的信号：逐游戏手写的模拟器是定制西装，VISTA 是一双什么都能戴的眼镜。

作者自己给出了最诚实的保留：模型训练晚于公开游戏发布，私有 ARC-AGI-3 测试集才是检验泛化的真考场。这句话要钉在墙上。但它不影响关键对比——同一模型、同一权重，框架前后判若两人。天花板在哪另说，地板已经抬高了。

下面是多数报道会错过的部分。若前沿模型长期被系统性低估，只因眼睛吃不饱，过去两年的智能体框架榜可能都要重算。每张对比"模型"的榜单，一半在比管道：谁给了像样的界面，谁逼它读表格。这是二阶效应——变的不仅是排名，是排名所测之物本身。还有条更锋利的线索藏在论文设计里：GUIDE.md/WORKING.md 这本笔记本，功劳或不亚于视觉。外部情景记忆加随时回看的自由。"它们只是瞎了"干净好引用，但也许它们还健忘，药方是做笔记。

VISTA 的教训不是"框架胜过模型"，而是我们一直在给瓶颈贴错标签。说是推理能力的差距，就去堆更大的训练；其实是感知和记忆的差距，解法是管道代码加一个文本文件。智能体的下一个突破，可能不需要任何新参数，只需要有人发现模型还看不见什么。

资料来源：[论文](https://arxiv.org/abs/2610.02200)（arXiv:2610.02200）；[MIT 协议开源代码](https://github.com/joshhhhhan/vista)与[项目主页](https://vista-research.github.io/)；团队在 ARC Prize 的[官方成绩单](https://arcprize.org/scorecards/39be671a-d0cc-48b4-ae08-1db4abc44c83)（见代码仓库）。

**讨论：** 如果补上 ARC-AGI-3 最后一公里的是一套框架而不是一个模型——你关于 AI 进步的哪些判断，其实是对管道的判断？
