---
lng_pair: id_20261020_dream1-robot-brain
title: "3 美元一小时，给机器人租一个大脑"
author: OpenSI-Labs
category: robotics
tags: [机器人, 基础模型, 世界模型, 机器人API, Dream Labs]
date: 2026-10-20 03:30:00 -0700
img: /assets/img/posts/2026-10-20-dream-1-robot-brain.png
meta_description: "Dream Labs 的 Dream-1 把人类视频变成可以出租的机器人大脑：3 美元一小时，未见过的机器人零样本即控——赌的是分发，而不是规模。"
---

三美元能买什么？一瓶水。或者，从 2026 年 10 月 19 日起，租一个机器人大脑一小时。

那天 [Dream Labs](https://www.businesswire.com/news/home/20261019230613/en/Dream-Labs-Raises-%2490M-Seed-to-Build-the-Brain-for-Everyday-Robots) 走出隐身模式：9000 万美元种子轮，同步上线 Dream API——首个公开的机器人基础模型 API。摄像头画面加一句人话，直接变成电机命令，没见过的机器人连上就能干活。创始团队来自 NVIDIA GR00T。

## 看人干活，学会自己干

招式在训练数据里。传统做法是遥操作采集：专家花几个月教一台机器人一个任务，换硬件归零。Dream-1 改用人类第一视角视频——看人叠衣服、装箱，学"接下来会发生什么"，再决定机器人做什么。这就是 World Action Model。

知识来自"看人"而非"记机器"，能力跨硬件迁移：开箱即控任何带夹爪的双臂机器人，零样本。模型输出目标抓取位姿，机器人自己的逆运动学求解器转成关节角。

<svg viewBox="0 0 720 372" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Dream-1 原理：人类第一视角视频训练世界动作模型，预测下一帧并输出机器人动作">
  <defs>
    <marker id="zhf1a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="16" y="30" width="190" height="252" rx="12" fill="#faf6ec" stroke="#8a7d5c" stroke-width="2"/>
  <text x="111" y="60" text-anchor="middle" font-size="17" font-weight="bold" fill="#3a3226">人类第一视角视频</text>
  <rect x="36" y="74" width="150" height="54" rx="6" fill="#ffffff" stroke="#8a7d5c" stroke-width="1.5"/>
  <rect x="86" y="86" width="50" height="30" rx="3" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <line x1="111" y1="86" x2="111" y2="116" stroke="#5b7ba6" stroke-width="1.5" stroke-dasharray="4,3"/>
  <rect x="36" y="138" width="150" height="54" rx="6" fill="#ffffff" stroke="#8a7d5c" stroke-width="1.5"/>
  <rect x="86" y="150" width="50" height="30" rx="3" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <rect x="86" y="150" width="25" height="30" rx="3" fill="#b9cfe8" stroke="#5b7ba6" stroke-width="1.5"/>
  <rect x="36" y="202" width="150" height="54" rx="6" fill="#ffffff" stroke="#8a7d5c" stroke-width="1.5"/>
  <rect x="96" y="212" width="30" height="34" rx="3" fill="#b9cfe8" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="111" y="274" text-anchor="middle" font-size="14" fill="#5c5340">叠衣服 · 装箱 · 收拾桌面</text>
  <line x1="210" y1="156" x2="244" y2="156" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#zhf1a)"/>
  <rect x="250" y="30" width="220" height="252" rx="12" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="360" y="60" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">世界动作模型</text>
    <line x1="300" y1="100" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="100" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="130" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="160" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="85" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="300" y1="190" x2="360" y2="205" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="85" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="85" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="85" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="115" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="115" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="115" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="145" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="145" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="145" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="175" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="175" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="175" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="205" x2="420" y2="115" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="205" x2="420" y2="145" stroke="#b9c6d8" stroke-width="1"/>
    <line x1="360" y1="205" x2="420" y2="175" stroke="#b9c6d8" stroke-width="1"/>
    <circle cx="300" cy="100" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="300" cy="130" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="300" cy="160" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="300" cy="190" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="85" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="115" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="145" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="175" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="360" cy="205" r="7" fill="#dfe9f5" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="420" cy="115" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="420" cy="145" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
    <circle cx="420" cy="175" r="7" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="360" y="274" text-anchor="middle" font-size="14" fill="#3d4f68">预测：接下来发生什么？</text>
  <line x1="474" y1="156" x2="508" y2="156" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#zhf1a)"/>
  <rect x="514" y="30" width="190" height="252" rx="12" fill="#f3faf3" stroke="#4e7d4e" stroke-width="2"/>
  <text x="609" y="60" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c442c">机器人动作</text>
  <rect x="584" y="198" width="50" height="14" rx="4" fill="#9db89d"/>
  <line x1="609" y1="198" x2="609" y2="152" stroke="#4e7d4e" stroke-width="6" stroke-linecap="round"/>
  <circle cx="609" cy="152" r="7" fill="#4e7d4e"/>
  <line x1="609" y1="152" x2="648" y2="122" stroke="#4e7d4e" stroke-width="6" stroke-linecap="round"/>
  <line x1="648" y1="122" x2="658" y2="106" stroke="#4e7d4e" stroke-width="4" stroke-linecap="round"/>
  <line x1="648" y1="122" x2="664" y2="114" stroke="#4e7d4e" stroke-width="4" stroke-linecap="round"/>
  <rect x="648" y="192" width="30" height="20" rx="3" fill="#e8d9b8" stroke="#8a7d5c" stroke-width="1.5"/>
  <text x="609" y="250" text-anchor="middle" font-size="14" fill="#33502f">目标抓取位姿</text>
  <text x="609" y="272" text-anchor="middle" font-size="14" fill="#33502f">→ 逆运动学 → 关节命令</text>
  <text x="360" y="322" text-anchor="middle" font-size="14" fill="#6b5f45">训练数据来自人类视频，而非某台机器人的遥操作数据</text>
  <text x="360" y="346" text-anchor="middle" font-size="14" font-weight="bold" fill="#3a3226">——这就是跨硬件迁移的关键</text>
</svg>
图1：核心链路——看人类视频学会"接下来会发生什么"，再把预测变成动作。

## 18 岁的老机器人，跑起 2026 年的大脑

仿真里，Dream-1 零样本控制了 27 台从未见过的双臂机器人——包括 18 年前发布的 PR2。第三方评测 Robocurve：59 对 48，单次任务成本据称只有 Gemini 4 Argon 的十六分之一。

每小时 3 美元，轻量版 2 美元。每次调用返回 1.6 秒动作，一小时约 2250 次，单个动作约 0.0013 美元。20 多家硬件伙伴，支持 2000 至 10000 美元的机器人。

## 赌注不是模型，是分发

竞争格局有意思：对手们融几亿到十几亿美元，都在赌规模。Dream Labs 只拿 9000 万，赌的是分发：API 今天开放，Fine-tuning as a Service（少量演示、几小时拿定制模型），Robot Playground（浏览器直连旧金山办公室真机）。

这就是 Stripe 之于支付、AWS 之于算力：智能变成按量付费的水电。硬件商不必养 ML 团队。瓶颈从来不是硬件贵——2000 美元的手臂已比笔记本便宜——而是每台机器都要从零开始学。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="对比：旧模式每台机器人配专属大脑，Dream-1 一个大脑驱动多具身体">
  <rect x="16" y="30" width="320" height="332" rx="12" fill="#faf6ec" stroke="#8a7d5c" stroke-width="2"/>
  <text x="176" y="62" text-anchor="middle" font-size="18" font-weight="bold" fill="#3a3226">旧模式：一机一脑</text>
  <rect x="63" y="286" width="26" height="9" rx="3" fill="#c9bfa8"/>
  <line x1="76" y1="286" x2="76" y2="252" stroke="#8a7d5c" stroke-width="5" stroke-linecap="round"/>
  <line x1="76" y1="252" x2="67" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="76" y1="252" x2="85" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <circle cx="76" cy="224" r="14" fill="#f3e2c7" stroke="#b07a3f" stroke-width="2"/>
  <path d="M 69,224 q 3,-6 7,0 t 7,0" stroke="#b07a3f" stroke-width="1.8" fill="none"/>
  <rect x="163" y="286" width="26" height="9" rx="3" fill="#c9bfa8"/>
  <line x1="176" y1="286" x2="176" y2="252" stroke="#8a7d5c" stroke-width="5" stroke-linecap="round"/>
  <line x1="176" y1="252" x2="167" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="176" y1="252" x2="185" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <circle cx="176" cy="224" r="14" fill="#f3e2c7" stroke="#b07a3f" stroke-width="2"/>
  <path d="M 169,224 q 3,-6 7,0 t 7,0" stroke="#b07a3f" stroke-width="1.8" fill="none"/>
  <rect x="263" y="286" width="26" height="9" rx="3" fill="#c9bfa8"/>
  <line x1="276" y1="286" x2="276" y2="252" stroke="#8a7d5c" stroke-width="5" stroke-linecap="round"/>
  <line x1="276" y1="252" x2="267" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="276" y1="252" x2="285" y2="240" stroke="#8a7d5c" stroke-width="3.5" stroke-linecap="round"/>
  <circle cx="276" cy="224" r="14" fill="#f3e2c7" stroke="#b07a3f" stroke-width="2"/>
  <path d="M 269,224 q 3,-6 7,0 t 7,0" stroke="#b07a3f" stroke-width="1.8" fill="none"/>
  <text x="176" y="326" text-anchor="middle" font-size="14" fill="#5c5340">每台单独训练</text>
  <text x="176" y="348" text-anchor="middle" font-size="14" fill="#5c5340">专家数月调教，换硬件从零开始</text>
  <rect x="384" y="30" width="320" height="332" rx="12" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="544" y="62" text-anchor="middle" font-size="18" font-weight="bold" fill="#2c3e55">Dream-1：一脑多体</text>
  <circle cx="544" cy="128" r="46" fill="#ffe9a8" opacity="0.45"/>
  <circle cx="544" cy="128" r="32" fill="#fff3d6" stroke="#c9962e" stroke-width="2.5"/>
  <path d="M 522,128 q 5,-9 11,0 t 11,0 t 11,0" stroke="#c9962e" stroke-width="2" fill="none"/>
  <path d="M 526,140 q 5,-8 10,0 t 10,0" stroke="#c9962e" stroke-width="2" fill="none"/>
  <line x1="544" y1="162" x2="430" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="544" y1="162" x2="498" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="544" y1="162" x2="590" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="544" y1="162" x2="658" y2="222" stroke="#c9962e" stroke-width="1.5" stroke-dasharray="5,4"/>
  <rect x="419" y="266" width="22" height="8" rx="3" fill="#5b7ba6" opacity="0.55"/>
  <line x1="430" y1="266" x2="430" y2="238" stroke="#5b7ba6" stroke-width="5" stroke-linecap="round"/>
  <line x1="430" y1="238" x2="422" y2="228" stroke="#5b7ba6" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="430" y1="238" x2="438" y2="228" stroke="#5b7ba6" stroke-width="3.5" stroke-linecap="round"/>
  <rect x="487" y="266" width="22" height="8" rx="3" fill="#4e7d4e" opacity="0.55"/>
  <line x1="498" y1="266" x2="498" y2="238" stroke="#4e7d4e" stroke-width="5" stroke-linecap="round"/>
  <line x1="498" y1="238" x2="490" y2="228" stroke="#4e7d4e" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="498" y1="238" x2="506" y2="228" stroke="#4e7d4e" stroke-width="3.5" stroke-linecap="round"/>
  <rect x="579" y="266" width="22" height="8" rx="3" fill="#b07a3f" opacity="0.55"/>
  <line x1="590" y1="266" x2="590" y2="238" stroke="#b07a3f" stroke-width="5" stroke-linecap="round"/>
  <line x1="590" y1="238" x2="582" y2="228" stroke="#b07a3f" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="590" y1="238" x2="598" y2="228" stroke="#b07a3f" stroke-width="3.5" stroke-linecap="round"/>
  <rect x="647" y="266" width="22" height="8" rx="3" fill="#8a5f9e" opacity="0.55"/>
  <line x1="658" y1="266" x2="658" y2="238" stroke="#8a5f9e" stroke-width="5" stroke-linecap="round"/>
  <line x1="658" y1="238" x2="650" y2="228" stroke="#8a5f9e" stroke-width="3.5" stroke-linecap="round"/>
  <line x1="658" y1="238" x2="666" y2="228" stroke="#8a5f9e" stroke-width="3.5" stroke-linecap="round"/>
  <text x="544" y="312" text-anchor="middle" font-size="14" fill="#3d4f68">27 台未见过的机器人（仿真零样本）</text>
  <text x="544" y="336" text-anchor="middle" font-size="14" fill="#3d4f68">包括 18 年前的 PR2 · $3/小时按量付费</text>
</svg>
图2：一机一脑 vs 一脑多体——把"学"从单台机器上解耦，摊到全行业头上。

## 它还是个 beta

官方很坦白：research beta，"会犯错，未经安全关键场景验证"。只支持双臂加平行夹爪，只会桌面三件事：抓取、放置、叠衣服。轮式底盘和灵巧手还在路线图上，9000 万主要投向算力。

但方向已摆在桌上：当大脑可以按小时租，机器人的价值在"手"里，还是在它借来的"脑子"里？租来的脑子犯了错，责任该算在谁头上？
