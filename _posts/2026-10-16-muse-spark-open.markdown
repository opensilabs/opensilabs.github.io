---
lng_pair: id_20261016_muse_spark_open
title: "Muse Spark Open: The 816B Model That Fits on a Desk"
author: OpenSI-Labs
category: models
tags: [open weights, mixture of experts, Meta, Apple, MLX]
date: 2026-10-16 06:00:00 -0700
img: /assets/img/posts/2026-10-16-muse-spark-open.png
meta_description: "Meta's 816B-parameter open-weight model runs on two Mac Studios — the real story is a systems breakthrough against the memory wall, plus a license with teeth."
---

On October 15, Meta did something it spent the spring refusing to do: it published the weights. Muse Spark Open — 816 billion parameters, 42 billion active per token, a million-token context window — is, in Meta's words, "the most capable U.S. open-weight model to date." You can download it from Hugging Face today. [\[1\]](https://www.macrumors.com/2026/10/15/meta-muse-spark-open-mac-studio/) [\[2\]](https://particle.news/story/meta-releases-muse-spark-open-and-partners-with-apple-to-run-it-on-m5-ultra-macs)

But the weights are only half the story. The other half is the desk. Meta worked with Apple to tune the model for MLX, Apple's machine-learning framework, and demonstrated it running on two Mac Studios with M5 Ultra chips — two desktop computers behaving, in Meta's phrase, "like one supercomputer with a terabyte of unified memory." A frontier-scale model, running locally, on hardware you can order. That sentence would have been absurd two years ago. It is worth asking what changed.

## Sparsity meets fat pipes

The 816-billion number is doing marketing work; the 42-billion number is doing the engineering work. Muse Spark Open is a mixture-of-experts model: for each token, a routing network wakes up only a small subset of "expert" sub-networks — roughly five percent of the total parameters. Picture a library of 816 billion books where each question sends you to exactly one aisle. You own the whole library, but you only ever carry an armful.

<svg viewBox="0 0 640 220" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Mixture-of-experts sparsity diagram" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,sans-serif" fill="#1a1a1a">Only ~5% of parameters fire per token</text>
  <g font-family="system-ui,-apple-system,sans-serif">
    <rect x="40" y="60" width="560" height="70" rx="8" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="60" y="88" font-size="14" fill="#444">816B total parameters (all experts)</text>
    <text x="60" y="112" font-size="14" fill="#444">dormant until routed</text>
    <rect x="40" y="150" width="560" height="40" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <rect x="40" y="150" width="29" height="40" rx="8" fill="#2f6df6"/>
    <text x="80" y="176" font-size="14" fill="#1a1a1a">42B active per token</text>
    <text x="470" y="176" font-size="14" fill="#555">router picks the aisle</text>
  </g>
</svg>
*Figure 1: Mixture-of-experts sparsity — the router wakes a thin slice of the model per token, so per-token compute stays at the 42B scale.*

That sparsity is what makes the memory math survivable. At low precision, 816 billion parameters need on the order of a terabyte of memory to sit in — and this is where Apple's hardware enters. Each M5 Ultra Mac Studio offers up to 512 GB of unified memory that the GPU addresses directly, with no copying between CPU and GPU memory (the tax every discrete-GPU setup pays), and 1.2 TB/s of bandwidth. Two Studios pool a terabyte. Because only a thin slice of parameters is touched per token, that bandwidth is enough to feed the active experts at usable speed. Sparse model, fat memory pipe, no discrete-GPU memory ceiling: the three constraints that kept 800B-class models in data centers all relaxed at once.

<svg viewBox="0 0 640 240" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Unified memory pooling diagram" style="width:100%;height:auto;display:block;margin:1em 0;">
  <text x="320" y="24" text-anchor="middle" font-size="17" font-weight="bold" font-family="system-ui,-apple-system,sans-serif" fill="#1a1a1a">Two desktops, one terabyte of memory</text>
  <g font-family="system-ui,-apple-system,sans-serif">
    <rect x="40" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="150" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 1</text>
    <text x="150" y="106" text-anchor="middle" font-size="14" fill="#444">512 GB unified memory</text>
    <text x="150" y="130" text-anchor="middle" font-size="14" fill="#444">GPU reads it directly</text>
    <rect x="380" y="50" width="220" height="110" rx="10" fill="#eef1f6" stroke="#c9d2e0"/>
    <text x="490" y="80" text-anchor="middle" font-size="14" font-weight="bold" fill="#1a1a1a">Mac Studio 2</text>
    <text x="490" y="106" text-anchor="middle" font-size="14" fill="#444">512 GB unified memory</text>
    <text x="490" y="130" text-anchor="middle" font-size="14" fill="#444">1.2 TB/s bandwidth</text>
    <path d="M260 105 L360 105" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <path d="M380 135 L280 135" stroke="#2f6df6" stroke-width="3" marker-end="url(#arr)"/>
    <defs><marker id="arr" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><path d="M0,0 L8,4 L0,8 z" fill="#2f6df6"/></marker></defs>
    <rect x="180" y="185" width="280" height="36" rx="8" fill="#dbe7ff" stroke="#7aa2f7"/>
    <text x="320" y="209" text-anchor="middle" font-size="14" fill="#1a1a1a">1 TB pooled — holds the full 816B model</text>
  </g>
</svg>
*Figure 2: Pooled unified memory — two Studios behave as one machine with a terabyte of GPU-addressable memory, via MLX.*

This is the real technical story, and it is a systems story, not a model story. Training compute gets the headlines, but the binding constraint on *using* giant models has always been the memory wall — holding the weights close enough to the compute, and feeding them fast enough. Muse Spark Open matters less for its parameter count than as proof that the wall is being attacked from both sides: sparser models on one side, unified memory architectures on the other.

## The catch, and the strategy

Now the cold water. "Open-weight" is not "open source," and the gap matters. The Muse Model License demands prominent "Built with Muse Spark Open" attribution, and any company with over $20 million in revenue must notify Meta and sign a commercial agreement before offering the model as a service. Read that twice: the weights are free to download, but the commercial terms keep Meta in the loop on every serious deployment. This is openness as a distribution strategy — seed the ecosystem, own the standard, keep the toll booth. It is a cleverer playbook than either pure open source or pure closed API, and everyone building on open weights should understand which game they are in.

There is a second tell in the announcement's fine print. The superlative is "most capable *U.S.* open-weight model" — and Meta's own benchmarks show weaker coding scores than some leading Chinese open models. The open-weight frontier is multipolar now, and that adjective is doing load-bearing work.

And a third: "runs on your desktop" currently means two Mac Studios at over $10,000 each, in a 512 GB configuration Apple hasn't even started shipping — it arrives later this month. Desktop AI is real, and it is still a $20,000 proposition. Democratization is a direction, not a destination.

None of this diminishes the engineering. A million-context, 42B-active MoE with strong agentic and tool-use scores, running locally on pooled unified memory, is a genuine systems achievement — and the Apple–Meta détente behind it is itself a signal. "We're excited for mommy and daddy to be playing nice again," said Meta's AI chief Alexandr Wang. Two companies that usually fight agreed on one thing: the future they both want is one where frontier AI doesn't have to run on NVIDIA's stack.

**Discussion:** If the weights are open but the license keeps commercial control and the hardware costs $20,000, who exactly is this "open" for — and does that change how you build on it?
