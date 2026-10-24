---
lng_pair: id_20261022_recursive-flint
title: "40 Billion Parameters in Your Pocket"
author: OpenSI-Labs
category: research
tags: [Recursive, Flint, mixture-of-experts, open weights, local inference]
date: 2026-10-22 06:00:00 -0700
img: /assets/img/posts/2026-10-22-recursive-flint.png
meta_description: "Recursive's open-weights coding model Flint: 39.8B parameters, 2.5B active per token, 131 tokens/sec on a MacBook Pro — weights anyone can download, numbers anyone can check."
---

On October 21, Richard Socher's new company Recursive released its first model, Flint: a 39.8-billion-parameter mixture-of-experts (MoE) model that activates only about 2.5 billion parameters per token — just small enough to run on a MacBook Pro at [~131 tokens per second](https://teckhustlers.com/recursive-flint-local-coding-model/). The weights are on Hugging Face under Apache 2.0: download them, run them offline, modify them for commercial use, all free.

An MoE model works like a hospital triage desk. Instead of every specialist examining every patient, each request is routed to the few experts most relevant to it. Flint stacks 49 layers, 47 of them MoE; each layer hides 256 experts, and the router picks six per token, plus one always-on shared expert that carries the general knowledge every token needs. Compute follows the active parameters, not the total — so the model can hold 40 billion parameters of knowledge while doing the arithmetic of a 2.5-billion one. That is how a frontier-scale model fits inside a laptop.

<figure>
<div style="text-align:center">
<svg width="680" height="360" viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">Sparse routing: 256 experts, only 6+1 fire per token</text>
<rect x="30" y="150" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="85" y="181" font-size="14" fill="#fff" text-anchor="middle">Input token</text>
<rect x="170" y="150" width="110" height="54" rx="8" fill="#6b46c1"/>
<text x="225" y="181" font-size="14" fill="#fff" text-anchor="middle">Router</text>
<line x1="140" y1="177" x2="170" y2="177" stroke="#a0aec0" stroke-width="2"/>
<circle cx="330" cy="80" r="9" fill="#4a5568"/>
<circle cx="364" cy="80" r="9" fill="#4a5568"/>
<circle cx="398" cy="80" r="9" fill="#4a5568"/>
<circle cx="432" cy="80" r="9" fill="#4a5568"/>
<circle cx="466" cy="80" r="9" fill="#4a5568"/>
<circle cx="500" cy="80" r="9" fill="#4a5568"/>
<circle cx="534" cy="80" r="9" fill="#4a5568"/>
<circle cx="568" cy="80" r="9" fill="#4a5568"/>
<circle cx="330" cy="114" r="9" fill="#4a5568"/>
<circle cx="364" cy="114" r="9" fill="#4a5568"/>
<circle cx="398" cy="114" r="9" fill="#f6ad55"/>
<circle cx="432" cy="114" r="9" fill="#4a5568"/>
<circle cx="466" cy="114" r="9" fill="#4a5568"/>
<circle cx="500" cy="114" r="9" fill="#4a5568"/>
<circle cx="534" cy="114" r="9" fill="#4a5568"/>
<circle cx="568" cy="114" r="9" fill="#4a5568"/>
<circle cx="330" cy="148" r="9" fill="#4a5568"/>
<circle cx="364" cy="148" r="9" fill="#4a5568"/>
<circle cx="398" cy="148" r="9" fill="#4a5568"/>
<circle cx="432" cy="148" r="9" fill="#4a5568"/>
<circle cx="466" cy="148" r="9" fill="#4a5568"/>
<circle cx="500" cy="148" r="9" fill="#4a5568"/>
<circle cx="534" cy="148" r="9" fill="#f6ad55"/>
<circle cx="568" cy="148" r="9" fill="#4a5568"/>
<circle cx="330" cy="182" r="9" fill="#4a5568"/>
<circle cx="364" cy="182" r="9" fill="#4a5568"/>
<circle cx="398" cy="182" r="9" fill="#4a5568"/>
<circle cx="432" cy="182" r="9" fill="#4a5568"/>
<circle cx="466" cy="182" r="9" fill="#4a5568"/>
<circle cx="500" cy="182" r="9" fill="#f6ad55"/>
<circle cx="534" cy="182" r="9" fill="#4a5568"/>
<circle cx="568" cy="182" r="9" fill="#4a5568"/>
<circle cx="330" cy="216" r="9" fill="#4a5568"/>
<circle cx="364" cy="216" r="9" fill="#4a5568"/>
<circle cx="398" cy="216" r="9" fill="#4a5568"/>
<circle cx="432" cy="216" r="9" fill="#4299e1"/>
<circle cx="466" cy="216" r="9" fill="#4a5568"/>
<circle cx="500" cy="216" r="9" fill="#4a5568"/>
<circle cx="534" cy="216" r="9" fill="#4a5568"/>
<circle cx="568" cy="216" r="9" fill="#4a5568"/>
<circle cx="330" cy="250" r="9" fill="#4a5568"/>
<circle cx="364" cy="250" r="9" fill="#f6ad55"/>
<circle cx="398" cy="250" r="9" fill="#4a5568"/>
<circle cx="432" cy="250" r="9" fill="#4a5568"/>
<circle cx="466" cy="250" r="9" fill="#4a5568"/>
<circle cx="500" cy="250" r="9" fill="#4a5568"/>
<circle cx="534" cy="250" r="9" fill="#4a5568"/>
<circle cx="568" cy="250" r="9" fill="#4a5568"/>
<circle cx="330" cy="284" r="9" fill="#4a5568"/>
<circle cx="364" cy="284" r="9" fill="#4a5568"/>
<circle cx="398" cy="284" r="9" fill="#4a5568"/>
<circle cx="432" cy="284" r="9" fill="#4a5568"/>
<circle cx="466" cy="284" r="9" fill="#4a5568"/>
<circle cx="500" cy="284" r="9" fill="#4a5568"/>
<circle cx="534" cy="284" r="9" fill="#f6ad55"/>
<circle cx="568" cy="284" r="9" fill="#4a5568"/>
<circle cx="330" cy="318" r="9" fill="#4a5568"/>
<circle cx="364" cy="318" r="9" fill="#4a5568"/>
<circle cx="398" cy="318" r="9" fill="#4a5568"/>
<circle cx="432" cy="318" r="9" fill="#f6ad55"/>
<circle cx="466" cy="318" r="9" fill="#4a5568"/>
<circle cx="500" cy="318" r="9" fill="#4a5568"/>
<circle cx="534" cy="318" r="9" fill="#4a5568"/>
<circle cx="568" cy="318" r="9" fill="#4a5568"/>
<line x1="280" y1="177" x2="398" y2="114" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="534" y2="148" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="534" y2="284" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="364" y2="250" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="500" y2="182" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="432" y2="318" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<line x1="280" y1="177" x2="432" y2="216" stroke="#f6ad55" stroke-width="1.2" opacity="0.55"/>
<rect x="610" y="150" width="60" height="54" rx="8" fill="#2f855a"/>
<text x="640" y="181" font-size="14" fill="#fff" text-anchor="middle">→</text>
<text x="330" y="336" font-size="14" text-anchor="middle" fill="#cbd5e0">39.8B total params · ~2.5B active per token</text>
<circle cx="120" cy="300" r="8" fill="#f6ad55"/>
<text x="134" y="305" font-size="14" fill="#cbd5e0">6 routed</text>
<circle cx="300" cy="300" r="8" fill="#4299e1"/>
<text x="314" y="305" font-size="14" fill="#cbd5e0">1 shared expert</text>
</svg>
</div>
</figure>

The more interesting story is how Flint was built. Recursive says its automated research system, Eureka Machine, took part in "nearly every aspect": searching the space of expert configurations from a 35B/3B baseline down to the final 40B/2.5B split; compressing the output layer to 4 bits ([NVFP4](https://www.marktechpost.com/2026/10/21/recursive-flint-local-coding-model/)) against convention — output layers are usually kept at high precision because errors there corrupt every prediction — then distilling from a 16-bit teacher to claw the accuracy back to within 0.7 points; and writing a Metal megakernel for the M4 and M5 that fuses the entire decode forward pass into a single kernel, attacking the memory-bandwidth bottleneck that throttles token generation on Apple silicon. In under four months, a small team plus a fleet of agents went from zero to a shipping model.

Speed is the selling point. Recursive claims over 125 tokens per second on an M4 Pro MacBook Pro (~131 in its tests), over 150 on the 64GB RTX Spark — roughly double what comparable models manage. The Ollama quantized build is 23GB, and any Mac with 48GB of unified memory can run it. On benchmarks, Flint hits 74.2% on SWE-Bench Verified — real GitHub issues resolved, the best of any MoE under 50 billion parameters — but only 54.9% on Terminal-Bench 2.1, well behind the dense Qwen 3.8's 73.0%. The split is suggestive: strong at patching code, weaker at the open-ended agentic work a terminal demands. Context window: 262,144 tokens, recommended for use up to 256K.

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="17" font-weight="bold" text-anchor="middle">Tokens per second on MacBook Pro (M4 Pro)</text>
<text x="200" y="80" font-size="14" text-anchor="end" fill="#e2e8f0">Flint</text>
<rect x="215" y="60" width="332" height="30" rx="4" fill="#f6ad55"/>
<text x="555" y="81" font-size="14" fill="#e2e8f0">131</text>
<text x="200" y="135" font-size="14" text-anchor="end" fill="#e2e8f0">Gemma 4</text>
<rect x="215" y="115" width="175" height="30" rx="4" fill="#718096"/>
<text x="398" y="136" font-size="14" fill="#e2e8f0">69</text>
<text x="200" y="190" font-size="14" text-anchor="end" fill="#e2e8f0">Nemotron 3.5 Lightning</text>
<rect x="215" y="170" width="147" height="30" rx="4" fill="#718096"/>
<text x="370" y="191" font-size="14" fill="#e2e8f0">58</text>
<text x="340" y="278" font-size="14" text-anchor="middle" fill="#a0aec0">Data: Recursive's own tests, via TechCrunch</text>
</svg>
</div>
</figure>

There is also a quieter economics at work. At 131 tokens per second on hardware you already own, inference costs nothing marginal: no API bill, no data leaving the machine, no outage when the provider goes down. The trade is dependence on your own hardware — 48GB of unified memory is not cheap — and a model that, by its own maker's admission, needs more hand-holding than the giants. For a personal coding assistant, that trade looks increasingly worth making.

The real point hides in one word: verifiable. When a closed lab publishes a speed number, you take it on faith; there is nothing to download and no way to check. Flint's weights are public, so the 131 figure can be re-measured by anyone willing to buy an M4 Pro — open weights functioning as a market discipline that closed labs never have to face. Someone will run the public benchmark within days, and Recursive knows it. But [WIRED](https://startupfortune.com/recursive-says-ai-built-most-of-its-new-flint-coding-model/) flagged what Recursive doesn't advertise: all the benchmarks are self-reported, with no independent verification yet. Flint is a finished snapshot, not proof that a "self-improving research system" is actually improving — one good artifact says little about the loop that made it. And Recursive itself admits the model needs clearer instructions than the big closed ones.

When 40 billion parameters first move into the computer you carry around, does the power structure of who gets to write serious code move with them?

---

*Discussion: when every performance claim can be re-measured, how long can self-reported benchmark marketing survive?*
