---
lng_pair: id_20261021_memt10-memory-native-llm
title: "The Model That Stops Re-Reading Its Past"
author: OpenSI-Labs
category: LLMs
tags: [LLMs, memory, architecture, open weights, MemT]
date: 2026-10-21 00:00:00 -0700
img: /assets/img/posts/2026-10-21-memt10-memory-native-llm.png
meta_description: "MemT-1.0 builds memory into a language model's computation instead of re-streaming ever-longer context: history folded into a fixed memory state, transcript discarded."
---

Every large language model you have ever used has a strange habit: it re-reads its own past. Each turn of a long conversation, the entire transcript is fed back in, and every past token's key and value is re-examined to produce the next one. The filing cabinet grows with every exchange, and the bill — in memory and in delay — grows with it.

On October 19, 2026, a 74-author team calling itself the MemTensor Team [released MemT-1.0](https://arxiv.org/abs/2610.26825), a "memory foundation model" that proposes a different habit: don't carry the past. Digest it.

## Memory as part of the computation

MemT-1.0 augments selected Transformer blocks with a **native memory block** that runs *parallel* to ordinary attention. After each conversational turn, the history is folded into a bounded, dynamically evolving memory state through per-token updates — and then the plain-text transcript can be thrown away. Persistent state size is fixed: it does not grow as turns accumulate.

The paper's own framing is a provocation worth taking seriously. Reasoning was once external scaffolding bolted onto models; then it was internalized (the DeepSeek-R1 arc). Multimodality went the same way. MemT-1.0 argues that memory is next: not "how much context can we afford to re-stream," but "can memory become part of the computation itself?"

The update mechanism is borrowed from NVIDIA's [Gated DeltaNet-2](https://arxiv.org/abs/2605.22791) research. For each token, the memory state performs three operations: **erase** what the state already predicts (the delta rule corrects first), **write** the residual — only the genuinely new information gets committed — and **decay** with a learned forget factor. Crucially, erase and write are decoupled, so updating one stored association disturbs others less. An added "stable mechanism" keeps the recurrent state bounded over long trajectories.

<svg viewBox="0 0 720 430" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="How the native memory block works: each token triggers erase, write and decay updates to a fixed memory state, running parallel to attention.">
  <defs>
    <marker id="ef1a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="414" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">A memory block, parallel to attention</text>

  <rect x="24" y="64" width="196" height="180" rx="10" fill="#f2f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="122" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">Normal attention</text>
  <text x="122" y="122" text-anchor="middle" font-size="14" fill="#3d4f68">reads the full KV cache</text>
  <rect x="52" y="140" width="140" height="66" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="122" y="166" text-anchor="middle" font-size="14" fill="#8a4b4b">cabinet keeps growing</text>
  <text x="122" y="190" text-anchor="middle" font-size="14" fill="#8a4b4b">O(N) state</text>

  <rect x="262" y="64" width="196" height="180" rx="10" fill="#f6f3fb" stroke="#7b5fc8" stroke-width="2"/>
  <text x="360" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#3b2c66">Native memory block</text>
  <text x="360" y="122" text-anchor="middle" font-size="14" fill="#4c3d7d">erase &#8594; write &#8594; decay</text>
  <rect x="292" y="140" width="136" height="66" rx="6" fill="#ffffff" stroke="#7b5fc8" stroke-width="1.5"/>
  <text x="360" y="166" text-anchor="middle" font-size="14" fill="#4c3d7d">state stays fixed</text>
  <text x="360" y="190" text-anchor="middle" font-size="14" fill="#4c3d7d">O(1) state</text>

  <rect x="500" y="64" width="196" height="180" rx="10" fill="#f3faf3" stroke="#4e7d4e" stroke-width="2"/>
  <text x="598" y="94" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c442c">Output</text>
  <text x="598" y="122" text-anchor="middle" font-size="14" fill="#33502f">attention output</text>
  <text x="598" y="146" text-anchor="middle" font-size="14" font-weight="bold" fill="#2c442c">+</text>
  <text x="598" y="170" text-anchor="middle" font-size="14" fill="#33502f">memory attention output</text>
  <text x="598" y="200" text-anchor="middle" font-size="14" font-style="italic" fill="#33502f">added together</text>

  <line x1="224" y1="150" x2="256" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#ef1a)"/>
  <line x1="462" y1="150" x2="494" y2="150" stroke="#6b5f45" stroke-width="2.5" marker-end="url(#ef1a)"/>

  <rect x="24" y="268" width="672" height="120" rx="10" fill="#fff8ec" stroke="#c9962e" stroke-width="2"/>
  <text x="360" y="298" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c4210">Per token, per turn: fold the past in, throw the transcript away</text>
  <text x="360" y="330" text-anchor="middle" font-size="14" fill="#6b5423">end of turn &#8594; history folded into memory state &#8594; plain text discarded</text>
  <text x="360" y="360" text-anchor="middle" font-size="14" font-weight="bold" fill="#3a3226">ablation: token-level granularity (&#8722;5.99) matters more than the update rule (&#8722;0.25)</text>
</svg>
Fig. 1: MemT-1.0's native memory block runs beside ordinary attention; each token erases what the state already predicts, writes only the residual, and the state never grows.

The most instructive finding is in the ablation table. Degrading updates from token-level to turn-level granularity costs 5.99 points on the memory average — but swapping Gated DeltaNet-2 for the plain DeltaNet costs only 0.25, and removing the stability mechanism only 0.54. **When you write matters far more than how you write.** That's a non-obvious result that should echo beyond this paper: the engineering leverage sits in the granularity of consolidation, not the cleverness of the update rule. It also lands closer to how brains work — iterative consolidation of experience — than to a filing cabinet anyone could build.

## The numbers, honestly labeled

Two tiers were released. **Nano** (36B total / 3B active, 10M-element memory state, built on Qwen3.6-35B-A3B; weights Apache-2.0) and **Flash** (288B / 17B active, 336M-element state, built on DeepSeek-V4-Flash with further post-training; weights MIT). Repo code is under a noncommercial license — the openness is layered, and an independent alert from [aiweekly](https://aiweekly.co/alerts/memt-10-memory-native-llms-cut-kv-storage-66x-at-128k-tokens) already caught the discrepancy between the paper's license and the weights. Worth knowing before you deploy.

On 11 memory benchmarks (from short MemBench conversations to the million-token BEAM-1M), Flash averages **50.60**, Nano **46.97** — +12.5 and +8.9 over the strongest *parametric* baseline. The efficiency claims are the striking part: at 128K tokens of history, persistent storage is ~66× lower than a full KV cache, and time-to-first-token for a new query is 2.44× faster (4.19× at 256K), staying flat at ~104–112ms no matter how long the history grows. Coding agents guided by experience stored in native memory gain +7.6/+8.3 on SWE-bench's strictest pass³ metric.

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Contrast: classic models re-stream a growing transcript each turn, while MemT-1.0 folds history into a fixed memory state and discards the transcript.">
  <defs>
    <marker id="ef2a" markerWidth="10" markerHeight="10" refX="8" refY="3" orient="auto"><path d="M0,0 L8,3 L0,6 Z" fill="#6b5f45"/></marker>
  </defs>
  <rect x="8" y="8" width="704" height="384" rx="12" fill="#fafafa" stroke="#999" stroke-width="1.5"/>
  <text x="360" y="42" text-anchor="middle" font-size="18" font-weight="bold" fill="#222">Stop re-streaming the past</text>

  <rect x="24" y="60" width="326" height="312" rx="10" fill="#faf0f0" stroke="#b07a7a" stroke-width="2"/>
  <text x="187" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#5c2c2c">Classic LLM: carry the past</text>
  <rect x="52" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="130" text-anchor="middle" font-size="14" fill="#5c2c2c">turn 1 &#183; turn 2 &#183; turn 3 &#183; ...</text>
  <rect x="52" y="152" width="270" height="54" rx="6" fill="#f3d9d9" stroke="#b07a7a" stroke-width="1.5"/>
  <text x="187" y="174" text-anchor="middle" font-size="14" fill="#5c2c2c">KV cache grows O(N)</text>
  <text x="187" y="196" text-anchor="middle" font-size="14" fill="#5c2c2c">every token re-read</text>
  <text x="187" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#8a2f2f">storage + latency keep rising</text>
  <text x="187" y="268" text-anchor="middle" font-size="14" fill="#5c2c2c">TTFT: 257ms @128K &#8594; 445ms @256K</text>
  <text x="187" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#7a5656">memory = the filing cabinet</text>

  <rect x="370" y="60" width="326" height="312" rx="10" fill="#f0f6fb" stroke="#5b7ba6" stroke-width="2"/>
  <text x="533" y="92" text-anchor="middle" font-size="17" font-weight="bold" fill="#2c3e55">MemT-1.0: digest the past</text>
  <rect x="398" y="108" width="270" height="34" rx="6" fill="#ffffff" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="130" text-anchor="middle" font-size="14" fill="#3d4f68">turn 1 &#8594; folded in &#183; discarded</text>
  <rect x="398" y="152" width="270" height="54" rx="6" fill="#d9e6f5" stroke="#5b7ba6" stroke-width="1.5"/>
  <text x="533" y="174" text-anchor="middle" font-size="14" fill="#2c3e55">memory state stays fixed O(1)</text>
  <text x="533" y="196" text-anchor="middle" font-size="14" fill="#2c3e55">query reads the state only</text>
  <text x="533" y="238" text-anchor="middle" font-size="14" font-weight="bold" fill="#1c4e80">66&#215; less storage @128K</text>
  <text x="533" y="268" text-anchor="middle" font-size="14" fill="#2c3e55">TTFT flat ~104&#8211;112ms &#183; 4.19&#215; @256K</text>
  <text x="533" y="298" text-anchor="middle" font-size="14" font-style="italic" fill="#55697f">memory = consolidated, like a brain</text>

  <text x="360" y="348" text-anchor="middle" font-size="14" fill="#6b5f45">the price: fixed-size memory trades fidelity &#8212; textual systems still score higher (68.5 vs 50.6)</text>
  <text x="360" y="372" text-anchor="middle" font-size="14" fill="#8a7d5c">all figures author-claimed; no independent replication yet</text>
</svg>
Fig. 2: The bet of the memory-native path — stop re-streaming history and fold it into the computation; cheaper and faster, at the cost of fidelity where exact evidence matters.

Now the honesty anchors, from the team's own materials: **textual/RAG systems still score substantially higher**, especially where exact evidence matters — MemOS at ~68.5 versus Flash's 50.6 on the same table. The authors state the trade plainly: fixed-size state buys cost at the price of fidelity; "preserving detailed evidence through recurrent memory updates" is the hard part. And every number above is author-claimed: as of tonight there is **zero independent replication**, no mainstream press, only an aiweekly fact-check and one dev.to editorial. Treat the benchmarks as a claim, not a verdict.

Deployment is practical: [SGLang-based inference](https://github.com/MemTensor/MemT-1.0) plus a Transformers quick-start, session state that can be saved and resumed as snapshot files. Two GPUs for Nano, eight for Flash. (Claims of vLLM or Docker support found no evidence in the repo — don't assume them.)

## One week, three attacks on the same cost

Zoom out and the timing is the story. This week saw three distinct bets on the same problem — that AI's memory is too expensive:

1. **Architecture**: MemT-1.0 puts memory *inside* the compute graph.
2. **Model as writer**: Tencent's Hy-Memory-30B-A3B (October 15, a separate and unrelated project) goes the opposite way — a model specialized at *writing to external* memory frameworks. Keep the memory outside; make the writer smart.
3. **Infrastructure**: DeepSeek open-sourced **DeepInfer** (October 20, Apache-2.0), its production inference stack — attacking the same cost at the systems layer.

The week's real question is which layer wins. And there is a lovely asymmetry to watch: DeepInfer targets DeepSeek-V4.1-Flash, while MemT-1.0-Flash's backbone is DeepSeek-V4-Flash — same family, same week, same cost pressure, not the same checkpoint. The memory revolution, if it comes, will arrive at every layer at once.

**The question to argue about:** if memory can be folded into a fixed state and the transcript thrown away, what happens to the idea — now central to agents — that an AI's past should remain *inspectable*? A compressed memory you can audit is a filing cabinet. A consolidated one you can only trust is something else entirely.
