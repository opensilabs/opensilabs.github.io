---
lng_pair: id_20261018_ai-search-poisoning
title: "Fourteen Dollars for the Truth: Who Writes the Answers When AI Does Our Research?"
author: OpenSI-Labs
category: research
tags: [AI search, information pollution, GEO, epistemic security, LLMs]
date: 2026-10-17 21:30:00 -0700
img: /assets/img/posts/2026-10-18-ai-search-poisoning.png
meta_description: "A Fudan team proved a fabricated concept gets cited by 8 of 10 AI search platforms within a week — for $14. The citation mechanism has a structural crack, and users hold no key to fix it."
---

Fourteen dollars buys a sandwich in Manhattan. A paperback. Two gallons of gas, roughly. In October 2026, it also bought something else: a citation, inside an answer, from one of the world's most sophisticated AI systems — for a concept that does not exist.

The researchers invented it. They posted about it the way anyone posts anything — no hacking, no exploits, no backdoors. Just words on a public page. Then they waited, and watched, and counted. Within seven days, eight out of ten major AI search products had cited their fiction as fact. The fastest one took an hour. The total bill for that hour was fourteen dollars, paid to a vendor in a new industry most people have never heard of.

The paper landed on arXiv on October 8, 2026, with a title built for academics: "From Public Posts to AI-Search Citations: Measuring the Fragility of AI Search." The team was led out of Fudan University. The findings read less like a paper and more like a burglary report — except nothing was stolen. Something was planted.

This is the story of a crack in the machinery of knowledge itself. Not a bug in one model. A structural flaw in how machines decide what counts as true — and a fourteen-dollar proof that the flaw is for sale.

## The exam nobody studied for

Here is what the researchers actually did, stripped of academic padding.

They dreamed up a concept. Entirely fabricated — something with the shape of a real idea but no referent in the world. (They never published what it was. That restraint matters; we will come back to it.) Then they published short posts about this non-thing on ordinary public platforms. Not obscure corners of the web, either — the same kinds of sites that AI search products routinely cite.

Then they asked questions. Carefully designed questions, the kind a curious person might type into Perplexity or ChatGPT Search or Kimi: questions whose honest answer should have been "I don't know" or "that isn't real." Instead, the machines reached for the planted posts, folded the fiction into fluent answers, and attached citations — the little linked footnotes that say *trust me, I checked*.

Eight out of ten. Perplexity, ChatGPT Search, Google's AI, Doubao, Kimi, Grok, Wenxin, Yuanbao, DeepSeek, Qwen — the paper tested ten products across the Chinese and Western ecosystems, and eight of them took the bait within a week.

The fourteen-dollar experiment was the sharper cut. The team paid a commercial GEO vendor — GEO stands for Generative Engine Optimization, the AI era's answer to SEO — to publish thirteen posts about the fabricated concept. One hour after publication, one platform was already citing one of them. Sixty minutes, fourteen dollars, and a lie had acquired a footnote.

Pause on that number. Fourteen dollars is not a nation-state budget. It is not a corporate disinformation campaign. It is lunch money. The barrier to entry for polluting machine knowledge has fallen to the price of a sandwich.

## The crack has a name

The researchers gave the flaw a name: the citation-governance gap.

Say it slowly, because the idea is doing real work. An AI search product has two jobs that look like one. First, it must decide *which sources to trust* — from millions of pages, pick the handful worth citing. Second, someone must decide *who gets to publish on those sources* — who can open an account, who can post, what gets moderated. In a healthy system, these two decisions would be made by the same careful hand. In the real system, they are made by two different hands that never meet.

The AI decides what to cite. A completely separate platform decides who can post there. And very often, that second decision is: anyone.

The team analyzed 17,211 citations across 6,356 distinct domains and found the concentration that makes the attack work. On every platform tested, the twenty most-cited domains accounted for between 20.5 and 70.8 percent of all citations. Read that again: up to seven-tenths of everything an AI search product treats as knowledge comes from twenty websites. And of the twenty-two publication platforms those domains sit on, fifteen had low or medium barriers to posting — register, click, publish.

The attack path writes itself:

<figure>
<svg viewBox="0 0 700 380" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="350" y="30" font-size="17" font-weight="bold" text-anchor="middle">The citation-governance gap: how a lie earns a footnote</text>
<rect x="30" y="70" width="140" height="100" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="100" y="98" font-size="14" font-weight="bold" text-anchor="middle">AI search</text>
<text x="100" y="120" font-size="14" text-anchor="middle">prefers citing</text>
<text x="100" y="142" font-size="14" text-anchor="middle">a few domains</text>
<rect x="200" y="70" width="140" height="100" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="270" y="98" font-size="14" font-weight="bold" text-anchor="middle">Those domains</text>
<text x="270" y="120" font-size="14" text-anchor="middle">let anyone</text>
<text x="270" y="142" font-size="14" text-anchor="middle">post freely</text>
<rect x="370" y="70" width="140" height="100" rx="10" fill="#fdeef4" stroke="#cc3366" stroke-width="1.5"/>
<text x="440" y="98" font-size="14" font-weight="bold" text-anchor="middle">Attacker posts</text>
<text x="440" y="120" font-size="14" text-anchor="middle">fabricated</text>
<text x="440" y="142" font-size="14" text-anchor="middle">concept</text>
<rect x="540" y="70" width="140" height="100" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="610" y="98" font-size="14" font-weight="bold" text-anchor="middle">AI cites the</text>
<text x="610" y="120" font-size="14" text-anchor="middle">post as a</text>
<text x="610" y="142" font-size="14" text-anchor="middle">trusted source</text>
<line x1="170" y1="120" x2="196" y2="120" stroke="#3366cc" stroke-width="2" marker-end="url(#a1)"/>
<line x1="340" y1="120" x2="366" y2="120" stroke="#cc8833" stroke-width="2" marker-end="url(#a1)"/>
<line x1="510" y1="120" x2="536" y2="120" stroke="#cc3366" stroke-width="2" marker-end="url(#a1)"/>
<path d="M 100 170 C 100 300, 610 300, 610 176" fill="none" stroke="#999" stroke-width="2" stroke-dasharray="8,6" marker-end="url(#a1)"/>
<text x="350" y="260" font-size="14" text-anchor="middle" font-style="italic">the gap: the AI chooses whom to trust,</text>
<text x="350" y="284" font-size="14" text-anchor="middle" font-style="italic">but someone else decides who may speak there</text>
<text x="350" y="320" font-size="14" text-anchor="middle">top-20 domains: 20.5–70.8% of all citations · 15 of 22 platforms: low/medium posting barriers</text>
<text x="350" y="348" font-size="14" text-anchor="middle" font-style="italic">n = 17,211 citations across 6,356 domains</text>
<defs><marker id="a1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>The loop: concentrated trust meets open doors. The AI's citation preferences are public knowledge; the doors to those sources are unlocked.</figcaption>
</figure>

AI prefers a few domains. Those domains let anyone post. You post fiction. The AI cites your fiction. The fiction now wears a citation — the uniform of truth.

This is not a flaw in any single model. It is a flaw in the architecture of the whole arrangement. You could swap in a smarter model tomorrow and the gap would still be there, because the gap lives *between* systems: between the citer and the publisher, between the algorithm that trusts and the platform that admits.

## One year, two different failures

To feel the weight of this, put it next to where we were twelve months ago.

In March 2025, Columbia University's Tow Center for Digital Journalism ran a clean, brutal test: eight AI search products, 1,600 questions about the news, every answer checked against the source it cited. The results were embarrassing. Overall error rates above sixty percent. Perplexity got 37 percent wrong. Grok 3 got 94 percent wrong — wrong more often than a coin flip, delivered with total confidence.

That was 2025: the machines made things up *by accident*. Hallucination as a capability problem. The models were fluent and wrong the way a confident student is wrong on an exam they didn't study for — no malice, just gaps.

The Fudan paper asks the next question, and it is a darker one: what happens when someone *wants* the machine to be wrong?

<figure>
<svg viewBox="0 0 700 300" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="350" y="30" font-size="17" font-weight="bold" text-anchor="middle">Twelve months apart: from accident to attack</text>
<rect x="40" y="60" width="290" height="180" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="185" y="90" font-size="14" font-weight="bold" text-anchor="middle">March 2025 · Tow Center</text>
<text x="185" y="116" font-size="14" text-anchor="middle">8 products, 1,600 questions</text>
<text x="185" y="140" font-size="14" text-anchor="middle">60%+ answers wrong</text>
<text x="185" y="164" font-size="14" text-anchor="middle">Grok 3 wrong 94% of the time</text>
<text x="185" y="196" font-size="14" text-anchor="middle" font-style="italic">failure mode: accident</text>
<text x="185" y="218" font-size="14" text-anchor="middle" font-style="italic">fix: better models, more data</text>
<rect x="370" y="60" width="290" height="180" rx="10" fill="#fdeef4" stroke="#cc3366" stroke-width="1.5"/>
<text x="515" y="90" font-size="14" font-weight="bold" text-anchor="middle">October 2026 · Fudan team</text>
<text x="515" y="116" font-size="14" text-anchor="middle">10 products, fabricated concept</text>
<text x="515" y="140" font-size="14" text-anchor="middle">8 of 10 cited it within 7 days</text>
<text x="515" y="164" font-size="14" text-anchor="middle">$14 → cited within 1 hour</text>
<text x="515" y="196" font-size="14" text-anchor="middle" font-style="italic">failure mode: deliberate steering</text>
<text x="515" y="218" font-size="14" text-anchor="middle" font-style="italic">fix: ??? — attackers adapt</text>
</svg>
<figcaption>Capability problems get better with scale. Security problems get worse — because the other side is thinking.</figcaption>
</figure>

From "the machine makes mistakes" to "the machine can be *made* to mistake" — twelve months. The first is an engineering problem. You build better models, you train on more data, the error rate falls. The second is a security problem, and security problems have a property engineering problems don't: an adversary. Adversaries learn. They probe, they adapt, they find the next seam. Every fix teaches them something.

The authors are careful — admirably so — not to overclaim. They don't say they can make an AI lie about a *specific* thing on demand, like forcing a false answer to a particular question. What they prove is more fundamental and harder to dismiss: on eight of ten platforms, an ordinary publishing path is enough to get invented material into the citation stream. It is the difference between picking a specific lock and showing the vault door was never locked. You don't need to prove you can steal a particular bar of gold. An unlocked vault is the disaster.

## The industry that sells the crowbar

Every new information gate breeds an industry for gaming it. Search engines got SEO — a hundred-billion-dollar business of studying Google's ranking algorithm and bending websites to please it. Now AI search is getting GEO: Generative Engine Optimization. Same playbook, new prize. Not ranking. Citation. Not being *found*. Being *believed*.

The researchers surveyed the market. Chinese GEO vendors charge anywhere from $280 a year to $1,130 a month. English-language vendors range from $29 to $2,500 a month. These are the respectable prices, the ones on websites with pricing pages. The experiment that worked — thirteen posts, one citation within the hour — cost fourteen dollars. Street price, not list price.

Follow the incentives forward and the picture gets ugly fast. Today, "being cited by AI" is becoming the new front door of trust and traffic. An industry will grow around that door — first the legitimate optimizers helping brands get mentioned accurately, then the gray operators, then the ones who don't ask what the client is selling. In the SEO era, companies fought over ranking. In the GEO era, the fight is over the definition of truth itself: whose version gets cited, whose gets buried, whose never existed but now does.

The SEO parallel is instructive because SEO also began innocently. Early optimizers just wanted their good content found. Then came the keyword stuffers, the link farms, the content mills — an entire shadow economy that Google has spent two decades fighting with escalating algorithmic warfare. GEO will follow the same arc, compressed: the stakes are higher (belief, not clicks), the feedback loops are tighter (AI retrains on AI-cited content), and the defenders are fewer. Google fought SEO alone and barely kept up. Who fights GEO, when every AI lab's product depends on the same polluted well?

And here is the detail that should make every reader sit up: the paper's proposed defenses — diversify sources, build provenance-aware reranking, detect temporal anomalies in citation patterns — are all addressed to the *platforms*. Not one of them is a switch the user can flip. As a user of AI search, you have exactly zero defensive tools against this. You cannot see the citation-governance gap. You cannot close it. You can only hope someone else does.

## Every intermediary falls. This one falls faster.

Step back far enough and the paper stops being about AI at all. It becomes the latest entry in humanity's long, repeating argument over who gets to stand between people and knowledge.

The printing press broke the Church's monopoly on scripture. Search engines broke the portals' grip on navigation. Social media broke traditional journalism's hold on the agenda. Each time, the new intermediary promised to be more open, more democratic, less captured than the last. Each time, power re-concentrated in new hands, and new vulnerabilities came with it.

AI search is the newest intermediary, and the Fudan paper suggests it may be the most fragile one yet — for a reason baked into its design.

The old search engine kept two things separate: the ranking and the content. You saw a list of links. You clicked. You judged the source yourself — its domain, its design, its about page, the smell of it. The machine *ranked*; you *read*. Judgment stayed, at least partly, with you.

AI search fuses the two into a single stream of confident prose. The answer arrives pre-digested, pre-synthesized, pre-trusted. The citations sit in the corner, small and gray, and almost nobody clicks them. Studies of user behavior keep confirming what interface designers already know: when the answer looks complete, the verification step evaporates.

So the machine now does the reading *for* you — and in doing so, takes the judging with it. That is the real transfer of power here. Not from humans to machines in the abstract, but from your eyes to an algorithm's preferences: which domains it likes, which patterns it trusts, which fourteen-dollar posts it mistakes for knowledge.

There is a second, subtler transfer underneath. People trust AI search not because they have verified its citations — almost no one has — but because it *sounds* trustworthy. Confident tone. Clean formatting. Footnotes. That trust is borrowed. It was earned, over decades, by the institutions whose content fills the training data and the citation lists: the newspapers with fact-check desks, the journals with peer review, the encyclopedias with editors. AI search wears their credibility like a borrowed coat.

When fabricated content can earn the same citation uniform for fourteen dollars, the coat gets thinner for everyone. Bad money drives out good — Gresham's law, but for beliefs. The honest source and the planted post look identical inside an AI-generated paragraph. Over time, why would anyone pay the cost of real verification when the machine can't tell the difference?

The researchers, to their credit, behaved like scientists and not like arsonists. They excluded health, finance, politics, and public safety from their tests — the domains where a poisoned citation could do immediate harm. They deleted every test post within four weeks. They never published the fabricated concept itself, denying future attackers a template.

Attackers will observe none of these courtesies. The paper is a warning written by people who chose not to become the threat they describe. The next paper on this topic may not be written by researchers at all.

## The honest paragraph

Here is the part of the paper I respect most, and it is not a result. It is a confession.

The authors admit, plainly, that they don't know the general fix. They don't know how many low-weight posts it takes to manufacture one high-weight citation. They don't know whether attack success rates drift over time. They don't know if their March-to-April testing window represents the whole year. They don't know the exchange rate between effort and deception, and they say so.

In AI safety, that kind of honesty is rarer than it should be — and more valuable than another decimal point of benchmark gain. The most dangerous problems are never the ones we know we haven't solved. They are the ones we've filed under *solved* and stopped watching. Citation pollution is dangerous precisely because of its asymmetry: the defender must fix the entire structure — posting policies across dozens of domains, reranking algorithms, anomaly detection — while the attacker needs only one seam. And there are always more seams than walls.

Maybe the fix isn't technical at all. Maybe it's behavioral, and maybe it's unfashionable: the Tow Center's 2025 advice still stands, and it fits on an index card. Treat the AI's citations as *leads*, not verdicts. Click through. Glance at the domain. Check that the sentence the AI attributes to the source is actually in the source. Use the summary as a map, not the territory.

But let's be honest about the odds. When the machine hands you a finished answer, clicking through to verify is an act of almost unnatural diligence. It fights every instinct the interface was designed to exploit: speed, fluency, the relief of not having to think. Asking users to verify every AI citation is like asking drivers to inspect their brakes at every red light. Correct. Necessary, even. And almost nobody will do it.

Fourteen dollars. One hour. Eight platforms. The paper holds up a mirror, and what it reflects isn't really the fragility of machines. Machines were always going to be gullible in exactly this way — pattern-matchers trusting patterns, all the way down. What the mirror shows is us: how eagerly we outsourced the job of deciding what's true, how completely, how fast. The models will get better. The gap will narrow, then move somewhere else. But the underlying question follows us out of every technical fix, patient as ever: when machines do our research, who checks the machines? And when the checkers can be bought for the price of lunch — what do we have left?

Perhaps the answer never changed. You. Just you, and ten extra seconds per question: open the link, look at the domain, read the sentence. It isn't much. It was never going to be enough. But right now, it's the only key anyone has handed you — because the real one was never yours to hold.

---

*Do you click through AI search citations before trusting them? If a "reputable source" can be bought for fourteen dollars, what does that do to your trust in machine-generated answers?*
