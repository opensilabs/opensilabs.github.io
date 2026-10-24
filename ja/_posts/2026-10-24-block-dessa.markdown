---
lng_pair: id_20261024_block-dessa
title: "一言も読まずに話すことを覚えたモデル"
author: OpenSI-Labs
category: research
tags: [Block, Dessa, speech-to-speech, full-duplex, voice AI, audio-only training]
date: 2026-10-24 07:00:00 -0700
img: /assets/img/posts/2026-10-24-block-dessa.png
meta_description: "BlockのDessaは人の会話の音声だけからゼロで学んだ全二重の音声対音声モデルで、テキストが言語能力の必須の土台だという前提に挑むが、いまの証拠はデモのみである。"
---

10月23日、BlockがDessaを発表した。一言も読まずに会話を覚えた音声モデルだ。テキストコーパスなし、事前学習済みモデルの土台なし。人の会話の録音だけから学んだ。研究責任者のラガヴァン・トゥライラトナムは音声の[「GPT-3モーメント」](https://panews.io/articles/01a16adb-b868-71d2-9020-e852cb11f62c)になりうると語る。

いまの音声アシスタントは三度の受け渡しのリレーだ。文字起こしが音声をテキストに変え、言語モデルが返答を書き、合成音声が読む。受け渡しのたびに、ためらいも皮肉もこぼれる。Dessaはこのリレーを一人の走者にまとめた。[音声が入り、音声が出る](https://aicoder.com/news/news-20261024-block-dessa-full-duplex-speech-model-trained-only-on-speech)。途中に文字起こしはない。しかも全二重で、話しながら聴き、割り込む。

<figure>
<div style="text-align:center">
<svg width="680" height="340" viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">バトンリレー vs 一人の走者</text>
<text x="170" y="58" font-size="14" font-weight="bold" text-anchor="middle">現在：音声→テキスト→音声</text>
<rect x="20" y="80" width="90" height="54" rx="8" fill="#2b6cb0"/>
<text x="65" y="111" font-size="14" fill="#fff" text-anchor="middle">あなたの声</text>
<rect x="135" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="180" y="111" font-size="14" fill="#fff" text-anchor="middle">文字起こし</text>
<rect x="250" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="295" y="111" font-size="14" fill="#fff" text-anchor="middle">テキストLLM</text>
<rect x="140" y="160" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="185" y="191" font-size="14" fill="#fff" text-anchor="middle">音声出力</text>
<text x="170" y="240" font-size="14" fill="#c53030" text-anchor="middle">抑揚・間・笑い：受け渡しのたびに失われる</text>
<text x="510" y="58" font-size="14" font-weight="bold" text-anchor="middle">Dessa：音声入力、音声出力</text>
<rect x="400" y="80" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="455" y="111" font-size="14" fill="#fff" text-anchor="middle">あなたの声</text>
<rect x="535" y="80" width="110" height="54" rx="8" fill="#276749"/>
<text x="590" y="111" font-size="14" fill="#fff" text-anchor="middle">Dessa</text>
<rect x="455" y="160" width="110" height="54" rx="8" fill="#276749"/>
<text x="510" y="191" font-size="14" fill="#fff" text-anchor="middle">音声の返答</text>
<text x="510" y="240" font-size="14" fill="#276749" text-anchor="middle">話しながら聴く：割り込み可能</text>
<line x1="110" y1="107" x2="135" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="225" y1="107" x2="250" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="295" y1="134" x2="230" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="535" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="590" y1="134" x2="510" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="510" y2="160" stroke="#a0aec0" stroke-width="2" stroke-dasharray="5,4"/>
</svg>
</div>
<figcaption style="text-align:center">左：音声をテキストに落として戻すたび、言葉以外が失われる。右：Dessaは信号全体を一つのモデルに保つ。</figcaption>
</figure>

問いは言語学習の前提だ。長年、テキストコーパスが必須の足場とされてきた。Dessaはその前提への挑戦だ。Blockによれば、学習に使った単語数はテキストLLMの[「数百分の一」](https://www.aichatdaily.com/ai-models/block-unveils-dessa-full-duplex-voice-model-trained-only)だという。会話1分の情報量は文字起こしより多い。学習はNVIDIA GB200 NVL72ラック1台だけ。推論はM4 Max以上で実時間より速いという。

Blockはこれを安全研究としても位置づける。いまの音声AIは感情に耳が聞こえない。早期アクセスは少数のAI安全研究者へ。ウェイティングリストは公開されたが、公開ウェイトも公開日もAPIも価格もまだない。

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">文字起こしが捨て去るもの</text>
<text x="340" y="58" font-size="14" text-anchor="middle">同じ言葉、違う意味――音にしか宿らないもの</text>
<rect x="40" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="130" y="108" font-size="14" text-anchor="middle">「本当に？」――平坦に</text>
<text x="130" y="130" font-size="14" text-anchor="middle">疑問</text>
<rect x="250" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="340" y="108" font-size="14" text-anchor="middle">「本当に？！」――上向きに</text>
<text x="340" y="130" font-size="14" text-anchor="middle">驚き、喜び</text>
<rect x="460" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="550" y="108" font-size="14" text-anchor="middle">「本当に。」――乾いた調子で</text>
<text x="550" y="130" font-size="14" text-anchor="middle">皮肉</text>
<text x="340" y="185" font-size="14" text-anchor="middle">さらに、間、笑い、ため息、割り込み、相づち――</text>
<text x="340" y="210" font-size="14" text-anchor="middle">テキストには記録されない会話の社会的な層。</text>
<text x="340" y="250" font-size="14" font-weight="bold" text-anchor="middle">Dessaは音そのものから学ぶ。だから何も捨てない。</text>
</svg>
</div>
<figcaption style="text-align:center">文字起こしが記録するのは言葉だけ。会話を動かすのはその周りのすべてだ。</figcaption>
</figure>

印象的な話はすべて、いまのところBlockの言葉とデモだ。パラメータ数、データセット規模、レイテンシの数値、正式なベンチマークは一つも公開されていない。「テキストを一切使わない」はBlockの説明で、未検証だ。[The Verge](https://dealroom.co/news/165548-jack-dorseys-block-unveils-dessa-a-full-duplex-voice-ai-trained-only-on/)は、Dessaが相手を「ロナウド」と取り違えたと指摘した。今日のDessaは注釈つきの存在証明だ。

その注釈こそ新視点だ。主張が検証に耐えれば、データ経済が変わる。テキストコーパスは有限で高価だ。人の会話は豊富で未転写が多い。音から学ぶモデルは、文書にならない話し言葉から学べる。主張が崩れても、訂正が境界を示す。言語のうちどれだけが言葉にあり、どれだけが声か。

*議論：音だけで言語を学べるなら、「言語を知る」とは何か――言葉か、その周りのすべてか？*
