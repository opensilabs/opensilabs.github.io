---
lng_pair: id_20261024_block-dessa
title: "没读过一个字，却学会了说话"
author: OpenSI-Labs
category: research
tags: [Block, Dessa, speech-to-speech, full-duplex, voice AI, audio-only training]
date: 2026-10-24 07:00:00 -0700
img: /assets/img/posts/2026-10-24-block-dessa.png
meta_description: "Block 的 Dessa 是只凭人类对话音频从零训练的全双工语音到语音模型，演示惊艳，但目前的证据也只有演示。"
---

10月23日，Jack Dorsey 的 Block 发布了 Dessa，一个离经叛道的语音模型：它学会对话，却从未读过一个字——没有文本语料，没有预训练模型打底，只有人的对话录音，从零训练。负责人 Ragavan Thurairatnam 更视之为语音领域的[“GPT-3 时刻”](https://panews.io/articles/01a16adb-b868-71d2-9020-e852cb11f62c)。

今天的语音助手是一场三棒接力：你说话，它转写成文字，模型写回复，合成器再念出来。每次交接都有损耗：犹豫、笑声、语调、讽刺尽失。Dessa 把接力压成单人：音频进，音频出，中间没有转写环节，是 Block 所说的[“真正的语音到语音模型”](https://aicoder.com/news/news-20261024-block-dessa-full-duplex-speech-model-trained-only-on-speech)。它还是全双工的，边说边听：可被打断，也会“嗯”一声表示跟进。演示里，它会句中发笑，对意外的巴黎之行报以哽咽般的感激。

更深的冲击不在音质，而在语言能力由什么构成：业界默认文本语料是必需的脚手架。Dessa 直接挑战这一假设：Block 称它所见的词比文本大模型[少几百倍](https://www.aichatdaily.com/ai-models/block-unveils-dessa-full-duplex-voice-model-trained-only)，因为一分钟对话的信息远多于转写。孩子先说话、多年后才识字，Block 团队想验证模型能否也如此。训练只用了一台 NVIDIA GB200 NVL72 机柜，推理在 MacBook Pro M4 Max 及以上机型本地快于实时，无需云端往返。

Block 把它定位为安全研究而非单纯产品：今天的语音 AI 几乎听不懂情绪，无法回应求助者的急切。早期使用权先给一小批安全研究者，公开候补已开放，尚无发布日期、接口与定价。

但诚实账本比往常更重要：目前所有亮点都建立在 Block 自述与自选演示上。参数量、数据集规模、延迟、正式基准，一项都未公布；“完全不用文本”只是 Block 的说法，未经独立验证。演示也并非完美：[The Verge](https://dealroom.co/news/165548-jack-dorseys-block-unveils-dessa-a-full-duplex-voice-ai-trained-only-on/)发现它大多自然，偶尔尴尬——有一次把对话对象认成了“罗纳尔多”。演示是制作者挑给你看的表演，不是评测。今天正确的读法是带星号的存在性证明：仅凭语音似乎能走这么远，仍待他人独立核查。

星号本身就是新意。如果说法经得起核查，数据经济学将改变：文本语料有限、官司缠身、日益昂贵，而人类对话取之不尽、不断新生、大多从未被转写。从声音学习的模型能从电话、会议、睡前故事继续进步。若说法站不住——实为“悄悄用了一点”——纠正本身也有价值：它将标出纯语音学习的边界。无论结果如何，Dessa 都逼出了业界回避已久的问题：语言里有多少在词语中，又有多少在声音里？

<figure>
<div style="text-align:center">
<svg width="680" height="340" viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">接力赛 vs. 单人全程</text>
<text x="170" y="58" font-size="14" font-weight="bold" text-anchor="middle">今天：语音 → 文字 → 语音</text>
<rect x="20" y="80" width="90" height="54" rx="8" fill="#2b6cb0"/>
<text x="65" y="111" font-size="14" fill="#fff" text-anchor="middle">你的声音</text>
<rect x="135" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="180" y="111" font-size="14" fill="#fff" text-anchor="middle">转写文本</text>
<rect x="250" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="295" y="111" font-size="14" fill="#fff" text-anchor="middle">文本大模型</text>
<rect x="140" y="160" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="185" y="191" font-size="14" fill="#fff" text-anchor="middle">语音输出</text>
<text x="170" y="240" font-size="14" fill="#c53030" text-anchor="middle">语气、节奏、笑声：每次交接都会丢失</text>
<text x="510" y="58" font-size="14" font-weight="bold" text-anchor="middle">Dessa：音频进，音频出</text>
<rect x="400" y="80" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="455" y="111" font-size="14" fill="#fff" text-anchor="middle">你的声音</text>
<rect x="535" y="80" width="110" height="54" rx="8" fill="#276749"/>
<text x="590" y="111" font-size="14" fill="#fff" text-anchor="middle">Dessa</text>
<rect x="455" y="160" width="110" height="54" rx="8" fill="#276749"/>
<text x="510" y="191" font-size="14" fill="#fff" text-anchor="middle">口头回复</text>
<text x="510" y="240" font-size="14" fill="#276749" text-anchor="middle">边说边听：可以被打断</text>
<line x1="110" y1="107" x2="135" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="225" y1="107" x2="250" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="295" y1="134" x2="230" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="535" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="590" y1="134" x2="510" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="510" y2="160" stroke="#a0aec0" stroke-width="2" stroke-dasharray="5,4"/>
</svg>
</div>
<figcaption style="text-align:center">左：今天的助手把语音压成文字再还原，丢掉词语之外的一切。右：Dessa 把完整信号留在同一模型里，而且边说边听。</figcaption>
</figure>

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">转写文本会丢掉什么</text>
<text x="340" y="58" font-size="14" text-anchor="middle">同样的话，不同的意思——只存在于声音里</text>
<rect x="40" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="130" y="108" font-size="14" text-anchor="middle">“真的？”——平直</text>
<text x="130" y="130" font-size="14" text-anchor="middle">一个问题</text>
<rect x="250" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="340" y="108" font-size="14" text-anchor="middle">“真的？！”——上扬</text>
<text x="340" y="130" font-size="14" text-anchor="middle">不信、惊喜</text>
<rect x="460" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="550" y="108" font-size="14" text-anchor="middle">“真的。”——干巴巴</text>
<text x="550" y="130" font-size="14" text-anchor="middle">讽刺</text>
<text x="340" y="185" font-size="14" text-anchor="middle">还有：停顿、笑声、叹息、打断、附和声——</text>
<text x="340" y="210" font-size="14" text-anchor="middle">对话的社会层面，文字从不记录。</text>
<text x="340" y="250" font-size="14" font-weight="bold" text-anchor="middle">Dessa 直接从声音本身学习，所以这些都不会被丢弃。</text>
</svg>
</div>
<figcaption style="text-align:center">转写只记录词语，对话运转靠词语周围的一切——这正是纯音频模型学习的东西。</figcaption>
</figure>

*讨论：如果模型仅凭声音就能学会语言，“掌握一门语言”到底指什么——词语，还是词语周围的一切？*
