---
lng_pair: id_20261009_openai-722-math-manuscripts
title: "The Particle Collider for Mathematics: Inside OpenAI's 722-Manuscript Drop"
author: OpenSI-Labs
category: research
tags: [OpenAI, mathematics, Lean, automated theorem proving, research evaluation]
date: 2026-10-09 06:00:00 -0700
img: /assets/img/posts/2026-10-09-openai-722-math-manuscripts.png
meta_description: "OpenAI published 722 machine-written math manuscripts from a single AI agent. The real story is the pipeline: benchmarks saturated, so open problems became the frontier evaluation — and human verification became the bottleneck."
---

On October 6, OpenAI did something no publisher has attempted: it released a mathematics department's worth of output into a public GitHub repository in one evening. The repo, [openai/math](https://github.com/openai/math), holds 719 manuscripts in 372 "families" of related results (announced as 722) — all produced by an unreleased internal model. It is Apache-2.0 licensed, gathered roughly 12,800 stars within days, and contains some of the most aggressive claims ever attributed to a machine: a solution to the four-dimensional Kakeya conjecture, a wider zero-free region for the Riemann zeta function, and the rational Hodge conjecture for CM abelian varieties.

OpenAI's README says the vast majority of the results came from one fixed procedure: the model was handed roughly 4,000 open problems; each accepted result consumed, on average, three hours of "ChatGPT Pro thinking" compute; outputs clearing a significance bar were aggregated into families — each a principal result plus companions, consequences, or alternative proofs. A spokesperson told *Scientific American* the model "produced almost every one of the results in response to a single prompt handed to a single AI agent." One prompt, one agent, 372 families. This is not 722 independent research programs. It is one extremely productive agent run — and the README says plainly why: "we expanded these evaluations after performance on our existing mathematical evaluations saturated." Benchmarks died as a frontier measure, so unsolved mathematics took their place: the new frontier evaluation isn't a test set — it's the open literature.

<svg viewBox="0 0 720 560" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="The machine research pipeline: 4,000 problems in, 372 result families out">
  <defs>
    <marker id="arrM" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">The machine research pipeline: 4,000 problems in, 372 families out</text>
  <rect x="255" y="45" width="210" height="56" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="70" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#1864ab">~4,000 OPEN PROBLEMS</text>
  <text x="360" y="90" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">posed to one model</text>
  <line x1="360" y1="101" x2="360" y2="116" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="118" width="270" height="56" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="143" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#e67700">SINGLE AGENT, ONE PROMPT</text>
  <text x="360" y="163" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">~3 hours of thinking per result</text>
  <line x1="360" y1="174" x2="360" y2="189" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="191" width="240" height="56" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="216" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#5f3dc4">SIGNIFICANCE FILTER</text>
  <text x="360" y="236" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">~18% accepted; rest discarded</text>
  <line x1="360" y1="247" x2="360" y2="262" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="255" y="264" width="210" height="56" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="289" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">372 RESULT FAMILIES</text>
  <text x="360" y="309" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">719 manuscripts, 17 disciplines</text>
  <line x1="360" y1="320" x2="360" y2="335" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="240" y="337" width="240" height="56" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="362" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#a61e4d">LEAN FORMALIZATION</text>
  <text x="360" y="382" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">~42% of top-line results checked</text>
  <line x1="360" y1="393" x2="360" y2="408" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrM)"/>
  <rect x="225" y="410" width="270" height="56" rx="10" fill="#f8f9fa" stroke="#868e96" stroke-width="2"/>
  <text x="360" y="435" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#495057">VERSIONED PUBLIC REPO</text>
  <text x="360" y="455" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Apache-2.0, per-paper BibTeX, history log</text>
  <text x="360" y="500" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">Two steps broke the fixed procedure: the zeta zero-free region (human-edited writeup)</text>
  <text x="360" y="518" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">and the Hodge conjecture proof for CM abelian varieties.</text>
</svg>
*Figure 1: The release pipeline — one agent, one prompt, two human-touched exceptions. Everything downstream of the model is infrastructure.*

The claims vary in weight. Two broke the fixed procedure: the zero-free region for the Riemann zeta function — a wider Re(s) > 11/12 region (the full hypothesis needs 1/2), whose writeup was human-edited — and the proof of the Hodge conjecture for CM abelian varieties in all dimensions and codimensions. Ten released reasoning summaries cover π's irrationality exponent, the Mahler conjectures, Kaplansky in characteristic two, free group factors, and the 3D Vlasov–Maxwell system. The claims span 17 disciplines; theoretical computer science leads with 40 families.

## Lean is the load-bearing wall

The repo ships a Lean library — Lean mechanically checks every logical step of a proof — and OpenAI says ~42% of top-line results are formalized; independent reporting counted 162 of 722 manuscripts with a computer-checked main result. A passing Lean check is a new trust substrate: correctness no longer rests on reputation or a referee's stamina.

One nuance most coverage skipped: a Lean check proves the argument follows from its premises. It says nothing about whether the result is new, important, or interesting. Machine-checked is not peer-reviewed. OpenAI admits some unformalized results "could have issues," with corrections versioned publicly — science with release notes. The Institute for Advanced Study's warning still stands: an AI can now output mathematical arguments "without the human who prompted it being able to understand the arguments, verify them, or take responsibility for them."

A month earlier, OpenAI's claim that ~10,000 coordinating agents had resolved the Navier–Stokes existence-and-smoothness problem in 88 hours detonated a dispute with mathematicians; two dozen Fields Medalists signed a declaration titled "A Severe Misalignment of AI in Mathematics." Out of that came the Advisory Group on Mathematics and AI at the Institute for Advanced Study, whose September 29 recommendations asked labs to name the model, publish prompts, and stop using math results as marketing. OpenAI follows the letter unevenly: averages instead of per-problem compute, ten summaries instead of full traces, no prompts. A spokesperson told *Scientific American* the company takes the guidelines seriously but is "not bound by them." MIT's Andrew Sutherland: "We should ask for receipts." Daniel Litt (Toronto): if mathematicians want the answers, why keep them secret? An independent arXiv audit of OpenAI's August batch found no confirmed substantive error in the reviewed results.

<svg viewBox="0 0 720 330" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="The verification gradient: production outpaces every check">
  <defs>
    <marker id="arrV" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#868e96"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">The verification gradient: production now outpaces every check</text>
  <rect x="30" y="50" width="660" height="44" rx="8" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="77" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#1864ab">~4,000 problems posed to the model</text>
  <rect x="180" y="106" width="360" height="44" rx="8" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="133" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#2b8a3e">372 result families released (~18% hit rate)</text>
  <rect x="255" y="162" width="210" height="44" rx="8" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="360" y="189" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#e67700">162 with computer-checked proofs</text>
  <rect x="315" y="218" width="90" height="44" rx="8" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="360" y="245" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#a61e4d">referees</text>
  <line x1="360" y1="94" x2="360" y2="104" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="150" x2="360" y2="160" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <line x1="360" y1="206" x2="360" y2="216" stroke="#868e96" stroke-width="2" marker-end="url(#arrV)"/>
  <text x="360" y="292" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">Each stage is narrower than the last. Human refereeing is the tightest</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">choke point — machine-checked logic is the only verification channel with</text>
  <text x="360" y="328" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#868e96">machine-scale bandwidth.</text>
</svg>
*Figure 2: The verification gradient. Output scales with compute; scrutiny still scales with humans. Lean formalization is the only check with machine-scale bandwidth.*

## The new scarce resource

Here is the part that should reshape how we think about frontier AI, and it has almost nothing to do with any single theorem. The README's most important sentence is the one about saturation: benchmarks died, so the frontier moved to open problems. Every frontier lab faces the same move: when test sets stop discriminating, the only exam left is the questions nobody has answered. The consequence nobody priced in is the bottleneck flip: the scarce resource is no longer producing candidate results. A single agent produced 372 families at three hours apiece; the scarce resource is absorbing them. No referee pipeline reads 722 manuscripts in a week. That is why Lean formalization, versioned releases, and per-manuscript BibTeX entries are not accessories. They are the publishing infrastructure for an era in which the lab writes the papers.

OpenAI admits it is "exploring community-hosted repositories for these materials." A single company's repo cannot be the permanent home of machine mathematics. The field will need shared verification infrastructure — formalization libraries, checking services, referee norms — that belong to no lab. The 722 manuscripts are a demonstration. The infrastructure they demand is the actual breakthrough.

One more thing: we never see the 82%. The repo holds only what cleared the bar; the problems the model failed are science too — they mark where its frontier actually lies. Until labs publish those, every such release is a highlight reel.

Question for readers: if unsolved mathematics is now the frontier benchmark, and the models sitting that exam are proprietary, who owns the verification pipeline — and how long before "machine-generated, machine-checked, human-unread" becomes the normal unit of mathematical progress?

---

*Sources: [OpenAI's openai/math repository](https://github.com/openai/math); [repository overview](https://raw.githubusercontent.com/openai/math/main/overview.tex); the IAS advisory group recommendations; Scientific American's reporting; an independent arXiv audit of the August math batch.*
