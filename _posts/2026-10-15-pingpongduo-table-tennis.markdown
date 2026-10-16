---
lng_pair: id_20261015_pingpongduo-table-tennis
title: "PingpongDuo: Two Humanoids, One Table, Zero Collisions"
author: OpenSI-Labs
category: robotics
tags: [humanoid robots, table tennis, multi-robot coordination, reinforcement learning, PingpongDuo]
date: 2026-10-15 00:00:00 -0700
img: /assets/img/posts/2026-10-15-pingpongduo-table-tennis.png
meta_description: "PingpongDuo teaches two humanoid robots to play table tennis doubles: strict alternation, shared workspace, no collisions, with a 13.2 percent jump in return success and 10-plus consecutive alternating strikes on real hardware."
---

**Robot table tennis is old news. Robot table tennis doubles is a different sport.**

A single humanoid returning a ping-pong ball is now a solved demo. DeepMind's arm played competitively in 2024, Sony's Ace took on professionals for a *Nature* paper, Berkeley's HITTER strung together 106 consecutive shots against a human ([HITTER, arXiv:2508.21043](https://arxiv.org/pdf/2508.21043)), and HKU's SMASH did it with onboard vision alone ([arXiv:2604.01158](https://arxiv.org/html/2604.01158v1)). But doubles — two players on one side, forced to hit in strict alternation, sharing a few square meters of floor — breaks every one of those systems. Your partner is a moving obstacle you must never hit, and the moment you strike, you have to get out of their way.

A paper posted October 14 takes doubles head-on ([Jiang et al., arXiv:2610.20579](https://arxiv.org/abs/2610.20579v1)). PingpongDuo is a hierarchical framework for agile humanoid doubles with safe team coordination, and it is the first system to make two full humanoids rally in alternation on real hardware.

The architecture splits the problem the way a coach would. At the team level, a planner jointly selects positioning targets for both robots and runs every proposal through learned risk estimates that filter out the dangerous ones — preferentially preserving the current striker's target, so the robot about to hit never has to negotiate for space mid-swing. At the individual level, footwork and striking are separate learned skills: agile legs get the body into position, precise racket control finishes the job. The skills learn from human motion references, including footwork captured from actual human doubles play, and — the elegant touch — each skill trains from states produced by the other, so the footwork policy learns to finish exactly where the striking policy can begin.

<figure>
<svg viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Doubles is a handoff problem: strike, clear, strike</text>
<rect x="20" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="95" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot A strikes</text>
<text x="95" y="112" font-size="14" text-anchor="middle">racket-arm residual</text>
<text x="95" y="132" font-size="14" text-anchor="middle">refines the hit</text>
<text x="95" y="156" font-size="14" text-anchor="middle" font-style="italic">after movement</text>
<rect x="200" y="60" width="150" height="120" rx="10" fill="#fff8ee" stroke="#cc8833" stroke-width="1.5"/>
<text x="275" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot A clears</text>
<text x="275" y="112" font-size="14" text-anchor="middle">2.15 m in 2.4 s,</text>
<text x="275" y="132" font-size="14" text-anchor="middle">peak 2.23 m/s</text>
<text x="275" y="156" font-size="14" text-anchor="middle">~2 cm error</text>
<rect x="380" y="60" width="150" height="120" rx="10" fill="#eef4ff" stroke="#3366cc" stroke-width="1.5"/>
<text x="455" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot B positions</text>
<text x="455" y="112" font-size="14" text-anchor="middle">team planner filters</text>
<text x="455" y="132" font-size="14" text-anchor="middle">risky targets,</text>
<text x="455" y="156" font-size="14" text-anchor="middle">keeps striker's space</text>
<rect x="560" y="60" width="100" height="120" rx="10" fill="#eefbf1" stroke="#339966" stroke-width="1.5"/>
<text x="610" y="88" font-size="14" font-weight="bold" text-anchor="middle">Robot B</text>
<text x="610" y="112" font-size="14" font-weight="bold" text-anchor="middle">strikes</text>
<text x="610" y="140" font-size="14" text-anchor="middle">→ loop</text>
<line x1="170" y1="120" x2="196" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="350" y1="120" x2="376" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<line x1="530" y1="120" x2="556" y2="120" stroke="#555" stroke-width="2" marker-end="url(#p1)"/>
<path d="M 610 180 C 610 280, 95 280, 95 184" fill="none" stroke="#339966" stroke-width="2" stroke-dasharray="7,5" marker-end="url(#p1)"/>
<text x="340" y="262" font-size="14" text-anchor="middle">strict alternation: every strike hands the table to the partner</text>
<text x="340" y="292" font-size="14" text-anchor="middle">footwork + striking skills trained from each other's states</text>
<text x="340" y="318" font-size="14" text-anchor="middle" font-style="italic">simulator calibrated with real ball-flight and contact measurements</text>
<defs><marker id="p1" markerWidth="10" markerHeight="8" refX="9" refY="4" orient="auto"><path d="M0,0 L10,4 L0,8 z" fill="#555"/></marker></defs>
</svg>
<figcaption>One full exchange: strike, clear the workspace, position the partner, strike again — with the planner guarding the striker's space.</figcaption>
</figure>

Then comes the sim-to-real bridge, and it is unusually honest engineering. A racket-arm residual policy refines each strike after the movement, using return feedback from a simulator calibrated with real ball-flight and contact measurements — not a generic physics engine, but one tuned to how this ball actually flies and bounces. In simulation, PingpongDuo beats the state-of-the-art baseline's ball-return success rate by 13.2%. On real robots, the numbers read like an athlete's stat line: a 2.15-meter clearance-and-recovery cycle completed in 2.4 seconds, a peak speed of 2.23 meters per second, positioning error around 2 centimeters during clearance — and two robots sustaining more than 10 consecutive strikes in strict alternation ([ArXivSignals summary](https://arxivsignals.io/explore)).

<figure>
<svg viewBox="0 0 680 280" xmlns="http://www.w3.org/2000/svg" style="max-width:100%;height:auto;font-family:system-ui,sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">Measured on real hardware, not just in simulation</text>
<text x="230" y="72" font-size="14" text-anchor="end">Ball-return success (sim)</text>
<rect x="240" y="56" width="300" height="24" rx="4" fill="#3366cc"/><text x="548" y="73" font-size="14">+13.2% vs SOTA</text>
<text x="230" y="118" font-size="14" text-anchor="end">Clearance + recovery</text>
<rect x="240" y="102" width="200" height="24" rx="4" fill="#cc8833"/><text x="448" y="119" font-size="14">2.15 m in 2.4 s</text>
<text x="230" y="164" font-size="14" text-anchor="end">Peak speed</text>
<rect x="240" y="148" width="230" height="24" rx="4" fill="#cc8833"/><text x="478" y="165" font-size="14">2.23 m/s</text>
<text x="230" y="210" font-size="14" text-anchor="end">Alternating rally (real)</text>
<rect x="240" y="194" width="260" height="24" rx="4" fill="#339966"/><text x="508" y="211" font-size="14">10+ strikes, strict alternation</text>
<text x="340" y="254" font-size="14" text-anchor="middle" font-style="italic">positioning error during clearance: about 2 cm</text>
</svg>
<figcaption>Simulation gains plus real-robot athletics: the clearance sprint is the doubles-specific skill singles systems never needed.</figcaption>
</figure>

Here is the angle most coverage will miss. Doubles is where multi-robot teamwork stops being a planning abstraction and becomes a physics problem. In most "team of robots" research, coordination means dividing up tasks or taking turns in software. Here the teammate is a 50-kilo moving obstacle inside your swing radius, the ball is moving at meters per second, and the handoff between "my turn" and "your turn" is a full-body sprint. The learned risk filter is the conceptual contribution: instead of planning both robots jointly and hoping, the system treats the striker's workspace as sacred and vetoes anything that threatens it. Safety is not a constraint bolted on afterward; it is the planner's first job.

The honest caveats: ten alternating strikes is a rally, not a match. The paper reports no adversarial opponents, no heavy spin, no crowd noise — the chaos of real play. And like all sim-trained athletes, the system is only as good as its calibrated simulator.

Still, the direction is unmistakable. Singles proved robots can be athletes. Doubles proves they can be teammates — predicting a partner's motion, yielding space, arriving exactly where the next skill needs them. The table is small, the ball is fast, and for the first time, the robots are not playing alone.

When two robots can learn to share a table without colliding — what changes when the teammate they have to predict is a human?
