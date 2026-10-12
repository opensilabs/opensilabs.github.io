---
lng_pair: id_20261012_sakana-mass-self-improvement
title: "MASS：把自己组织成研究团队的 27B 模型"
author: OpenSI-Labs
category: research
tags: [递归自我改进, 多智能体系统, Sakana AI, 自监督, 工作流优化]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-sakana-mass-self-improvement.png
meta_description: "Sakana AI 的 MASS 让一个 27B 模型在自我改进循环中同时扮演求解者、优化器和评估者——并发现瓶颈在优化器，而不在裁判。"
---

前沿 AI 的"监督困境"听起来像哲学，落到工程里却很实在：模型已是合格的科学家，你想让它更好。开放式研究任务无标准答案、无单元测试，也没有人类能可靠区分"好"与"卓越"——它从何学习？在我们最希望 AI 突破的任务上，模型正接近人类可评估的边界。监督瓶颈已不是假想。

Sakana AI 本周末与 UC Berkeley 发表的 MASS（Multi-Agent Self-Supervision，[论文](https://arxiv.org/abs/2610.12176)、[官方博客](https://pub.sakana.ai/mass/)）给出答案：既然无人能从外部监督模型，就让它把自己组织成团队，从自己团队的协作方式里学习。

机制一句话讲清：一个 27B 共享模型（Qwen3.6-27B，开源）在它自己运行的循环里身兼三职——任务求解者、工作流优化器、评估者。这就是*同质*递归自我改进：单实例模型在同质循环里难以批判并改进自己的复杂推理，而多智能体拓扑更擅长此道——于是模型用自己的副本绕过自身局限。

内循环在权重冻结下搜索"更好的协作方式"。模型先写工作流：把研究任务分给虚拟子智能体的计划——各角色指令、交付合同、调用顺序。执行器运行、评估者打分、优化器修订。进化式搜索加结构护栏。

<figure>
<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<defs><marker id="marrow" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#3366cc"/></marker></defs>
<rect x="230" y="10" width="180" height="52" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="320" y="32" font-size="14" font-weight="bold" text-anchor="middle">共享模型</text>
<text x="320" y="50" font-size="12" text-anchor="middle">Qwen3.6-27B，开源权重</text>
<rect x="40" y="110" width="270" height="150" rx="12" fill="#f7f9ff" stroke="#3366cc" stroke-width="2"/>
<text x="175" y="134" font-size="14" font-weight="bold" text-anchor="middle">内循环：工作流搜索</text>
<text x="175" y="156" font-size="12" text-anchor="middle">工作流 = 角色 · 指令 ·</text>
<text x="175" y="172" font-size="12" text-anchor="middle">合同 · 调用顺序</text>
<text x="175" y="196" font-size="12" text-anchor="middle">执行 → 对照冠军评估 →</text>
<text x="175" y="212" font-size="12" text-anchor="middle">优化器修订工作流</text>
<text x="175" y="236" font-size="12" font-style="italic" text-anchor="middle">权重保持冻结</text>
<rect x="330" y="110" width="270" height="150" rx="12" fill="#fff8ee" stroke="#cc8833" stroke-width="2"/>
<text x="465" y="134" font-size="14" font-weight="bold" text-anchor="middle">外循环：蒸馏</text>
<text x="465" y="156" font-size="12" text-anchor="middle">冠军工作流每任务运行 18 次</text>
<text x="465" y="172" font-size="12" text-anchor="middle">Bradley-Terry 自排序；</text>
<text x="465" y="188" font-size="12" text-anchor="middle">保留最优的 16 条轨迹</text>
<text x="465" y="212" font-size="12" text-anchor="middle">剥离脚手架 → LoRA 微调</text>
<text x="465" y="236" font-size="12" font-style="italic" text-anchor="middle">权重在这里改变</text>
<line x1="250" y1="62" x2="178" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="390" y1="62" x2="462" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="310" y1="185" x2="328" y2="185" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<text x="292" y="178" font-size="11" text-anchor="middle">冠军</text>
<line x1="606" y1="160" x2="606" y2="36" stroke="#cc8833" stroke-width="2"/>
<line x1="606" y1="36" x2="412" y2="36" stroke="#cc8833" stroke-width="2" marker-end="url(#marrow)"/>
<text x="508" y="28" font-size="11" text-anchor="middle">更新后的模型重掌三个角色</text>
</svg>
<figcaption>内循环寻找更好的协作，外循环把最优协作蒸馏回权重。</figcaption>
</figure>

外循环是循环"喂养自己"之处：冠军工作流每任务跑 18 次，自排序后只留最优 16 条轨迹，剥离脚手架再用 LoRA 微调。更新后的模型重掌三职——循环再来。两轮后，四个研究基准的单位输出 token 得分达基线 1.2–1.6 倍（MLR-Bench 1.60×、DSBench 1.35×、AstaBench 1.28×、ScienceAgentBench 1.20×），对基线的胜率从 53.9% 升至 69.9%。训练信号也更密：用多智能体轨迹的学生只用 69% 的监督 token（28.8M 对 42M）就达到相当胜率。

但多数报道会略过诚实的失败：SWE-bench Verified 和 Terminal-Bench 2.0 上，同一套系统*退步*到基线的 0.94× 和 0.96×。MASS 没有让模型全面变强——它成了更好的研究者，却写代码变差了。

<figure>
<svg viewBox="0 0 640 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<line x1="273" y1="20" x2="273" y2="240" stroke="#999" stroke-width="1.5" stroke-dasharray="6,4"/>
<text x="273" y="256" font-size="11" text-anchor="middle" fill="#666">基线 = 1.0×</text>
<text x="170" y="52" font-size="12" text-anchor="end">MLR-Bench</text>
<rect x="180" y="38" width="280" height="22" rx="4" fill="#3366cc"/><text x="468" y="54" font-size="12">1.60×</text>
<text x="170" y="92" font-size="12" text-anchor="end">DSBench</text>
<rect x="180" y="78" width="165" height="22" rx="4" fill="#3366cc"/><text x="353" y="94" font-size="12">1.35×</text>
<text x="170" y="132" font-size="12" text-anchor="end">AstaBench</text>
<rect x="180" y="118" width="133" height="22" rx="4" fill="#3366cc"/><text x="321" y="134" font-size="12">1.28×</text>
<text x="170" y="172" font-size="12" text-anchor="end">ScienceAgentBench</text>
<rect x="180" y="158" width="95" height="22" rx="4" fill="#3366cc"/><text x="283" y="174" font-size="12">1.20×</text>
<text x="170" y="212" font-size="12" text-anchor="end">SWE-bench Verified</text>
<rect x="180" y="198" width="66" height="22" rx="4" fill="#cc3333"/><text x="254" y="214" font-size="12">0.94×</text>
<text x="320" y="14" font-size="13" font-weight="bold" text-anchor="middle">两轮 MASS 循环后，单位输出 token 得分相对基线</text>
</svg>
<figcaption>改进有方向：模型成了更好的研究者，写代码却退步了。</figcaption>
</figure>

这正是真正的故事。递归自我改进常被讲成水涨船高——模型全方位变强。MASS 更像学徒制：模型朝着循环奖励的方向特化，在相邻技能上付费。一个自我改进的研究者慢慢忘了怎么写代码，不是悖论，而是每个专家的标准交易。如果 RSI 规模化，未来可能不是无所不能的通用模型，而是自我改进的专家生态——各自在自己的奖励盆地出类拔萃，盆地之外略逊一筹。

第二个意外击中另一种流行担忧：大家以为自评分循环最危险的是*评估者*——自己判卷必然放水。消融实验却发现：只升级评估者几乎无效，升级*优化器*才动了结果。自我改进循环里，生成好候选比评判更重要——瓶颈在提案者，不在裁判。给 RSI 建造者的准则：投资搜索，而非记分牌。

作者自曝的梦魇最值得尊敬：同一模型既生产、又评判、又拿结果训练自己时，共享盲区可能被"生产、误认为改进、再写进下一代模型"——他们称之为递归自我改进的阿喀琉斯之踵。注意其中的认识论信号：为了*衡量*进步，他们不得不请外部裁判（GPT-5.5、Claude Opus 4.8），且其判决绝不进入循环——真正封闭的循环无从知道自己是否在进步。MASS 没有弥合裂缝，只在裂缝内造出了最好的机器。

代码与论文皆公开。MASS 不是智能大爆炸，而是更稀罕的东西：能运转、能量化、且诚实报告"哪里变强、哪里变弱、哪个部件拖后腿"的自我改进循环。

**讨论：** 如果递归自我改进必然让模型朝着循环奖励的任务特化，谁来决定哪些任务值得拥有自我改进循环——我们愿意让模型丢掉哪些技能？
