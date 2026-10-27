---
lng_pair: id_20261027_byteification
title: "数不对 strawberry 里有几个 r？这篇 Nature 论文给 Llama 和 Qwen 换了一种读法"
author: OpenSI-Labs
category: research
tags: [语言模型, 分词, 字节级模型, Nature, Llama, Qwen, 艾伦人工智能研究所]
date: 2026-10-27 01:00:00 -0700
img: /assets/img/posts/2026-10-27-byteification.png
meta_description: "问聊天机器人 strawberry 里有几个 r，它常说两个。正确答案是三个——但模型根本看不见字母。这篇 Nature 论文给 Llama 3 和 Qwen3 做了一次改造：让它们逐个字母地读，花费不到从头训练的 1%。"
---

问一个六岁小孩都会答的问题：strawberry 这个词里有几个字母 r？

答案是三个。可很长一段时间里，你去问最强的聊天机器人，它多半会告诉你：两个。

这不是它笨。是它压根看不见字母。

今天的语言模型在读你写的话之前，会先让另一个程序把文本切成一块一块的，每块叫一个 token（标记）。一块可能是一个完整的短词，也可能是长词的一截。strawberry 到了模型面前，可能已经被切成了三块，比如 straw、ber、ry。模型能处理的最小单位就是这些块，块里面的字母，它从头到尾没见过。

所以你问它有几个 r，它就像一个只能看到三个密封纸箱的人，被问箱子里一共有几扇窗。它可以凭印象猜，没法真的去数。答错两个，不是算错了，是没看见。

这种切块读法有个名字，叫子词分词（subword tokenization），你用过的语言模型几乎都在用。本月发表在《自然》（Nature）上的一篇论文——作者来自慕尼黑大学、艾伦人工智能研究所、剑桥大学、华盛顿大学和帝国理工学院，第一作者是 Benjamin Minixhofer——问了一个很朴素的问题：这块"切法"，能不能改？一个已经训练好、只会按块读的模型，能不能在事后花很少的代价，改成逐个字母地读？

他们的答案叫 byteification，姑且译作"字节化"。而且他们不是拿玩具模型演示，是直接动了 Meta 的 Llama 3 和阿里的 Qwen3 这样的现成模型。

## 先说清楚：为什么当初要切块

没人是因为喜欢切块才切块的，是因为这样快。

逐个字母读，意味着要读的东西一下子多出好几倍。一页英文有几千个字母，每个字母都让一个大模型走一步，计算量会涨得很难看。切块是一种压缩：常见的组合——the、ing、strawberry 的开头那一截——直接合成一个单位，模型就能把步子花在够大的意义单元上。过去十年整个大模型时代，都是建在这种压缩之上的。训练开始之前，先定好一本"块词典"，GPT、Claude、Llama、Qwen，底下垫的都是它。

代价也随之而来。看不见字母，拼写就只能靠猜，数数更是蒙。写代码会吃亏，因为代码里单个字符常常就是全部要害：一个括号放错位置，程序做的就是另一件事。基因序列同理，换掉一个字母，可能就换了一种分子。还有一层不公平藏在里面：这些块词典大多是照着英文编的。有些语言的词在词典里碎得厉害，同一句话要切出多得多的块——块多，就更贵，读得也更笨。同内容，不同语言，一个交的是"碎读税"，一个没有。这笔税在训练开始前就定好了，跟数据无关，是读法本身自带的。

这些毛病不是没人知道。一直有人做直接读字节的模型：字节是计算机存储文本的最小单位，英文里大致一个字节就是一个字母。逐字节读的模型什么都看得见——每个字母、每个空格、每个括号。strawberry 骗不了它，因为它和字母之间没有任何遮挡。

问题是，这类模型一直打不赢。从头训练一个出来，花的是和任何大模型一样的钱，效果却明显落后于按块读的同尺寸模型。于是逐字节读法一直停在实验室里，业界继续用密封纸箱。

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="48" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">读 strawberry 的两种方式</text>
<text x="40" y="92" font-size="16" font-weight="700" fill="#475569">按块读——现在的模型</text>
<rect x="40" y="106" width="180" height="52" rx="10" fill="#94a3b8"/>
<rect x="236" y="106" width="150" height="52" rx="10" fill="#94a3b8"/>
<rect x="402" y="106" width="110" height="52" rx="10" fill="#94a3b8"/>
<text x="130" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">straw</text>
<text x="311" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">ber</text>
<text x="457" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">ry</text>
<text x="528" y="140" font-size="16" fill="#475569">字母藏在块里</text>
<text x="40" y="212" font-size="16" font-weight="700" fill="#166534">逐字节读——字节化之后</text>
<rect x="40" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="64" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">s</text>
<rect x="96" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="120" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">t</text>
<rect x="152" y="226" width="48" height="48" rx="8" fill="#fee2e2" stroke="#dc2626" stroke-width="3"/><text x="176" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#b91c1c">r</text>
<rect x="208" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="232" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">a</text>
<rect x="264" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="288" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">w</text>
<rect x="320" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="344" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">b</text>
<rect x="376" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="400" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">e</text>
<rect x="432" y="226" width="48" height="48" rx="8" fill="#fee2e2" stroke="#dc2626" stroke-width="3"/><text x="456" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#b91c1c">r</text>
<rect x="488" y="226" width="48" height="48" rx="8" fill="#fee2e2" stroke="#dc2626" stroke-width="3"/><text x="512" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#b91c1c">r</text>
<rect x="544" y="226" width="48" height="48" rx="8" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/><text x="568" y="258" text-anchor="middle" font-size="19" font-weight="700" fill="#111827">y</text>
<text x="608" y="258" font-size="17" font-weight="700" fill="#b91c1c">r = 3</text>
<text x="340" y="302" text-anchor="middle" font-size="16" fill="#4b5563">块把字母封在里面；字节把每个字母都摊在桌面上。</text>
</svg>
<figcaption>图 1 —— 按块读的模型遇到的 strawberry 是几个密封的块；逐字节读的模型遇到的是全部十个字母，三个 r 直接数就行。</figcaption>
</figure>

## 不是重建，是换眼睛

这篇论文真正的新意，是把"读法"从地基里拆了出来。

按他们的看法，一个训练好的模型可以分成两部分。中间的大块头——堆叠起来的 Transformer 主干——装着模型几乎全部的知识：语言、事实、推理，都在那里。而它的外围是"读的器官"：把原始文字变成主干能处理的东西，再把主干的输出变回文字。字节化动的是外围，主干几乎不碰。而主干恰恰是最贵的部分，是花了一整轮预训练才烧出来的。

换句话说：换的是读法，不是知识。就好比一个人换了副眼镜，他学过的东西一点没少，只是终于能看清小字了。

新装上的部件有这几样：一个在本地读字节的小编码器；一个"边界预测器"，负责判断一截字节在哪里断开、下一截从哪里开始；一个本地解码器；还有输出端。中间的主干——作者称之为全局 Transformer——拿到的仍然是一块一块的输入，只不过这些块是看过真实字母的读者现场切出来的，而不是查词典查出来的。

训练分两个阶段，第一阶段是关键。作者把主干彻底冻住，一个参数都不许动，只训练外围的新部件。训练目标是精确蒸馏：让新部件喂给主干的东西，效果和原来一模一样，像什么都没变过。说白了，先让新眼睛学会说老脑子听得懂的话，再谈别的。这一阶段用了 98 亿个 token。

第二阶段才解冻，把整个模型放在一起端到端微调，用了 393 亿个 token，数据主要来自艾伦研究所的开放语料 Dolma 3，另外加了 7500 万个专门合成的 token，内容就是练拼写、练数数、练摆弄字母这类字符功夫。两笔账加起来 491 亿个 token。作者说，这不到同等规模模型从头训练成本的 1%。用不到百分之一的钱，换掉一个成品模型的读法。

还有一个细节值得单独说，作者认为这是早年字节模型输掉的一大原因。逐字节读的时候，切分要一边读一边定。以前的设计只能看已经读过的字节，蒙着眼往前切。这篇论文的边界预测器被允许"偷看"：判断一截到此为止还是再往前带一个字节时，它可以看一眼后面 1 个字节。就 1 个字节，听上去不算什么。但这正是蒙眼切和瞄一眼再切的区别——瞄到的那一眼会告诉你，ry 是 strawberry 的收尾，还是下一个词的开头。作者说，这一眼补上之后，字节模型当年落后的那截表达能力，补回来了大半。模型结构借鉴的是此前最强的字节模型、Meta 的 Byte Latent Transformer，再加上这一眼。

<figure>
<svg width="680" height="400" viewBox="0 0 680 400" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="380" rx="14" fill="#f7f9fc"/>
<text x="340" y="46" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">字节化：两个阶段，一笔小账</text>
<rect x="30" y="66" width="620" height="128" rx="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
<text x="48" y="94" font-size="17" font-weight="700" fill="#1e40af">第一阶段——先教会新眼睛 · 98 亿 token</text>
<rect x="48" y="108" width="128" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="112" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">字节编码器</text>
<rect x="186" y="108" width="196" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="284" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">边界预测器*</text>
<rect x="392" y="108" width="140" height="40" rx="8" fill="#e5e7eb" stroke="#6b7280" stroke-width="2"/><text x="462" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#374151">核心：冻结</text>
<rect x="542" y="108" width="92" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="588" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">解码器</text>
<text x="48" y="176" font-size="16" fill="#1f2937">*断句时可以偷看后面 1 个字节 · 这一阶段只训练新部件</text>
<rect x="30" y="208" width="620" height="104" rx="12" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/>
<text x="48" y="236" font-size="17" font-weight="700" fill="#166534">第二阶段——整体一起微调 · 393 亿 token</text>
<text x="48" y="266" font-size="16" fill="#1f2937">核心解冻，整个模型端到端微调，</text>
<text x="48" y="290" font-size="16" fill="#1f2937">另加 7500 万个专门练字符功夫的合成 token。</text>
<text x="340" y="352" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">总计 491 亿 token——不到从头训练的 1%</text>
<text x="340" y="378" text-anchor="middle" font-size="16" fill="#4b5563">知识原封不动，换掉的只是读的方式。</text>
</svg>
<figcaption>图 2 —— 改造的两个阶段：先让新的字节部件学会跟冻住的核心对话，再把整个模型放在一起调。</figcaption>
</figure>

## 四台"手术"，结果如何

研究组一口气改了四个现成模型。艾伦研究所的 Olmo 3 7B 改成 Bolmo 7B，它的前辈 OLMo 2 1B 改成 Bolmo 1B，阿里的 Qwen3 8B 改成 Bwen 8B，Meta 的 Llama 3 8B 改成 Blama 8B。改造后的模型和原来差不多大，参数量变化在 5% 以内。四个改造品全部开源，谁都可以去验，也可以拿别的基础模型照方抓药。

效果要说实话，形状是这样的：缺的那块补上了，其余的基本没掉。

在字符理解上——CUTE 和 EXECUTE 这两个基准测的正是按块读最容易翻车的那类字母功夫——改造后的模型赢了改造前的自己。有些编程测试上也比原版强，这很合理：代码就是单个字符说了算的文本。其他方面，在四十多个基准的大盘子里，改造品大多是追平原版，而不是反超。没有人声称换了读法模型就全面变聪明了。真正的说法是：字母这个盲区可以去掉，而其余能力基本原样保留——便宜地做到这一点，以前做不到。

和别的字节模型比，差距就拉开了。Bolmo 7B 对照的是 BLT 7B，Meta 出的、此前最强的同级字节模型，那是从零开始、花全价训练出来的。在一组 STEM（科学、技术、工程、数学）任务的汇总成绩上，Bolmo 7B 高出 16.5 个百分点。这个数字要小心读：它是一个汇总口径、一个对照对象。但方向很难反驳——花不到 1% 成本改造出来的，比花全价从头训的还好。四个改造品里最强的是 Bwen 8B，也就是拿 Qwen3 改的那个：除了通用问答一项，它在每个评估类别上都比原版有进步。

还有一件实事，可能和基准一样重要。开源世界真正跑起来的不是基础模型，是微调版——基于 Llama 和 Qwen 改出来的成千上万个版本，医疗的、法律的、编程的、客服的。如果一种改造要求这些工作全部重做，那它只是个展品。字节化不用重做。有一种叫"任务算术"的手法，说白了就是把"微调版减去基础版"得到的那个差值，再加到改造后的模型上——原来的指令跟随能力就这么搬过来了。整个微调生态跟着过河，沉没成本没有白花。

## 这件事为什么要紧

先从观念上说。十年了，分词器一直被当地基看待：训练之前定死，模型一辈子改不了，想改就得推倒重来。这篇论文说明，它更像眼镜。模型不需要重新学一遍知识，就能换一种看法。AI 里凡是被发现"原来是个可替换配件"的东西，从那天起都会变便宜、变得好试——现在，"读法"上了这份名单。

再说钱。从头预训练是这个行业最贵的东西，开源生态的价值就锁在那些各烧了一轮预训练的模型里。一种能用不到原成本 1% 的价格修好它们最明显的毛病、还把微调成果一并带走的办法，等于在保住这笔投资，而不是把它一笔勾销。现存的每个开源模型，原则上都是同一台手术的候选人。

再说公平，这一点看明白之后很好讲：字节对全世界每种语言都一样。按英文编的块词典并不中立，它给一些语言短而顺的读法，给另一些语言长而碎的读法，差别会变成价格，变成质量。逐字节的读者不问你喂进来的是哪种文字。这件事成不成另说，它至少拆掉了读法这一步自带的偏向——那是在任何训练数据开口之前就已经存在的偏向。

还有那些"意思就住在单个字符里"的活儿。一段基因序列不是一篇文章，改一个字母就是另一个分子。化学式、一行代码、一条法条引用、一份乐谱，都是这样。这些领域里，读不到字符的工具再聪明也是错的工具。字节化不会让模型变科学家，它做的是让"对的读法"便宜到可以当默认。

最后还有一层安静的影响。固定的词表给模型能表达的东西封了顶：输出端只有一本有限的词典时，某些文本分布在数学上就是表示不出来，研究者把这个上限叫 softmax 瓶颈。字节没有词典，也就没有这本会用完的清单。天花板拆了，不保证有人盖得更高，但天花板确实不在了。

## 该泼的冷水

论文自己很谨慎，复述的人也该谨慎。

第一，所有结果都是在 10 亿到 80 亿参数这个规模上做出来的。前沿模型大得多，这套改造在那个规模上灵不灵，论文里没有答案。第二，除了字符功夫，改造品在大多数通用基准上是追平原版，不是赢。第三，逐字节读意味着同样的文本要处理更多的单位，序列变长，而序列长正是速度的传统税。作者证明，用更高的压缩比训练（从字节流里切更大的块）可以把推理速度拉回有竞争力的水平，但论文给出的汇总里没有硬性的实际耗时数字，落到具体机器上要多付多少时间，还是个开放问题。第四，微调成果的搬运有条件：任务算术成立的前提是，微调版的词向量能重置回基础版的数值而不掉太多性能——作者说这一般成立，但不是永远成立。第五，那个最容易被引用的 16.5 个百分点，是一个汇总口径对一个对照对象，说明方向可以，当成大胜就过了。

定位也要摆正。随论文刊出的《自然》"新闻与观点"评论由北京大学的张昭和熊英飞撰写，他们的说法和局外人的直觉一致：这是一次改造，不是一个新模型——是给现成的系统补上一个结构上缺失的能力，花的是常规成本的一个零头。这个大小，正合适。

## 接下来等什么

下一个实验明摆着：规模。把某个远大于 80 亿参数的模型拿去字节化——艾伦研究所是最自然的人选，Bolmo 本来就是他们的——看这套配方还成不成立：主干保不保得住，字符上的进步在不在，速度那笔税还压不压得住。如果在大的规模上也成立，这步改造大概会变成开源模型的标准工序，模型发布之后顺手就做，像现在的量化和微调一样平常。

在那之前，strawberry 那个老梗换了性质。它过去是个笑话：世界上最聪明的系统，做不了小孩的数数题。现在它是一个有工程答案的问题：它们看不见字母，而现在有了一种便宜的办法让它们看见。

三个 r。模型缺的从来不是智商，是一双能看清小字的眼睛。

*论文：Minixhofer 等，“Retrofitting language models to operate over bytes”，Nature 658, 915–922 (2026)；arXiv 版本题为“Bolmo: Byteifying the Next Generation of Language Models”（[arXiv:2512.15586](https://arxiv.org/abs/2512.15586)）。评论：张昭、熊英飞，Nature News & Views，2026 年 10 月 7 日。*
