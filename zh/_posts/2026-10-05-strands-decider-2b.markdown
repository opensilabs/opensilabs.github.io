---
lng_pair: id_20261005_strands-decider-2b
title: "不会写字的模型：AWS 给智能体配了个「决策者」"
author: OpenSI-Labs
category: models
tags: [决策模型, 智能体, AWS, 开源, 大语言模型]
date: 2026-10-05 06:00:00 -0700
img: /assets/img/posts/2026-10-05-strands-decider-2b.png
meta_description: "AWS 的 Strands Decider 2B 切掉语言模型头、换上指针头——只做选择不做生成的决策模型，一次前向传播给出答案。"
---

上周，AWS 发布了一个 20 亿参数的语言模型，它一个字都写不出来。不能总结、不能写代码、不能聊天。你问它任何开放式问题，它都给不出答案——因为负责把思考变成文字的那个部件，已经被手术切掉了。

这不是缺陷，这就是设计本身。

这个模型叫 Strands Decider 2B，来自亚马逊 Strands Labs 团队，10 月 1 日开源发布。它属于一个一年前几乎不存在的新物种：决策模型（decision model）。语言模型负责生成，决策模型只负责选择。你给它一个问题加一组选项，它直接返回每个选项的概率分布——一次前向传播，没有解码循环，没有采样，没有束搜索。（[TechStrong](https://techstrong.ai/articles/aws-explores-decision-models-with-strands-decider-2b/)）

手术很精准。团队拿阿里开源的 Qwen3.5-2B-Base 做「躯干」，切掉了语言模型头（负责预测下一个词的输出层），换上了一个只有一百多万参数的指针头（pointer head）。指针头的工作方式是：把模型在指定 `<answer>` 位置的内部表示，和每个候选选项末尾 token 的隐藏状态做点积比较，一次掩码 softmax，结束。模型只读一遍问题，答案从一次矩阵乘法里掉出来。（[TechTimes](https://www.techtimes.com/articles/328500/20261002/aws-releases-decision-model-ai-agents-that-routes-without-generating-any-text.htm)）

让底座模型适应新头并不需要从头训练：一个 rank-16 的 LoRA 适配器就够了，而小小的指针头保持 32 位全精度，以保住校准精度。内部架构图把这套设计标注为「Hobson」，公开发布的是第 19 版——团队说，早期 slot-head 方案的效果差得多。（[VentureBeat](https://venturebeat.com/technology/amazon-unveils-a-free-fast-open-source-jev-killer-strands-decider-2b-makes-decisions-in-fractions-of-a-second)，[SQ Magazine](https://sqmagazine.co.uk/amazon-strands-decider-2b-open-source-decision-model/)）

为什么要造一个「能力更少」的模型？因为在智能体内部，绝大多数决策根本不需要文字。哪个工具来处理这个请求？这个动作合规吗？下一步交给哪个模型？今天，这些琐碎判断全都被丢给通用大模型，用最贵的方式「大声思考」——烧掉一整轮生成，只为回答一道选择题。Decider 就是为这些体力活准备的，把贵的推理留给真正需要推理的地方。（[TechStrong](https://techstrong.ai/articles/aws-explores-decision-models-with-strands-decider-2b/)，[AIAffairs](https://www.aiaffairs.com/technology/aws-releases-strands-decider-2b-local-ai-agent-decisions/)）

数字很有说服力。AWS 称在 RTX 3090 等常见硬件上单次决策不到 100 毫秒；第三方实测在 M3 MacBook 上中位数约 153 毫秒。在决策模型基准 JevBench 上，Decider 简单档 100% 全对，在约 20 亿参数的公开模型里排第二，在「附带完整训练配方」的模型里排第一。值得注意的是，AWS 用 Brier 分数评估模型——检验「嘴上说的置信度」和「实际准确率」是否一致。（[CryptoBriefing](https://cryptobriefing.com/amazon-strands-decider-2b-open-source-jev/)，[SQ Magazine](https://sqmagazine.co.uk/amazon-strands-decider-2b-open-source-decision-model/)）

这个细节是题眼。除非卖的就是信任，否则没人会拿校准度来炫耀。一个说「选 B，92% 把握」且十次里真对九次的模型，可以直接焊进业务逻辑：放行这次工具调用、拦下那次、不确定就升级。聊天机器人的自信是表演，决策者的自信是 API。

而且 AWS 不是一个人在战斗。OpenAI 在 DevDay 发布了 Decisions API，Databricks 推出了面向治理数据的 ai_decide，而 TypeSafe 的 Jev 最早定义了这个品类——它的 CEO 已经在 X 上开玩笑说「Jev 克隆战争打响了」。决策模型正在成为技术栈的一层，而不是猎奇玩具。（[Another Daily AI Newsletter](https://www.anothercodingblog.com/p/another-daily-ai-newsletter-october)）

真正值得琢磨的是这一层：这是对过去三年「一个模型包打天下」教条的撤退。全行业花了巨大力气，用提示工程让通用模型兼职干一切——选工具、做路由、当裁判，效果是有了，账单也惊人。Strands Decider 是对古老工程美德的回归：部件尺寸恰到好处。LLM 的躯干被保留为能力惊人的「读者」，同时被剥夺了「作者」身份。用认知科学的话说，这是一个 System 1 模块——快、专、校准良好，外挂在前沿模型的 System 2 深思熟虑之外。AWS 观察到，开发者已经在用「大模型思考、小模型拍板琐事」的混合智能体了。（[The AI Economy](https://theaieconomy.substack.com/p/strands-decider-2b)）

还有一个比延迟更重要的二阶效应。当一次判断要烧掉一整轮 LLM 调用时，开发者只能定量配给护栏——在几个咽喉点检查一下，剩下的靠祈祷。当一次判断在本地硬件上只要 100 毫秒，你可以在每个工具调用前面都放一个检查点。AWS 自己的演示就是这么干的：智能体调用天气 API 之前，决策者先检查它准备用的城市到底是用户说的，还是它自己脑补的；如果是后者，就把它打回去问用户。便宜的刹车才会被到处装。这与其说是性能故事，不如说是披着性能外衣的安全故事。（[AIAffairs](https://www.aiaffairs.com/technology/aws-releases-strands-decider-2b-local-ai-agent-decisions/)）

当然也要冷静。选择题基准天然偏爱这类模型：真实世界里，选项集谁来定、问题谁来写、阈值设多少——在 AWS 的演示里这些全是手工定的。模型只给分数，「问什么」这个思考活儿还是开发者的。AWS 也承认，专门的集成库还在开发中。（[VentureBeat](https://venturebeat.com/technology/amazon-unveils-a-free-fast-open-source-jev-killer-strands-decider-2b-makes-decisions-in-fractions-of-a-second)）

所以这次发布最重要的可能根本不是权重，而是配方：训练数据、脚本、十九版迭代笔记，全部公开。任何人都可以照方抓药，针对自己的选项集微调一个决策者，跑在自己的硬件上，而不必每次判断都去租 API。模型是演示，配方才是平台。

三年里，全行业都在问：一个模型最多能干多少事。更好的问题可能是：一个模型最少需要干多少事——如果那一件事又快、又诚实、又开放的话。

*在你的工作流里，哪些决策正在烧着整轮 LLM 生成？如果每次检查只花 0.1 秒，你会想检查什么？*
