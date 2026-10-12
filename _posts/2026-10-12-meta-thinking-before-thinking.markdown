---
lng_pair: id_20261012_meta-thinking-before-thinking
title: "Thinking Before Thinking: The Agent That Learned to Manage Itself"
author: OpenSI-Labs
category: research
tags: [meta-reasoning, AI agents, inference scaling, LLM control, test-time compute]
date: 2026-10-12 06:00:00 -0700
img: /assets/img/posts/2026-10-12-meta-thinking-before-thinking.png
meta_description: "Meta's 'Thinking Before Thinking' splits the AI agent into workers that do the work and a controller that decides what work to do — and finds that spending compute on control itself is a new scaling axis."
---

Every AI agent does two jobs at once: the work, and deciding what to do next — push on, backtrack, try something new, stop? In today's harnesses those control decisions are tangled into the work itself, made on the fly against the full messy history.

A new paper from Meta Superintelligence Labs argues that tangling *is* the bottleneck. As runs get longer, *controlling the run becomes a task in its own right* — deserving its own architecture. ["Thinking Before Thinking: Scaling Agentic Inference Through Meta-Reasoning"](https://arxiv.org/abs/2609.38147) (Dahal et al., arXiv:2609.38147, 29 Sep 2026) proposes a clean split: workers do the task; a separate **controller** does nothing but decide what workers do next.

## The four-stroke engine

The controller runs a loop with four sequential stages, each an agentic process in its own right:

1. **Assess** — *What have we learned?* The controller updates a compact, self-written account of the run from new worker outputs — thousands of characters, not the million-plus that direct-control agents accumulate.
2. **Propose** — *What could we do next?* It lists candidate computations *before* committing, deliberately *without* knowing the remaining budget, so expensive-but-valuable options survive instead of being censored early.
3. **Evaluate** — *Which option is worth its cost?* It weighs proposals against the remaining budget — prompted qualitative judgment, explicitly *not* a learned value-of-computation model.
4. **Dispatch** — *What should the worker receive?* It writes the worker's instructions and selects which prior outputs each worker sees. Choosing the context *is* choosing the computation. Or it stops, promoting an existing artifact to the final answer.

Everything workers produce is stored as an **artifact** with a stable ID, and the edges recording "artifact X was used to produce artifact Y" form a **graph** — a diagnostic instrument measuring not just success, but *how*: reuse of earlier work, whether any artifact held a correct answer (coverage), whether the right one was submitted (selection).

<svg viewBox="0 0 720 460" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="The meta-reasoning control loop: controller cycles through Assess, Propose, Evaluate, Dispatch while workers produce artifacts stored in a graph">
  <defs>
    <marker id="mArr" markerWidth="10" markerHeight="10" refX="8" refY="5" orient="auto"><path d="M0,0 L10,5 L0,10 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="30" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="18" font-weight="700" fill="#212529">The controller runs its own loop — workers just work</text>
  <rect x="60" y="60" width="600" height="180" rx="12" fill="#f8f9fa" stroke="#adb5bd" stroke-width="2"/>
  <text x="360" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="16" font-weight="700" fill="#495057">CONTROLLER (decides, never executes)</text>
  <rect x="90" y="110" width="120" height="60" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="150" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#1864ab">Assess</text>
  <text x="150" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">update compact state</text>
  <rect x="230" y="110" width="120" height="60" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="290" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#1864ab">Propose</text>
  <text x="290" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">list options (no budget)</text>
  <rect x="370" y="110" width="120" height="60" rx="8" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="430" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#e67700">Evaluate</text>
  <text x="430" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">worth the cost?</text>
  <rect x="510" y="110" width="120" height="60" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="570" y="136" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#1864ab">Dispatch</text>
  <text x="570" y="156" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">or Stop</text>
  <line x1="210" y1="140" x2="228" y2="140" stroke="#1c7ed6" stroke-width="2" marker-end="url(#mArr)"/>
  <line x1="350" y1="140" x2="368" y2="140" stroke="#1c7ed6" stroke-width="2" marker-end="url(#mArr)"/>
  <line x1="490" y1="140" x2="508" y2="140" stroke="#1c7ed6" stroke-width="2" marker-end="url(#mArr)"/>
  <text x="360" y="205" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">controller sees only its compact state + artifact graph — never raw history</text>
  <rect x="180" y="270" width="160" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="260" y="298" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#a61e4d">WORKERS</text>
  <text x="260" y="320" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">execute, never decide</text>
  <rect x="380" y="270" width="160" height="70" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="460" y="298" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#2b8a3e">ARTIFACT GRAPH</text>
  <text x="460" y="320" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">persistent shared memory</text>
  <line x1="570" y1="170" x2="570" y2="265" stroke="#1c7ed6" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#mArr)"/>
  <line x1="260" y1="270" x2="260" y2="245" stroke="#c92a2a" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#mArr)"/>
  <text x="360" y="385" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">Direct control interleaves deciding with doing.</text>
  <text x="360" y="408" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#212529">Meta-reasoning separates them into two tiers.</text>
  <text x="360" y="440" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Caption: The controller's four stages are themselves agentic; workers receive only task + selected context.</text>
</svg>

## The numbers that matter

On **ProgramBench** — 200 tasks that reconstruct real codebases (FFmpeg, SQLite) from documentation plus an execute-only reference binary, graded by hidden behavioral tests — meta-reasoning with GPT-5.5 hits **71.5%** against **58.0%** for Codex and 63.7% for a direct-control baseline using the same workers and budget. With Opus 4.8: **67.2%** vs 65.5% for Claude Code. Across three models and four benchmark families (including IMO ProofBench-Advanced, ARC-AGI-2), it wins all 12 matched comparisons, gaining 3.6–4.2 points on average.

But the striking number isn't 71.5%. It's the budget sweep: as the allowance grows from 400 to 1,200 calls, meta-reasoning climbs **64.1% → 71.5%** while direct control sits flat near 64%. Direct control *stops early*, using roughly **18%** of its allowance. Meta-reasoning uses 89–101% — and converts it into gains. The controller doesn't just spend more; it finds more worth doing.

Two more findings matter. The controller's verdicts rank answer correctness far better than workers' self-confidence (AUC **0.88** vs **0.55**, near chance). And the artifact graph shows ~**10×** more recorded dependencies for only ~2× the artifacts: work builds on work instead of starting cold.

The paper is honest about limits: the controller's overhead *hurts* at small budgets (at 400 calls it trails direct control), the Evaluate stage is qualitative rather than a learned optimizer, and on one chess subset, "unproductive reconsideration" actually destabilized correct answers. This is a preprint; treat the numbers as the authors' until reproduced.

## Why this is bigger than one harness

**A third scaling axis.** Two years of work taught the field that training compute scales capability, and inference-time compute does too ([Snell et al., 2024](https://arxiv.org/abs/2408.03314)). This paper proposes the next axis: *of your inference budget, how much goes to deciding versus doing?* As models get cheaper per call, deliberation that looks wasteful at 400 calls pays at 1,200. "Test-time scaling" stops meaning "more samples" and starts meaning "better-directed work."

**The unlearned controller is the tell.** The most interesting negative space: Evaluate is *prompted judgment*, not a learned model. Yet [rational metareasoning (2024)](https://arxiv.org/abs/2410.05563) showed value-of-computation can be learned, and [Meta-Harness (2026)](https://arxiv.org/abs/2603.28052) showed harness code itself can be optimized by search. So this paper is a staging post: prove structured control helps *before* learning it. Whoever learns the controller next likely takes the next 5–10 points — and the contemporaneous [ROFT result](https://arxiv.org/abs/2609.35741), where merely *articulating* experience improves action with no reward signal, suggests the training signal is already lying around.

**Correlated risk.** The uncomfortable corollary: meta-reasoning *concentrates* failure risk in the controller. A bad worker wastes one branch; a bad controller poisons the whole run's compact state. That's the opposite of the independent-sampling robustness in ["Large Language Monkeys"](https://arxiv.org/abs/2407.21787). For deployment, controller calibration may matter more than worker quality — and the low-budget crossover becomes a testable prediction: meta-reasoning helps where uncertainty is high and horizons long, hurts where tasks are short and checkable.

There is a historical rhyme: RL split *acting* from *evaluating* (actor-critic); operating systems split *mechanism* from *policy*. Now *doing* splits from *directing*. If the split holds, "controller skill" becomes separately benchmarkable — a manager track distinct from the worker track — and we may see different models serving each role. The agent stops being one model and becomes a two-tier cognitive organization.

<svg viewBox="0 0 720 420" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Budget scaling comparison: meta-reasoning keeps improving with larger budgets while direct control plateaus early">
  <defs>
    <marker id="mArr2" markerWidth="10" markerHeight="10" refX="8" refY="5" orient="auto"><path d="M0,0 L10,5 L0,10 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="30" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="18" font-weight="700" fill="#212529">Control converts budget into gains — direct control stalls</text>
  <text x="80" y="70" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">ProgramBench score (%)</text>
  <line x1="80" y1="90" x2="80" y2="330" stroke="#495057" stroke-width="2"/>
  <line x1="80" y1="330" x2="660" y2="330" stroke="#495057" stroke-width="2"/>
  <text x="370" y="360" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">model-call budget →</text>
  <text x="60" y="140" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">72</text>
  <text x="60" y="200" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">68</text>
  <text x="60" y="260" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">64</text>
  <text x="60" y="320" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">60</text>
  <line x1="80" y1="140" x2="660" y2="140" stroke="#e9ecef" stroke-width="1"/>
  <line x1="80" y1="200" x2="660" y2="200" stroke="#e9ecef" stroke-width="1"/>
  <line x1="80" y1="260" x2="660" y2="260" stroke="#e9ecef" stroke-width="1"/>
  <polyline points="150,262 370,190 590,148" fill="none" stroke="#1c7ed6" stroke-width="4"/>
  <circle cx="150" cy="262" r="7" fill="#1c7ed6"/>
  <circle cx="370" cy="190" r="7" fill="#1c7ed6"/>
  <circle cx="590" cy="148" r="7" fill="#1c7ed6"/>
  <text x="150" y="290" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">400</text>
  <text x="370" y="290" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">800</text>
  <text x="590" y="290" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" fill="#495057">1200</text>
  <text x="150" y="248" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#1c7ed6">64.1%</text>
  <text x="590" y="134" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#1c7ed6">71.5%</text>
  <polyline points="150,258 370,262 590,256" fill="none" stroke="#c92a2a" stroke-width="4" stroke-dasharray="10,6"/>
  <circle cx="150" cy="258" r="7" fill="#ffffff" stroke="#c92a2a" stroke-width="3"/>
  <circle cx="370" cy="262" r="7" fill="#ffffff" stroke="#c92a2a" stroke-width="3"/>
  <circle cx="590" cy="256" r="7" fill="#ffffff" stroke="#c92a2a" stroke-width="3"/>
  <text x="610" y="230" text-anchor="start" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#1c7ed6">meta-reasoning</text>
  <text x="610" y="285" text-anchor="start" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#c92a2a">direct control</text>
  <text x="360" y="395" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#868e96">Caption: GPT-5.5 on ProgramBench. Direct control plateaus near 64% and stops early (uses ~18% of budget).</text>
</svg>

The deepest shift may be conceptual. Cognitive science has studied metacognition for decades, and recent work shows LLMs maintain *decomposable, steerable* metacognitive states. If metacognition is a natural subspace of model internals rather than a prompting trick, explicit controller architectures work *with* the grain of the model. The 1980s dreamed of systems that reasoned about their own reasoning and drowned in hand-coded rules. The missing piece was letting a model do the metareasoning in language.

**Discussion:** If "controller skill" becomes a separately measurable capability — a manager track distinct from the worker track — what gets benchmarked first: the quality of the decisions, or the calibration of knowing when to stop deciding and act?
