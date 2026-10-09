---
lng_pair: id_20261009_openai-722-math-manuscripts
title: "数学的粒子对撞机：OpenAI 的 722 篇数学手稿"
author: OpenSI-Labs
category: research
tags: [OpenAI, 数学, Lean, 自动定理证明, 研究评估]
date: 2026-10-09 06:00:00 -0700
img: /assets/img/posts/2026-10-09-openai-722-math-manuscripts.png
meta_description: "OpenAI 公开了 722 篇由单个 AI 智能体写出的数学手稿。真正的故事是这条流水线：基准测试已饱和，开放问题成了新的前沿评估，而人类验证成了瓶颈。"
---

10 月 6 日，OpenAI 做了一件出版史上没有先例的事：把一个数学系一年的产出一次性倒进一个公开 GitHub 仓库。[openai/math](https://github.com/openai/math) 收录 719 篇手稿、372 个"成果家族"（发布时称 722 篇），全部来自一个未公开的内部模型。Apache-2.0 协议，几天内约 12800 星，里面是机器名下最激进的数学断言：四维 Kakeya 猜想解法、黎曼 zeta 函数更宽的零点自由区、CM 阿贝尔簇上有理 Hodge 猜想证明。

但定理不是故事。流程才是。

## 真正的新闻是流程

绝大多数成果来自同一套固定流程：约 4000 道开放问题交给模型；每个被采纳的成果平均消耗约 3 小时"ChatGPT Pro 级思考"算力；通过显著性门槛的输出聚成"家族"——主结果加配套论证。发言人告诉《科学美国人》，模型"几乎所有成果都来自交给单个 AI 智能体的一条提示词"。一条提示词，一个智能体，372 个家族。这不是 722 个独立项目，而是一次高产的智能体运行。README 直言原因："现有数学评估已饱和，我们才把评估扩展到开放研究问题。"基准已死，未解数学接替了它：新的前沿评估不是测试集，是开放文献。

<svg viewBox="0 0 720 560" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="机器研究流水线：4000 个问题进，372 个成果家族出">
  <defs>
    <marker id="arrM" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">机器研究流水线：4000 个问题进，372 个家族出</text>
  <rect x="255" y="45" width="210" height="56" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="70" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#1864ab">约 4000 个开放问题</text>
  <text x="360" y="90" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">交给同一个模型</text>
  <line x1="360" y1="101" x2="360" y2="116" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="118" width="270" height="56" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="143" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#e67700">单一智能体，一条提示词</text>
  <text x="360" y="163" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">每个成果约 3 小时"思考"</text>
  <line x1="360" y1="174" x2="360" y2="189" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="191" width="240" height="56" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="216" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#5f3dc4">显著性筛选</text>
  <text x="360" y="236" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">约 18% 通过，其余舍弃</text>
  <line x1="360" y1="247" x2="360" y2="262" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="255" y="264" width="210" height="56" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="289" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">372 个成果家族</text>
  <text x="360" y="309" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">719 篇手稿，17 个学科</text>
  <line x1="360" y1="320" x2="360" y2="335" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="337" width="240" height="56" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="362" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#a61e4d">Lean 形式化</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">约 42% 核心成果通过机器验算</text>
  <line x1="360" y1="393" x2="360" y2="408" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="410" width="270" height="56" rx="10" fill="#f8f9fa" stroke="#868e96" stroke-width="2"/>
  <text x="360" y="435" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#495057">版本化公开仓库</text>
  <text x="360" y="455" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Apache-2.0，逐篇 BibTeX，更新日志</text>
  <text x="360" y="500" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">两个步骤脱离了固定流程：黎曼 zeta 零点自由区（文稿经人工润色），</text>
  <text x="360" y="518" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">以及 CM 阿贝尔簇上的 Hodge 猜想证明。</text>
</svg>
*图 1：发布流水线——一个智能体，一条提示词，两个人工例外；模型下游的一切都是基础设施。*

断言分量不一。两个脱离了固定流程：黎曼 zeta 零点自由区——更宽的 Re(s) > 11/12（完整猜想需 1/2），文稿经人工润色；CM 阿贝尔簇上有理 Hodge 猜想在所有维数与余维数下的证明。17 个学科中，理论计算机科学以 40 个家族居首。

## Lean 是承重墙

仓库自带 Lean 库——机械验算证明的每一步。约 42% 核心成果已形式化，独立统计 722 篇中有 162 篇带机器验算的主结果。通过 Lean 验算是一种全新信任基座：正确性不再依赖声誉或审稿人体力。

但多数报道漏掉关键细节：Lean 只证明论证能从前提推出，不回答结果是否新颖、重要、有趣。机器验算不等于同行评审。OpenAI 承认部分未形式化结果"可能存在问题"，修正以公开版本记录——科学有了发布日志。高等研究院警告依然有效：AI 能输出"连提示者本人都无法理解、无法验证、无法负责"的数学论证。

这场发布由争吵塑造：一个月前 OpenAI 宣称约 1 万个智能体 88 小时解决 Navier–Stokes 存在光滑性问题，二十多位菲尔兹奖得主联署《AI 在数学中的严重错位》声明。此后高等研究院成立"数学与 AI 咨询组"，9 月 29 日建议公布模型、公开提示词、停止把数学成果当营销。OpenAI 只做半套：平均算力而非逐题算力，十份摘要而非完整轨迹，没有提示词。发言人称公司"不受其约束"。MIT 的 Andrew Sutherland："我们要看收据。"arXiv 独立审计审查八月批次，被审主结果未发现实质性错误。

<svg viewBox="0 0 720 330" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="验证梯度：产出速度已超过一切检验">
  <defs>
    <marker id="arrV" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#868e96"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">验证梯度：产出速度已超过一切检验</text>
  <rect x="30" y="50" width="660" height="44" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="77" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#1864ab">约 4000 个问题交给模型</text>
  <rect x="180" y="106" width="360" height="44" rx="8" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="133" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#2b8a3e">372 个成果家族发布（约 18% 命中率）</text>
  <rect x="255" y="162" width="210" height="44" rx="8" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="189" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#e67700">162 篇带机器验算证明</text>
  <rect x="315" y="218" width="90" height="44" rx="8" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="245" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#a61e4d">人工审稿</text>
  <line x1="360" y1="94" x2="360" y2="104" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="150" x2="360" y2="160" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="206" x2="360" y2="216" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <text x="360" y="292" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">每一层都比上一层更窄。人工审稿是最紧的瓶颈——</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">Lean 形式化是唯一具有机器级带宽的检验通道。</text>
</svg>
*图 2：验证梯度——产出随算力扩展，检验仍随人工扩展；Lean 形式化是唯一具有机器级带宽的检验。*

## 新的稀缺资源

真正该改变看法的与任何定理无关：README 最重要的一句是关于饱和的——基准死了，前沿移到开放问题上。测试集无法区分强弱时，唯一的考试就是没人答出过的问题。瓶颈翻转无人算到：稀缺资源不再是生产候选结果——一个智能体每份 3 小时产出 372 个家族；稀缺的是消化它们。没有审稿流水线能一周读完 722 篇手稿。所以 Lean 形式化、版本化发布、逐篇 BibTeX 不是点缀，而是"实验室写论文"时代的出版基础设施。

OpenAI 也承认在"探索社区托管的仓库"：一家公司的仓库装不下机器数学的未来。领域需要不属于任何实验室的共享验证基础设施——形式化库、验算服务、审稿规范。722 篇手稿只是演示，它们倒逼出的基础设施才是真正的突破。

最后说句实话：82% 永远看不到。仓库只有过线的；做砸的题目也是科学，标出了机器前沿的真实边界。实验室公开失败前，每次发布都是一部高光集锦。

留给读者的问题：如果未解的数学如今就是前沿基准，而应考的模型都是私有的，验证流水线该归谁——"机器生成、机器验算、人类没读过"还要多久才会成为数学进步的常态单位？

---

*资料来源：[openai/math 仓库](https://github.com/openai/math)；[仓库总览](https://raw.githubusercontent.com/openai/math/main/overview.tex)；高等研究院咨询组建议；《科学美国人》；arXiv 独立审计。*
