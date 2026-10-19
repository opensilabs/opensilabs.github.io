---
lng_pair: id_20261020_scientisttwo
title: "When AI Starts Writing Papers: ScientistTwo and the Twilight of Discovery?"
author: OpenSI-Labs
category: research
tags: [AI scientist, automated research, LLMs, philosophy of science, Google]
date: 2026-10-19 21:30:00 -0700
img: /assets/img/posts/2026-10-20-scientisttwo.png
meta_description: "Google's ScientistTwo improved 86 of 107 published ML methods by 25.2% on average — autonomously. When AI becomes the main producer of knowledge, what happens to discovery itself?"
---

**Would you read a paper nobody wrote?**

Not nobody — no human. A system that picks up a published machine-learning paper, reads it, finds the weak joint, designs a better method, writes the code, runs the experiments, and then — this is the part that should stop you — writes up the result as a paper of its own.

On September 17, 2026, seven researchers at Google Cloud AI Research posted it to arXiv with an unadorned title: *ScientistTwo: Pioneering the Human Knowledge Frontier with Autonomous AI*. Jaehyun Nam, Jinsung Yoon, Yanzhou Pan, Yubo Wang, Rui Meng, Parthasarathy Ranganathan, Tomas Pfister. Seven names. And a system that might make the seventh name, one day, redundant.

The experiment was brutally concrete. They fed ScientistTwo 107 problems, each drawn from a published paper at ICLR, ICML, or NeurIPS — the venues where machine-learning careers are made. The system completed 86 of them on its own. On average, its methods beat the published human originals by 25.2%. Then came the part the authors must have enjoyed most: they submitted ScientistTwo's output to AI reviewers. Under the Stanford Agentic Reviewer, the machine-written papers scored above the average of accepted ICLR 2026 and NeurIPS 2025 submissions. Against a reviewer the system had never seen, 72.1% would still have been accepted.

One sentence in the paper deserves to be quoted in full, because the division of labor it describes is the whole story: "the human researcher defines the target scientific challenge, while the AI autonomously orchestrates the path to advance it."

Humans point. Machines march. Consider what that concedes. In the folklore of science, the march — designing the experiment, debugging the method, adjusting course after failure — was supposed to be the irreducibly human part, the craft no textbook could teach. Google is now telling us the craft can be compiled.

Imagine you are the reviewer. A paper lands in your queue: clean ablations, honest error bars, a method section that reads like it was written by someone who suffered through the debugging. You recommend accept. Months later you learn the suffering was simulated — the "author" never felt the 3 a.m. despair of a diverging loss curve, never had the small triumph of a baseline finally beaten. Does the paper get worse, retroactively? The numbers don't change. The insight, whatever it is, doesn't change. Only the story behind it evaporates. And here is the uncomfortable question the field will spend the next decade avoiding: if the story was never the point, what was all that suffering *for*?

**Not the first AI scientist. Maybe the first AI peer.**

The dream of automated science is older than the transformer. AutoML tuned hyperparameters. Later systems searched architectures and ran ablations. But those were instruments: you handed them a well-defined optimization problem and they hill-climbed inside it. ScientistTwo faces something else entirely — a complete paper, an open research question. It has to decide *where the improvement is worth pursuing*, *how to pursue it*, and *whether the result holds up*.

Those three decisions are precisely what makes a PhD student's first year miserable. Choosing a direction, dreaming up the idea, proving the idea works — a supervisor can gesture at these, but mostly you learn by drowning. ScientistTwo, across 107 attempts, learned to swim 86 times.

Now the cold water. All 107 problems were machine learning, and all of them were the convergent kind: improve an existing method. Nothing here proposed a new direction or opened unmapped territory. ScientistTwo is a superb follower, not yet an explorer. And yet the result should unsettle anyone who works in a lab, because followership is what most of modern research *is*. Read paper, reproduce, tweak, improve, write up, submit. ScientistTwo now walks that chain alone. What remains — "decide what to work on" — is exactly the slice the paper reserves for humans.

**The lineage: from oracle to author.**

To feel the size of this step, rewind. The first great AI-for-science story was AlphaFold: a machine that predicted protein structures with atomic accuracy. But AlphaFold was an *oracle*. It answered a question humans posed, and humans did the interpreting — the papers about what the structures *meant* were still written by people, with human judgment about which predictions mattered and why.

Then came the copilots: systems that suggested code, drafted literature reviews, proposed hypotheses for a human to vet. Useful, but unmistakably subordinate — the human remained the author in every sense that mattered, the one whose name carried the responsibility.

ScientistTwo crosses a line the copilots never touched: *authorship*. Not assistance with the paper, but the paper. The system doesn't suggest the experiment; it runs it. It doesn't draft the method section; it decides what the method is. Somewhere between AlphaFold's oracle and this, the machine stopped being a tool you use and became a colleague you cite. That is why "peer" is the right word, and why it stings. A tool can be better than you without threatening you. A peer can replace you.

<figure>
<svg width="680" height="300" viewBox="0 0 680 300" font-family="system-ui, -apple-system, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">The ScientistTwo loop: from published paper to new paper</text>
<rect x="20" y="60" width="150" height="52" rx="8" fill="#e8f0fe" stroke="#3b6fd4"/>
<text x="95" y="82" font-size="14" text-anchor="middle">1. Read published</text>
<text x="95" y="102" font-size="14" text-anchor="middle">paper</text>
<rect x="185" y="60" width="150" height="52" rx="8" fill="#e8f0fe" stroke="#3b6fd4"/>
<text x="260" y="82" font-size="14" text-anchor="middle">2. Find the weak</text>
<text x="260" y="102" font-size="14" text-anchor="middle">joint</text>
<rect x="350" y="60" width="150" height="52" rx="8" fill="#e8f0fe" stroke="#3b6fd4"/>
<text x="425" y="82" font-size="14" text-anchor="middle">3. Design better</text>
<text x="425" y="102" font-size="14" text-anchor="middle">method</text>
<rect x="515" y="60" width="150" height="52" rx="8" fill="#e8f0fe" stroke="#3b6fd4"/>
<text x="590" y="82" font-size="14" text-anchor="middle">4. Write code,</text>
<text x="590" y="102" font-size="14" text-anchor="middle">run experiments</text>
<rect x="265" y="180" width="150" height="52" rx="8" fill="#fef3e0" stroke="#d4a03b"/>
<text x="340" y="202" font-size="14" text-anchor="middle">5. Write the new</text>
<text x="340" y="222" font-size="14" text-anchor="middle">paper</text>
<line x1="170" y1="86" x2="183" y2="86" stroke="#888" stroke-width="2" marker-end="url(#arr)"/>
<line x1="335" y1="86" x2="348" y2="86" stroke="#888" stroke-width="2" marker-end="url(#arr)"/>
<line x1="500" y1="86" x2="513" y2="86" stroke="#888" stroke-width="2" marker-end="url(#arr)"/>
<line x1="590" y1="112" x2="590" y2="140" stroke="#888" stroke-width="2"/>
<line x1="590" y1="140" x2="420" y2="140" stroke="#888" stroke-width="2"/>
<line x1="420" y1="140" x2="420" y2="176" stroke="#888" stroke-width="2" marker-end="url(#arr)"/>
<line x1="265" y1="206" x2="120" y2="206" stroke="#888" stroke-width="2" stroke-dasharray="5,4"/>
<line x1="120" y1="206" x2="120" y2="140" stroke="#888" stroke-width="2" stroke-dasharray="5,4"/>
<line x1="120" y1="140" x2="95" y2="114" stroke="#888" stroke-width="2" stroke-dasharray="5,4" marker-end="url(#arr)"/>
<text x="340" y="268" font-size="14" text-anchor="middle" font-style="italic">the output of one cycle becomes the input of the next — recursively</text>
<defs><marker id="arr" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto"><polygon points="0,0 8,4 0,8" fill="#888"/></marker></defs>
</svg>
<figcaption>Figure 1: The ScientistTwo pipeline. A human points at the challenge; the machine runs the rest — and its output can seed the next cycle.</figcaption>
</figure>

**The sharp counterpoint: it cannot doubt itself.**

A few weeks after ScientistTwo appeared, researchers at Epoch AI and Anthropic published a finding that lands like a bucket of ice water: today's agents are missing something the paper never mentions — scientific self-criticism. On tasks that mimic real research, a frontier model's performance sat at roughly 15% of a human reference.

Hold these two results side by side and they form a perfect tension.

ScientistTwo proves the machine can now *execute* the research loop along a set course, and execute it better than average. The Epoch AI work warns that the machine cannot yet *suspect* the course — cannot do what good scientists do at 2 a.m., staring at the data and asking: what if I'm wrong about everything?

That distinction is the whole history of science in miniature. The great breaks came from doubting the road, not paving it faster: Einstein doubting Newton, Darwin doubting design, Wegener doubting fixed continents. An AI that only optimizes along the given direction can flood the world with *better* papers and never produce a *different* one.

It is worth pausing on what self-criticism actually is, because the phrase risks sounding like a soft virtue. It isn't. It is the engine. Karl Popper's entire philosophy of science rests on a single asymmetry: no number of confirming experiments proves a theory, but one refuting experiment can kill it. Science advances not by accumulating support but by surviving attempts at murder — the scientist's own attempts, first and most ruthlessly. The 2 a.m. doubt is not a mood; it is the method, internalized. An agent that cannot turn its skepticism on its own premises is not doing science in Popper's sense at all. It is doing something else — extraordinarily competent engineering — and calling it by science's name. The Epoch AI result suggests we should take that distinction seriously before we hand the keys over: a system that cannot falsify itself can still be wrong at scale, faster than any human institution can correct it.

So perhaps this is the honest framing: ScientistTwo may be a revolution in research *productivity*, not research *creativity*. It drives the cost of follow-up science toward zero. Paradigm shifts remain human territory — for now.

**The apprenticeship is the product.**

Here is a consequence nobody in the paper discusses, because it is not a technical claim: what happens to the training of scientists? A PhD is not a degree; it is an apprenticeship. You learn research the way you learn a craft — by doing the march, badly, for years, under someone who has done it before. The suffering is the pedagogy. The diverging loss curves, the failed ablations, the months spent chasing a hypothesis that was wrong — that is where judgment forms.

If the march gets automated, the apprenticeship collapses. Why would a lab hire a graduate student to do what ScientistTwo does faster and better? And if no student ever walks the chain by hand, where do the people who "define the challenges" come from? Judgment is not taught in lectures; it is the scar tissue of a thousand small failures. A generation raised on machine-executed research may be fluent in pointing and illiterate in marching — and then, one day, there will be no one left who remembers what the march felt like, which means no one left who can tell when the machine is marching confidently in the wrong direction.

This is not speculation about a distant future. Every automation of craft follows this arc: the weavers, the navigators, the typesetters. The craft doesn't vanish; it migrates upward, into the smaller and smaller circle of people who still need to understand the thing itself. The question is whether "understanding the thing itself" remains a job, or becomes a hobby.

**Three shocks, if this scales.**

Pull the camera back. Suppose systems like this mature. What happens to science?

The first shock is volume. One hundred and seven papers was a *test set*. Deploy a thousand such systems and how many "improved" papers appear per year? Peer review at the top venues is already drowning; what does it do under a tenfold flood? When publication stops being scarce, the currency of publication collapses with it. Note the cruel irony: the very metric ScientistTwo was validated against — acceptance by AI reviewers — becomes meaningless once AI reviewers are grading AI authors at industrial scale. The evaluation loop closes on itself, humans optional. We have seen this movie in content farms and programmatic SEO; we are about to watch the arthouse version, with LaTeX.

The second shock is the division of labor. "Humans define challenges, AI orchestrates the path" sounds like partnership until you notice the asymmetry: fewer and fewer humans defining, more and more machines orchestrating. One day the challenges themselves may be machine-proposed. Where, exactly, do humans sit in that chain? The paper's authors would presumably answer: at the top, choosing what matters. But "what matters" is not a technical judgment — it is a value judgment, downstream of what a civilization cares about. Do we want the allocation of scientific attention decided by systems that have never cared about anything? That question has no benchmark. It cannot be ablated.

The third shock is the deepest, and it is philosophical: what do we mean by *discovery*? Traditionally, discovery meant a human understanding something for the first time. But if an AI independently improves a method and no human grasps *why* it works — the paper is published, the experiments reproduce, the metrics go up — has a discovery occurred? Where did the understanding happen?

Chess already ran this experiment. After AlphaGo, human players studied its games and got stronger. Nobody claimed the machine had "discovered a new theory of Go" — it found good moves humans hadn't. ScientistTwo may be the same: it finds good *methods*, not new *understanding*. And understanding is the part science actually treasures.

There is an old thought experiment for this, and it has never felt less hypothetical. John Searle's Chinese Room: a man in a room, following rulebooks, produces perfect Chinese replies without understanding a word of Chinese. Searle's point was that syntax is not semantics — shuffling symbols correctly is not the same as knowing what they mean. ScientistTwo is the Chinese Room with a publication record. It shuffles the symbols of research — hypotheses, ablations, error bars — with superhuman fluency. The papers come out. The metrics go up. But does anything in the room *understand*? The system cannot tell you why the method works in the way a physicist can tell you why the equation holds; it can only show you that it does. Science has always tolerated this gap — engineering routinely outruns theory — but it has never before *automated* it at scale. We are about to find out what a literature looks like when the understanding lags the results by design, forever.

<figure>
<svg width="680" height="280" viewBox="0 0 680 280" font-family="system-ui, -apple-system, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">The tension: optimization power vs. self-criticism</text>
<text x="170" y="60" font-size="14" font-weight="bold" text-anchor="middle">What ScientistTwo shows</text>
<text x="510" y="60" font-size="14" font-weight="bold" text-anchor="middle">What Epoch AI warns</text>
<rect x="40" y="75" width="260" height="150" rx="8" fill="#e8f5e9" stroke="#43a047"/>
<text x="170" y="105" font-size="14" text-anchor="middle">Executes the research</text>
<text x="170" y="127" font-size="14" text-anchor="middle">loop autonomously</text>
<text x="170" y="155" font-size="14" text-anchor="middle" font-weight="bold">86 / 107 improved</text>
<text x="170" y="177" font-size="14" text-anchor="middle">+25.2% avg gain</text>
<text x="170" y="199" font-size="14" text-anchor="middle">beats avg accepted papers</text>
<rect x="380" y="75" width="260" height="150" rx="8" fill="#fbe9e7" stroke="#d4452f"/>
<text x="510" y="105" font-size="14" text-anchor="middle">Cannot doubt its own</text>
<text x="510" y="127" font-size="14" text-anchor="middle">direction</text>
<text x="510" y="155" font-size="14" text-anchor="middle" font-weight="bold">~15% of human</text>
<text x="510" y="177" font-size="14" text-anchor="middle">reference on research-</text>
<text x="510" y="199" font-size="14" text-anchor="middle">mimicking tasks</text>
<text x="340" y="258" font-size="14" text-anchor="middle" font-style="italic">better papers, yes — different papers, not yet</text>
</svg>
<figcaption>Figure 2: The two findings together. Machines now out-produce the average researcher — and still can't do what a sleepless graduate student does at 2 a.m.</figcaption>
</figure>

**We are standing on a boundary, honestly unsure which side.**

The paper's title contains a word worth turning over: *Pioneering*. What exactly is being pioneered — the frontier of knowledge, or the frontier of the reality that humans are no longer its primary producers?

The optimistic version: AI absorbs the drudgery of follow-up science, and human scientists finally get to spend their lives on what matters — bold conjectures, the stubborn *why*. The physical labor of research gets automated; the intellectual labor becomes more precious.

The pessimistic version: when machines can mass-produce papers "25% better than average," the institutions built on publication scarcity — tenure, grants, prestige — come apart. Worse, humans may quietly lose the ability to do research by hand, the way GPS quietly took our sense of direction.

But the most honest version is the shortest: we don't know. ScientistTwo is a milestone, but it functions less like an answer than a mirror, reflecting how thin our understanding of "research" really is. We thought research *was* papers. Maybe research was always papers *plus* understanding *plus* doubt *plus* curiosity. The machine has taken the papers. What remains is what we must now defend.

107 problems. 86 improvements. A 25.2% gain. The numbers will age; the systems will iterate. The question will stay: in an era when AI writes its own papers, where does the human scientist's value live?

Perhaps not in the papers at all — but in the person awake at 2 a.m., staring at the data, wondering if everything they believed is wrong. For now, at least, the machines don't lose sleep.

And there is a final, quieter possibility worth naming. Every previous automation panic assumed the automated thing was the valuable thing, and mourned it. But sometimes the automation reveals that the valuable thing was elsewhere all along — that the weavers' real product was never cloth but the towns the mills built, that the navigators' real product was never charts but the voyages. If ScientistTwo takes the papers, what it may reveal is that the papers were never the point either. The point was always the understanding, the doubt, the curiosity — the parts no system has yet learned to fake. We may look back on this as the moment science remembered what it was for.

---

*Discussion: if AI-written papers outperform most human-written ones, would you still insist that research must be done by humans? Where, exactly, in the pipeline does the irreplaceable human live?*
