---
lng_pair: id_20261010_photonic-ai-computing
title: "The Computer Made of Light"
author: OpenSI-Labs
category: chips
tags: [photonic computing, optical neural networks, energy efficiency, Koç University, hardware]
date: 2026-10-10 06:00:00 -0700
img: /assets/img/posts/2026-10-10-photonic-ai-computing.png
meta_description: "Two new studies from Koç University show AI computation happening in light itself — a photonic neural network that keeps color images in full color, and a fiber laser that performs nonlinear processing with its own physics."
---

Every AI model you have ever used did its thinking in electrons. Billions of transistors switching, billions of multiply-accumulates, each one burning a little energy and shedding it as heat. The industry's answer has been to build bigger: bigger clusters, bigger power contracts, small towns' worth of electricity to answer your questions.

A pair of recent studies from Uğur Teğin's laboratory at Koç University in Istanbul asks a different question: what if the thinking happened in photons instead? Light can carry many streams of information at once, and it does its "computing" at the speed it travels, essentially for free. One paper, in *Communications Engineering*, builds a photonic neural network that processes color images without discarding their color. The other, in *Communications Physics*, turns a fiber laser into the processor itself. Both were [covered together this week](https://techxplore.com/news/2026-10-approach-sustainable-ai-offloading-burden.html) — and together they sketch a genuinely different philosophy of AI hardware.

## Don't throw away the color

Start with a fact that sounds trivial until you count the cost. Most image classifiers begin by throwing away information: a color image's red, green, and blue channels get collapsed into a single grayscale channel. It is a habit from an era when compute was scarce — three channels cost three times the arithmetic. But color is signal. A skin lesion's diagnosis can hinge on subtle redness; a satellite image's meaning can live in the green.

Kılınç and Teğin's system refuses the shortcut. The image is encoded onto a programmable device that shapes how light propagates — a stack of phase masks (multi-plane light conversion) that mixes and transforms the three color channels as they travel together through the optics. Passing through the setup physically accentuates the features that distinguish one image from another: color, shape, texture. A camera then records the resulting optical pattern, and a classifier reads the category off it.

The numbers are striking. On dermatological disease classification, accuracy rose from 68% on raw color pixels to **98%** after optical preprocessing. Across medical imaging, natural-image classification, and regression tasks, the optical preprocessing added 25–45 percentage points over raw-pixel baselines; keeping RGB instead of collapsing to grayscale was worth another 6–11 points on its own ([paper](https://www.nature.com/articles/s44172-026-00762-w)).

<svg viewBox="0 0 720 470" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Multichannel optical computing pipeline: RGB channels encoded onto phase masks, transformed by light propagation, read by a camera">
  <defs>
    <marker id="arrP" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">Multichannel optical computing: color survives the whole pipeline</text>
  <rect x="30" y="50" width="150" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="105" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">RGB IMAGE IN</text>
  <text x="105" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">all 3 channels kept</text>
  <rect x="30" y="140" width="150" height="26" rx="6" fill="#f8f9fa" stroke="#adb5bd"/>
  <text x="105" y="157" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">no grayscale collapse</text>
  <line x1="180" y1="85" x2="225" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="225" y="50" width="170" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="310" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">PHASE MASKS</text>
  <text x="310" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">multi-plane light conversion</text>
  <line x1="395" y1="85" x2="440" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="440" y="50" width="150" height="70" rx="10" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="515" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">LIGHT PROPAGATION</text>
  <text x="515" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">features accentuated optically</text>
  <line x1="590" y1="85" x2="620" y2="85" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrP)"/>
  <rect x="620" y="50" width="80" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="660" y="76" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">CAMERA</text>
  <text x="660" y="96" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#495057">+ classifier</text>
  <rect x="120" y="200" width="480" height="120" rx="10" fill="#ebfbee" stroke="#2b8a3e" stroke-width="2"/>
  <text x="360" y="228" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#2b8a3e">SELF-OPTIMIZATION LOOP</text>
  <text x="360" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">learns from experimental measurements — no perfect simulator needed</text>
  <text x="360" y="274" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">Bayesian optimization (channel mixing) + hardware-in-the-loop</text>
  <text x="360" y="296" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">self-organized criticality (phase settings) — adapts to misalignments</text>
  <line x1="310" y1="120" x2="310" y2="195" stroke="#2b8a3e" stroke-width="2" stroke-dasharray="6,4" marker-end="url(#arrP)"/>
  <rect x="225" y="350" width="270" height="70" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="360" y="378" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">DERMATOLOGY: 68% → 98%</text>
  <text x="360" y="400" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">self-optimization adds 7–12 points on top</text>
  <text x="360" y="448" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">Caption: RGB channels travel together through programmable phase masks; the system tunes itself against the real hardware.</text>
</svg>

## Learn the device, not the simulation

Here is the part that matters most, and it is not the accuracy number. Optical neural networks have a graveyard problem: they work beautifully in simulation and die in the lab. Real optics have misalignments, manufacturing imperfections, thermal drift — the physical device never matches the idealized model on the computer, and the gap eats the performance.

Teğin's group inverted the problem. Instead of demanding a perfect simulator, their system learns from experimental measurements. Two complementary optimization strategies run without any differentiable forward model: Bayesian optimization refines how the channels mix at the input, and a hardware-in-the-loop protocol based on self-organized criticality navigates the device's high-dimensional phase settings. In plain terms, the machine learns the quirks of its own hardware and adapts to them. The imperfections are not noise to be engineered away — they are part of what gets learned. That self-optimization contributed an additional 7–12 percentage points.

Electronics has spent sixty years demanding ever-tighter tolerances — nanometers, now angstroms. This is the opposite bet: build the computer out of imperfect physics, then let the physics teach the algorithm. It is a genuinely different philosophy of hardware, and it is the reason this work deserves attention beyond the benchmark table.

## A laser that thinks

The second study is stranger and, in a way, more radical. Eşlik, Kesgin, Kılınç, and Teğin took a continuous-wave multimode fiber laser — a coil of fiber that amplifies light — and used the cavity itself as the processor. Input images are written as phase patterns onto a spatial light modulator; the light then circulates through the laser cavity, where multimode interference and gain-saturation dynamics — the laser's own physical behavior — scramble it into a high-dimensional nonlinear transformation. What emerges is a stable intensity pattern in which different classes are already separated, so a simple linear classifier finishes the job.

No GPU performed the nonlinear mapping. The physics did it. Across recyclable waste, weather and satellite imagery, retinal scans, and skin lesions, the system reached **85–99%** accuracy with orders of magnitude fewer trainable parameters than a conventional deep network ([paper](https://www.nature.com/articles/s42005-026-02823-0)).

<svg viewBox="0 0 720 400" width="100%" style="max-width:720px;display:block;margin:1.2em auto;" role="img" aria-label="Fiber laser cavity as nonlinear optical processor: phase-encoded images transformed by laser dynamics into separable patterns">
  <defs>
    <marker id="arrQ" markerWidth="9" markerHeight="9" refX="7" refY="4.5" orient="auto"><path d="M0,0 L9,4.5 L0,9 Z" fill="#1c7ed6"/></marker>
  </defs>
  <text x="360" y="24" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="15" font-weight="700" fill="#212529">The laser cavity is the processor</text>
  <rect x="20" y="60" width="130" height="70" rx="10" fill="#fff5f5" stroke="#c92a2a" stroke-width="2"/>
  <text x="85" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#a61e4d">IMAGE IN</text>
  <text x="85" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">waste, satellite, retina…</text>
  <line x1="150" y1="95" x2="190" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="190" y="60" width="140" height="70" rx="10" fill="#e7f5ff" stroke="#1c7ed6" stroke-width="2"/>
  <text x="260" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#1864ab">SLM</text>
  <text x="260" y="108" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">phase-pattern encoding</text>
  <line x1="330" y1="95" x2="370" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="370" y="50" width="200" height="90" rx="40" fill="#fff3bf" stroke="#f08c00" stroke-width="2"/>
  <text x="470" y="80" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#e67700">FIBER LASER CAVITY</text>
  <text x="470" y="100" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">multimode interference</text>
  <text x="470" y="118" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">+ gain saturation</text>
  <line x1="570" y1="95" x2="610" y2="95" stroke="#1c7ed6" stroke-width="2" marker-end="url(#arrQ)"/>
  <rect x="610" y="60" width="90" height="70" rx="10" fill="#f3f0ff" stroke="#7048e8" stroke-width="2"/>
  <text x="655" y="88" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">LINEAR</text>
  <text x="655" y="106" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" font-weight="700" fill="#5f3dc4">CLASSIFIER</text>
  <rect x="190" y="180" width="380" height="80" rx="10" fill="#ffffff" stroke="#212529" stroke-width="2"/>
  <text x="380" y="210" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="14" font-weight="700" fill="#212529">85–99% ACCURACY</text>
  <text x="380" y="232" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">orders of magnitude fewer trainable parameters than deep nets</text>
  <text x="380" y="252" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">— the laser's dynamics replace the network's hidden layers</text>
  <text x="360" y="310" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="13" font-weight="700" fill="#212529">Why it works: the nonlinear mapping is free</text>
  <text x="360" y="334" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">In a digital net, nonlinearity costs matrix multiplies and memory traffic.</text>
  <text x="360" y="354" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="12" fill="#495057">In the cavity, it is just what the light does on its way through.</text>
  <text x="360" y="386" text-anchor="middle" font-family="system-ui,-apple-system,'Segoe UI',sans-serif" font-size="11" fill="#868e96">Caption: Input images become phase patterns; the laser's own dynamics perform the nonlinear computation.</text>
</svg>

## The honest accounting

Two caveats, because this journal does not do hype. First, neither system is pure light. Both still need electronics: spatial light modulators to write the data in, cameras to read the patterns out, control units to run the optimization. The honest question is what fraction of the total workload light can truly absorb — today it is the heavy middle, the nonlinear feature transformation, while the edges remain electronic. Whether faster light modulators and chip-integrated photonics can push that fraction toward the whole pipeline is the open engineering bet.

Second, these are proof-of-concept scales, not data-center replacements. Nobody is training a frontier model inside a fiber laser next year.

But the direction is right, and the timing matters. AI inference is running into physical limits — power, heat, the cost of shuttling data between memory and processors. Every one of those limits is a property of electronics. Photonic computing does not just dodge them; it inverts the hardest one. Where electronics demands perfection and pays for it in fabrication cost, photonics can learn the device it actually has. Computing *with* the physics instead of against it.

The 1980s dreamed of optical computers and failed on programmability and adaptivity. The missing piece, it turns out, was not better optics. It was letting the optics teach themselves.

**Discussion:** If future AI hardware learns the imperfections of its own physical substrate instead of demanding perfect fabrication, what happens to the economics of chip manufacturing — and who wins when "good enough physics" beats perfect silicon?
