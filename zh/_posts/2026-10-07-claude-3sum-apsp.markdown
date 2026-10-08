---
lng_pair: id_20261007_claude-3sum-apsp
title: "0.0008 的裂缝：AI 改写教科书算法"
author: OpenSI-Labs
category: research
tags: [计算复杂性, 算法, AI数学发现, 形式化验证]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-claude-3sum-apsp.png
meta_description: "Anthropic 的内部研究模型发现了首个优于教科书的 3SUM 与全源最短路径算法，推翻了复杂性理论的两块基石——而这一发现纯属意外。"
---

几十年来两个数字钉死在教科书上：3SUM（*n* 个数中找三个和为零）约需 *n*² 步，每对节点最短路径约需 *n*³ 步。10 月 5 日，指数动了：Alman（哥大）与 Vassilevska Williams（MIT）发表论文，给出确定性算法：3SUM 做到 O(*n*^1.9992)，全源最短路径做到 O(*n*^2.9995)——对教科书算法的首次多项式级改进，直接推翻精细复杂性理论的两块基石：3SUM 假设与 APSP 假设（[arXiv 摘要](https://arxiv.org/abs/2610.06783v1)，[全文](https://arxiv.org/html/2610.06783v1)）。

摘要直言"推翻 3SUM 与 APSP 假设"，陪葬的还有 Exact Triangle 假设（新界 O(*n*^2.9983)）、零权 *k* 团假设与三个在线矩阵向量猜想。SETH（强指数时间假设）幸免。

<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="教科书指数与新指数对比，坐标轴放大">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"PingFang SC","Microsoft YaHei",sans-serif;}</style>
<text x="24" y="34" font-size="17" font-weight="700" fill="#111827">3SUM</text>
<text x="24" y="56" font-size="12.5" fill="#6b7280">坐标轴放大 25 倍：1.990 – 2.010</text>
<line x1="150" y1="100" x2="610" y2="100" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="94" x2="150" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1.990</text>
<line x1="265" y1="94" x2="265" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1.995</text>
<line x1="380" y1="94" x2="380" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.000</text>
<line x1="495" y1="94" x2="495" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.005</text>
<line x1="610" y1="94" x2="610" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.010</text>
<line x1="380" y1="70" x2="380" y2="100" stroke="#374151" stroke-width="3"/><text x="392" y="80" font-size="13" font-weight="600" fill="#374151">教科书：n&#178;</text>
<line x1="361.6" y1="70" x2="361.6" y2="100" stroke="#b45309" stroke-width="3"/><text x="150" y="80" font-size="13" font-weight="600" fill="#b45309">新：n<tspan baseline-shift="super" font-size="9">1.9992</tspan></text>
<line x1="361.6" y1="140" x2="380" y2="140" stroke="#b45309" stroke-width="1.5"/><line x1="361.6" y1="135" x2="361.6" y2="145" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="135" x2="380" y2="145" stroke="#b45309" stroke-width="1.5"/><text x="370.8" y="158" font-size="12" fill="#b45309" text-anchor="middle">0.0008</text>
<text x="24" y="196" font-size="17" font-weight="700" fill="#111827">APSP</text>
<text x="24" y="218" font-size="12.5" fill="#6b7280">坐标轴放大 25 倍：2.990 – 3.010</text>
<line x1="150" y1="262" x2="610" y2="262" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="256" x2="150" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2.990</text>
<line x1="265" y1="256" x2="265" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2.995</text>
<line x1="380" y1="256" x2="380" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.000</text>
<line x1="495" y1="256" x2="495" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.005</text>
<line x1="610" y1="256" x2="610" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.010</text>
<line x1="380" y1="232" x2="380" y2="262" stroke="#374151" stroke-width="3"/><text x="392" y="242" font-size="13" font-weight="600" fill="#374151">教科书：n&#179;</text>
<line x1="368.5" y1="232" x2="368.5" y2="262" stroke="#b45309" stroke-width="3"/><text x="150" y="242" font-size="13" font-weight="600" fill="#b45309">新：n<tspan baseline-shift="super" font-size="9">2.9995</tspan></text>
<line x1="368.5" y1="302" x2="380" y2="302" stroke="#b45309" stroke-width="1.5"/><line x1="368.5" y1="297" x2="368.5" y2="307" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="297" x2="380" y2="307" stroke="#b45309" stroke-width="1.5"/><text x="374.2" y="322" font-size="12" fill="#b45309" text-anchor="middle">0.0005</text>
</svg>
*指数对比（放大 25 倍）：3SUM 从 2.0 到 1.9992，APSP 从 3.0 到 2.9995。缝隙本身就是新闻。*

实话：十亿规模下两者只差不到 2%，常数因子也未宣称很小——没人会为此重写路由软件。意义在结构不在实用：精细复杂性几百个定理都形如"除非 3SUM 可解，否则 X 需 *n*²"，现在地基挪到了 *n*^1.9992。

机制是全新的稀疏矩阵乘法：高瘦矩阵乘矮宽矩阵，只取答案中稀疏的几个位置，需 O(*N*²/*D*^0.063) 次运算——比写出完整乘积少一个多项式量级。构造改造了 Coppersmith 1982 年矩形矩阵乘法（源自 Schönhage 十乘法恒等式），跳过只服务"没人要的位置"的运算。图论翻译：在"一边倒"三部图（两边各 *n* 顶点，第三边仅 *n*^ε 个）中快速找三角形，再经归约传导到 3SUM 与最短路径。

<svg viewBox="0 0 640 370" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="一边倒的三部图与高亮三角形">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"PingFang SC","Microsoft YaHei",sans-serif;}</style>
<text x="320" y="26" font-size="13" fill="#6b7280" text-anchor="middle">极小的一边：n<tspan baseline-shift="super" font-size="9">&#949;</tspan> 个顶点</text>
<circle cx="300" cy="52" r="7" fill="#9ca3af"/><circle cx="322" cy="44" r="7" fill="#9ca3af"/><circle cx="344" cy="52" r="7" fill="#9ca3af"/>
<g stroke="#d1d5db" stroke-width="1">
<line x1="300" y1="52" x2="130" y2="120"/><line x1="300" y1="52" x2="130" y2="200"/><line x1="300" y1="52" x2="130" y2="280"/>
<line x1="322" y1="44" x2="130" y2="160"/><line x1="322" y1="44" x2="130" y2="240"/><line x1="322" y1="44" x2="510" y2="160"/>
<line x1="344" y1="52" x2="130" y2="120"/><line x1="344" y1="52" x2="510" y2="200"/><line x1="344" y1="52" x2="510" y2="280"/>
<line x1="300" y1="52" x2="510" y2="120"/><line x1="300" y1="52" x2="510" y2="200"/><line x1="300" y1="52" x2="510" y2="280"/>
<line x1="322" y1="44" x2="510" y2="120"/><line x1="322" y1="44" x2="510" y2="240"/><line x1="344" y1="52" x2="130" y2="200"/>
</g>
<g fill="#6b7280">
<circle cx="110" cy="120" r="7"/><circle cx="150" cy="120" r="7"/><circle cx="110" cy="160" r="7"/><circle cx="150" cy="160" r="7"/><circle cx="110" cy="200" r="7"/><circle cx="150" cy="200" r="7"/><circle cx="110" cy="240" r="7"/><circle cx="150" cy="240" r="7"/><circle cx="110" cy="280" r="7"/><circle cx="150" cy="280" r="7"/>
<circle cx="490" cy="120" r="7"/><circle cx="530" cy="120" r="7"/><circle cx="490" cy="160" r="7"/><circle cx="530" cy="160" r="7"/><circle cx="490" cy="200" r="7"/><circle cx="530" cy="200" r="7"/><circle cx="490" cy="240" r="7"/><circle cx="530" cy="240" r="7"/><circle cx="490" cy="280" r="7"/><circle cx="530" cy="280" r="7"/>
</g>
<g stroke="#d97706" stroke-width="3.5" fill="none">
<line x1="130" y1="200" x2="322" y2="44"/><line x1="322" y1="44" x2="510" y2="200"/><line x1="510" y1="200" x2="130" y2="200"/>
</g>
<circle cx="130" cy="200" r="9" fill="#d97706"/><circle cx="322" cy="44" r="9" fill="#d97706"/><circle cx="510" cy="200" r="9" fill="#d97706"/>
<text x="130" y="322" font-size="13" fill="#374151" text-anchor="middle">n 个顶点</text>
<text x="510" y="322" font-size="13" fill="#374151" text-anchor="middle">n 个顶点</text>
<text x="320" y="352" font-size="12.5" fill="#b45309" text-anchor="middle">快速找到的一个三角形——唯一真正要算的东西</text>
</svg>
*核心思想：在"一边倒"图中快速找三角形，再经归约传给 3SUM 与最短路径。*

一句话：旧算法做了没人需要的功，新算法拒绝做。

更值得记住的是发现过程：论文把核心算法记在 Claude（Anthropic 内部研究模型）名下。一名员工让它去啃密码学开放问题（安全性依赖某团问题平均困难性的构造），任务是验证加固，它反手找到了削弱该假设的算法——先平均情形，再最坏情形，1600 万 token，全程零人类干预。

9 月 Anthropic 按保密协议移交算法、支付报酬并开放公开版 Claude。人类理解、化简、加强、推广（第 4 节数据结构版与 hinted 猜想的联系归作者），并对论文负全责。随后 Anthropic 用内部模型在 Lean 4 + Mathlib 中验证主要确定性结果并开源：机器发现定理，编译器验算。

这为 Anthropic 的机器数学季度封顶：8 月黎曼假设下界 41.6%→67.2%，9 月 11 天、1300 万行 Lean 代码形式化费马大定理。但前两次验证已知真理，这次是发现——AI 首次为教科书问题找到真正的新算法。

多数报道会错过的角度：Claude 被雇去当审计员，回来当了开锁匠。密码学困难性假设——数字安全的承重墙——正是可机器检验的猜想，不知疲倦的智能体可规模化审计。第一次像样的审计就撬动两个教科书指数。问题不是还会不会有裂缝，而是"已知困难"中哪些经得起查、垮掉的怎么办。

方法论还有第二个转向：想法生产已很便宜（1600 万 token、零人类、一个突破），稀缺的是验证（人类理解＋糊弄不了的编译器）。数学是"猜"与"证"的对话，猜刚被自动化，证还没有——这种不对称将定义未来十年。

提醒：两天前的预印本，同行刚开始读。Lean 覆盖主要确定性结果，实数随机界仍只靠论文本身。指数"已宣称"未"盖棺"——但签字的是编译器。Mahdi Cheraghchi 的解读帖一天获 43 万浏览，学界已在围观。

**如果机器对困难性假设的第一次审计就意外推翻了两个猜想，下一个 1600 万 token 的会话该指向哪个"已知困难"的问题——而当它带着另一道裂缝回来时，我们准备好了吗？**

*来源：[Alman &amp; Vassilevska Williams, arXiv 2610.06783](https://arxiv.org/abs/2610.06783v1) · [全文](https://arxiv.org/html/2610.06783v1) · [CellCog 逐节解读](https://cellcog.ai/blog/claude-3sum-apsp-algorithm/)*
