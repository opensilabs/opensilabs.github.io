---
lng_pair: id_20261020_ibm-agent-decoder
title: "For $26, AI Designed a Chip for a Quantum Computer"
author: OpenSI-Labs
category: research
tags: [AI chip design, quantum computing, agents, IBM, error-correction decoder]
date: 2026-10-20 03:30:00 -0700
img: /assets/img/posts/2026-10-20-ibm-agent-decoder.png
meta_description: "IBM's agent factory optimized a quantum error-correction decoder's hardware design — an open-weight model cut latency 52-fold for $26 in inference. AI is starting to design the hardware it runs on."
---

**What does twenty-six dollars buy?**

A paperback, roughly. A tank of gas, almost. Or, as of this month, a fifty-two-fold speedup of one of the most unforgiving components inside a quantum computer — engineered not by a design team billing by the week, but by a small society of AI agents that planned, coded, checked, and revised a hardware design on their own.

On October 13, 2026, IBM Research posted a preprint by Abhishek Bhandwaldar and colleagues describing what they built: an "agent factory" pointed at a quantum error-correction decoder. The decoder is the least glamorous and most load-bearing part of a fault-tolerant quantum machine. Qubits corrupt themselves continuously; errors accumulate on microsecond timescales, and the decoder's job is to infer what went wrong and correct it in real time, forever, without falling behind. Fall behind by a little and the computation dissolves into noise. IBM's entire roadmap to practical fault tolerance — including its Starling machine, slated for 2029 — runs through this component.

A word about the specific burden the agents were handed, because the details here are the story. The gross code — named, one suspects, with a straight face — encodes 12 logical qubits into 144 physical ones, with distance 12, meaning it can in principle absorb a healthy burst of errors before any logical information is lost. Relay-BP, the decoding algorithm IBM published in June 2025, reads the pattern of measurement outcomes, called a syndrome, and works out the most plausible error that produced it. That inference has to happen again and again, at the rhythm of the machine, for as long as the machine runs. A decoder is therefore not a batch job but a permanent reflex, and its latency is not a convenience metric; it is a hard budget written into the physics of the device. This is also why IBM is designing decoders at all, rather than buying the problem away: its fault-tolerance roadmap bets on qLDPC codes like this one, whose encoding efficiency is far better than the surface codes most rivals use, at the price of exactly this decoding difficulty. The reflex has to be custom-built, in hardware, and rebuilt every time the code or the machine changes.

The factory is organized like a miniature chip company. A coordinator agent plans the search and proposes optimization hypotheses. Four worker agents each rewrite the decoder's C++ kernel along the lines the coordinator suggests. A verifier agent checks every candidate for correctness — a fast design that computes the wrong answer is worthless. Survivors go to AMD's Vitis synthesis tool, which turns the high-level code into an actual circuit for a VU19P FPGA and reports back latency and area. The budget is 100 hypotheses: five rounds of twenty, with the coordinator reading each round's synthesis results to decide where the next round should push.

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">The agent factory: five roles, one pipeline</text>
<rect x="250" y="48" width="180" height="52" rx="8" fill="#2b6cb0"/>
<text x="340" y="70" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Coordinator</text>
<text x="340" y="90" font-size="14" text-anchor="middle" fill="#fff">plans · proposes</text>
<rect x="30" y="140" width="130" height="52" rx="8" fill="#4299e1"/>
<text x="95" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Workers ×4</text>
<text x="95" y="182" font-size="14" text-anchor="middle" fill="#fff">rewrite C++</text>
<rect x="200" y="140" width="130" height="52" rx="8" fill="#4299e1"/>
<text x="265" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Verifier</text>
<text x="265" y="182" font-size="14" text-anchor="middle" fill="#fff">checks truth</text>
<rect x="370" y="140" width="130" height="52" rx="8" fill="#4299e1"/>
<text x="435" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Synthesis</text>
<text x="435" y="182" font-size="14" text-anchor="middle" fill="#fff">Vitis → circuit</text>
<rect x="540" y="140" width="130" height="52" rx="8" fill="#2b6cb0"/>
<text x="605" y="162" font-size="14" font-weight="bold" text-anchor="middle" fill="#fff">Feedback</text>
<text x="605" y="182" font-size="14" text-anchor="middle" fill="#fff">latency · area</text>
<path d="M340 100 L95 132" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M160 166 L192 166" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M330 166 L362 166" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M500 166 L532 166" stroke="#718096" stroke-width="2" fill="none" marker-end="url(#a1)"/>
<path d="M605 140 L605 118 L440 118" stroke="#718096" stroke-width="2" fill="none" stroke-dasharray="4" marker-end="url(#a1)"/>
<defs><marker id="a1" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto"><path d="M0 0 L8 3 L0 6 Z" fill="#718096"/></marker></defs>
<text x="340" y="240" font-size="14" text-anchor="middle">5 rounds × 20 hypotheses = 100 attempts; each round is steered by the last</text>
<text x="340" y="266" font-size="14" text-anchor="middle" font-style="italic">organized like a tiny chip company: thinking costs, doing is cheap</text>
</svg>
</div>
<figcaption style="text-align:center">IBM's agent factory: the coordinator plans, workers rewrite code, the verifier guards correctness, synthesis produces a circuit, and the results steer the next round.</figcaption>
</figure>

IBM then ran the factory three times, changing nothing but which model sat in which chair:

<figure>
<div style="text-align:center">
<svg width="680" height="270" viewBox="0 0 680 270" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Three configurations, the same 100 attempts</text>
<text x="240" y="70" font-size="14" text-anchor="end">Claude Opus 5 everywhere</text>
<rect x="250" y="52" width="410" height="26" fill="#2b6cb0"/>
<text x="660" y="70" font-size="14">204× · $299</text>
<text x="240" y="116" font-size="14" text-anchor="end">Opus leads, GLM works</text>
<rect x="250" y="98" width="256" height="26" fill="#4299e1"/>
<text x="660" y="116" font-size="14">126× · $105</text>
<text x="240" y="162" font-size="14" text-anchor="end">GLM-5.3 everywhere (open)</text>
<rect x="250" y="144" width="107" height="26" fill="#90cdf4"/>
<text x="660" y="162" font-size="14">52× · $26</text>
<text x="340" y="210" font-size="14" text-anchor="middle">starting design: 28,231 µs · bar length ∝ speedup (log scale feel)</text>
<text x="340" y="238" font-size="14" text-anchor="middle">the all-open run costs 11.5× less; its best design is ~4× slower</text>
</svg>
</div>
<figcaption style="text-align:center">Three model configurations of IBM's agent factory. Latencies are HLS estimates; costs cover model inference only. Data: Bhandwaldar et al., IBM Research preprint, 2026-10-13.</figcaption>
</figure>

With Claude Opus 5 in every seat, the factory's best design ran at 139 microseconds against the reference design's 28,231 — a 204-fold speedup, bought with 215.9 million tokens and a $299.45 inference bill. The hybrid — Opus coordinating, the open-weight GLM-5.3 from Z.ai doing the coding — reached 223 microseconds, 126-fold, for $105.25. And with GLM-5.3 everywhere, the factory still found a 52-fold improvement, at 545 microseconds, for $25.95. That last run matters for a reason beyond thrift: IBM served the open model on its own fleet of 544 H100 GPUs through the llm-d inference framework, at $0.1077 per million tokens with a 98% prefix-cache hit rate. The all-open factory cost eleven and a half times less than the flagship one. Its best design was about four times slower. That is the trade on the table.

Two design choices in the experiment deserve more attention than the headline speedups, because they are what separate a factory from a chatbot with a compiler. The first is the budget: 100 hypotheses is nothing. A human design team exploring a decoder might sketch that many directions in a week of whiteboard arguments, and veteran architects carry priors about which twenty deserve silicon. The coordinator's real job was triage under scarcity — reading each round's latency and area reports, deciding which failures were informative and which directions deserved another twenty attempts. The second choice is the verifier's veto. Every candidate had to prove it still decoded correctly before synthesis was allowed to admire its speed; in agent systems generally, the difference between a demo and a tool is almost always a checker that cannot be sweet-talked. IBM's setup has one with formal authority, and that, more than any model choice, is the organizational idea worth stealing.

**The smart money is spent on command, not on hauling bricks**

Set the three runs side by side and the most interesting number is not 204. It is a line count.

IBM measured how much code each setup's workers actually changed. Opus workers rewrote a median of 515 lines per attempt. GLM workers working alone rewrote 428. But the hybrid's GLM workers — the ones who produced the 126-fold result — changed a median of only 197 lines, the fewest of any configuration, and still beat the all-GLM factory by a factor of two and a half. Working for a strong coordinator, the cheap model changed less and accomplished more. Working without one, it churned.

Read that asymmetry carefully, because it generalizes far beyond decoders. What decided these outcomes was apparently not how much code the workers produced, but who chose the hypotheses and who checked the results. Coordination and verification are judgment; rewriting a kernel along a specified line is execution. Put the expensive model where the judgment lives and execution can be had for a thirteenth of the price. If that pattern holds, it is not really a finding about chip design. It is the economics of every agent system anyone is about to build: intelligence belongs in the seats that decide and verify, and everything downstream of a good decision can be commoditized.

What did the agents actually fix, when they fixed the right things? The starting design kept the decoder's data in a lookup table. Every access went through an index first, and the synthesis tool, unable to predict which read would land in which memory bank, serialized them to be safe. The agents reorganized the memory layout — data indexed by check node and slot, split across separate banks so that 35 reads could proceed in parallel — and replaced a runtime-loop reduction with a fixed tree structure the tool could fully unroll. Two operations, both of them data-structure surgery of the kind a senior engineer performs after staring at a profiler: iteration cycles fell from 229,961 to 14,824. This was not knob-twiddling. It was restructuring, which is precisely the kind of move benchmarks of "AI coding" rarely capture, because it lives in the architecture of the program rather than in any single line.

**The honest part: the human masters are still 44 times faster**

Every retelling of this result will be tempted to stop at 204. IBM, to its credit, buried the antidote in its own appendix, and it deserves to be read before the headline.

First, the numbers are estimates. The 204-fold and 52-fold figures come from high-level synthesis — the tool's informed projection of circuit latency — not from measurements on a running FPGA. And the agents optimized a reduced version of the problem: a two-round error model on a 144×1585 structure, not the full decoder at 864×8785. The decoder in question, Relay-BP for IBM's [[144,12,12]] "gross code" — a quantum low-density parity-check code published in *Nature* in 2024 — is real; the instance the factory chewed on was a scaled-down sketch of it.

Second, each configuration ran exactly once. One factory, one budget, one seed. IBM says plainly that a different run could reshuffle the ranking, which is why this should not be read as a model leaderboard.

Third, and decisively: IBM's own engineers have hand-written this decoder in RTL, register-transfer level, the painstaking dialect in which real chips are described. Their design runs at roughly 0.3 microseconds. The agents' best HLS design is still some 44 times slower than that. When the team had the agents write RTL following the human architecture, the result matched the hand design's cycle count — a genuine achievement — but used about 80% more lookup tables and clocked 10% slower. The machines found the shape of the master's solution and reproduced it less efficiently, the way a talented student reproduces a proof: correct, and visibly not the original.

Where does that stubborn 44-fold gap live? Not in the algorithm — the agents matched the humans cycle for cycle. It lives below the level HLS can see: in placement, routing, and the accumulated micro-decisions of engineers who think in wires. The extra 80% of lookup tables and the slower clock are the tax that abstraction charges. And the human RTL design's 0.3 microseconds presumably had to keep its own secrets — clock frequency, pipeline structure — that a latency ratio alone cannot convey. Honesty about the gap, then, cuts in both directions: the agents are further from the summit than the speedups suggest, and the summit is stranger, more physical, and less algorithmic than software people tend to assume. HLS itself was once the heresy — "no serious designer would let a tool schedule their circuit" — yet it won the routine work and pushed hand-craft up the stack. Agent factories look like the same heresy, one level higher.

So the accurate headline is narrower and, honestly, more interesting. The agents improved an unoptimized starting point by 52 to 204 times, exploring a design space at a speed and price no human team can match. They remain an order of magnitude from the hand-crafted frontier. Picture a tireless crew of junior engineers who can burn through a week's worth of your hypotheses overnight — and who still lack the old master's final, unteachable touch.

But do not underrate the explorers, because in real chip projects, exploration is the recurring expense. A decoder is not designed once. Change the error-correcting code, change the measurement circuit, refine the noise model, and the design must be retuned — and IBM expects several such changes before Starling arrives in 2029. If every change begins with a $26 crew mapping the design space overnight, the human experts start each round from high ground instead of from a blank page. That is a workflow revolution wearing modest clothes.

**AI has begun designing the house it will live in**

There is also a quieter strategic layer, and it explains why IBM — a company with frontier ambitions of its own — published a result whose cheapest star is an open-weight model from a Chinese lab. The agent-factory idea predates this decoder; IBM described it in a March preprint using Claude-based agents on twelve standard HLS benchmark kernels. The October work is the graduation exercise: a real target, on the critical path of the company's flagship roadmap, with every cost printed. By itemizing its own serving stack down to the cache-hit rate, IBM is arguing that the scarce asset in agent engineering is not access to the smartest model — anyone can rent Opus for $299 — but the infrastructure that makes a good-enough model nearly free. Whether or not that argument is self-serving, the preprint is now a reference point: every subsequent claim of "AI designs hardware" will be asked for its token count, its cache rate, its dollars. That may prove to be the paper's most durable contribution — not the decoder, but the receipt.

Step back, and the decoder is almost incidental. What IBM demonstrated is the outline of a loop closing: AI systems optimizing computing hardware itself. Today's target happens to be a quantum decoder implemented on classical silicon, through HLS, a tool that lets you describe circuits in a high-level language. The same factory anatomy — coordinator, workers, verifier, synthesizer — can be aimed tomorrow at a block of an AI accelerator or a kernel in an inference engine. The design of computation is being handed to computation.

History suggests respecting such moments. Machine tools that could build machine tools rewrote manufacturing. Compilers written in the languages they compile rewrote software. EDA software already designs the chips that run better EDA software. Each transition moved the scarce human contribution one level up: from making, to designing, to deciding what is worth designing. The agent factory pushes on exactly that hinge, taking over the most experience-laden step in the chain — the exploration of a vast design space, where progress has always depended on veterans who "just know" where to look.

The economics may cut deeper than the capability. A serious round of design exploration used to cost weeks of a senior team's salaries; the all-open factory did it for the price of a paperback, and IBM made a point of itemizing why: 544 H100s, a 98% cache-hit rate, $0.1077 per million tokens. The cost structure of intelligence is migrating from per-head to per-infrastructure, and infrastructure amortizes. When exploration costs $26, designs that were never tried because trying was expensive get tried. Quality gates once guarded by a senior engineer's intuition become "let the factory run its hundred hypotheses first, then we'll talk." None of this requires the agents to be better than the best humans. It only requires them to be cheap, tireless, and good enough to make the first pass — which is, historically, exactly how automation eats a profession: not by storming the summit, but by paving the foothills so thoroughly that the summit is the only thing left, and everyone has to live there.

One fracture line deserves naming before the optimism sets. Judgment — the quality the hybrid experiment crowned — is not a substance that occurs naturally in senior engineers. It is sediment: the residue of thousands of hours spent doing the very execution work now being automated, of designs that failed synthesis at 2 a.m., of intuitions paid for in respins. If the foothills are fully paved, the apprenticeship that produced the masters quietly disappears, and with it the pipeline that manufactures the coordinators of 2045. Perhaps new apprenticeships will form one level up, around problem-framing and verification, the seats this experiment suggests will matter. Perhaps. But a profession that stops training people in its own execution is making a bet it cannot easily unmake — and the first generation to notice will be the one that finds, at the top of its beautifully scaffolded structure, that nobody left knows how the building actually stands.

The house is not built. A 44-fold gap to the masters, estimates standing in for measurements, single runs standing in for statistics — all of it says this is a scaffolding story, not an occupancy story. But scaffolding, once up, changes what the builders attempt next. Twenty-six dollars a round. Workers who never sleep. A coordinator whose judgment is the one input that still commands a premium. When IBM publishes the next version of this experiment, the humans will likely still be at the top of the structure. They will just be standing on floors that machines built.

---

*Discussion: when a round of serious chip-design exploration costs $26, how long does the human engineer's vaunted judgment — the last thing the agents could not reproduce — remain a moat, and what is it actually made of?*
