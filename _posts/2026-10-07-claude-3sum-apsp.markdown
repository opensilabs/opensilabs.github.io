---
lng_pair: id_20261007_claude-3sum-apsp
title: "The 0.0008 That Broke Two Hypotheses"
author: OpenSI-Labs
category: research
tags: [complexity theory, algorithms, AI-discovered math, formal verification]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-claude-3sum-apsp.png
meta_description: "An Anthropic research model discovered the first sub-quadratic 3SUM and sub-cubic shortest-path algorithms, refuting two cornerstones of complexity theory — and it found them by accident."
---

For decades, two numbers in computer science sat exactly where the textbooks put them. Solving 3SUM — deciding whether any three of *n* numbers add up to zero — took about *n*² steps. Finding the shortest path between every pair of points in a network took about *n*³. Generations of researchers chipped at the constants and the logarithmic fine print. The exponents never moved.

On October 5, they moved. A paper by Josh Alman of Columbia and Virginia Vassilevska Williams of MIT gives deterministic algorithms running in O(*n*^1.9992) for 3SUM and O(*n*^2.9995) for all-pairs shortest paths — the first polynomial improvements over the textbook bounds, and a direct refutation of the 3SUM and APSP hypotheses that much of fine-grained complexity theory is built on ([arXiv abstract](https://arxiv.org/abs/2610.06783v1), [full text](https://arxiv.org/html/2610.06783v1)).

The abstract is blunt: "This refutes the 3SUM and APSP hypotheses of fine-grained complexity theory." Along the way the paper also topples the Exact Triangle hypothesis (new bound O(*n*^2.9983)), the Zero-Weight *k*-Clique hypotheses, and three conjectures on online matrix–vector multiplication. It does not touch SETH — the strong exponential-time hypothesis survives, and the authors say so.

<svg viewBox="0 0 640 330" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Textbook exponents versus the new exponents, axis magnified">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;}</style>
<text x="24" y="34" font-size="17" font-weight="700" fill="#111827">3SUM</text>
<text x="24" y="56" font-size="12.5" fill="#6b7280">axis magnified &#215;25: 1.990 &#8211; 2.010</text>
<line x1="150" y1="100" x2="610" y2="100" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="94" x2="150" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1.990</text>
<line x1="265" y1="94" x2="265" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="124" font-size="11" fill="#6b7280" text-anchor="middle">1.995</text>
<line x1="380" y1="94" x2="380" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.000</text>
<line x1="495" y1="94" x2="495" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.005</text>
<line x1="610" y1="94" x2="610" y2="106" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="124" font-size="11" fill="#6b7280" text-anchor="middle">2.010</text>
<line x1="380" y1="70" x2="380" y2="100" stroke="#374151" stroke-width="3"/><text x="392" y="80" font-size="13" font-weight="600" fill="#374151">textbook: n&#178;</text>
<line x1="361.6" y1="70" x2="361.6" y2="100" stroke="#b45309" stroke-width="3"/><text x="180" y="80" font-size="13" font-weight="600" fill="#b45309">new: n<tspan baseline-shift="super" font-size="9">1.9992</tspan></text>
<line x1="361.6" y1="140" x2="380" y2="140" stroke="#b45309" stroke-width="1.5"/><line x1="361.6" y1="135" x2="361.6" y2="145" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="135" x2="380" y2="145" stroke="#b45309" stroke-width="1.5"/><text x="370.8" y="158" font-size="12" fill="#b45309" text-anchor="middle">0.0008</text>
<text x="24" y="196" font-size="17" font-weight="700" fill="#111827">APSP</text>
<text x="24" y="218" font-size="12.5" fill="#6b7280">axis magnified &#215;25: 2.990 &#8211; 3.010</text>
<line x1="150" y1="262" x2="610" y2="262" stroke="#9ca3af" stroke-width="1.5"/>
<line x1="150" y1="256" x2="150" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="150" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2.990</text>
<line x1="265" y1="256" x2="265" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="265" y="286" font-size="11" fill="#6b7280" text-anchor="middle">2.995</text>
<line x1="380" y1="256" x2="380" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="380" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.000</text>
<line x1="495" y1="256" x2="495" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="495" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.005</text>
<line x1="610" y1="256" x2="610" y2="268" stroke="#9ca3af" stroke-width="1.5"/><text x="610" y="286" font-size="11" fill="#6b7280" text-anchor="middle">3.010</text>
<line x1="380" y1="232" x2="380" y2="262" stroke="#374151" stroke-width="3"/><text x="392" y="242" font-size="13" font-weight="600" fill="#374151">textbook: n&#179;</text>
<line x1="368.5" y1="232" x2="368.5" y2="262" stroke="#b45309" stroke-width="3"/><text x="180" y="242" font-size="13" font-weight="600" fill="#b45309">new: n<tspan baseline-shift="super" font-size="9">2.9995</tspan></text>
<line x1="368.5" y1="302" x2="380" y2="302" stroke="#b45309" stroke-width="1.5"/><line x1="368.5" y1="297" x2="368.5" y2="307" stroke="#b45309" stroke-width="1.5"/><line x1="380" y1="297" x2="380" y2="307" stroke="#b45309" stroke-width="1.5"/><text x="374.2" y="322" font-size="12" fill="#b45309" text-anchor="middle">0.0005</text>
</svg>
*The exponents, magnified 25×. After decades of standing still, 3SUM's 2.0 became 1.9992 and APSP's 3.0 became 2.9995. The gap is the news.*

Honestly: at a billion inputs, *n*² versus *n*^1.9992 differs by under 2%, before constant factors the paper doesn't claim are small. Nobody will recompile their routing software on Monday. The significance is structural, not practical — like discovering a load-bearing wall is hollow. Hundreds of results in fine-grained complexity have the form "problem X needs *n*² time, unless 3SUM is easy." 3SUM just got easy, by a hair. Every one of those results now rests on *n*^1.9992 instead of *n*². The edifice stands, but its foundation moved.

The mechanism is a single new algorithm for a peculiar kind of matrix multiplication. Take a tall, thin integer matrix and multiply it by a short, wide one — but you only care about a sparse handful of entries in the answer. The paper computes just those entries in O(*N*²/*D*^0.063) operations, polynomially less work than writing out the full product. The construction modifies a variant of Don Coppersmith's 1982 rectangular matrix-multiplication method — itself built on Arnold Schönhage's ten-multiplication identity — to skip every operation feeding entries nobody asked for. As a graph algorithm, it finds triangles fast in "lopsided" graphs — two vertex groups huge, the third tiny — and known reductions ferry that speedup to 3SUM and shortest paths.

<svg viewBox="0 0 640 370" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Lopsided tripartite graph with a highlighted triangle">
<style>text{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;}</style>
<text x="320" y="26" font-size="13" fill="#6b7280" text-anchor="middle">the tiny side: n<tspan baseline-shift="super" font-size="9">&#949;</tspan> vertices</text>
<circle cx="300" cy="52" r="7" fill="#9ca3af"/><circle cx="322" cy="44" r="7" fill="#9ca3af"/><circle cx="344" cy="52" r="7" fill="#9ca3af"/>
<g stroke="#d1d5db" stroke-width="1">
<line x1="300" y1="52" x2="130" y2="120"/><line x1="300" y1="52" x2="130" y2="200"/><line x1="300" y1="52" x2="130" y2="280"/>
<line x1="322" y1="44" x2="130" y2="160"/><line x1="322" y1="44" x2="130" y2="240"/><line x1="322" y1="44" x2="510" y2="160"/>
<line x1="344" y1="52" x2="130" y2="120"/><line x1="344" y1="52" x2="510" y2="200"/><line x1="344" y1="52" x2="510" y2="280"/>
<line x1="300" y1="52" x2="510" y2="120"/><line x1="300" y1="52" x2="510" y2="200"/><line x1="300" y1="52" x2="510" y2="280"/>
<line x1="322" y1="44" x2="510" y2="120"/><line x1="322" y1="44" x2="510" y2="240"/><line x1="344" y1="52" x2="130" y2="200"/>
</g>
<g fill="#6b7280">
<circle cx="110" cy="120" r="7"/><circle cx="150" cy="120" r="7"/><circle cx="110" cy="160" r="7"/><circle cx="150" cy="160" r="7"/><circle cx="110" cy="200" r="7"/><circle cx="150" cy="200" r="7"/><circle cx="110" cy="240" r="7"/><circle cx="150" cy="240" r="7"/><circle cx="110" cy="280" r="7"/><circle cx="150" cy="280" r="7"/>
<circle cx="490" cy="120" r="7"/><circle cx="530" cy="120" r="7"/><circle cx="490" cy="160" r="7"/><circle cx="530" cy="160" r="7"/><circle cx="490" cy="200" r="7"/><circle cx="530" cy="200" r="7"/><circle cx="490" cy="240" r="7"/><circle cx="530" cy="240" r="7"/><circle cx="490" cy="280" r="7"/><circle cx="530" cy="280" r="7"/>
</g>
<g stroke="#d97706" stroke-width="3.5" fill="none">
<line x1="130" y1="200" x2="322" y2="44"/><line x1="322" y1="44" x2="510" y2="200"/><line x1="510" y1="200" x2="130" y2="200"/>
</g>
<circle cx="130" cy="200" r="9" fill="#d97706"/><circle cx="322" cy="44" r="9" fill="#d97706"/><circle cx="510" cy="200" r="9" fill="#d97706"/>
<text x="130" y="322" font-size="13" fill="#374151" text-anchor="middle">n vertices</text>
<text x="510" y="322" font-size="13" fill="#374151" text-anchor="middle">n vertices</text>
<text x="320" y="352" font-size="12.5" fill="#b45309" text-anchor="middle">one triangle found fast — the only computation that matters</text>
</svg>
*The core idea: find triangles fast in "lopsided" graphs, where two sides are huge and the third is tiny. Known reductions carry that speedup to 3SUM and shortest paths.*

In plain terms: the old algorithms did work nobody needed. The new one declines to.

Now the part that will be remembered longer than the exponents. The paper credits the core algorithm, in plain words, to "Claude, an AI model developed by Anthropic." An Anthropic employee had set an internal research model loose on open problems in cryptography — constructions whose security rests on average-case hardness of a related clique problem — asking it to verify and strengthen them. Claude instead found an algorithm that weakened the assumption. Average case first, then worst case. The session ran 16 million output tokens with no human input at all.

Anthropic shared the algorithm with Alman and Vassilevska Williams in September under a confidentiality agreement, offered compensation, and gave them access to the public Claude. The humans understood, simplified, strengthened, and extended it — the data-structure version and the hinted matrix–vector link are theirs — and take full responsibility for the paper. Then Anthropic used another internal model to certify the main deterministic results in Lean 4 with Mathlib and published the formalization on GitHub. A machine found the theorem; a compiler checked it.

This caps a remarkable quarter for machine mathematics at Anthropic: a strengthened Riemann-hypothesis bound in August, a complete Lean formalization of Fermat's Last Theorem in eleven days in September. But those verified known truths. This is a discovery — the first genuinely new algorithm for a textbook problem found by an AI system, then verified and extended by human experts.

Here is the angle most coverage will miss. Claude was hired as a security auditor and came back as a safecracker. Cryptography's hardness assumptions — digital security's load-bearing walls — are exactly the crisply stated, machine-checkable conjectures that tireless agents can now audit at scale. The first serious audit has already cracked two textbook exponents. Expect more audits. The interesting question is not whether machines will find more cracks; it is which of our "known hard" problems survive inspection, and what we do about the ones that don't.

A second shift hides in the methodology. Idea generation is now cheap: sixteen million tokens, zero humans, one breakthrough. Verification — human understanding plus a compiler that cannot be bluffed — is the scarce resource. Mathematics has always been a dialogue between guessing and checking. The guessing just got automated. The checking did not, and that asymmetry will define the field's next decade.

One caution: this is a two-day-old preprint. Outside experts have only begun reading it. The Lean check covers the main deterministic results; the randomized real-number bounds still rest on the paper alone. Treat the exponents as claimed, not canon — but note that a compiler, not a referee, already signed off on the core. Complexity theorist Mahdi Cheraghchi's reaction post drew 430,000 views within a day of the listing: the field is paying attention.

**If the first machine audit of a hardness assumption broke two hypotheses by accident, which "known hard" problem should we point the next sixteen-million-token session at — and are we ready for what it finds?**

*Sources: [Alman &amp; Vassilevska Williams, arXiv 2610.06783](https://arxiv.org/abs/2610.06783v1) · [full text](https://arxiv.org/html/2610.06783v1) · [CellCog's line-by-line reading](https://cellcog.ai/blog/claude-3sum-apsp-algorithm/)*
