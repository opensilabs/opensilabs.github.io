---
lng_pair: id_20261026_cnn-skin-cancer
title: "The Giants Guessed. The Old Network Looked."
author: OpenSI-Labs
category: research
tags: [medical AI, computer vision, Inception v3, multimodal LLMs, dermatology, evaluation]
date: 2026-10-26 00:05:00 -0700
img: /assets/img/posts/2026-10-26-cnn-skin-cancer.png
meta_description: "On 200 biopsy-proven skin lesions, a 2015 CNN fine-tuned for twenty minutes named the right diagnosis 62.5% of the time; GPT-6 Astra and Claude Fable 5.1 managed 42%. The deeper story is how the giants failed — favourite answers, confident prose detached from looking, and a discharge paradox that turns on a single threshold."
---

The lesion was an invasive melanoma on a patient's ear, less than 0.8 millimetres thick — thin enough to cure if caught, lethal if waved through. Shown its clinical photograph and its dermoscopic image, GPT-6 Astra called it a seborrhoeic keratosis, a harmless warty growth, and said the patient could be discharged. Claude Fable 5.1 said the same. A convolutional network first published by Google in 2015, fine-tuned for about twenty minutes on public data, called it a melanoma.

That network was not supposed to win. On October 25, Dr Magnus Lynch — a consultant dermatologist and Mohs surgeon at Guy's Hospital in London, and an honorary reader at King's College London — published [a test he ran himself](https://lynchlab.net/llm-skin-cancer), with every prompt, every model reply and the scoring code [released for anyone to re-run](https://d2gaqzonlm544h.cloudfront.net/skin-ai/data/llm-skin-cancer-test.zip). His question was narrow and clinical: given the two photographs a dermatologist actually works from, can the most capable AI models of October 2026 name what a skin lesion is? The answer has ricocheted around the research community for two days, because the frontier models did not merely lose. They lost by twenty points to an architecture old enough to be taught as history — and the way they lost says something uncomfortable about what general-purpose models do when they appear to look at an image.

## A test designed to be hard

The 200 lesions came from MILK10k, a public dataset released through the International Skin Imaging Collaboration in 2025. Every one was confirmed by histopathology — the tissue diagnosis is ground truth, not another doctor's opinion. One hundred were lesions that must not be sent home: 30 melanomas, 25 basal cell carcinomas, 25 squamous cell carcinomas and 20 actinic keratoses. The other hundred were safe to discharge: 50 benign moles and 50 seborrhoeic keratoses. Each lesion came with two images — a clinical close-up and a polarized dermatoscope view, the magnified, lit image of pigment patterns beneath the skin's surface that dermatologists are trained to read.

Crucially, every lesion in the set, benign ones included, had worried a clinician enough to be biopsied. These are not textbook examples; they are the hard residue — moles that looked dangerous and cancers that looked innocent.

The two language models were used as a clinician might use them: both images, the most likely of the six diagnoses (or "unsure"), a confidence, a second choice, and a judgement on whether the lesion could be safely discharged. Default settings, one run each, no refusals.

The CNN, Inception v3, was deliberately unglamorous — Lynch notes it is a baseline, not the state of the art. It arrived pretrained on everyday photographs, then had all its layers fine-tuned on 68,011 dermoscopic and clinical images from the [ISIC Archive](https://www.isic-archive.com), on a single H100 GPU, in roughly twenty minutes. The hygiene was strict: the 200 test lesions, and every other photograph of the same lesions or the same patients, were removed from its training and validation data before fine-tuning began. The finished model is a 44-megabyte file that runs entirely inside a phone browser using WebGPU; nothing is uploaded anywhere.

## Sixty-two against forty-two

The headline number deserves its plainness. Naming the correct diagnosis first, out of six: the CNN scored 125 of 200 — 62.5%. Claude Fable 5.1 scored 85 (42.5%); GPT-6 Astra scored 84 (42.0%). Allow each system its second choice and the gap persists: 173 against 138 and 134.

The pattern underneath is more damning than the totals. On melanomas — the diagnosis where an error can kill — the CNN named 13 of 30 first; the LLMs managed 11 and 8. On the harmless lesions that fill real clinics, the CNN recognised 37 of 50 moles and 26 of 50 keratoses; Astra recognised 16 and 13, Fable 33 and just 6. The giants were not uniformly a bit worse. They were worst exactly where volume and danger live: telling a cancer from a mole that merely looks like one.

<figure>
<div style="text-align:center">
<svg width="680" height="330" viewBox="0 0 680 330" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="21" font-weight="bold" text-anchor="middle">Naming the diagnosis: first choice and top-two</text>
<text x="340" y="56" font-size="16" text-anchor="middle" fill="#4a5568">Share of 200 biopsy-proven lesions named correctly (%)</text>
<rect x="150" y="70" width="18" height="14" fill="#2b6cb0"/><text x="174" y="83" font-size="16">First choice</text>
<rect x="380" y="70" width="18" height="14" fill="#90cdf4"/><text x="404" y="83" font-size="16">In first two choices</text>
<text x="205" y="128" font-size="17" font-weight="bold" text-anchor="end">Inception v3 (2015)</text>
<rect x="215" y="108" width="275" height="24" fill="#2b6cb0"/>
<text x="500" y="127" font-size="20" font-weight="bold">62.5</text>
<rect x="215" y="138" width="381" height="24" fill="#90cdf4"/>
<text x="606" y="157" font-size="20" font-weight="bold">86.5</text>
<text x="205" y="202" font-size="17" font-weight="bold" text-anchor="end">Claude Fable 5.1</text>
<rect x="215" y="182" width="187" height="24" fill="#4a5568"/>
<text x="412" y="201" font-size="20" font-weight="bold">42.5</text>
<rect x="215" y="212" width="304" height="24" fill="#a0aec0"/>
<text x="529" y="231" font-size="20" font-weight="bold">69</text>
<text x="205" y="276" font-size="17" font-weight="bold" text-anchor="end">GPT-6 Astra</text>
<rect x="215" y="256" width="185" height="24" fill="#718096"/>
<text x="410" y="275" font-size="20" font-weight="bold">42</text>
<rect x="215" y="286" width="295" height="24" fill="#cbd5e0"/>
<text x="520" y="305" font-size="20" font-weight="bold">67</text>
</svg>
</div>
<figcaption style="text-align:center">The old network named the right diagnosis 62.5% of the time; the two frontier models managed 42%.</figcaption>
</figure>

## How the giants failed: favourite answers and fluent blindness

Each language model had a favourite answer, and it reached for it constantly. Auditing the raw outputs, [a forensic analysis of Lynch's published data](https://duklee.net/blog/2026-10-25-cnn-outperforms-frontier-llms-skin-cancer-diagnosis-deep-dive/) found that GPT-6 Astra called 75 of the 200 lesions basal cell carcinoma — three times the true count of 25 — including 14 of the 30 melanomas. Its perfect record on actual basal cell carcinomas is an artefact of over-calling: when a third of everything is labelled BCC, you never miss one, but two of every three BCC calls are wrong. Claude Fable 5.1 had the mirror-image habit, calling 53 lesions actinic keratosis against a true count of 20, and filing 16 of the 25 squamous cell carcinomas — real cancers — under that pre-malignant label. This is mode collapse wearing a white coat: under uncertainty, the model does not spread its bets; it retreats to the answer its training made most sayable.

The confidence made it worse. One melanoma in Lynch's set has very little pigment — the kind human clinicians dread. Astra named it a basal cell carcinoma with 95% confidence. Both LLMs looked at the ear melanoma, described it, and discharged it. The failure has a name in the analysis: verbal–visual decoupling. A frontier multimodal model does not examine an image the way the CNN does. The image is chopped into patches, tokenized, and handed to a language engine whose native skill is producing plausible text. These models have read every dermatology textbook; they can recite the vocabulary of dermoscopy — pigment networks, arborizing vessels, blue-white veils — with perfect fluency. But fluency is not perception. Too often, the description is generated because it is the kind of thing one says about such lesions, not because the corresponding structure, a pattern tens of micrometres across, was actually resolved in the pixels. The CNN, by contrast, has no vocabulary at all. Fine-tuned end to end on 68,011 examples, its filters are tuned to precisely those sub-surface spatial patterns, and nothing else competes for its attention. It cannot explain itself. It can only look.

Lynch also re-ran the encounter the way it would happen outside a clinic: as a worried patient, with the clinical photo alone, asking "do I need to see a doctor?" As pure diagnosis, performance collapsed — first-choice accuracy of roughly 24–26%, and on 100 further biopsy-proven melanomas, Fable named melanoma first in only 3 cases, told 14 patients a routine appointment would do, and told one patient with an invasive melanoma that it could be left alone. The models almost always advised seeing a doctor; what they could not do was say, correctly, why.

## The discharge paradox: the number nobody quoted

Here is the part of Lynch's table that complicates every triumphant headline — including, honestly, his own. Diagnosis is only half the clinical task. The other half is triage: keep, or send home?

At its preset threshold — the operating point chosen on validation data — the winning CNN kept 77 of the 100 dangerous lesions and sent 76 of the 100 harmless ones home. Sounds balanced, until you reach the melanoma line: it would have discharged 18 of the 30 melanomas. The two LLMs, for all their diagnostic mediocrity, discharged only 3 and 4 melanomas — because they kept almost everything, sending home just 32 and 22 of the 100 harmless lesions. Their "safety" is the safety of a smoke alarm that rings at toast: sensitivity bought by refusing to ever say "fine", at the price of flooding clinics with the worried well. Neither extreme is a doctor.

The resolution of the paradox is the deepest technical point in the study, and it favours the old architecture again. A classifier outputs a continuous score, and where you set the threshold is a choice — a dial. Slide the CNN's dial along its ROC curve (area under the curve 0.86 on this deliberately hard set, 0.96 on ordinary archive images) until its willingness to discharge matches the LLMs' caution, and it keeps 98 or 99 of the 100 dangerous lesions while discharging only 1 or 2 melanomas — better than either giant on both sides of the ledger at once. The LLMs offer no dial. Their operating point is buried in prose, set by the habits of their training — part textbook, part liability instinct — and it cannot be inspected, audited or moved by the clinician who is asked to trust it.

<figure>
<div style="text-align:center">
<svg width="680" height="470" viewBox="0 0 680 470" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="30" font-size="21" font-weight="bold" text-anchor="middle">The discharge paradox: safety depends on the threshold</text>
<text x="40" y="72" font-size="18" font-weight="bold">Harmless lesions sent home (of 100)</text>
<text x="290" y="109" font-size="16" text-anchor="end">CNN, preset threshold</text>
<rect x="300" y="88" width="274" height="24" fill="#2b6cb0"/>
<text x="584" y="108" font-size="20" font-weight="bold">76</text>
<text x="290" y="143" font-size="16" text-anchor="end">GPT-6 Astra</text>
<rect x="300" y="122" width="115" height="24" fill="#718096"/>
<text x="425" y="142" font-size="20" font-weight="bold">32</text>
<text x="290" y="177" font-size="16" text-anchor="end">Claude Fable 5.1</text>
<rect x="300" y="156" width="79" height="24" fill="#4a5568"/>
<text x="389" y="176" font-size="20" font-weight="bold">22</text>
<text x="40" y="218" font-size="18" font-weight="bold">Melanomas wrongly sent home (of 30)</text>
<text x="290" y="257" font-size="16" text-anchor="end">CNN, preset threshold</text>
<rect x="300" y="236" width="216" height="24" fill="#c53030"/>
<text x="526" y="256" font-size="20" font-weight="bold">18</text>
<text x="290" y="291" font-size="16" text-anchor="end">CNN, threshold matched to the LLMs</text>
<rect x="300" y="270" width="24" height="24" fill="#2b6cb0"/>
<text x="334" y="290" font-size="20" font-weight="bold">1–2</text>
<text x="290" y="325" font-size="16" text-anchor="end">GPT-6 Astra</text>
<rect x="300" y="304" width="36" height="24" fill="#718096"/>
<text x="346" y="324" font-size="20" font-weight="bold">3</text>
<text x="290" y="359" font-size="16" text-anchor="end">Claude Fable 5.1</text>
<rect x="300" y="338" width="48" height="24" fill="#4a5568"/>
<text x="358" y="358" font-size="20" font-weight="bold">4</text>
</svg>
</div>
<figcaption style="text-align:center">At its factory setting the CNN sent 18 melanomas home. Match its threshold to the LLMs' caution and it sends home 1–2 — while keeping 98–99 of the 100 dangerous lesions.</figcaption>
</figure>

## Why fit beat scale

Step back, and the result is less mysterious than it first looks. This task is a closed set of six answers over a narrow, learnable visual distribution — precisely the shape of problem a specialist classifier is built for. The CNN's inductive bias is an asset here: translation-invariant filters, trained on nothing but the target domain, with every parameter serving the discrimination that matters. Its training distribution *is* the test distribution. The generalists bring a billion facts about everything and a vision system that must serve all of them at once; the specialist brings 68,011 examples of one thing.

The economics underline it. The CNN's education cost twenty minutes on one rented GPU; it then runs free, offline, inside a browser, at zero marginal cost and with perfect privacy — no patient's skin is uploaded to anyone's cloud. The published logs put the API bill for testing the two giants on 200 lesions at a few US dollars each; the real cost of the generalist route is not the dollars but the dependency — a remote, versioned, silently-updated model whose behaviour you cannot freeze, threshold or audit.

## What this test does not show

Honesty about limits is what separates this little study from a stunt, and Lynch states most of them himself. First: this is one clinician's self-published test, not peer-reviewed science. Two hundred lesions show a pattern; they cannot finely rank systems, thirty melanomas carry wide uncertainty, and each LLM case was run once — ask again and some answers change. Second: the CNN enjoyed home-field advantage. It never saw the test lesions or their patients, but it was raised on the same archive, the same cameras, the same diagnostic culture; the LLMs were dropped into a specialism cold. Third: the giants were tested one-shot, at default settings, with no tools, no image enhancement, no chance to crop, zoom, compare or reconsider — no serious clinical deployment would use them that way, and an agent wrapped around them would surely do better. Fourth — and it cuts at the winner — none of this makes the CNN a medical device. At its preset threshold it would have sent 18 melanomas home; modern ensembles and regulated diagnostic products, as Lynch himself points out, perform considerably better than his deliberately dated baseline. Nobody should be discharged by any of these three systems.

One caveat points the other way: MILK10k has been public since 2025, so the LLMs may well have absorbed it in training — contamination that would have helped them, not the CNN. And a disclosure worth copying: Lynch notes his analysis and first drafts were produced with Claude Code — a tool from Anthropic, maker of one of the models that lost. He published the data anyway.

## The lesson is about instruments

The comfortable reading of this story is "small beats big", and it is wrong. The CNN did not out-reason anyone; it out-*fitted* them, on a task whose shape rewards fit. The uncomfortable reading is about what we have been measuring. Our flagship evaluations grade models on naming things — exam questions with answer keys — while real work, in medicine and far beyond it, runs on operating points: calibrated scores, explicit thresholds, error costs that differ by direction. On the naming test the giants scored 42%. On the triage test their caution was an uninspectable side effect of their prose style. A system that cannot show you its threshold is asking to be trusted on the strength of its tone of voice.

The likely future is neither the giant nor the antique, but a division of labour: the generalist as the conversational front door — taking the history, explaining, escalating — wired to narrow instruments that do the looking, each with a dial a professional can set and a score a regulator can audit. Twenty minutes of fine-tuning just demonstrated, in public, with the receipts attached, how good the instrument half of that future already is.

So here is the question this test leaves on the table: when a model cannot show you its threshold — only its confidence — what exactly is its "this looks harmless" worth?
