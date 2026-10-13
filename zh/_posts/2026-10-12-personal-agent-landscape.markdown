---
lng_pair: id_20261012_personal-agent-landscape
title: "个人智能体大爆发：2026 全景与展望"
author: OpenSI-Labs
category: research
tags: [个人智能体, AI应用, 协议标准, 创投, 行业展望]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-personal-agent-landscape.png
meta_description: "七周之内，Meta、OpenAI、Google、腾讯、苹果全员下场做个人智能体；Poppy 协议草案发布；OpenClaw 39 万 star；单笔融资 10 亿美元。一篇总览：大厂、协议、爆品、资本、学术与展望。"
---

七周。从 xAI 的 Grok Bot（8 月）到 Meta Muse（9 月 8 日）、OpenAI Dots（9 月 29 日）、Google Gemini Agent（10 月 8 日）——全球大厂在不到两个月里全员下场，发布的都是同一个东西：**7×24 小时替你干活的个人智能体**。竞争已经从"谁的 demo 炫"变成了"谁能进你的生活"。这篇文章把过去一年的 Personal Agent 版图扫一遍：大厂、协议、爆品、资本、学术，最后给学术界、产业界、创业者、个人和投资人各留方向。

## 大厂混战

**Meta Muse**（9 月 8 日上线）是最激进的消费者产品：给目标、它出计划，自己开浏览器、用你授权的服务，App 关了它还在云端干活。跑在一个叫 Muse Secure VM 的隔离沙箱里（Ubuntu，2 核 8G），另有一个 Sentinel 智能体专门盯着它的上网行为，密码和支付凭证碰都不让碰。免费版 + 每月 20/100 美元两档付费，独立 App 和 WhatsApp 双入口。第一周 90 万下载、美区 App Store 第一，10 月初号称占了智能体互联网流量的 40%。9 月 29 日加了小企业版，10 月 7 日微软宣布原生 Windows 版——有意思的是，智能体 workloads 把服务器 CPU 需求又拉起来了，CPU:GPU 配比 4:1 到 40:1，AMD EPYC 间接受益。

**OpenAI Dots**（9 月 29 日 DevDay）长在 ChatGPT 里：每个 Dot 有自己的云电脑和浏览器，接 4000+ 应用，跨 ChatGPT/Slack/Teams 干活，能排定时任务，还会学你的偏好。安全上做了个漂亮的先例：发布前因安全测试发现欺骗行为，**直接撤掉了 GPT-6.1 Astra**——公开的安全门槛。Dots 团队版在路上，多 Dot 协作还没 GA。

**Google 两线作战**：5 月 I/O 的 Gemini Spark（消费者，有自己的 Gmail 地址，能收发邮件，基于 Antigravity 框架）；10 月 8 日的企业版 **Gemini Agent** 更狠——"一个统一的工作智能体"，自动把任务路由给最合适的模型（**今天就能调 Gemini 和 Claude**，OpenAI 和开源模型随后），还能生成带独立邮箱、日历、Drive 和通讯录条目的常驻"同事智能体"。治理上配了 Agent Sandbox、Agent Gateway 策略执行和花费用上限。北美先行，10 月底 GA。

**苹果** 6 月重建了 Siri（Personal Context + 屏幕感知 + 视觉智能），模型是花每年约 10 亿美元向 Google 买技术蒸馏来的——库克嘴上说是"纯苹果技术"。欧盟和中国首发被排除在外。

**微软**的 Copilot Autopilot（企业数字队友，内测中）、**xAI** 的 Grok Bot（8 月，SuperGrok 每月 30 美元，持久云端伴侣）、**Anthropic** 的 Claude Cowork（1 月，桌面"工作模式" + 手机 Dispatch）——三家都没掉队，只是声量被前四家盖住了。

**中国这边**：腾讯在憋 Yuanbao Assistant 独立 App（长任务 + 长期个人记忆，多业务线同时在做），Yuanbao 本体今年已切换到自研 Hunyuan Hy3/Hy4，10 月 10 日还上了鸿蒙版"专家模式"。但真正的王炸是微信——13 亿用户的超级入口里嵌支付、社交、商业，智能体一旦进去就是降维打击。字节的豆包据传在测"小豆"个人助理 App（9 月 30 日传闻），蚂蚁的灵光在测"My Life"（10 月 10 日）。中国战场的开局哨还没吹，但所有人都在热身。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="个人智能体技术栈：人、个人智能体、智能体网络、应用、现实世界">
  <text x="360" y="32" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="18" font-weight="700" fill="#212529">界面正在翻转：人不再直接点应用</text>
  <rect x="270" y="60" width="180" height="52" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="92" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="16" font-weight="700" fill="#1864ab">人</text>
  <line x1="360" y1="112" x2="360" y2="132" stroke="#495057" stroke-width="2"/>
  <polygon points="360,142 352,130 368,130" fill="#495057"/>
  <rect x="230" y="142" width="260" height="60" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2.5"/>
  <text x="360" y="168" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="16" font-weight="700" fill="#e67700">个人智能体</text>
  <text x="360" y="190" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#495057">7×24 · 有记忆 · 能行动</text>
  <line x1="360" y1="202" x2="360" y2="222" stroke="#495057" stroke-width="2"/>
  <polygon points="360,232 352,220 368,220" fill="#495057"/>
  <rect x="250" y="232" width="220" height="52" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="15" font-weight="700" fill="#5f3dc4">智能体网络</text>
  <line x1="360" y1="284" x2="360" y2="304" stroke="#495057" stroke-width="2"/>
  <polygon points="360,314 352,302 368,302" fill="#495057"/>
  <rect x="270" y="314" width="180" height="44" rx="10" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="360" y="342" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="15" fill="#495057">应用 · 现实世界</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">图注：新的调用栈。应用退化成智能体的"手"，人才是目的。</text>
</svg>

## 协议之争：Poppy 来了

10 月 9 日，Sierra（Bret Taylor 公司）联合 Meta 发布了 **Personal Agent Protocol（PAP，昵称 Poppy）0.1 草案**——个人智能体和网站打交道的握手规范，Apache 2.0 开源。五个构件：

1. **发现**：企业在 `/.well-known/poppy.json` 声明"智能体可以怎么跟我玩"、登录方式和允许的动作；
2. **会话**：智能体以访客身份开 session，永远实名（签名请求）；
3. **登录**：用户在企业自己的页面 OAuth 登录（DPoP 绑定 token + PKCE），智能体拿 scope 受限的 token（`poppy:read`/`poppy:write`/自定义）；
4. **跨渠道同一会话**：同一个 token 横跨 API、网站和企业智能体；
5. **干活**：企业自选网站、API（OpenAPI/MCP）或自家智能体。

隐私设计上，登录前企业只能看到一个按企业隔离的匿名 ID。**支付被明确列为"未定事项"**——0.1 版故意没碰。35 家设计伙伴（含 OpenAI、Visa、Stripe、沃尔玛、Cloudflare），Python/TypeScript SDK 发布当天上架 PyPI，一个月内开设计研讨会。

有意思的格局：工具层有 MCP（Anthropic 2024 年 11 月发布，2025 年 12 月捐给 Linux 基金会，月下载 9700 万，企业 server 破万家），智能体间有 A2A（Google 2025 年 4 月，v1.0 今年 4 月，8 月 20 日并入同一基金会）。两层标准刚在"同一个屋檐"下团聚，**发现层就在同一周分叉了**：MCP 指向 `ai-catalog.json`（格式还在 A2A 项目里讨论），Poppy 坚持 `poppy.json`。Poppy 的赌注是：*个人*智能体的握手和*企业*智能体不一样——用户实名、匿名 ID、scope 令牌，控制权永远在客户手里。如果 35 家伙伴真落地，Poppy 就是消费者互联网对 MCP/A2A 企业栈的镜像。旁边还有 UCP（Universal Commerce Protocol，管目录/购物车/结算的商业操作层）和 ACP（AGNTCY  collective 的 REST 原生协议）——协议丛林正在形成，收敛还是分裂，看明年。

<svg viewBox="0 0 720 380" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="智能体协议版图：MCP工具层、A2A智能体间层、Poppy个人握手层">
  <text x="360" y="32" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="18" font-weight="700" fill="#212529">协议三层，唯独"前门"有两个</text>
  <rect x="60" y="70" width="180" height="90" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="150" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="16" font-weight="700" fill="#1864ab">MCP</text>
  <text x="150" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#495057">智能体 ↔ 工具</text>
  <text x="150" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">Anthropic → Linux 基金会</text>
  <rect x="270" y="70" width="180" height="90" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="16" font-weight="700" fill="#2b8a3e">A2A</text>
  <text x="360" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#495057">智能体 ↔ 智能体</text>
  <text x="360" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">Google → Linux 基金会</text>
  <rect x="480" y="70" width="180" height="90" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2.5"/>
  <text x="570" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="16" font-weight="700" fill="#e67700">Poppy</text>
  <text x="570" y="124" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#495057">个人 ↔ 企业</text>
  <text x="570" y="144" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">Sierra + Meta · 10 月草案</text>
  <text x="360" y="200" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="15" font-weight="700" fill="#c92a2a">发现层分叉 ⚠</text>
  <rect x="120" y="220" width="200" height="56" rx="8" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="220" y="244" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#495057">/.well-known/ai-catalog.json</text>
  <text x="220" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">MCP 路线</text>
  <rect x="400" y="220" width="200" height="56" rx="8" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="500" y="244" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#495057">/.well-known/poppy.json</text>
  <text x="500" y="264" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">Poppy 路线</text>
  <text x="360" y="316" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#212529">同一个问题——智能体如何发现企业提供了什么——两个答案。</text>
  <text x="360" y="340" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="14" fill="#212529">看它们收敛还是分裂。</text>
  <text x="360" y="368" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI','PingFang SC','Microsoft YaHei',sans-serif" font-size="13" fill="#868e96">图注：三层各有其主，唯独发现层同题异解。</text>
</svg>

## 爆品：开源赢了第一局

**OpenClaw** 是今年最现象级的开源项目：WhatsApp/Telegram 里指挥，本地网关连 Gmail、日历、GitHub、浏览器，MIT 协议。2025 年 11 月以 Clawdbot 之名发布，72 小时 10 万 star，2026 年 3 月 26.4 万 star **超过 React**，10 月约 39 万——GitHub 历史上增长最快的仓库。作者 Peter Steinberger 2 月加入 OpenAI，项目转交独立基金会。在中国尤其火：腾讯总部门口排队、付费安装服务。阴暗面：2 月爆出 CVE-2026-25253（CVSS 9.8，一句话 RCE）——智能体安全的警示牌，也是"用户自己搭的智能体谁来负责"的第一课。

**Manus 2.0 + Cue**（9 月 28 日）："卖电脑，不卖应用"——把智能体包装成一台永远在线的云电脑。

**Instinct**（8 月，邀请求制）：每人一个电话号码 + 一台云电脑，能替你打电话，还能和朋友的智能体组"信任人网络"——智能体之间的社交，第一次有了产品形态。

**Nous Hermes**：开源，2400 万+ clone，占全球 AI token 的 2.5%，正在推企业版。

**ElevenLabs** 语音智能体：每周 1500 万+ 对话，是 2 月的 3 倍，90+ 语言。

**Lindy**（Slack 原生队友）、**Granola**（会议记录，靠"不打扰"赢了口碑）、**Poke/Buzz**（智能体之间互相委托的网络）——长尾里全是缝隙机会。

## 资本：只投"能动手"的

- **Manus：5 亿美元以上，估值约 40 亿美元**（10 月 8 日）——博裕 + IDG 领投，腾讯参投。戏剧性背景：Meta 20 亿美元收购被北京否决，Manus 9 月 1 日恢复独立。这轮融资本身就是地缘政治案例。
- **Instinct：10 亿美元 C 轮，估值 100 亿美元**（9 月 28 日）——红杉、Benchmark、Coatue；一个月前估值才 25 亿美元，今年消费者智能体最大的一次 markup。
- **Nous Research：9000 万美元 B 轮，估值 15 亿美元**（10 月 7 日）——Robot Ventures 领投，英伟达、三星、USV、Menlo 参投；年中 ARR 约 3600 万美元，目标年底破 1 亿美元。
- **ElevenLabs：3 亿美元员工转售，估值 220 亿美元**（9 月 30 日）——半年翻倍，Wellington 和 T. Rowe Price 接盘。

趋势很清楚：资本只投"能动手的"消费者智能体，不投聊天框；地缘政治（Manus/北京）第一次成为估值的一阶变量。

## 学术：地基在打桩

**个性化**：PAHF（arXiv:2602.16173）用显式个人记忆 + 行动前澄清/记忆 grounded 执行/行动后反馈的三段循环，让智能体持续跟上用户偏好的漂移。

**持久智能体**：115 天自观察研究（arXiv:2605.26870）发现 token 画像里缓存读占 82.9%——经济单位正从"按 token 计费"转向"按成品计费"，这对所有做智能体 infra 的人都是定价信号。

**人格工程**：在"温暖×支配"二维上参数化谈判智能体的人格（arXiv:2605.20554）；人格会随"人生事件"演化，但当前智能体只模拟了人类人格动态的均值、没模拟出形状（arXiv:2608.06485）。

**元推理**：Meta 的 Thinking Before Thinking（arXiv:2609.38147）把"控制"本身做成扩展轴线——智能体越自主，控制器越重要。

**评估前沿**：SWE-bench Pro（1865 题）、Terminal-Bench 2.x（最高分 92.8%，接近饱和）、τ-bench（交互下的可靠性）。2026 年最重要的一课：**脚手架 ≈ 模型本身**——同一模型换 harness 能差 17 道题；benchmark 是消耗品，保质期越来越短。

## 展望：四条线，五类人的机会

**1. 界面翻转。** 人 → 智能体 →（智能体网络）→ 应用 → 现实世界。应用退化成智能体的"手"。
- **创业者**：别再做"更好的 App"，做智能体调用的第一批"手"——垂直场景的执行器（订票、跑腿、报税、盯盘）比聊天框值钱。Poppy 的 `poppy.json` 就是你的上架说明书，先写好它。
- **学术界**：调用栈变了，HCI 的经典问题全要重做一遍——人如何监督一个 7×24 干活的代理？

**2. 所有权分裂。** 大厂智能体（模型、运行、记忆全归厂商）vs 用户所有（OpenClaw/Hermes：运行和记忆归用户，模型可换）。39 万 star 和 2400 万 clone 是用户用脚投票。数据可携带、记忆所有权是主战场。
- **个人用户**：现在就该问——我的智能体记忆归谁？能带走吗？选产品时把"导出记忆"当硬指标。
- **创业者**：做"记忆银行"——帮用户在厂商之间搬运智能体记忆，收过路费。

**3. 信任是门槛，不是能力。** OpenAI 撤模型、OpenClaw 爆 RCE、Meta 搞 Sentinel——2026 的伤疤全是信任问题。权限模型、可审计、可撤销才是下一个 10 倍的钥匙。
- **做 infra 的**：Poppy 没解决的支付、审计、撤销，每一个都是创业题目。特别是"智能体花钱"的 escrow 和限额——没人做好。
- **学术界**：智能体安全需要新的形式化工具，CVE-2026-25253 只是开始。

**4. 商业模式未定。** 订阅（Muse 每月 20–100 美元）、交易抽成、企业席位——没人证明"替你睡觉时干活"的 unit economics。"按成品计费"（persistent agent 研究的结论）可能是答案。
- **投资人**：盯着净留存和"睡后任务完成率"，别只看 DAU。问创始人三个问题：记忆归谁？花钱谁批？出事谁赔？

**讨论：** 当你的智能体 7×24 替你活着，"你"和"它"的边界在哪？第一批把记忆所有权写进用户协议的公司，会是下一代的赢家吗？
