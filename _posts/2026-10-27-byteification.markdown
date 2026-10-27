---
lng_pair: id_20261027_byteification
title: "Why Llama Can't Count the R's in 'Strawberry' — and the Nature Paper That Taught It To"
author: OpenSI-Labs
category: research
tags: [language models, tokenization, byte-level models, Nature, Llama, Qwen, Allen Institute for AI]
date: 2026-10-27 01:00:00 -0700
img: /assets/img/posts/2026-10-27-byteification.png
meta_description: "Ask a chatbot how many r's are in 'strawberry' and it often says two. There are three — but the model never sees the letters. A Nature paper from Ai2, LMU Munich, Cambridge and others shows how to retrofit Llama 3 and Qwen3 to read byte by byte, for under 1% of the cost of training them."
---

Ask a strong chatbot a question a six-year-old can answer: how many r's are there in "strawberry"?

The answer is three. Chatbots have a long record of saying two, and the mistake is not a failure of intelligence. It is a failure of eyesight. Before a language model reads anything you type, another piece of software chops your text into chunks called tokens. A token might be a whole short word, or a syllable-like fragment of a longer one. "Strawberry" might arrive at the model as two or three chunks — say, "straw", "ber", "ry". The model works with those chunks. The letters inside them are never shown to it at all.

So when you ask about the r's, the model is in the position of a person asked to count the windows in a house they have only ever seen as three sealed boxes. It can guess from memory. It cannot look. The chunks are the smallest thing it can see, and anything smaller — a single letter — is below its resolution.

This way of reading is called subword tokenization, and nearly every language model you have used does it. A paper published in *Nature* this month — by Benjamin Minixhofer and colleagues at LMU Munich, the Allen Institute for AI, the University of Cambridge, the University of Washington and Imperial College London — asks a simple question about it: what if the chopping is not permanent? What if a model that was trained to read in chunks could be taught, cheaply and after the fact, to read letter by letter instead? Their answer is a procedure they call byteification, and it works on models that already exist, including Meta's Llama 3 and Alibaba's Qwen3.

## Why we chop text in the first place

Nobody chose tokens because they are elegant. They chose them because they are fast.

Reading letter by letter means reading a lot. A page of English is a few thousand letters; feed every one of them through a large neural network, one step at a time, and the computation balloons. Tokens compress the text. Frequent combinations — "the", "ing", the start of "strawberry" — collapse into single units, so the model spends its steps on units big enough to carry meaning. The whole modern era of language models was built on this compression. A fixed dictionary of chunks, decided before training begins, sits underneath GPT, Claude, Llama, Qwen and nearly everything else.

The blind spots come free with the compression. Spelling is hard when you cannot see letters. Counting is guesswork. Code suffers, because in code a single character is often the whole story — one bracket in the wrong place and the program does something else entirely. Genetic sequences suffer for the same reason: swap one letter in a stretch of DNA and you may have changed what it does. And there is a quieter unfairness baked in. The chunk dictionaries were built mostly on English. Languages whose words fragment badly under those dictionaries get chopped into many more tokens for the same sentence — which means they cost more to process and are handled worse. Same sentence, higher bill, clumsier reading. The tax depends on what language you happen to write in.

None of this was a secret. Researchers have long built models that read raw bytes instead — a byte being the smallest unit a computer stores, roughly one per letter for English text. A byte-level model sees everything: every letter, every space, every bracket. It cannot be fooled by "strawberry", because there is nothing between it and the letters. The trouble is that these models kept losing. Trained from scratch, they lagged behind the chunk-reading models of the same size, and training one costs the same fortune as training any large model. So byte reading stayed a research curiosity, and the rest of the field kept its sealed boxes.

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="48" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">Two ways of reading “strawberry”</text>
<text x="40" y="92" font-size="16" font-weight="700" fill="#475569">TOKEN READING — today's models</text>
<rect x="40" y="106" width="180" height="52" rx="10" fill="#94a3b8"/>
<rect x="236" y="106" width="150" height="52" rx="10" fill="#94a3b8"/>
<rect x="402" y="106" width="110" height="52" rx="10" fill="#94a3b8"/>
<text x="130" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">straw</text>
<text x="311" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">ber</text>
<text x="457" y="140" text-anchor="middle" font-size="19" font-weight="700" fill="#ffffff">ry</text>
<text x="528" y="140" font-size="16" fill="#475569">letters hidden</text>
<text x="40" y="212" font-size="16" font-weight="700" fill="#166534">BYTE READING — after byteification</text>
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
<text x="340" y="302" text-anchor="middle" font-size="16" fill="#4b5563">Chunks hide the letters inside them. Bytes put every letter on the table.</text>
</svg>
<figcaption>Figure 1 — A token reader meets “strawberry” as a few sealed chunks; a byte reader meets all ten letters, and the three r's can simply be counted.</figcaption>
</figure>

## Surgery, not a rebuild

The move the *Nature* paper makes is to stop treating the reading method as part of the model's foundations. In their picture, a trained model has two separable parts. There is the core — the big transformer stack in the middle, which holds nearly everything the model knows about language, facts and reasoning. And there is the reading apparatus around it: the parts that turn raw text into something the core can work on, and turn the core's output back into text. Byteification replaces the reading apparatus and leaves the core — the expensive part, the part that took a full pretraining run to build — almost entirely alone.

Think of it as changing how a person reads rather than what they know. The knowledge stays. The eyes change.

The replacement parts are a small local encoder that reads the incoming bytes, a component called a boundary predictor that decides where one meaningful chunk ends and the next begins, a local decoder, and the output head that produces bytes at the other end. The core in the middle — the authors call it the global transformer — receives, for each chunk the boundary predictor carves out, a summary built from the actual bytes. The core still thinks in chunks. It just gets chunks that were cut from real letters, by a reader that saw them.

Training this hybrid happens in two stages, and the first stage is the clever one. The authors freeze the core completely — not one of its weights is allowed to move — and train only the new parts around it. The training signal is exact distillation: the new front end is taught to feed the frozen core representations that make it behave as it did before, as if nothing about its input had changed. In plain language, the new eyes learn to speak the old brain's language before anyone asks the brain to adjust. This stage uses 9.8 billion tokens of text.

Then, in stage two, everything is unfrozen and the whole model is fine-tuned together, end to end, on a further 39.3 billion tokens, mostly from Dolma 3, the Allen Institute's open training corpus, plus 75 million synthetic tokens built specifically to teach character-level skills — spelling, counting, letter manipulation. Total bill: 49.1 billion tokens. The authors put that at less than 1% of what training a model of this size from scratch normally costs. Under 1% to change how a finished model reads.

One design detail deserves a paragraph of its own, because the authors identify it as a large part of why earlier byte models lost. When a byte reader cuts a stream of letters into chunks, it has to decide where to cut while reading left to right. Earlier designs made that decision causally — looking only at the bytes already seen. The boundary predictor in this paper is allowed a peek: when deciding whether a chunk ends here, it may look at one byte of the future. One byte sounds like nothing. It is the difference between deciding where a word ends while blindfolded and deciding with a glance at the next letter — the glance tells you whether "ry" completes "strawberry" or starts something new. The authors argue that this small look-ahead closes much of the expressivity gap that held byte models back. Their design borrows the shape of the strongest earlier byte model, Meta's Byte Latent Transformer, and adds the peek.

<figure>
<svg width="680" height="400" viewBox="0 0 680 400" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="380" rx="14" fill="#f7f9fc"/>
<text x="340" y="46" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">Byteification: two stages, one small bill</text>
<rect x="30" y="66" width="620" height="128" rx="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
<text x="48" y="94" font-size="17" font-weight="700" fill="#1e40af">STAGE 1 — teach the new eyes · 9.8B tokens</text>
<rect x="48" y="108" width="128" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="112" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">byte encoder</text>
<rect x="186" y="108" width="196" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="284" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">boundary predictor*</text>
<rect x="392" y="108" width="140" height="40" rx="8" fill="#e5e7eb" stroke="#6b7280" stroke-width="2"/><text x="462" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#374151">core: FROZEN</text>
<rect x="542" y="108" width="92" height="40" rx="8" fill="#ffffff" stroke="#2563eb" stroke-width="2"/><text x="588" y="134" text-anchor="middle" font-size="16" font-weight="700" fill="#1f2937">decoder</text>
<text x="48" y="176" font-size="16" fill="#1f2937">*may peek 1 byte ahead when deciding where to cut · only the new parts train</text>
<rect x="30" y="208" width="620" height="104" rx="12" fill="#dcfce7" stroke="#16a34a" stroke-width="2"/>
<text x="48" y="236" font-size="17" font-weight="700" fill="#166534">STAGE 2 — tune everything together · 39.3B tokens</text>
<text x="48" y="266" font-size="16" fill="#1f2937">Core unfrozen; the whole model is fine-tuned end to end,</text>
<text x="48" y="290" font-size="16" fill="#1f2937">with 75M extra synthetic tokens that drill character skills.</text>
<text x="340" y="352" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">Total: 49.1B tokens — under 1% of a from-scratch run</text>
<text x="340" y="378" text-anchor="middle" font-size="16" fill="#4b5563">The model's knowledge is kept. Only its way of reading is replaced.</text>
</svg>
<figcaption>Figure 2 — The retrofit in two stages: first the new byte-level parts learn to talk to the frozen core, then the whole model is tuned together.</figcaption>
</figure>

## Four models, converted

The team applied the recipe to four open models. Olmo 3 7B, from the Allen Institute, became Bolmo 7B. Its smaller predecessor OLMo 2 1B became Bolmo 1B. Qwen3 8B Base became Bwen 8B, and Llama 3 8B became Blama 8B. The converted models are nearly the same size as the originals — parameter counts move by less than 5% in either direction — and the whole family is openly released, so anyone can check the claims or repeat the surgery on another patient. That the patients include two of the most widely used open model families in the world — Llama and Qwen — is part of the point: the demonstration was run where the open ecosystem actually lives.

What do the converted models actually do? The honest summary is: they gain the thing they were missing, and they keep almost everything else.

On character understanding — tested on the CUTE and EXECUTE benchmarks, which probe exactly the letter-level skills that chunk readers fumble — the byteified models beat the very models they were converted from. On some coding evaluations they also come out ahead of their sources, which fits the story: code is text where single characters carry weight. Elsewhere, across a broad spread of more than 40 benchmarks, they mostly approach their subword sources rather than surpassing them. That is the real shape of the result. Nobody is claiming a byteified model is suddenly smarter across the board. The claim is that the letter blind spot can be removed while the rest of the model's ability stays essentially intact — and that used to be the part nobody could do cheaply.

The comparison against other byte models is sharper. Bolmo 7B was measured against BLT 7B, Meta's byte-level model and the strongest previously published one of comparable size, which was trained from scratch at full pretraining cost. On an aggregate of STEM tasks, Bolmo 7B beat it by 16.5 percentage points. Read that number carefully: it is one aggregate, against one baseline. But the direction is hard to argue with — the retrofit, at under 1% of the training cost, produced a better byte-level model than the expensive from-scratch route did. Of the four conversions, Bwen 8B, the one built from Qwen3, was the strongest: it improved on its source model in every evaluation category except one, general question answering.

There is a practical bonus that may matter as much as the benchmarks. The open-model world does not run on base models; it runs on fine-tunes — the thousands of versions of Llama and Qwen that people have adapted for medicine, law, coding, customer support, everything. A conversion method that forced all of that work to be redone would be a curiosity. Byteification does not. Using a technique called task arithmetic — essentially, adding the difference between a fine-tuned model and its base back onto the converted model — the instruction-following of the original fine-tunes carries over to the byteified versions. The ecosystem transfers. The sunk work survives the surgery.

## Why this matters, stated plainly

Start with the idea that quietly changes status in this paper. For a decade, the tokenizer has been treated as part of a model's foundation: fixed before training, identical for the model's whole life, unchangeable afterwards without starting over. Byteification shows it behaves more like a pair of glasses. The model does not have to be re-taught what it knows in order to see differently. Anything in AI that turns out to be a replaceable attachment rather than a foundation stone gets cheaper and easier to experiment with from that day on — and reading, of all things, is now on that list.

Then the economics. Full pretraining runs are the most expensive objects in the field; the open ecosystem's value is locked inside models that each cost one. A method that upgrades those models' most obvious defect for under 1% of their original cost — and carries their fine-tunes along — is a way of protecting that investment rather than writing it off. Every existing open model is, in principle, a candidate for the same operation.

Then the fairness point, which is easy to state once you see it. A byte is a byte in every language on Earth. The chunk dictionaries that English-centric tokenizers use are not neutral: they give some languages short, efficient readings and others long, fragmented ones, and the difference shows up in price and in quality. A reader that works from bytes does not care which script it was fed. Whatever else byte-level models do, they remove a bias that was built into the reading step itself, before any training data had a say.

Then the work where characters are the content. A gene sequence is not a paragraph; change one letter and you have a different molecule. A chemical formula, a line of code, a legal citation, a musical score — in all of these, the meaning lives at the level of single characters, and a reader that cannot see characters is the wrong instrument, however smart it is. Byteification does not make models into scientists. It makes the right kind of reader cheap enough to be the default.

And one more, quieter point. A fixed vocabulary puts a ceiling on what a model can express: with a finite dictionary of output chunks, some distributions over text simply cannot be represented exactly — a limit researchers call the softmax bottleneck. Bytes have no dictionary. There is no fixed list to run out of. Removing the ceiling does not guarantee anyone builds higher, but the ceiling is gone.

## The honest limits

The paper is careful, and a fair account should be too.

Everything here was demonstrated at 1 to 8 billion parameters. Frontier models are far larger, and nothing in the paper shows the retrofit behaves the same at that scale. The gains, beyond character skills, are parity rather than victory: on most general benchmarks the converted models approach their sources, they do not beat them. Reading byte by byte also means longer sequences — more units to process for the same text — and longer sequences are the classic tax on speed. The authors show that training with higher compression ratios (bigger chunks cut from the byte stream) can bring inference speed back to competitive levels, but the paper's headline summaries offer no hard wall-clock numbers, so the real-world speed cost on a given setup is an open question. The fine-tune transfer has a condition attached, too: task arithmetic works when the fine-tune's embeddings can be reset to the base model's values without a large performance loss. The authors say this holds generally, but not always. And the 16.5-point STEM figure, the number most likely to be quoted, is one aggregate against one baseline — evidence of direction, not a rout.

There is also the framing to keep straight. Zhang and Xiong, writing the *Nature* News & Views commentary that accompanied the paper, put the contribution the way an outsider would: a retrofit, not a new model — a way to give existing systems a capability they structurally lacked, at a small fraction of the usual cost. That is exactly the right size for the claim.

## What to watch

The obvious next experiment is scale. Someone — the Allen Institute is the natural candidate, since Bolmo is theirs — byteifies a model much larger than 8 billion parameters and reports whether the recipe still holds: whether the core stays intact, whether the character gains survive, whether the speed tax stays manageable. If it holds at scale, expect the conversion to become a standard step, something open models simply undergo after release, the way they now get quantized and fine-tuned as a matter of routine.

Until then, the strawberry test has a new status. It used to be a joke about how the smartest systems in the world could not do a child's counting task. It is now a question with an engineering answer: they could not see the letters, and now there is a cheap way to let them. Three r's. The model just needed to be able to look.

*Paper: Minixhofer et al., “Retrofitting language models to operate over bytes”, Nature 658, 915–922 (2026); arXiv version: “Bolmo: Byteifying the Next Generation of Language Models” ([arXiv:2512.15586](https://arxiv.org/abs/2512.15586)). Commentary: Zhang & Xiong, Nature News & Views, 7 October 2026.*
