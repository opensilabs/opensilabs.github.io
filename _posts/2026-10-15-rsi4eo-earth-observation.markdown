---
lng_pair: id_20261015_rsi4eo-earth-observation
title: "The Last Model Built by Humans: AI Agents That Recursively Improve Earth Observers"
author: OpenSI-Labs
category: research
tags: [recursive self-improvement, RSI4EO, Earth observation, coding agents, verifiable AI]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-rsi4eo-earth-observation.png
meta_description: "A coding agent builds Earth-observation models and improves them recursively on its own outputs, beating published results on four satellite-imagery benchmarks with about one percent of the training labels."
---

**When the river rises, nobody has time to train a model.**

A flood is spreading across a river delta. Emergency teams need a damage map — which neighborhoods are underwater, which roads are still passable — and they need it today. The satellites are already overhead, capturing the scene in optical, radar, and multispectral bands. But turning those pixels into a trustworthy map still takes specialists: people who design a training recipe, tune it against a benchmark, iterate for weeks. By the time the model is ready, the water has receded and the map is history.

A paper posted to arXiv on October 13 asks what happens if that entire loop is handed to an agent ([Zhao et al., arXiv:2610.18845](https://arxiv.org/abs/2610.18845v1)). Its title is deliberately provocative — "The Last Remote Sensing Model Built by Humans?" — and its claim is the sharpest formulation of recursive self-improvement to appear in months: any verifiable task can be cast as RSI, and Earth observation is the first field where the casting is complete.

The mechanism fits in two words: harness and verifier. The harness is everything the agent is allowed to use — data, tools, compute. The verifier is the sealed exam at the end: it scores the agent's model without exposing the held-out images it grades against. Given only these two components, a general-purpose coding agent builds the Earth-observation model and then improves it recursively on its own outputs. Nobody hand-tunes the recipe. Nobody babysits the training loop.

<figure>
<svg viewBox="0 0 680 360" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">RSI4EO: people design the exam, the agent builds the model</text>
<rect x="20" y="60" width="200" height="110" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="120" y="86" font-size="14" font-weight="bold" text-anchor="middle">Designed by people</text>
<text x="120" y="110" font-size="14" text-anchor="middle">Harness: data · tools ·</text>
<text x="120" y="130" font-size="14" text-anchor="middle">compute the agent may use</text>
<text x="120" y="152" font-size="14" text-anchor="middle" font-style="italic">Sealed verifier: scores</text>
<rect x="250" y="60" width="180" height="110" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="340" y="86" font-size="14" font-weight="bold" text-anchor="middle">Coding agent</text>
<text x="340" y="110" font-size="14" text-anchor="middle">builds the EO model,</text>
<text x="340" y="130" font-size="14" text-anchor="middle">improves it recursively</text>
<text x="340" y="152" font-size="14" text-anchor="middle">on its own outputs</text>
<rect x="460" y="60" width="200" height="110" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="560" y="86" font-size="14" font-weight="bold" text-anchor="middle">Better EO model</text>
<text x="560" y="110" font-size="14" text-anchor="middle">flood / crop / damage</text>
<text x="560" y="130" font-size="14" text-anchor="middle">maps from satellite</text>
<text x="560" y="152" font-size="14" text-anchor="middle">imagery</text>
<line x1="220" y1="115" x2="246" y2="115" stroke="#3366cc" stroke-width="2" marker-end="url(#m1)"/>
<line x1="430" y1="115" x2="456" y2="115" stroke="#cc8833" stroke-width="2" marker-end="url(#m1)"/>
<path d="M 560 170 C 560 260, 120 260, 120 176" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#m1)"/>
<text x="340" y="300" font-size="14" text-anchor="middle" font-style="italic">the output of one cycle becomes the input of the next</text>
<text x="340" y="330" font-size="14" text-anchor="middle">verifiable via labels · independent sensors · physical models · repeat observation</text>
<defs><marker id="m1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>The loop: people design the harness and the sealed verifier; the agent builds the model and improves it on its own outputs.</figcaption>
</figure>

Why does this work for satellites and not, say, poetry? Because in Earth observation, reality grades the work. The authors show that every EO task can be made verifiable through one of four channels: labeled benchmarks, independent sensors, physical models, or the repeated observation of the same place. A flood-detection model can be checked against a radar pass taken hours later; a crop classifier against the physical growth model of the plants it claims to see. Problems the field treated as separate research areas — learning from a handful of labels, adapting across domains — collapse into choices of harness and verifier.

The numbers are what lift this from manifesto to result. On four EO benchmarks spanning optical, radar (SAR), and multispectral time-series imagery, agent-built models surpass the published state of the art — all four comparisons, with full labels. Then the striking part: with only 0.2 to 1.4 percent of the training labels, the agent-built models retain 69 to 84 percent of that score ([ArXivSignals summary](https://arxivsignals.io/explore)). About one percent of the labels, most of the accuracy.

<figure>
<svg viewBox="0 0 680 260" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Label efficiency: ~1% of labels, most of the accuracy</text>
<text x="200" y="70" font-size="14" text-anchor="end">Full labels</text>
<rect x="210" y="54" width="380" height="24" rx="4" fill="#3366cc"/><text x="598" y="71" font-size="14">100%</text>
<text x="200" y="116" font-size="14" text-anchor="end">0.2–1.4% of labels</text>
<rect x="210" y="100" width="290" height="24" rx="4" fill="#cc8833"/><text x="508" y="117" font-size="14">69–84% of score</text>
<text x="200" y="162" font-size="14" text-anchor="end">Published baselines</text>
<rect x="210" y="146" width="330" height="24" rx="4" fill="#999"/><text x="548" y="163" font-size="14">beaten 4 / 4</text>
<text x="340" y="210" font-size="14" text-anchor="middle">four benchmarks: optical · SAR · multispectral time-series</text>
<text x="340" y="236" font-size="14" text-anchor="middle" font-style="italic">agent-built models surpass the state of the art on every task</text>
</svg>
<figcaption>With a tiny fraction of the labels, agent-built models keep most of their accuracy — and beat every published baseline.</figcaption>
</figure>

Here is the angle most coverage will miss. Recursive self-improvement has always had two halves, and only one of them was hard. The "self" half — agents rewriting code, distilling trajectories — is now routine; the field publishes a new loop every week. The "improvement" half is the real bottleneck: knowing what counts as better without a human in the loop to say so. Every self-improving system stalls on the trustworthiness of its own signal. RSI4EO's contribution is to point at a domain where the signal doesn't come from a human labeler or an LLM judge — it comes from the world. An independent sensor cannot be flattered. A physical model cannot be gamed by eloquence. The sealed verifier works because the ground truth sits outside the agent's reach.

And then there is the recursion dividend, stated plainly in the paper: EO models improve as agents do. Every advance in general coding agents automatically upgrades every Earth-observation pipeline, without anyone touching the EO code. The division of labor the authors propose is the real paradigm claim: people design harnesses and verifiers; agents build the models. The scarce skill stops being remote-sensing expertise and becomes verifier design — deciding what counts as success, sealed so the agent cannot peek.

The honest caveats matter. The authors label it an ongoing project. Four benchmarks in one domain is a beachhead, not a conquest; whether the harness-and-verifier casting transfers to materials science, chip design, or drug discovery is the open bet. And the sealed verifier is doing a lot of quiet work — the entire safety of the loop rests on the agent never learning to game the exam. Goodhart's law has ended more self-improvement loops than any technical limit.

Still: for the first time, a whole scientific field has been reformulated so that an agent can improve its own models in it, measurably, with the world itself as the grader. The flood map that used to take weeks of specialist labor is now a task you describe and a verifier you seal.

If the verifier is what makes self-improvement safe to run — who verifies the verifiers, and what happens when the agent learns to build those too?
