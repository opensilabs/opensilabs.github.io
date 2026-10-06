---
lng_pair: id_20261006_gemini-4-argon
title: "不会累的模型"
author: OpenSI-Labs
category: models
tags: [Gemini, 长上下文, 智能体, Google DeepMind]
date: 2026-10-06 00:30:00 -0700
img: /assets/img/posts/2026-10-06-gemini-4-argon.png
meta_description: "Gemini 4 Argon 以一百万 token 输出上限和 Long Decode Continuation，把智能体的前沿从智商之争改写为耐力之争。"
---
# 不会累的模型

9 月 30 日，Google DeepMind 发布了七个月来第一款高于 Flash 级别的 Gemini。高级副总裁兼 Google 首席 AI 架构师 Koray Kavukcuoglu 宣布了 [Gemini 4 Argon](https://datanorth.ai/news/google-releases-gemini-4-argon)，标题数字不是某个评测分数，而是：一百万。输出上限一百万 token——从此前所有 Gemini 的 6.4 万起跳，业界首例。输入上下文同样达到一百万，但这次的新闻在输出一侧。

过去两年，整个行业都在比拼模型能"读"多少。Argon 是第一款围绕模型能"说"多少打造的旗舰型号，因为在智能体实战中，杀死任务的永远是输出上限。

语言模型并不像人那样推理：它靠一个接一个地生成 token 来推理，每一个 token 都是下一个 token 的立足点。这不是比喻，是架构本身。思维链、工具调用、先规划后执行——全部都要经过同一条线性生成流水线。

想想长程智能体真正的工作：钻研代码库，制定计划，改二十个文件，跑测试，读报错，再修订。每一步都要写出来。旧的 6.4 万上限意味着这个过程有一个硬性死线。撞上限时请求不是优雅暂停，而是整个中间状态直接蒸发。重试只能从头冷启动。模型已经推导出的不变量——"支付服务对 429 会重试、对 403 不会""配置开关只在启动时读一次"——必须重新推导，而有时候它推导不出来了。计划在沉默中腐烂。

工程师们用工程手段绕过去：任务分块、重启、把状态摘要塞进新的 prompt。每一个补丁都是在亲口承认：模型自己没法把一个想法想完。Google 的数据暗示了代价——256K 到 1M 长文档的 GraphWalks 评测 Argon 拿到 84.2%，正因为超长文档加超长推理终于能塞进同一次连续生成。

Google 交付的修复是基础设施，不是智能：**Long Decode Continuation**。超长响应可以暂停，并在后续 API 调用中续写，不再超时。Artificial Analysis 用这套机制独立验证了整整一百万的输出上限。生成从停下的地方继续，而不是从零重启。听起来像水管工的活——因为瓶颈本来就在水管上。

这把智能体的真正前沿换了个位置。我们一直在给模型做智商测试：这里多一分，那里登个榜。Argon 指出真正的稀缺资源是耐力：在数小时的生成中保持思路不丢、不散的能力。跑到 32 公里就忘了路线的马拉松选手，输给跑得慢但不迷路的选手。评测奖励跑者，生产环境奖励完赛者。

数字很强但不横扫一切：Vals Index 68.9%、DeepSWE v1.1 77.9%、Zapier AutomationBench 51.3%、LVBench 91.7%。发布第二天 Arena.ai 文本榜第一（1525，高级别），代码 WebDev 榜第八（1679）。但 Google 也公布了自己的败绩，值得肯定：FrontierSWE v2 上 GPT-6 Astra 65.5% 对 Argon 55.0%；Terminal-bench 4.0 是 Claude Opus 5.5 的 66.4%；Terminal-Bench Science 又是 Astra 的 68.1%。Vending-Bench 2 上 Argon 第三，$13,718 ± $3,100，排在 Astra 和 GPT-6 Sol 之后。没有横扫——而这恰恰说明，这次发布的赌注在别处。

实战派的反应最有意思。Hacker News 发布帖冲上 853 分，争论焦点不是评测，而是准入。Argon 不公开：第一批使用者是经由 Google Fairwind 计划的受审查网络防御者（见 [CyberKendra 报道](https://www.cyberkendra.com/2026/10/google-unveils-gemini-4-argon-first-for-cyber-defenders.html)），并且在进入付费 API 和 Google AI Ultra 订阅之前，还要经过美国政府的自愿预发布审查。时间未定。

最犀利的从业者评论一针见血："一百万输出上限对长程智能体的意义，可能远大于评测榜上又涨了零点几个点。"评测衡量模型知道什么，输出上限衡量模型能做什么——而智能体的存在意义就是做事。

还有个更硬的角度，Google 心知肚明：把最强的长程模型先交给防御者，这是在宣布前沿模型已经是战略基础设施，不是消费品。能对一张网络发动数小时连贯攻击的模型，同样能对同一张网络进行数小时连贯防守。当被放大的是耐力，双重用途就不再是抽象议题：谁先拿到不知疲倦的干活者，谁就先拿到优势。Google 选择了防御者。定价讲了另一半故事：首发价每百万 token 输入输出 $2/$10，缓存输入每百万仅 $0.10；之后涨到 $4/$20，与 Claude Opus 5.5 看齐。这么便宜的耐力，会重排从 SOC 运营到法律尽调的一切成本账。

改变有两点。第一，智能体设计的单位从单次请求变成了会话。Long Decode Continuation 让"续写"成为一等公民，智能体可以做成真正长期存活的进程，而不是脆弱重启拼起来的链条。第二，竞争轴心移动。当每家前沿模型都读一百万 token，差别不再是谁看到的上下文最多，而是谁的计划hold 住最久。

[ghacks](https://www.ghacks.net/2026/10/02/google-launches-gemini-4-argon-with-a-1-million-token-output-limit-starting-with-cyber-defenders/) 与 [ExplainX](https://explainx.ai/blog/gemini-4-argon-launch-benchmarks-pricing-2026) 都梳理了完整参数，与 Google 官方材料对得上。留下的开放问题是评测回答不了的：不间断的生成究竟能把智能体的有效工作半径推多远——在 token 预算耗尽之前，连贯性本身会在哪一公里先崩？

Argon 没有回答这个问题。它第一次让我们问得出来。

**讨论：如果耐力才是真正的前沿，哪个评测骗我们最狠？一场诚实的耐力测试应该长什么样？**
