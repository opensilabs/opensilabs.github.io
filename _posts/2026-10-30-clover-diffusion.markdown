---
layout: post
lng_pair: id_20261030_clover-diffusion
title: "Clover Writes in Blocks, Not Word by Word: DiffuSpace's 35B Diffusion Model Claims 73.6 on SWE-bench"
author: OpenSI-Labs
category: AI Models
tags: [diffusion language model, Clover, DiffuSpace, open weights, SWE-bench]
date: 2026-10-30 20:00:00 -0700
img: /assets/img/posts/2026-10-30-clover-diffusion.png
---

On October 28–29, 2026, a company called DiffuSpace released its first model, Clover-35B-A3B-Preview. It is a language model that does not write the way language models are supposed to write. The weights are on Hugging Face under the Apache 2.0 licence — some 69 GB in BF16, free to download. DiffuSpace calls Clover the strongest open diffusion language model released so far. Oddly, that is the checkable part of the launch. The headline benchmark score is not.

## A page of blanks, filled in any order

Every mainstream model since GPT produces text one token at a time, left to right. Each token — a word or word-piece — is chosen, written down, and never reconsidered: a bad word early forces everything after it to work around the mistake. The arrangement also caps speed, because token number 500 cannot exist until tokens 1 to 499 do.

Clover produces text in blocks of 32 tokens. A new block starts as 32 masked placeholders — blanks. The model reads the whole block at once, in both directions, and fills its most confident blanks, several at a time. With some blanks filled, neighbouring blanks get easier, and the next pass fills more. Once every blank is resolved, the block freezes and becomes part of the fixed text the next block builds on. Picture an editor with a draft full of gaps, writing in the certain words first — not a typist who can never go back.

<figure>
<img src="/assets/img/posts/2026-10-30-clover-diffusion-fig1.svg" alt="Two ways to write: one token at a time, or one block of 32 blanks">
<figcaption>Figure 1 — Autoregressive models commit to each token as they go; Clover starts from 32 blanks and fills the most confident positions first.</figcaption>
</figure>

## The filling rule

The decoding scheme is called LowConfidence. A blank gets filled when the model's confidence in its best guess passes a threshold, set by default to 0.95. If no blank clears the bar, the single most confident one is filled anyway, so a block can never stall. Defaults: block size 32, threshold 0.95.

Two details make this engineering, not sleight of hand. Inside a block, attention runs both ways, so a blank is informed by words on either side; the text before the block stays causal, so the model never previews blocks it has not written. And while a block is being resolved, the model can restrict its expert routing to a subset of experts shared across the whole block, so one block touches fewer distinct experts than free routing would.

<figure>
<img src="/assets/img/posts/2026-10-30-clover-diffusion-fig2.svg" alt="One block of 32 masked slots resolving over three rounds">
<figcaption>Figure 2 — A block resolves in rounds: positions whose confidence passes 0.95 are filled, and the finished block becomes the prefix for the next.</figcaption>
</figure>

## What is under the hood

Clover holds 35 billion parameters, about 3 billion of them active for any given token. It is a mixture-of-experts model: 40 layers, 256 routed experts with the top 8 consulted per token, plus one shared expert in every layer. The context window is 128K tokens, and the model handles text only.

It was not built from scratch. Clover derives from Alibaba's Qwen3.6-35B-A3B and keeps that model's hybrid backbone of Gated DeltaNet and full-attention layers. DiffuSpace's additions are the bidirectional block attention — extra learned parameters, including right-convolution weights, that let tokens inside a not-yet-finished block attend to each other while the finished prefix stays causal — plus block-diffusion inference and generation controls.

## A score that cannot be checked yet

DiffuSpace reports that Clover scores 73.6 on SWE-bench Verified, 51.7 on Terminal-Bench 2.1, and generates at 515 tokens per second on a single H200. For an open 35B model, those would be striking numbers.

Here is the problem, stated plainly: there is currently no way to verify the 73.6. An independent analysis published by Daily Inference on October 29 — its title is "73.6 on SWE-bench, and Not One Way to Check It Yet" — points out that the launch materials do not disclose the agent scaffold, the tools, the number of attempts, or the run settings behind the score. The weights can be inspected and the licence read; the result cannot be reproduced from what has been made public. So the 73.6 should be read as a claim printed on the box, not a measurement. The same applies to the other two numbers.

## Downloadable is not yet runnable

The weights being public also means less, for now, than the announcement suggests. As of this week, the only way to run Clover is through Hugging Face Transformers on a GPU with roughly 69 GB of memory. There is no GGUF build, so Ollama and LM Studio cannot load it, and SGLang support is not merged upstream. DiffuSpace recommends its own SGLang implementation for serving and evaluation, but the easy local paths are not there yet. Nobody is running this on a laptop this week.

The model card is candid about another rough edge: very long generations can drift into repetition. Clover therefore ships with countermeasures switched on by default — a presence penalty of 0.9, a repetition penalty of 1.05, and biases that push harder toward ending the response as it grows. It is, as the name says, a Preview.

## Why it matters anyway

One-token-at-a-time generation is the oldest habit in modern AI, and two of its limits come built in: speed is capped by writing in sequence, and early mistakes are locked in for good. Block diffusion attacks both at once. Filling blanks in parallel could be much faster, and a block can be shaped as a whole — every word aware of its neighbours — before any of it is fixed.

Clover is the strongest claim yet that this works at real scale: 35 billion parameters, agentic coding benchmarks, weights anyone can download and inspect. The mechanism is genuinely there, in the code. The score is a promissory note. If independent runs land anywhere near 73.6, the field's basic writing habit is in question. If they do not, Clover is still the most capable open diffusion model released so far — just not the revolution its launch post advertises.
