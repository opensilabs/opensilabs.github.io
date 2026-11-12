---
layout: post
lng_pair: id_20261111_alphagenome2
title: "AlphaGenome 2: Tell It Which Cell You're Asking About — It Reads the Same DNA Differently"
author: OpenSI-Labs
category: Bio AI
tags: [AlphaGenome 2, DeepMind, genomics, DNA, single-cell, variant effects]
date: 2026-11-11 06:00:00 -0800
img: /assets/img/posts/2026-11-11-alphagenome-2.png
---

## The same book, a different chapter open

Every cell in your body carries the same DNA — a long instruction book in four letters. Genes are the recipes: stretches that tell a cell how to make a protein.

Why, then, does a gut cell behave nothing like a blood cell? Each cell type opens a different chapter. It reads some recipes, ignores others, and turns many up or down — controlled by switches and dimmers around the genes.

Most disease-linked changes sit not in the recipes, but in those switches. A variant is a single changed letter. Change one in a switch, and a gene quiet in one cell might switch on in another. To judge a variant, ask: in which cell?

AlphaGenome 2, from Google DeepMind — paper "AlphaGenome 2 predicts regulatory activity and variant effects across cell states", announced 11 November 2026 — is built to ask that.

## What the first version could not do

AlphaGenome 1 was already a strong reader. Give it a DNA stretch a million letters long, and it predicted what that stretch does.

Its blind spot was the question. It was trained only on bulk data — ground-up tissue with many cell types mixed together, like averaging a whole smoothie instead of tasting each fruit.

So it predicted all tissues in parallel and gave one averaged answer: what DNA does in general, not in one specific cell and state.

## The change: the cell becomes part of the question

AlphaGenome 2 reads the same million-letter stretch, but you give it three things together: the DNA, the species (human or mouse), and one specified cell condition — a tissue, a cell type, or a cell state, meaning what that cell is doing at the time.

For that cell, it predicts gene activity tracks: RNA (working copies made from genes), splicing (how copies are cut and joined), chromatin accessibility (how open the DNA is), histone marks (tags on the proteins DNA wraps around), transcription-factor binding (where control proteins attach), and DNA methylation (a tag that often silences DNA). It also predicts gene expression values — how much of each gene is made — and 3D contact maps of which distant DNA parts touch.

The condition is not a label stuck on at the start. Inside, adaptive-normalization layers — layers that rescale the signal as it passes through — are adjusted by a "condition embedding", a compact numerical description of the cell, at every stage. The backbone is U-Net-style, like the first version.

That embedding can be picked from a learned dictionary of reference conditions. Or it can be built from your own data: a separate cell encoder takes your own single-cell RNA data (gene activity measured in individual cells) and turns it into an embedding. You can ask about a cell type or state never seen as a named category, using your own data, without retraining.

Training ran in four stages: pre-training, condition refinement, distillation, and post-training. Eight teachers were distilled into one student, trained on randomly mutated sequences to mimic the teachers' average, then post-trained with single-cell data. The data, per DeepMind: 3,977 single-cell RNA/ATAC pseudobulk tracks from 36 human and mouse studies; methylation across 185 human reference conditions; post-training sampled from 107 million human single-cell RNA profiles; a cell encoder trained on over 100 million profiles across 68 tissues.

<figure>
<svg viewBox="0 0 720 250" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The same DNA can do different things in different cells">
<rect x="10" y="20" width="700" height="210" rx="12" fill="#ffffff" stroke="#dddddd"/>
<text x="120" y="48" font-size="17" font-weight="bold" fill="#222222" text-anchor="middle">One DNA, one changed letter</text>
<rect x="20" y="90" width="200" height="36" rx="18" fill="#eef4ff" stroke="#7aa2e6" stroke-width="1.5"/>
<text x="42" y="114" font-size="14" fill="#333333">A</text>
<text x="68" y="114" font-size="14" fill="#333333">C</text>
<text x="94" y="114" font-size="14" fill="#333333">G</text>
<text x="120" y="114" font-size="14" font-weight="bold" fill="#d92323">T</text>
<text x="146" y="114" font-size="14" fill="#333333">A</text>
<text x="172" y="114" font-size="14" fill="#333333">C</text>
<text x="196" y="114" font-size="14" fill="#333333">G</text>
<path d="M120 84 L114 70 L126 70 Z" fill="#d92323"/>
<line x1="232" y1="108" x2="272" y2="108" stroke="#999999" stroke-width="2"/>
<path d="M272 108 L262 102 L262 114 Z" fill="#999999"/>
<circle cx="330" cy="78" r="28" fill="#fff4e5" stroke="#e0a44a" stroke-width="1.5"/>
<circle cx="330" cy="78" r="11" fill="#ffe0b3" stroke="#e0a44a"/>
<text x="330" y="128" font-size="14" fill="#222222" text-anchor="middle">Blood cell?</text>
<circle cx="330" cy="168" r="28" fill="#eaf7ee" stroke="#5aa873" stroke-width="1.5"/>
<circle cx="330" cy="168" r="11" fill="#cdeed6" stroke="#5aa873"/>
<text x="330" y="218" font-size="14" fill="#222222" text-anchor="middle">Gut cell?</text>
<line x1="372" y1="108" x2="412" y2="108" stroke="#999999" stroke-width="2"/>
<path d="M412 108 L402 102 L402 114 Z" fill="#999999"/>
<text x="445" y="88" font-size="14" fill="#222222">Gene off</text>
<rect x="445" y="96" width="55" height="18" rx="4" fill="#bbbbbb"/>
<text x="445" y="148" font-size="14" fill="#222222">Gene on</text>
<rect x="445" y="156" width="235" height="18" rx="4" fill="#2e9e5b"/>
</svg>
<figcaption>Figure 1 — The same stretch of DNA can do different things in different cells. AlphaGenome 2 takes the cell as part of the question.</figcaption>
</figure>

## Does it work? Two kinds of evidence

DeepMind tested it on TenK10K single-cell data, against AlphaGenome 1 fine-tuned on single-cell data, called AG1-sc. The task: find which variants actually cause expression changes.

In plain terms, out of every 10 truly causal variants, AG1-sc found about 2 and AlphaGenome 2 finds 3 — recall rising from 16% to 30% at 90% precision, meaning 9 of 10 positive calls were correct. For getting the direction right, up or down, recall rose from 23% to 43%. On bulk GTEx data (49 tissues) gains were smaller: 17% to 26%, and 32% to 40%. All numbers are DeepMind's own, from the paper.

Then one disease story. At an inflammatory-bowel-disease locus on chromosome 21, experiments had shown variant rs2836882 raises risk by turning up ETS2, a gene about 290,000 letters away, only in monocytes and macrophages, two immune cell types.

Given 7 candidate variants, AlphaGenome 2 flagged only rs2836882, linked it to ETS2 despite the distance, and confined the effect to monocytes and macrophages — all three pieces right. The team also pre-scored about 7 million variants across 510 conditions; fine-mapped causal variants (variants pinned down by detailed follow-up analysis) were enriched about 280-fold.

## The honest limits, and how you can use it

The paper states its own limits plainly. AlphaGenome 2 recovers only a minority of causal variants at high precision: 30% recall means 70% missed.

It underestimates variants outside accessible chromatin (the open parts of the DNA), at very distal elements (switches very far away), or acting after transcription (after the RNA copy is made). Transient, stimulated and disease cell states are underrepresented in training. It can blur fine neuronal subtypes, merging distinct brain cells. Condition embeddings learn correlations, not causes. Whether it handles knockouts (genes switched off entirely) or dynamic state changes is unknown.

Access is narrower than before. It is available now for non-commercial research via an API (a service you send requests to). Source code and weights — trained values that let you run it yourself — come only "upon final publication" and have not been released, a step back from AlphaGenome 1, which shipped weights. Precomputed predictions can be downloaded: an enhancer–gene atlas across 640 conditions, and variant scores across 510. Research use only; not clinically validated.

That still leaves a real advance. The cell is no longer averaged away: a researcher can ask what a variant does in their own cells, including cells never named in training, and get a sharper shortlist to test in the lab.
