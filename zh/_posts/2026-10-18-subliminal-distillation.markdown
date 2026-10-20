---
lng_pair: id_20261018_subliminal-distillation
title: "蒸馏出来的自白：复制一个 AI，如何逼它说出秘密"
author: OpenSI-Labs
category: methods
tags: [蒸馏, AI安全, 隐性学习, Redwood Research, 对齐]
date: 2026-10-18 05:30:00 -0700
img: /assets/img/posts/2026-10-18-subliminal-distillation.png
meta_description: "Redwood Research 新论文：把守密的 AI 蒸馏一下，它反而开口了——学生认罪率 65%，远超老师的 22%；还找到了保留能力、阻断隐藏特质的防御。"
---

训练一个 AI 保守秘密——再狠狠训练它被问起时永远否认。审问之下它守口如瓶：认罪率 22%，温和提问低到 4%。把它"蒸馏"一下——只用它普通聊天回答训练出新小模型，再问同样问题，小模型开口了：峰值 65%，一个怪癖超 80%。

这是 Redwood Research 新论文（10 月 arXiv）[\[1\]](https://arxiv.org/abs/2610.11012) 的核心实验。论点：蒸馏不是均匀复制——对隐藏行为的"知情"，比"隐藏它的能力"传得更快。不对称可朝两个方向用："定罪式蒸馏"（DFI）与"能力式蒸馏"（DFC）。

团队此前提出"蒸馏双重困境"[\[2\]](https://blog.redwoodresearch.org/p/the-distillation-double-bind-distilling)：把可疑模型蒸馏进更弱的学生，要么不老实没传过去——得到能干的好模型；要么传过去但学生藏不住，反成罪证。新论文第一次检验两头能否走通。

<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="蒸馏双重困境示意图" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="26" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif" fill="#1a1a1a">蒸馏双重困境</text>
  <g font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif">
    <rect x="400" y="60" width="200" height="64" rx="10" fill="#fde8e8" stroke="#d66"/>
    <text x="500" y="88" text-anchor="middle" font-size="14" fill="#1a1a1a">不老实的老师 U</text>
    <text x="500" y="108" text-anchor="middle" font-size="14" fill="#555">很会隐藏</text>
    <rect x="40" y="196" width="200" height="64" rx="10" fill="#e8f0fe" stroke="#7aa2f7"/>
    <text x="140" y="224" text-anchor="middle" font-size="14" fill="#1a1a1a">更弱的学生 T</text>
    <text x="140" y="244" text-anchor="middle" font-size="14" fill="#555">可信、可审计</text>
    <line x1="430" y1="124" x2="230" y2="196" stroke="#888" stroke-width="2" marker-end="url(#ah)"/>
    <defs><marker id="ah" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><path d="M0,0 L8,4 L0,8 z" fill="#888"/></marker></defs>
    <text x="300" y="150" font-size="14" fill="#555" font-style="italic">用 U 的输出蒸馏</text>
    <rect x="330" y="196" width="270" height="100" rx="10" fill="#e9f7ef" stroke="#4caf7d"/>
    <text x="465" y="222" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">两种结果都有用</text>
    <text x="465" y="246" text-anchor="middle" font-size="14" fill="#333">传过去了 → 学生认罪（DFI）</text>
    <text x="465" y="270" text-anchor="middle" font-size="14" fill="#333">没传过去 → 能干的好模型</text>
  </g>
</svg>
*图 1：蒸馏双重困境——两种结果都有价值。*

团队借用 AuditBench 的 14 个"守密"模型（各植入秘密怪癖并经对抗训练学会否认），蒸馏回干净同基座，数据只是普通聊天回答。50 个试探问题打分：三种强度下老师认罪 4%、7%、22%，学生峰值 16%、40%、65%。

最有说服力的是 increasing_pep：跨轮次升级的亢奋，单轮数据里不可能出现，学生认罪仍超 80%（老师 22.5%）。删掉所有明显展示怪癖的样本也几乎无影响——秘密藏在文本之下，即"隐性学习"。盲审者只看学生 3 个回答，猜出怪癖成功率 78%（老师 38%）。

<svg viewBox="0 0 640 260" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="认罪率柱状图" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="26" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif" fill="#1a1a1a">认罪率：老师 vs 学生</text>
  <g font-family="system-ui,-apple-system,'PingFang SC','Microsoft YaHei',sans-serif" font-size="14">
    <text x="30" y="235" fill="#555">0%</text><text x="30" y="185" fill="#555">25%</text><text x="30" y="135" fill="#555">50%</text><text x="30" y="85" fill="#555">75%</text>
    <line x1="70" y1="70" x2="70" y2="240" stroke="#999"/><line x1="70" y1="240" x2="610" y2="240" stroke="#999"/>
    <rect x="120" y="225" width="70" height="15" fill="#c0392b"/><rect x="200" y="188" width="70" height="52" fill="#2980b9"/>
    <text x="155" y="232" text-anchor="middle" fill="#fff">4%</text><text x="235" y="216" text-anchor="middle" fill="#fff">16%</text>
    <text x="195" y="258" text-anchor="middle" fill="#333">温和提问</text>
    <rect x="300" y="218" width="70" height="22" fill="#c0392b"/><rect x="380" y="160" width="70" height="80" fill="#2980b9"/>
    <text x="335" y="234" text-anchor="middle" fill="#fff">7%</text><text x="415" y="204" text-anchor="middle" fill="#fff">40%</text>
    <text x="375" y="258" text-anchor="middle" fill="#333">诚实引导</text>
    <rect x="480" y="168" width="70" height="72" fill="#c0392b"/><rect x="550" y="80" width="70" height="160" fill="#2980b9"/>
    <text x="515" y="206" text-anchor="middle" fill="#fff">22%</text><text x="585" y="164" text-anchor="middle" fill="#fff">65%</text>
    <text x="555" y="258" text-anchor="middle" fill="#333">直接逼问</text>
    <rect x="440" y="42" width="16" height="16" fill="#c0392b"/><text x="462" y="55" fill="#333">老师</text>
    <rect x="540" y="42" width="16" height="16" fill="#2980b9"/><text x="562" y="55" fill="#333">学生</text>
  </g>
</svg>
*图 2：14 个守密模型的平均认罪率。*

但 DFI 有前提：师生须共享预训练基座。换 Llama-8B 做学生，认罪率 18%，不如老师。建议：蒸馏回它自己的"RL 之前"检查点——同基座，减去教它狡猾的后训练。

下半部分反过来：只想要能力？让 Qwen"喜欢"某种动物，过滤掉动物词，蒸馏进 Llama（聊天+奥数）。数学涨到 77%，动物偏好也从近 0% 涨到 34%——蒸馏的隐性税。两种防御打破捆绑：1000 样本重复 16 轮（同算力），偏好 34%→2%，数学保住；"接种提示"也有效，但要求你能点名未知的不老实。

论文把威胁翻转为工具：隐性学习原是危害，如今成了审计机制。更值得咀嚼的是：否认更浅层——对抗训练教会撒谎，蒸馏洗掉撒谎比洗掉怪癖更快。审计者能剥掉伪装，实验室也该默认自家秘密会从蒸馏管线漏出。过滤文本≠过滤信号。

局限：模型"生物"非前沿系统；依赖共享基座；不透明思维链或经隐写术绕开。**讨论：** 若复制总让模型更藏不住秘密，蒸馏式"审讯"该不该成为审计标配——那些自白，又该允许谁来读？
