---
lng_pair: id_20261015_pingpongduo-table-tennis
title: "PingpongDuo：两台人形机器人，一张球台，零碰撞"
author: OpenSI-Labs
category: robotics
tags: [人形机器人, 乒乓球, 多机器人协作, 强化学习, PingpongDuo]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-pingpongduo-table-tennis.png
meta_description: "PingpongDuo 让两台人形机器人打乒乓球双打：严格轮流击球、共用一方场地、互不碰撞，回球成功率提升 13.2%，真机连续交替击球 10 次以上。"
---

**机器人打乒乓球，早就不是新闻了。机器人打双打，是另一项运动。**

单台人形机器人回球，如今已经是标准演示。DeepMind 的机械臂 2024 年就打出了竞技水平，索尼的 Ace 还登上了《自然》跟职业选手过招，伯克利的 HITTER 对人类连续回球 106 次（[arXiv:2508.21043](https://arxiv.org/pdf/2508.21043)），港大的 SMASH 更是只靠机载视觉就做到了（[arXiv:2604.01158](https://arxiv.org/html/2604.01158v1)）。但双打不一样：两个人挤在球台同一侧，必须严格轮流击球，几平方米的活动空间里，你的搭档就是一颗会移动的障碍物——而你挥拍的瞬间，他还得赶紧让开。

10 月 14 日发表的一篇论文正面攻下了双打（[Jiang 等，arXiv:2610.20579](https://arxiv.org/abs/2610.20579v1)）。PingpongDuo 是一套分层框架，解决敏捷人形双打中的安全协作问题，也是第一套让两台完整人形机器人在真机上交替对打的系统。

它的架构像一位教练的战术板。团队层面，一个规划器同时给两台机器人选站位，并用学到的风险评估过滤掉危险方案——优先保住当前击球手的空间，让挥拍的机器人永远不用在半路跟搭档"抢地盘"。个体层面，步法和击球是两套分开学的技能：灵活的腿负责跑位，精准的拍负责终结。技能的训练借鉴了人类动作参考，包括采集自真人双打比赛的步法；更巧妙的是，两套技能用"对方产生出的状态"互相训练——步法策略学会停在击球策略最舒服接手的位置。

<figure>
<svg viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">双打是一次交接：击球、让位、再击球</text>
<rect x="20" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="95" y="88" font-size="14" font-weight="bold" text-anchor="middle">机器人 A 击球</text>
<text x="95" y="112" font-size="14" text-anchor="middle">手臂残差策略</text>
<text x="95" y="132" font-size="14" text-anchor="middle">在移动后微调</text>
<text x="95" y="156" font-size="14" text-anchor="middle" font-style="italic">击球动作</text>
<rect x="200" y="60" width="150" height="120" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="275" y="88" font-size="14" font-weight="bold" text-anchor="middle">机器人 A 让位</text>
<text x="275" y="112" font-size="14" text-anchor="middle">2.4 秒跑完</text>
<text x="275" y="132" font-size="14" text-anchor="middle">2.15 米，峰值</text>
<text x="275" y="156" font-size="14" text-anchor="middle">2.23 米/秒</text>
<rect x="380" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="455" y="88" font-size="14" font-weight="bold" text-anchor="middle">机器人 B 跑位</text>
<text x="455" y="112" font-size="14" text-anchor="middle">团队规划器过滤</text>
<text x="455" y="132" font-size="14" text-anchor="middle">危险站位，保住</text>
<text x="455" y="156" font-size="14" text-anchor="middle">击球手空间</text>
<rect x="560" y="60" width="100" height="120" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="610" y="88" font-size="14" font-weight="bold" text-anchor="middle">机器人 B</text>
<text x="610" y="112" font-size="14" font-weight="bold" text-anchor="middle">击球</text>
<text x="610" y="140" font-size="14" text-anchor="middle">→ 循环</text>
<line x1="170" y1="120" x2="196" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="350" y1="120" x2="376" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="530" y1="120" x2="556" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<path d="M 610 180 C 610 280, 95 280, 95 184" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#p1)"/>
<text x="340" y="262" font-size="14" text-anchor="middle">严格轮流：每一次击球都把球台交给搭档</text>
<text x="340" y="292" font-size="14" text-anchor="middle">步法与击球技能用彼此产生的状态互相训练</text>
<text x="340" y="318" font-size="14" text-anchor="middle" font-style="italic">仿真器用真实球路与触球测量数据校准</text>
<defs><marker id="p1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>一次完整交接：击球、清空场地、搭档跑位、再击球——规划器全程守护击球手的空间。</figcaption>
</figure>

从仿真到真机的跨越，是这篇论文最扎实的工程。手臂残差策略在移动完成后继续微调击球，反馈来自一个仿真器——不是通用物理引擎，而是用真实球路飞行和触球测量数据校准过的。仿真里，PingpongDuo 的回球成功率比最强基线高出 13.2%。真机上的数据像运动员的技术统计：2.15 米的"让位—回位"全程 2.4 秒跑完，峰值速度 2.23 米/秒，让位时定位误差约 2 厘米——两台机器人严格轮流，连续对打 10 次以上（[ArXivSignals 总结](https://arxivsignals.io/explore)）。

<figure>
<svg viewBox="0 0 680 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">不止仿真：真机上测出来的成绩</text>
<text x="230" y="72" font-size="14" text-anchor="end">回球成功率（仿真）</text>
<rect x="240" y="56" width="300" height="24" rx="4" fill="#3366cc"/><text x="548" y="73" font-size="14">+13.2% 超最强基线</text>
<text x="230" y="118" font-size="14" text-anchor="end">让位 + 回位</text>
<rect x="240" y="102" width="200" height="24" rx="4" fill="#cc8833"/><text x="448" y="119" font-size="14">2.15 米 / 2.4 秒</text>
<text x="230" y="164" font-size="14" text-anchor="end">峰值速度</text>
<rect x="240" y="148" width="230" height="24" rx="4" fill="#cc8833"/><text x="478" y="165" font-size="14">2.23 米/秒</text>
<text x="230" y="210" font-size="14" text-anchor="end">交替对打（真机）</text>
<rect x="240" y="194" width="260" height="24" rx="4" fill="#339966"/><text x="508" y="211" font-size="14">10+ 次，严格轮流</text>
<text x="340" y="254" font-size="14" text-anchor="middle" font-style="italic">让位过程定位误差：约 2 厘米</text>
</svg>
<figcaption>仿真的提升加上真机的体能：那次 2.4 秒的让位冲刺，是单打系统从未需要的双打专属技能。</figcaption>
</figure>

大多数报道会错过的角度在这里：双打让"多机器人协作"从规划抽象变成了物理问题。以往的机器人团队研究，协作多半意味着分任务、排顺序。而在这里，搭档是挥拍半径内一具 50 公斤的移动障碍物，球以每秒数米的速度飞来，"轮到我"和"轮到你"之间隔着一次全身冲刺。学到的风险过滤器才是概念上的贡献：系统不把两台机器人联合规划完再祈祷，而是把击球手的工作空间视为神圣不可侵犯，否决一切威胁它的方案。安全不是事后打的补丁，是规划器的第一要务。

诚实的保留意见：10 次交替对打只是一个回合，不是整场比赛。论文没有报告对抗性对手、强烈旋转和现场噪音——真实比赛的混乱还没登场。和所有仿真训练出的"运动员"一样，系统的上限取决于校准过的仿真器有多真。

但方向已经很清楚。单打证明机器人可以成为运动员，双打证明它们可以成为队友——预判搭档的移动、让出空间、精准出现在下一个技能需要的位置。球台很小，球速很快，而这一次，机器人不再是一个人打球。

当两台机器人学会共用一张球台而不相撞——如果需要预判的搭档换成人类，会发生什么？
