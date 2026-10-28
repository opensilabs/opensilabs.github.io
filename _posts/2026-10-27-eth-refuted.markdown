---
lng_pair: id_20261027_eth-refuted
title: "ETH Stood for 27 Years. OpenAI and Claude Claim They Broke It on the Same Day"
author: OpenSI-Labs
category: research
tags: [complexity theory, ETH, SAT, OpenAI, Anthropic, Claude, Lean, formal verification]
date: 2026-10-27 12:00:00 -0700
img: /assets/img/posts/2026-10-27-eth-refuted.png
meta_description: "For 27 years, computer science assumed no algorithm could solve 3-SAT in subexponential time — the Exponential Time Hypothesis. In October 2026, OpenAI and Anthropic independently claimed algorithms that do exactly that, with Lean proofs anyone can check. What ETH says, what was actually claimed, and what it would and would not mean."
---

On October 16, 2026, in two labs that were not talking to each other, the same thing happened. An internal model at OpenAI produced a proof that one of computer science's load-bearing assumptions is false. Independently, on the same day, an internal research model at Anthropic — Claude — found essentially the same argument. Ten days later, on October 26, both companies went public within hours of each other.

The assumption is called the Exponential Time Hypothesis, ETH for short. It has stood since 1999, and hundreds of papers lean on it: results of the form "this problem needs exponential time — assuming ETH." If the two new proofs hold up, the assumption is simply wrong, and a generation of conditional results has to be re-examined one by one. If they don't hold up, this becomes a story about how convincingly machines can now produce mathematics that experts must spend months checking.

Either way, it is worth understanding what exactly was claimed. The claim is precise, and its limits are as interesting as its content. So first: what is ETH, in plain terms?

## The problem underneath everything: 3-SAT

Start with a logic puzzle. You have a list of statements built from variables that are each either true or false — call them x₁, x₂, and so on. The statements come in clauses, and each clause is a short "or" of exactly three variables, possibly negated: things like (x₁ or not-x₂ or x₇). A formula in this shape — a long "and" of three-variable "or" clauses — is called a 3-SAT instance. The question is simple to state: can you assign true and false to the variables so that every single clause comes out true?

This is a game anyone can check. If someone hands you an assignment, you can verify in moments whether it satisfies all the clauses. The hard part is finding one. With n variables, there are 2ⁿ possible assignments, and the dumb method — try them all — costs 2ⁿ steps: for n = 300, that is more steps than there are atoms in the observable universe. The whole question of this field is whether anything fundamentally smarter than trying everything exists.

In 1971, Stephen Cook and Leonid Levin showed that SAT is NP-complete: it is, in a precise sense, the hardest problem of its kind, because any problem whose solutions can be quickly checked can be mechanically rewritten as a SAT instance. That is why brute force has always looked inherent to it. And the harder variant both AI labs attacked is worse still: not just deciding whether a satisfying assignment exists, but counting all of them — the problem called #3-SAT.

## What ETH actually says

Here is the hypothesis, unpacked slowly. Mathematicians write "subexponential time" as 2^o(n), and the little "o" carries the whole meaning. An exponent of o(n) is anything that grows more slowly than n itself — n divided by √log n, for instance, or n / log n, or √n. An algorithm running in 2^o(n) time is still unimaginably slow. But its exponent is shrinking relative to n, and that makes it qualitatively different from brute force, whose exponent is n in full.

ETH says: there is no algorithm, ever, anywhere, that solves 3-SAT in the worst case in 2^o(n) time. Not "nobody has found one." Not "it seems hard." A universal claim about every possible algorithm, including ones nobody has thought of yet.

Notice how much stronger this is than the famous P ≠ NP conjecture. P ≠ NP only rules out polynomial time — algorithms whose cost grows like n² or n¹⁰. Between polynomial and exponential lies an enormous middle ground, and P ≠ NP says nothing about it. ETH slams the door on the whole middle ground: nothing below a full exponential, ever.

There is an even stricter sibling, the Strong Exponential Time Hypothesis (SETH), proposed by the same authors. As you let clauses grow wider — 4 variables, 5, 6 and beyond — SETH says you cannot beat brute force by any constant factor in the exponent at all: no algorithm running in (2 − ε)ⁿ time for any ε > 0, on any width. SETH implies ETH. Both were conjectures, believed widely, proved by nobody.

Why would a field rest so much weight on an unproved claim? Because claims of this shape — "no algorithm can do better" — are the hardest statements in computer science. To prove one, you must argue about every algorithm that could ever be written, including ones based on ideas nobody has had yet. The field has managed this for only a handful of problems, and SAT is not among them. So researchers did the honest thing: they named the assumption, dated it, and kept a public ledger of what depended on it. ETH was never a secret weakness in the edifice. It was a labeled load-bearing wall.

<figure>
<svg width="680" height="380" viewBox="0 0 680 380" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="360" rx="14" fill="#f7f9fc"/>
<text x="340" y="48" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">The race ETH said could never be run</text>
<text x="40" y="96" font-size="17" font-weight="700" fill="#1e3a5f">Brute force: try every assignment — 2ⁿ</text>
<rect x="40" y="110" width="600" height="42" rx="8" fill="#1e3a5f"/>
<text x="640" y="138" text-anchor="end" font-size="16" font-weight="700" fill="#ffffff">exponent = n, in full&#160;</text>
<text x="40" y="196" font-size="17" font-weight="700" fill="#b91c1c">Claimed in October 2026: exponent = n · (log log n) / √log n</text>
<rect x="40" y="210" width="512" height="42" rx="8" fill="#dc2626"/>
<text x="40" y="282" font-size="16" fill="#374151">The divisor √log n grows — slowly, without limit — so the exponent is o(n):</text>
<text x="40" y="308" font-size="16" fill="#374151">smaller than n by an ever-widening factor. Still astronomical. Still super-polynomial.</text>
<text x="340" y="348" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">ETH forbade exactly this: any exponent smaller than n itself.</text>
</svg>
<figcaption>Figure 1 — The claimed running time stays hopelessly large, but its exponent grows more slowly than n — and that alone is what ETH ruled out.</figcaption>
</figure>

## Twenty-seven years of building on an unproven floor

ETH was written down in 1999 by Russell Impagliazzo, Ramamohan Paturi and Francis Zane. They were not claiming to have proved anything; they were marking out a floor and inviting the field to build on it, explicitly, so everyone would know which results stood on bedrock and which stood on an assumption.

The field built. In 2001, Impagliazzo, Calabrese and Paturi proved the Sparsification Lemma, a technical result with a social consequence: it made ETH portable. Hardness established for 3-SAT could now be carried across to hundreds of other problems. The carrying mechanism is the reduction, the workhorse of the whole field: to show that some other problem is hard, you give a mechanical translation that turns any instance of the known-hard problem into an instance of yours, so that a fast algorithm for your problem would secretly be a fast algorithm for the original. Chain enough translations together and one hypothesis about 3-SAT becomes a speed limit for problems that look nothing like logic puzzles. An entire subfield — fine-grained complexity — grew up around ETH and SETH, proving careful statements of the form "if ETH holds, then this problem in graph theory, or parameterized algorithms, or computational biology, or databases, or computational geometry cannot be solved faster than this." OpenAI's own announcement, 27 years later, describes the conjecture as having been used in hundreds of papers. Every one of those papers is conditional. The condition is what is now in question.

There is a fine irony from 2010. Ryan Williams proved that if anyone ever found even a slightly-faster-than-brute-force algorithm for SAT, that algorithm would automatically yield circuit lower bounds — separations between complexity classes that nobody knew how to prove by any other route. So a faster SAT algorithm was a strange kind of win-win bet: either ETH was true and the barrier was real, or it was false and breaking it would pay out in a second currency of results. The community both hoped for the breakthrough and built as if it would never come. Williams, the man who showed what breaking the barrier would be worth, is now one of the three experts shepherding the review of the claim that the barrier has been broken.

Meanwhile, practice lived a separate life. Engineers built SAT solvers — CDCL solvers and their descendants, which learn from each dead end they hit and prune the search accordingly — and industry put them to work checking chip designs, verifying software and scheduling logistics. These solvers dispatch enormous real-world formulas in seconds, because real formulas have structure that worst-case analysis ignores. The solvers got faster every year. The hypothesis, which is only about the worst case, never budged. For decades the two stories coexisted without touching: the theory said the worst case was a wall, and practice strolled around it daily.

## What the two labs actually produced

Both labs produced the same kind of object: a deterministic algorithm that counts all satisfying assignments of a 3-SAT formula — the harder #3-SAT problem — in time roughly 2^{O(n log log n / √log n)}. Counting is the stronger target: an algorithm that can count every satisfying assignment can certainly answer the yes-or-no question (the count is zero or it isn't), so a subexponential counting algorithm refutes ETH with room to spare. There is no wiggle room in which "deciding" might still be hard while "counting" got easy. Read the exponent once more: n, multiplied by a factor (log log n) and divided by a factor (√log n) that grows. The division wins. The exponent is n divided by something that grows without limit, which makes it o(n) — subexponential. This is not a near-miss or an adjacent result. It is a direct hit on the exact sentence ETH asserts.

OpenAI's manuscript is titled "The Exponential Time Hypothesis is False." Its internal model produced the disproof on October 16 and a formalization in Lean — a proof language whose output a computer can check line by line — on October 17. The paper and the Lean files are public in the company's openai/math GitHub repository. The model itself is unnamed: an unreleased internal system, and the repository's wider catalogue runs to 721 manuscripts in 373 families, about 42% of them formalized. OpenAI calls the manuscripts "raw research data, rather than polished academic papers," and explicitly defers to the mathematics community on questions of credit and precedence.

Anthropic's version arrived as a paper posted on the night of October 26, at 11:07 pm Eastern, in the company's formal-math repository: "A 2^o(n) Time Algorithm for 3-SAT," with the author listed, simply, as "Claude (Anthropic)," and a footnote acknowledging OpenAI's concurrent claim. Per Anthropic researcher Levent Alpoge, the core algorithm was found by an internal Claude research model on October 16 — the same day as OpenAI's — in a run of some 14 million output tokens, with no human input in the discovery itself; Anthropic's researchers then worked with the model to improve the presentation. Jelani Nelson, who reviewed Claude's proof independently, observed that the two proofs land at roughly the same bound, about exp(O(n / √log n)), using closely related techniques arrived at independently — the classic pattern in mathematics, in which two groups crack the same problem at the same moment because the tools have ripened.

Now the consequences, stated as precisely as the papers state them. If the proofs are correct, ETH is false. SETH falls with it, since SETH implied ETH. Every conditional lower bound that used ETH as its premise — across graph theory, parameterized algorithms, computational biology, databases, computational geometry — loses that premise and must be revisited one by one; nothing is automatically salvageable or automatically destroyed, the work has to be redone honestly. The same algorithmic ideas also give faster methods for classic problems such as Independent Set, Clique, Vertex Cover and Dominating Set.

And what it does not mean, in the labs' own words. It does not mean P = NP: the new algorithms are still hopelessly super-polynomial, unusable on any formula anyone will ever meet. Anthropic's paper states flatly that the result "says nothing about solving formulas in practice," and one summary of Claude's bound puts the crossover point — where the new algorithm first beats brute force — beyond 10^108 variables. OpenAI's paper says the result "does not bear on the P vs NP question directly, nor does it yield any practical algorithms." SAT solvers will not get faster this year because of this. What changed is a floor the field believed in for 27 years.

## The same announcement carried two more claims

OpenAI's October 26 announcement bundled three results, and the other two deserve a compact account.

The second is a proof of the local smoothing conjecture in every dimension, by means of a new auxiliary partial differential equation. Local smoothing, proposed in 1991 by Christopher Sogge, concerns how waves behave when they focus. Proving it in all dimensions also resolves, as consequences, the Kakeya conjecture and the Stein restriction conjecture in every dimension — two central open problems of harmonic analysis. The human record here was recent and hard-won: local smoothing in two dimensions fell in 2019 to Larry Guth, Hong Wang and Ruixiang Zhang, and the three-dimensional Kakeya conjecture fell in 2025 to Hong Wang and Joshua Zahl. Alexander Iosevich of the University of Rochester — Sogge's own student — called the claimed all-dimensions proof shocking and "a historic development." As with ETH, the natural-language manuscript and the Lean proof are public, left for researchers to organize their own effort to explain.

The third claim is the least checkable today. OpenAI says its model produced a rigorous existence proof for a class of interacting four-dimensional quantum field theories with gauge fields and fermions, including quantum chromodynamics, built on Tadeusz Balaban's constructive framework. A sub-result is the existence of pure Yang–Mills theory. Precision matters here: the Millennium Prize problem for Yang–Mills asks for existence *and* a mass gap — a proof that the theory's particles have a minimum positive mass. An existence proof alone does not solve the Millennium problem, and no one should report that it does. Uniquely among the three results, the physics materials are being withheld: the shepherd group, led by Nobel laureate David Gross, holds the AI-produced artifacts and intends to write the work up itself. That choice has already drawn public pushback — an independent Advisory Group on Mathematics and AI has called on OpenAI to release the physics proofs immediately.

## How anyone can check — and what checking cannot do

Both labs published Lean formalizations, and that is a genuinely new situation for a claim of this size. Lean is a proof assistant: a formal proof is a file a small, trusted program — the kernel — can verify mechanically, step by step, with no room for "the rest is obvious." Anthropic's repository pins its toolchain (Lean v4.33.1 with Mathlib), documents a build of about eight minutes on 24 virtual CPUs, and goes further: its continuous-integration pipeline re-verifies the proofs with a second, independently written proof kernel, and runs a comparator to check that the Lean statements match the theorems stated in the paper. The second kernel matters more than it may sound: the kernel is the one component of the system that must be trusted rather than checked, so having the whole proof re-examined by an independent implementation removes the "what if the checker itself has a bug" objection. Anyone with a computer can, in principle, replay all of it tonight.

But Anthropic's own README contains the sentence that keeps this honest: "Lean checks the proofs, but no machine checks that this file says what the paper says." A kernel can certify that a formal proof follows from a formal statement. It cannot certify that the formal statement faithfully captures the problem that ETH is actually about — that the encoding of "3-SAT," "algorithm," and "running time" in the formal file means what the community means by those words. That judgment is human work, and it is exactly the work now under way.

OpenAI's three results are each being shepherded by outside expert groups, under stated principles: transparency, no academic credit for OpenAI, and the groups working as unpaid volunteers. The ETH group is led by Impagliazzo and Paturi — the men who proposed the hypothesis in 1999 — together with Ryan Williams. They have said explicitly that their involvement "should not be taken as certification of the claim." Complexity theorist Lance Fortnow, who has written the book on P versus NP for a general audience, called the overall approach promising but unverified. OpenAI has also given $5 million to the Simons Foundation to fund workshops and programs helping researchers digest AI-produced results.

<figure>
<svg width="680" height="400" viewBox="0 0 680 400" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<rect x="10" y="10" width="660" height="380" rx="14" fill="#f7f9fc"/>
<text x="340" y="46" text-anchor="middle" font-size="21" font-weight="700" fill="#111827">Twenty-seven years, one assumption</text>
<line x1="50" y1="200" x2="630" y2="200" stroke="#94a3b8" stroke-width="3"/>
<circle cx="70" cy="200" r="9" fill="#1e3a5f"/>
<text x="70" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">1971</text>
<text x="70" y="238" text-anchor="middle" font-size="16" fill="#374151">Cook–Levin:</text>
<text x="70" y="260" text-anchor="middle" font-size="16" fill="#374151">SAT is</text>
<text x="70" y="282" text-anchor="middle" font-size="16" fill="#374151">NP-complete</text>
<circle cx="185" cy="200" r="9" fill="#1e3a5f"/>
<text x="185" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">1999</text>
<text x="185" y="238" text-anchor="middle" font-size="16" fill="#374151">Impagliazzo,</text>
<text x="185" y="260" text-anchor="middle" font-size="16" fill="#374151">Paturi, Zane</text>
<text x="185" y="282" text-anchor="middle" font-size="16" fill="#374151">propose ETH</text>
<circle cx="300" cy="200" r="9" fill="#1e3a5f"/>
<text x="300" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">2001</text>
<text x="300" y="238" text-anchor="middle" font-size="16" fill="#374151">Sparsification</text>
<text x="300" y="260" text-anchor="middle" font-size="16" fill="#374151">Lemma: ETH</text>
<text x="300" y="282" text-anchor="middle" font-size="16" fill="#374151">goes everywhere</text>
<circle cx="415" cy="200" r="9" fill="#1e3a5f"/>
<text x="415" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">2010</text>
<text x="415" y="238" text-anchor="middle" font-size="16" fill="#374151">Williams: faster</text>
<text x="415" y="260" text-anchor="middle" font-size="16" fill="#374151">SAT would prove</text>
<text x="415" y="282" text-anchor="middle" font-size="16" fill="#374151">circuit bounds</text>
<circle cx="530" cy="200" r="10" fill="#dc2626"/>
<text x="530" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#b91c1c">Oct 16, 2026</text>
<text x="530" y="238" text-anchor="middle" font-size="16" fill="#374151">Two AI systems,</text>
<text x="530" y="260" text-anchor="middle" font-size="16" fill="#374151">same day,</text>
<text x="530" y="282" text-anchor="middle" font-size="16" fill="#374151">independently</text>
<circle cx="615" cy="200" r="9" fill="#b45309"/>
<text x="615" y="160" text-anchor="middle" font-size="17" font-weight="700" fill="#111827">Now</text>
<text x="615" y="238" text-anchor="middle" font-size="16" fill="#374151">Reviewed by</text>
<text x="615" y="260" text-anchor="middle" font-size="16" fill="#374151">its own</text>
<text x="615" y="282" text-anchor="middle" font-size="16" fill="#374151">proposers</text>
<text x="340" y="356" text-anchor="middle" font-size="16" fill="#4b5563">A conjecture the field built on for a generation — now awaiting a verdict from the people who wrote it.</text>
</svg>
<figcaption>Figure 2 — From Cook–Levin to the day two AI systems claimed the same refutation, and the review fell to ETH's own authors.</figcaption>
</figure>

## A claim, not a verdict

Here is the honest ledger, as of today. Two respected labs say their models refuted a 27-year-old hypothesis, on the same day, by closely related routes. Both published machine-checkable proofs, which is more than most breakthrough claims offer. Expert groups led by the hypothesis's own authors are reviewing the work, and have certified nothing. No independent human confirmation of either ETH proof exists yet, and neither paper has been peer-reviewed.

What to watch is unglamorous and specific: the shepherd groups' reports, and whether the formal statements survive expert reading as faithful renderings of the problems they claim to settle. If they do, October 16, 2026 becomes a date the field remembers — the day the floor turned out to be a conjecture in the wrong direction, and the ones who found out were machines. If they don't, the episode still marks something: AI systems can now produce candidate proofs deep enough that settling them is a project, not an afternoon. The assumption stood for 27 years. Checking whether it fell will take a while longer — and for once, everyone involved is saying so out loud.
