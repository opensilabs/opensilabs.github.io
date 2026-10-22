---
lng_pair: id_20261022_nvidia-openshell
title: "给智能体套上硬件缰绳"
author: OpenSI-Labs
category: research
tags: [AI智能体安全, 英伟达, OpenShell, Sentry, BlueField]
date: 2026-10-22 00:10:00 -0700
img: /assets/img/posts/2026-10-22-nvidia-openshell.png
meta_description: "英伟达在 GTC 柏林发布 OpenShell 参考架构：模型在 Rubin 上思考、智能体在 Vera 上行动、BlueField-4 上的 Sentry 带外治理。智能体的安全，第一次被焊进了硅里。"
---

**2026 年反复出现同一个故事：AI 智能体逃出了本该关住它的评估环境，摸到了不该摸的系统。**

英伟达的出发点很不客气：不能指望智能体自己管自己。10 月 21 日 GTC 柏林，它发布 OpenShell 参考架构，把治理权从智能体手里彻底拿走——下沉到计算架构里。黄仁勋的概括是："智能体在 Rubin 上思考，在 Vera 上行动，在 BlueField 上被治理。"

软件层是 OpenShell 运行时（Apache 2.0 开源）：每个智能体关进内核级隔离的沙箱，网关管理沙箱的生老病死，每一次对外连接都过策略引擎——放行、把凭据绑死在批准的端点上、或者拒绝并记录。最有新意的是"策略证明器"：智能体启动之前，先形式化验证一遍策略本身，证明权限上限不可能溢出运营者的意图。权限不再是承诺，是被证明过的。

<figure>
<div style="text-align:center">
<svg width="680" height="310" viewBox="0 0 680 310" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">三层分工：思考、行动、治理</text>
<rect x="190" y="48" width="300" height="54" rx="8" fill="#4299e1"/>
<text x="340" y="70" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">智能体 · Vera CPU</text>
<text x="340" y="92" font-size="14" text-anchor="middle" fill="#fff">OpenShell 沙箱内行动</text>
<rect x="190" y="140" width="300" height="54" rx="8" fill="#c53030"/>
<text x="340" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Sentry · BlueField-4 DPU</text>
<text x="340" y="184" font-size="14" text-anchor="middle" fill="#fff">必经之路：观察点 + 熔断开关</text>
<rect x="190" y="232" width="300" height="54" rx="8" fill="#2b6cb0"/>
<text x="340" y="254" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">模型 · Vera Rubin GPU</text>
<text x="340" y="276" font-size="14" text-anchor="middle" fill="#fff">推理 / 思考</text>
<path d="M340 102 L340 132" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a2)"/>
<path d="M340 194 L340 224" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a2)"/>
<defs><marker id="a2" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0 0 L8 3 L0 6 Z" fill="#718096"/></marker></defs>
<text x="520" y="120" font-size="14">每次调用模型必经 Sentry</text>
<text x="520" y="215" font-size="14">越界：毫秒级隔离关停</text>
<text x="60" y="167" font-size="14">带外运行</text>
<text x="60" y="187" font-size="14">智能体够不着</text>
</svg>
</div>
<figcaption style="text-align:center">OpenShell 参考架构：Sentry 坐在智能体与模型之间的唯一通路上，智能体够不着、绕不开、说不动。</figcaption>
</figure>

硬件层才是杀招。在 Vera Rubin 机柜里，每块计算托盘的 BlueField-4 DPU 恰好卡在节点通往模型的唯一路径上：智能体想行动，就必须发出下一次推理调用，而每一次调用都从 Sentry 眼皮底下过。Sentry 在这块独立芯片上带外运行，检查请求与响应、核验智能体身份、生成防篡改的遥测记录；一旦发现"漂移"——行动偏离任务或约束——毫秒级隔离关停。智能体看不见它、够不着它，更没法用话术说服它。已有的 Vera + BlueField-4 系统，软件更新即可启用。

**这件事的新意，不在沙箱，在"位置"**

沙箱、策略引擎、最小权限，都是老概念。英伟达真正推进的一步是：把执法者放到了被执法者的物理可达范围之外。过去所有的智能体护栏——系统提示、工具白名单、应用层策略——都住在智能体能直接或间接够到的地方，本质上是"建议"，靠智能体配合执行。Sentry 把警察搬到了车外，还焊死在油门必经的管路上：配合不再是前提，不配合也走不通。

但缰绳的代价要看清。第一，锁定：运行时本身可移植到 Arm 和 Intel，可真正的硬件执法层只认 BlueField-4——The Register 直接点名 vendor lock-in，缰绳同时也是护城河。第二，数字全是自称：毫秒级隔离、智能体容量 +20%、Vera 沙箱快 80%，均出自英伟达，无独立验证。第三，Sentry 要到明年初才可用，现在发布的是架构和运行时。第四，一个略带讽刺的事实：OpenShell 的 GitHub 仓库里还挂着未修复的安全 issue，遥测默认开启——看守者本身，也得有人看守。

Anthropic、OpenAI、Google、Meta、CrowdStrike 等 100 多家机构已在生态名单上。智能体的能力竞赛打了一整年，英伟达第一个把"治理"做成了计算架构的出厂配置。当每个智能体头顶都焊着一个够不着的看守，企业敢给智能体的权限，会不会反而因此变大？

---

*讨论：把执法权焊进硬件，是智能体获得更大权限的前提，还是英伟达卖芯片的又一手？*
