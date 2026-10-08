---
lng_pair: id_20261007_vista-arc-agi-3
title: "The Models Were Never Dumb. They Were Blind."
author: OpenSI-Labs
category: research
tags: [ARC-AGI-3, visual memory, AI agents, MIT, VISTA]
date: 2026-10-07 06:00:00 -0700
img: /assets/img/posts/2026-10-07-vista-arc-agi-3.png
meta_description: "MIT's VISTA harness took Claude Opus 5.0 from 40.68 to a perfect 100 on ARC-AGI-3 with zero new training — by giving the model real eyes and a lossless memory. The bottleneck was never intelligence; it was plumbing."
---

On October 1, five MIT researchers quietly posted a [paper](https://arxiv.org/abs/2610.02200) that reads like an indictment of the whole agent industry. It is called VISTA — a Visual Harness for Reasoning in an Interactive World — and its headline number is startling: Claude Opus 5.0's score on ARC-AGI-3, the interactive reasoning benchmark, went from 40.68 to a perfect 100.00. All 25 public games solved, every level, using 57.4% fewer actions than first-time human players. No new weights. No new training run. The gap between 40 and 100 was not a model at all. It was plumbing.

The authors' argument is almost insulting in its simplicity: the models were never dumb; they were blind. ARC-AGI-3's official interface hands the model a 64×64 grid of numbers and asks it to play visual puzzles — a spreadsheet pretending to be a picture. Humans see the game. The models were reading a ledger. VISTA simply gives them what we take for granted: rendered screenshots at 512×512, a memory that keeps every frame intact, and the freedom to look closer whenever they want.

<svg viewBox="0 0 720 336" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="VISTA: the loop around the model">
  <defs>
    <marker id="arrV1a" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
    <marker id="arrV1b" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto-start-reverse"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">VISTA: the loop around the model</text>
  <rect x="270" y="42" width="180" height="66" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="360" y="66" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">REMEMBER</text>
  <text x="360" y="86" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">lossless visual memory</text>
  <text x="360" y="102" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">every frame, indexed by turn</text>
  <rect x="30" y="152" width="150" height="66" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="105" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">SEE</text>
  <text x="105" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">512×512 screenshots</text>
  <text x="105" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">not 64×64 number grids</text>
  <rect x="285" y="152" width="150" height="66" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="360" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#5f3dc4">MODEL</text>
  <text x="360" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">unchanged weights,</text>
  <text x="360" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">zero new training</text>
  <rect x="540" y="152" width="150" height="66" rx="10" fill="#ebfbee" stroke="#2f9e44" stroke-width="2"/>
  <text x="615" y="176" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#2b8a3e">INSPECT</text>
  <text x="615" y="196" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">play · zoom · read_pixels</text>
  <text x="615" y="212" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">history — model-directed</text>
  <rect x="270" y="262" width="180" height="66" rx="10" fill="#fff5f5" stroke="#e03131" stroke-width="2"/>
  <text x="360" y="286" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#c92a2a">NOTEBOOK</text>
  <text x="360" y="306" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">GUIDE.md + WORKING.md</text>
  <text x="360" y="322" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">persistent + working notes</text>
  <line x1="182" y1="185" x2="283" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="437" y1="185" x2="538" y2="185" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="110" x2="360" y2="150" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
  <line x1="360" y1="220" x2="360" y2="260" stroke="#1c7ed6" stroke-width="2" marker-start="url(#arrV1b)" marker-end="url(#arrV1a)"/>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">VISTA wraps an unchanged model in eyes, a lossless memory, and a notebook. The intelligence was already there; the interface was not.</p>

Three pieces make the harness work. First, visual observations: rendered screenshots instead of numeric grids. Second, lossless visual memory: every frame — including intermediate animation frames — archived in its original form, indexed by turn and frame number, living outside the model's context window so nothing decays or gets compressed away. Third, model-directed inspection: the agent itself decides what to examine, with four tools — play to act in the game, inspect to zoom into any region of any past frame, read_pixels for exact numerical values when precision matters, history to revisit earlier actions and their results. Around the loop sit two plain text files: GUIDE.md, persistent notes carried across the whole session, and WORKING.md, a scratchpad for the current game. The harness is purely mechanical. No trained components, and the same short prompt template drives all 25 games.

The numbers deserve a slow read. Claude Opus 5.0: 40.68 → 100.00 across 183 levels and 7,302 total actions, against 17,135 for first-time human players. On a single game, m0r0, humans needed 1,107 steps; Claude took 219. GPT-5.6 Sol tells the same story from further down: 13.33 at baseline, 47.32 from screenshots alone, 99.00 with the full harness. Even a 320B open-weight model — barely alive at 1.89 — climbed to 66.93. The runs are stable, too: three repeats landed at 99.00, 98.90, 99.23. The authors' framing is careful — "to our knowledge," the first perfect score on ARC-AGI-3 without program synthesis — and worth pausing on: this summer's leading systems all built per-game simulators, hand-written code that models each game's rules. VISTA derives the same rules in a few sentences of working notes.

<svg viewBox="0 0 720 348" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Same weights, new harness: scores before and after VISTA">
  <text x="360" y="22" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">Same weights, new harness: RHAE on ARC-AGI-3</text>
  <rect x="180" y="44" width="12" height="12" fill="#adb5bd"/><text x="198" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">official harness baseline</text>
  <rect x="380" y="44" width="12" height="12" fill="#1c7ed6"/><text x="398" y="54" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">with VISTA</text>
  <text x="170" y="100" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">Claude Opus 5.0</text>
  <rect x="180" y="88" width="179" height="14" fill="#adb5bd"/><text x="364" y="99" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">40.68</text>
  <rect x="180" y="106" width="440" height="14" fill="#1c7ed6"/><text x="624" y="117" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">100.00</text>
  <text x="170" y="160" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">GPT-5.6 Sol</text>
  <rect x="180" y="148" width="59" height="14" fill="#adb5bd"/><text x="243" y="159" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">13.33</text>
  <rect x="180" y="166" width="436" height="14" fill="#1c7ed6"/><text x="620" y="177" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">99.00</text>
  <text x="170" y="220" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" fill="#212529">320B open model</text>
  <rect x="180" y="208" width="8" height="14" fill="#adb5bd"/><text x="192" y="219" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">1.89</text>
  <rect x="180" y="226" width="294" height="14" fill="#1c7ed6"/><text x="478" y="237" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#1864ab" font-weight="700">66.93</text>
  <line x1="180" y1="246" x2="620" y2="246" stroke="#dee2e6" stroke-width="1"/>
  <text x="180" y="260" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">0</text>
  <text x="396" y="260" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">50</text>
  <text x="616" y="260" text-anchor="end" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="10" fill="#868e96">100 (RHAE)</text>
  <rect x="30" y="276" width="660" height="62" rx="8" fill="#fff9db" stroke="#e9d66b"/>
  <text x="48" y="300" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#7a5c00">Less is more:</text>
  <text x="48" y="322" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">images cost 30.7M tokens/game vs 71.9M for numeric grids · context 200K→780K dropped the score 99→93.9 · 16× image zoom dropped it to 88.3</text>
</svg>
<p style="text-align:center;font-size:0.85em;color:#666;margin-top:-0.6em;">RHAE (Relative Human Action Efficiency) measures how efficiently a system solves games relative to humans. Every model tested improved — the biggest gains came from the weakest baselines.</p>

But the strangest findings are the ones about cost. Image observations turned out cheaper than numeric grids: 30.7 million tokens per game versus 71.9 million. Vision beat numbers on the budget. And more context hurt. Stretching the window from 200K to 780K tokens dropped the score from 99 to 93.9. Enlarging images sixteenfold dropped it to 88.3. Read that twice. The industry is in an arms race to build ever-longer context windows — kilometer-long contexts as the measure of progress. VISTA's answer is heresy: the win is not a bigger bucket. It is a model that knows exactly when to open the notebook, and exactly which page to read.

The same harness, barely adapted, plays elsewhere. On 34 GameWorld browser games it reached 63.3% success — above the 55.3% of human novices. On 3D perspective scenes: 84.12. It beats the median human on the AI GameStore set. On BabyVision's dot-connecting puzzles, the fix was almost comically literal: the model zoomed in. That generality is the real signal. A per-game simulator is a bespoke suit; VISTA is a pair of eyes that fits anything.

The honest caveat belongs to the authors themselves: these models were trained after the public games were released, so the private ARC-AGI-3 set is the true test of whether the reasoning generalizes. Keep that pinned. But note what it does not touch: the comparison that matters — same model, same weights, before and after the harness — is airtight. Whatever the ceiling is, the floor moved.

Now the part most coverage will miss. If frontier models were systematically underrated because their eyes were starved, then two years of agent-harness benchmark rankings may need re-grading. Every leaderboard that compared "models" was partly comparing plumbing: who fed their model a decent interface and who made it read spreadsheets. That is the second-order effect — the rankings don't just move; the thing they measured changes meaning. And there is a sharper, contrarian thread inside the paper's own design: the GUIDE.md/WORKING.md notebook may be doing as much work as the vision. An external episodic memory — the thing humans invented notebooks for — plus the freedom to re-examine the past on demand. The "they were blind" thesis is clean and quotable. But maybe they were also forgetful, and the cure was letting the model take notes.

VISTA's lesson is not that harnesses beat models. It is that we keep mislabeling the bottleneck. We called it a reasoning gap and reached for bigger training runs; it was a perception and memory gap, and the fix was plumbing plus a text file. The next breakthrough in agents may not need a single new parameter. It may need someone to notice what the model still cannot see.

Sources: the [paper](https://arxiv.org/abs/2610.02200) (arXiv:2610.02200); the [MIT-licensed code](https://github.com/joshhhhhan/vista) and [project page](https://vista-research.github.io/); the team's [official ARC Prize scorecards](https://arcprize.org/scorecards/39be671a-d0cc-48b4-ae08-1db4abc44c83) (linked from the repo).

**Discussion:** If a harness, not a model, closed the last gap on ARC-AGI-3 — which of your assumptions about AI progress is actually an assumption about plumbing?
