---
lng_pair: id_20261028_nemotron-transcribe
title: "Nemotron 3.5 Transcribe: NVIDIA's 30B Speech Model That Wakes Only 4B Parameters at a Time"
author: OpenSI-Labs
category: research
tags: [NVIDIA, Nemotron, speech recognition, ASR, open weights, mixture of experts, diarization]
date: 2026-10-28 09:00:00 -0700
img: /assets/img/posts/2026-10-28-nemotron-transcribe.png
meta_description: "NVIDIA's open-weight Nemotron 3.5 Transcribe transcribes 40 languages, translates between English and 31, and runs on a single chip because only about 4B of its 30B parameters work on any given piece of audio. The headline numbers are NVIDIA's own — and the limits are real."
---

On October 28, 2026, NVIDIA released Nemotron 3.5 Transcribe, a speech model whose weights anyone can download and use commercially. It transcribes recorded audio in 40 languages, translates between English and 31 languages, takes recordings up to an hour long, and tells apart as many as eight speakers. The checkpoints sit on Hugging Face and ModelScope in three precisions (BF16, FP8, NVFP4), run under vLLM or NVIDIA's NeMo-Speech.cpp, and are also served as hosted endpoints by Baseten, DeepInfra and Simplismart.

The unusual part is that you can talk to it. Transcription is normally a fixed machine: audio in, text out. Here, a plain-language instruction picks the output style — a verbatim transcript that keeps every "um" and false start, or a cleaned one with the fillers dropped. You can hand it vocabulary to listen for, such as drug names or product names, and you can ask questions about what a recording says. It also performs diarization — labeling who spoke when — so a meeting comes back as a conversation rather than a wall of text.

## A 30B model that mostly sits idle

The headline size is 30 billion parameters. The working size is much smaller, because the model is a mixture of experts: it is built from many specialist sub-networks, and for each slice of audio a router wakes only a few of them while the rest sit idle and cost nothing on that pass. About 4 billion parameters are active at any moment. Capacity and running cost, normally welded together, come apart.

That is why one chip is enough — a Jetson AGX Thor robotics board, a DGX Spark desktop, or a Blackwell datacenter GPU. Artificial Analysis measured the model tied with Mistral's Voxtral Small for first place among open-weight speech models, at 2.8% on its AA-WER measure — while activating roughly 4B parameters against Voxtral's 24B.

<figure>
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="340" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">30B on the shelf, about 4B on the clock</text>
<text x="40" y="98" font-size="15" font-weight="700" fill="#374151">Total parameters: 30B</text>
<rect x="40" y="112" width="600" height="46" rx="8" fill="#cbd5e1"/>
<rect x="40" y="112" width="80" height="46" rx="8" fill="#0e7c86"/>
<text x="52" y="142" font-size="17" font-weight="700" fill="#ffffff">~4B</text>
<text x="140" y="142" font-size="15" fill="#374151">active per pass: ~4B</text>
<text x="640" y="142" text-anchor="end" font-size="15" fill="#374151">idle: ~26B</text>
<text x="40" y="212" font-size="16" fill="#374151">A router wakes a few expert sub-networks per slice of audio; the rest cost nothing.</text>
<text x="340" y="272" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">One chip is enough: Jetson AGX Thor · DGX Spark · Blackwell</text>
<text x="340" y="316" text-anchor="middle" font-size="26" font-weight="700" fill="#0e7c86">30B &#8594; ~4B</text>
</svg>
<figcaption>Figure 1 — Mixture of experts splits capacity from running cost: the model owns 30B parameters but pays for about 4B on each pass.</figcaption>
</figure>

## The scoreboard, with the label left on

The yardstick is word error rate: the share of words in a transcript that are wrong. Lower is better. NVIDIA reports that on the Hugging Face Open ASR Leaderboard's English track, Nemotron 3.5 Transcribe ranks first among open-weight models at 5.33% average word error rate, and on the multilingual track it posts 4.62% mean word error rate across seven languages, the lowest among the open models in its model card's comparison. For speaker attribution it reports a diarization error rate of 18.26%, the lowest across 21 languages on David AI's benchmark of 14 systems. Keep the attribution attached: those are NVIDIA's numbers, and nobody outside NVIDIA has reproduced them yet.

## The dataset may outlast the model

The same day brought Granary v2, NVIDIA's open speech dataset: 463,062 hours of speech in 48 languages, drawn from 16 corpora (version 1 covered 25 languages). Every recording ships with three transcript styles — fully verbatim, formatted (spelled-out numbers become digits), and clean. The audio itself is not in the download; the dataset is a manifest that points back to the original sources, each under its own license. Models get replaced every few months. Half a million hours of openly indexed speech, in 48 languages, is infrastructure other teams will build on for years.

## An afternoon of teaching

Speech models stumble on jargon, and NVIDIA's own demo shows both the stumble and the fix. On Eka Care's benchmark of Indian medical speech, the model out of the box was wrong on roughly a fifth to a third of words. A better prompt cut the errors substantially. Then fine-tuning — extra training on examples from the target domain — for about 14 GPU-hours on a single GB300 chip brought the word error rate on speakers the model had never heard from 22.44% down to 12.17%, roughly 45.8% fewer errors, ahead of dedicated baselines. The plain reading: a hospital or a law firm can teach this model its own vocabulary in an afternoon, on one chip.

<figure>
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="310" rx="14" fill="#f7f9fc"/>
<text x="340" y="50" text-anchor="middle" font-size="20" font-weight="700" fill="#111827">Teaching it medical speech, in three steps</text>
<rect x="40" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#1e3a5f" stroke-width="2"/>
<text x="130" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">Out of the box</text>
<text x="130" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#1e3a5f">22.44% word error rate</text>
<text x="130" y="208" text-anchor="middle" font-size="14" fill="#374151">on speakers never heard before</text>
<rect x="240" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#0e7c86" stroke-width="2"/>
<text x="330" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">A better prompt</text>
<text x="330" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#0e7c86">errors cut substantially</text>
<text x="330" y="208" text-anchor="middle" font-size="14" fill="#374151">no extra training</text>
<rect x="440" y="96" width="180" height="150" rx="10" fill="#ffffff" stroke="#b91c1c" stroke-width="2"/>
<text x="530" y="128" text-anchor="middle" font-size="15" font-weight="700" fill="#374151">Fine-tune: ~14 GPU-hours</text>
<text x="530" y="176" text-anchor="middle" font-size="17" font-weight="700" fill="#b91c1c">12.17% word error rate</text>
<text x="530" y="208" text-anchor="middle" font-size="14" fill="#374151">on a single GB300 chip</text>
<text x="222" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="422" y="180" text-anchor="middle" font-size="22" font-weight="700" fill="#6b7280">&#8594;</text>
<text x="340" y="292" text-anchor="middle" font-size="16" font-weight="700" fill="#111827">≈ 45.8% fewer errors — Eka Care benchmark of Indian medical speech (NVIDIA demo)</text>
</svg>
<figcaption>Figure 2 — On jargon-heavy medical speech, prompting helped and an afternoon of fine-tuning on one chip cut the error rate nearly in half.</figcaption>
</figure>

## What it cannot do

It reads files. There is no live streaming, so real-time captions and live voice agents are out of scope — and that half of the voice market had a busy month without it: ElevenLabs launched Realtime, Mistral shipped Voxtral 3, and Salesforce released Launa-Omni. For genuinely small jobs, NVIDIA's own Parakeet, at 1.1B parameters, remains the tiny sibling.

What changes here is ownership. Transcription is turning into something you run yourself instead of renting by the minute from an API — which means a hospital's or a boardroom's audio never has to leave the building. That matters most for exactly the recordings that most need transcribing, and are hardest to send away.
