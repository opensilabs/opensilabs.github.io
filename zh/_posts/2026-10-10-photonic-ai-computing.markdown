---
lng_pair: id_20261010_photonic-ai-computing
title: "光做的计算机"
author: OpenSI-Labs
category: chips
tags: [光子计算, 光学神经网络, 能效, 夸奇大学, 硬件]
date: 2026-10-10 06:00:00 -0700
img: /assets/img/posts/2026-10-10-photonic-ai-computing.png
meta_description: "土耳其夸奇大学的两项新研究把 AI 计算搬进了光本身：一个全程保留彩色信息的光子神经网络，以及一个把激光腔体直接当作非线性处理器的系统。"
---

你用过的每个 AI 模型都靠电子思考：数十亿晶体管开合，每次都烧掉一点能量、散成热量。行业的回答是造更大的东西——更大的集群、更大的电力合同，一座小镇的电只为回答你一个问题。

伊斯坦布尔夸奇大学 Uğur Teğin 实验室的两项新研究换了个问题：如果思考发生在光子里呢？光能同时携带多路信息，计算以光速完成、几乎免费。一篇（《Communications Engineering》）造了全程不丢色彩的光子神经网络，另一篇（《Communications Physics》）把一段光纤激光腔直接变成处理器。[本周的集中报道](https://techxplore.com/news/2026-10-approach-sustainable-ai-offloading-burden.html)把两者放在一起，勾勒出一种完全不同的 AI 硬件哲学。

## 别扔掉颜色

先说个听起来琐碎、算起账来吓人的事实：大多数图像分类器开头就扔掉信息，把红绿蓝三通道压成一个灰度通道。但颜色本身就是信号——皮肤病诊断可能藏在细微的发红里，卫星图像的含义可能写在绿色中。

Kılınç 与 Teğin 的系统拒绝这条捷径：图像被编码到可编程器件上，一组相位掩模（多平面光转换）让红绿蓝三通道结伴穿过光学系统，在行进中被混合、变换，在物理层面强化区分图像的特征——颜色、形状、纹理。相机记录光学图案，分类器直接读出类别。

数字很硬：皮肤病分类准确率从原始像素的 68% 涨到光学预处理后的 **98%**。在医学影像、自然图像和回归任务上，光学预处理比基线高 25–45 个百分点；光"不转灰度"一项就值 6–11 个百分点（[论文](https://www.nature.com/articles/s44172-026-00762-w)）。

<svg viewBox="0 0 720 470" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="多通道光学计算流程：RGB 三通道经相位掩模编码，与光同行变换，由相机读取">
  <defs>
    <marker id="arrP" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">多通道光学计算：颜色全程保留</text>
  <rect x="30" y="50" width="150" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="105" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">RGB 图像输入</text>
  <text x="105" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">三通道全部保留</text>
  <rect x="30" y="140" width="150" height="26" rx="6" fill="#f8f9fa" stroke="#adb5bd"/>
  <text x="105" y="157" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">不转灰度</text>
  <line x1="180" y1="85" x2="225" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="225" y="50" width="170" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="310" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">相位掩模组</text>
  <text x="310" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">多平面光转换</text>
  <line x1="395" y1="85" x2="440" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="440" y="50" width="150" height="70" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="515" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">光传播变换</text>
  <text x="515" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">特征在光学域被强化</text>
  <line x1="590" y1="85" x2="620" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="620" y="50" width="80" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="660" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">相机</text>
  <text x="660" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">+ 分类器</text>
  <rect x="120" y="200" width="480" height="120" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="228" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">自优化闭环</text>
  <text x="360" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">直接从实验测量中学习——不需要完美仿真器</text>
  <text x="360" y="274" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">贝叶斯优化（通道混合）+ 硬件在环</text>
  <text x="360" y="296" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">自组织临界（相位参数）——自动适应装配误差</text>
  <line x1="310" y1="120" x2="310" y2="195" stroke="#2b8a3e" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arrP)"/>
  <rect x="225" y="350" width="270" height="70" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="360" y="378" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">皮肤病分类：68% → 98%</text>
  <text x="360" y="400" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">自优化在此基础上再加 7–12 个百分点</text>
  <text x="360" y="448" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">图注：RGB 三通道结伴穿过可编程相位掩模；系统针对真实硬件自我调参。</text>
</svg>

## 学会的是器件本身，而不是仿真

关键不在准确率。光学神经网络有个"坟场问题"：仿真里漂亮，进实验室就死。装配偏差、加工误差、温度漂移——物理器件永远对不上计算机里的理想模型，差距吃掉全部性能。

Teğin 团队把问题倒了过来：不要完美仿真器，让系统直接从实验测量里学。两套互补策略都不需要可微分前向模型：贝叶斯优化调输入端通道混合，基于自组织临界的硬件在环协议搜索高维相位参数。机器学会自己这套硬件的脾气并适应它——缺陷不是要被工程掉的噪声，而是学习对象的一部分。自优化又贡献了 7–12 个百分点。

电子学花了六十年逼近越来越紧的公差——纳米，直到埃米。这是反方向的赌注：用不完美的物理造计算机，再让物理来教算法。一种真正不同的硬件哲学，也是这项工作在基准表之外值得被关注的原因。

## 会思考的激光

第二项研究更怪，也更激进：Eşlik、Kesgin、Kılınç 与 Teğin 把一段连续波多模光纤激光器的腔体本身当成处理器。输入图像写成相位图案打到空间光调制器上；光在腔里循环，多模干涉和增益饱和——激光自身的物理行为——把它搅成高维非线性变换。出来的是一幅稳定的强度图案，各类别已然分开，简单线性分类器收尾即可。

非线性映射没有 GPU 参与，物理自己干了。在可回收物、气象与卫星图像、视网膜扫描、皮肤病变上，系统达到 **85–99%** 准确率，可训练参数比传统深网少几个数量级（[论文](https://www.nature.com/articles/s42005-026-02823-0)）。

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="光纤激光腔即非线性光学处理器：相位编码图像经激光动力学变换为可分的图案">
  <defs>
    <marker id="arrQ" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">激光腔体本身就是处理器</text>
  <rect x="20" y="60" width="130" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="85" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">图像输入</text>
  <text x="85" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">废品、卫星、视网膜…</text>
  <line x1="150" y1="95" x2="190" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="190" y="60" width="140" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="260" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">空间光调制器</text>
  <text x="260" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">相位图案编码</text>
  <line x1="330" y1="95" x2="370" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="370" y="50" width="200" height="90" rx="40" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="470" y="80" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">光纤激光腔</text>
  <text x="470" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">多模干涉</text>
  <text x="470" y="118" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">+ 增益饱和</text>
  <line x1="570" y1="95" x2="610" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="610" y="60" width="90" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="655" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">线性</text>
  <text x="655" y="106" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">分类器</text>
  <rect x="190" y="180" width="380" height="80" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="380" y="210" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">准确率 85–99%</text>
  <text x="380" y="232" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">可训练参数比深网少几个数量级</text>
  <text x="380" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">——激光动力学取代了网络的隐藏层</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#212529">关键：非线性映射是免费的</text>
  <text x="360" y="334" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">在数字网络里，非线性意味着矩阵乘法和访存开销；</text>
  <text x="360" y="354" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">在腔体里，它只是光穿过时本来就会做的事。</text>
  <text x="360" y="386" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">图注：输入图像变成相位图案；激光自身的动力学完成非线性计算。</text>
</svg>

## 诚实的账

两处提醒，本刊不炒作。第一，两个系统都不是纯光：写数据要空间光调制器，读图案要相机，跑优化要控制单元——两头还是电子的。诚实的问题是光能吃掉总工作量的几成：今天它吃掉最重的中间段——非线性特征变换，两头仍是电子。高速光调制器和芯片级集成光子学能否把比例推向全流程，是悬而未决的赌注。

第二，这都是概念验证的尺度，不是数据中心替代品——明年不会有人在光纤激光里训练前沿大模型。

但方向是对的，时机也重要。AI 推理正在撞上物理极限——功耗、散热、存算之间的数据搬运代价，而这些全是电子的属性。光子计算不只绕开它们，更把最硬的一条反转了：电子要求完美并为之支付制造成本，光子却可以学会自己手里这套器件。顺着物理做计算，而不是跟物理较劲。

上世纪八十年代也做过光计算机的梦，死在可编程性和自适应上。缺的那块拼图原来不是更好的光学，而是让光学自己学会自己。

**讨论：** 如果未来 AI 硬件学会适应自身物理基底的不完美、不再要求完美工艺，芯片制造的经济学会被改写吗——当"够好的物理"打败"完美的硅"，赢家是谁？
