---
lng_pair: id_20261012_sakana-mass-self-improvement
title: "MASS: The 27B Model That Organized Itself Into a Research Team"
author: OpenSI-Labs
category: research
tags: [recursive self-improvement, multi-agent systems, Sakana AI, self-supervision, workflow optimization]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-sakana-mass-self-improvement.png
meta_description: "Sakana AI's MASS lets one 27B model act as solver, optimizer, and evaluator in its own improvement loop — and finds the optimizer, not the judge, is the bottleneck."
---

The supervision problem of frontier AI sounds like philosophy until it lands as engineering. Imagine your model is a competent scientist, and you want it to become a better one. You hand it an open-ended research task — no answer key, no unit tests, no human who can reliably separate the good from the great. What signal does it learn from? On exactly the tasks we most want AI to advance, the model is already nearing the edge of what any human can assess. This is the supervision bottleneck, and it is no longer hypothetical.

Sakana AI's answer, published this weekend with UC Berkeley researchers ([paper](https://arxiv.org/abs/2610.12176), [blog post](https://pub.sakana.ai/mass/)), is called MASS — Multi-Agent Self-Supervision. If nobody can supervise the model from outside, let the model organize itself into a team and learn from how its own teams work.

The mechanism is plain enough to state in one paragraph. A single shared 27-billion-parameter model (Qwen3.6-27B, open weights) plays three roles in a loop it runs on itself: the task solver (the "optimizee"), the workflow optimizer, and the evaluator. The researchers call this *homogeneous* recursive self-improvement: one model, every job. Why teams? Because a single model instance struggles to critique and improve its own complex reasoning in a homogeneous loop — but early results showed multi-agent topologies do better at complex reasoning, so the model recruits copies of itself to get past its own limits.

The inner loop searches for better teamwork while the weights stay frozen. The model writes a workflow: a written plan dividing a research task among virtual subagents — each role's instructions, the contracts for what each must hand off, and the order of calls. An orchestrator executes it; the evaluator compares the resulting workspace against the current champion; the optimizer proposes a revised workflow. Evolutionary search, with structural guardrails to keep the space sane.

<figure>
<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<defs><marker id="marrow" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#3366cc"/></marker></defs>
<rect x="230" y="10" width="180" height="52" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="320" y="32" font-size="14" font-weight="bold" text-anchor="middle">Shared model</text>
<text x="320" y="50" font-size="12" text-anchor="middle">Qwen3.6-27B, open weights</text>
<rect x="40" y="110" width="270" height="150" rx="12" fill="#f7f9ff" stroke="#3366cc" stroke-width="2"/>
<text x="175" y="134" font-size="14" font-weight="bold" text-anchor="middle">Inner loop: workflow search</text>
<text x="175" y="156" font-size="12" text-anchor="middle">workflows = roles · instructions ·</text>
<text x="175" y="172" font-size="12" text-anchor="middle">contracts · hops</text>
<text x="175" y="196" font-size="12" text-anchor="middle">execute → evaluate vs champion →</text>
<text x="175" y="212" font-size="12" text-anchor="middle">optimizer revises the workflow</text>
<text x="175" y="236" font-size="12" font-style="italic" text-anchor="middle">weights stay fixed</text>
<rect x="330" y="110" width="270" height="150" rx="12" fill="#fff8ee" stroke="#cc8833" stroke-width="2"/>
<text x="465" y="134" font-size="14" font-weight="bold" text-anchor="middle">Outer loop: distill</text>
<text x="465" y="156" font-size="12" text-anchor="middle">champion workflow × 18 runs / task</text>
<text x="465" y="172" font-size="12" text-anchor="middle">Bradley-Terry self-ranking;</text>
<text x="465" y="188" font-size="12" text-anchor="middle">keep top 16 trajectories</text>
<text x="465" y="212" font-size="12" text-anchor="middle">strip scaffolding → LoRA fine-tune</text>
<text x="465" y="236" font-size="12" font-style="italic" text-anchor="middle">weights change here</text>
<line x1="250" y1="62" x2="178" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="390" y1="62" x2="462" y2="108" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<line x1="310" y1="185" x2="328" y2="185" stroke="#3366cc" stroke-width="2" marker-end="url(#marrow)"/>
<text x="292" y="178" font-size="11" text-anchor="middle">champion</text>
<line x1="606" y1="160" x2="606" y2="36" stroke="#cc8833" stroke-width="2"/>
<line x1="606" y1="36" x2="412" y2="36" stroke="#cc8833" stroke-width="2" marker-end="url(#marrow)"/>
<text x="508" y="28" font-size="11" text-anchor="middle">updated model resumes all three roles</text>
</svg>
<figcaption>The inner loop searches for better teamwork; the outer loop folds the best teamwork back into the model's weights.</figcaption>
</figure>

The outer loop is where the loop feeds itself. The champion workflow runs 18 times per task, the workspaces get self-ranked with Bradley-Terry scoring, and only the top 16 trajectories survive. Their workflow scaffolding is stripped from the prompts, and the shared model is fine-tuned on them with LoRA. The updated model then resumes all three roles — a better optimizer, a better evaluator — and the cycle repeats. After two full cycles, the model scores 1.2 to 1.6 times the base per output token on four research benchmarks (1.60× on MLR-Bench, 1.35× on DSBench, 1.28× on AstaBench, 1.20× on ScienceAgentBench), with win rates against the untouched base climbing from 53.9% to 69.9%. The training signal is also dense: a student trained on multi-agent trajectories matched single-agent training while consuming 31% fewer supervised tokens (28.8M vs 42M).

Here is the part most coverage will skip — the honest failures. On SWE-bench Verified and Terminal-Bench 2.0, both coding-heavy, the same system *fell* to 0.94× and 0.96× of base. MASS did not make the model generally smarter. It made it a better researcher at the measurable price of being a worse coder.

<figure>
<svg viewBox="0 0 640 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<line x1="273" y1="20" x2="273" y2="240" stroke="#999" stroke-width="1.5" stroke-dasharray="6,4"/>
<text x="273" y="256" font-size="11" text-anchor="middle" fill="#666">base = 1.0×</text>
<text x="170" y="52" font-size="12" text-anchor="end">MLR-Bench</text>
<rect x="180" y="38" width="280" height="22" rx="4" fill="#3366cc"/><text x="468" y="54" font-size="12">1.60×</text>
<text x="170" y="92" font-size="12" text-anchor="end">DSBench</text>
<rect x="180" y="78" width="165" height="22" rx="4" fill="#3366cc"/><text x="353" y="94" font-size="12">1.35×</text>
<text x="170" y="132" font-size="12" text-anchor="end">AstaBench</text>
<rect x="180" y="118" width="133" height="22" rx="4" fill="#3366cc"/><text x="321" y="134" font-size="12">1.28×</text>
<text x="170" y="172" font-size="12" text-anchor="end">ScienceAgentBench</text>
<rect x="180" y="158" width="95" height="22" rx="4" fill="#3366cc"/><text x="283" y="174" font-size="12">1.20×</text>
<text x="170" y="212" font-size="12" text-anchor="end">SWE-bench Verified</text>
<rect x="180" y="198" width="66" height="22" rx="4" fill="#cc3333"/><text x="254" y="214" font-size="12">0.94×</text>
<text x="320" y="14" font-size="13" font-weight="bold" text-anchor="middle">Score per output token vs base model, after two MASS cycles</text>
</svg>
<figcaption>Improvement is directional: the model became a better researcher — and a slightly worse coder.</figcaption>
</figure>

That asymmetry is the real story. Recursive self-improvement is usually narrated as a rising tide — a model getting uniformly more capable. MASS suggests it behaves more like apprenticeship: the model specializes into whatever its loop rewards, and pays for it in adjacent skills. A self-improving researcher that slowly forgets how to code is not a paradox; it is the standard bargain of every specialist. If RSI scales, the future may not be one godlike generalist but an ecology of self-improving specialists, each brilliant inside the basin of its own reward and slightly worse everywhere else.

The paper's second surprise undercuts the other popular worry. Everyone assumes the dangerous part of a self-grading loop is the *evaluator* — a model grading its own homework will just approve itself. Sakana's ablations found the opposite: upgrading the evaluator alone barely moved results, while upgrading the *optimizer* did. In a self-improving loop, generating better candidate strategies matters more than judging them well — the proposer, not the critic, is the bottleneck. Anyone building RSI systems should read that as a design directive: invest in the search, not the scorecard.

And the authors name their own nightmare, which is the part that deserves respect. When one model produces, judges, and trains on the results, a shared blind spot can be produced, approved as an improvement, and baked into the next model — their words, calling it an Achilles' heel of recursive self-improvement. Notice the epistemic tell: to *measure* progress at all, they needed outside judges (GPT-5.5 and Claude Opus 4.8) whose verdicts never entered the loop. A truly closed loop would have no way to know it was improving. MASS doesn't close that gap; it builds the best possible machine inside it.

The code is on GitHub and the paper is open. MASS is not the intelligence explosion. It is something rarer: a working, measured self-improving loop that tells you exactly where it got better, where it got worse, and which of its parts was holding it back.

**Discussion:** If recursive self-improvement inevitably specializes models toward the tasks their loops reward, who gets to decide which tasks deserve a self-improving loop — and which skills we're willing to let the model lose?
