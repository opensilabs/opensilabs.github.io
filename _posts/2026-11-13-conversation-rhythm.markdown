---
layout: post
lng_pair: id_20261113_conversation
title: "Why Do Some Conversations Get More Fun the Longer They Go, While Others Just Get Dull?"
author: OpenSI-Labs
category: Society
tags: [conversation, psychology, Dartmouth, Science Advances, communication, pink noise]
date: 2026-11-13 06:00:00 -0800
img: /assets/img/posts/2026-11-13-conversation-rhythm.png
---

## Why some chats spark and others die

Everyone knows the feeling. You meet someone, and within minutes you are talking easily, finishing each other's thoughts one moment and chasing a new topic the next. Another time, the same small talk feels like hard work. Nothing goes wrong. It just never catches.

What makes the difference? A new study in *Science Advances* by Kathryn C. O'Nell, Emily S. Finn and Kiara L. Sanchez at Dartmouth College suggests it is not only what people say. It is also the shape a conversation takes over time — how two people's meanings move closer together and farther apart, and whether that movement has a particular rhythm.

That matters because conversation is how much of human life gets done. If enjoyment depends partly on a measurable pattern, not charm alone, something mysterious becomes easier to understand.

## Listening to the shape of talk

The researchers worked with a large collection of recordings called CANDOR. It holds 1,656 open-ended video conversations between strangers. Each lasted 34.1 minutes on average and ran to roughly 320 turns — one person speaks, then the other replies, and so on.

For every turn, the team measured how close the two speakers' meanings were. Psychologists call this semantic similarity. In everyday words: is the second person talking about much the same thing, in much the same way, as the person just before them? A high score means the two are closely aligned. A low score means they have moved apart — a new subject, a different angle, a story of their own.

Plot those scores from start to finish and you get a wavy line, rising when the pair converge and falling when they diverge. The researchers cared less about whether the line sat high or low than about how it wiggled.

To describe that, they borrowed an idea from physics, where patterns of ups and downs are described by the colour of their noise. White noise is pure static: each moment jumps randomly, with no memory of what came before. Red noise is like a stuck record — it barely changes at all. Pink noise sits in between. It has structure at many time scales at once, small wiggles inside larger drifts. It wanders away and comes back, the way breathing speeds and slows or a river runs fast in one stretch and pools in another.

## A rhythm, not a flat line

Almost every conversation in CANDOR had that in-between character. In 94% of them, the similarity trajectory showed pink-noise structure. On the researchers' scale, white noise scores 0.5 and pure pink noise scores 1.0. The average conversation scored 0.62 — away from random jumping, partway toward pink.

The important result is what that predicted. Pairs with a stronger pink-noise character — measured by what the team calls the pink noise ratio — reported enjoying the conversation more and feeling more connected to the other person.

That overturns a common assumption. The best conversations were not the ones where the line stayed high and flat, two people in perfect agreement from start to finish. A flat line would be red noise, not pink. What predicted enjoyment was movement with memory: closeness that could loosen and then return.

<figure>
<svg viewBox="0 0 640 300" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Schematic line chart showing semantic closeness rising and falling over a conversation">
<text x="320" y="28" text-anchor="middle" font-size="18" font-family="sans-serif" font-weight="bold">Closeness that drifts and returns</text>
<line x1="70" y1="250" x2="600" y2="250" stroke="#333" stroke-width="1.5"/>
<line x1="70" y1="50" x2="70" y2="250" stroke="#333" stroke-width="1.5"/>
<line x1="70" y1="82" x2="600" y2="82" stroke="#999" stroke-width="1.2" stroke-dasharray="6 5"/>
<text x="600" y="72" text-anchor="end" font-size="14" font-family="sans-serif" fill="#666">Always agreeing — flat</text>
<path d="M 70 150 C 110 110, 140 105, 175 135 S 235 195, 275 175 S 330 95, 370 110 S 430 185, 470 160 S 545 105, 600 130" fill="none" stroke="#2563eb" stroke-width="3" stroke-linecap="round"/>
<text x="335" y="282" text-anchor="middle" font-size="14" font-family="sans-serif">Conversation turns</text>
<text x="22" y="150" text-anchor="middle" font-size="14" font-family="sans-serif" transform="rotate(-90 22 150)">How close the two people's meanings are</text>
</svg>
<figcaption>Schematic illustration only — not the paper's data. The blue line sketches the idea: two speakers' meanings drift apart and come back together at several scales during a conversation, rather than staying flat.</figcaption>
</figure>

One way to read this — and this is an interpretation, not a claim the paper itself makes — is that a good conversation is a shared rhythm of coming together and drifting apart. You meet on common ground, one of you wanders off with a new thought, then you find each other again. Total agreement, held for half an hour, would be dull. So would total disconnection. The pleasure lives in the movement between the two.

## Practice helps, and machines show it too

Two extra findings make the pattern harder to dismiss as a quirk of one dataset.

First, the pink-noise structure got stronger with practice, as if people settle into this way of talking the more they do it. Second, when large language models were asked to generate enjoyable conversations, their scripts also carried stronger pink noise than baseline scripts. The models were told nothing about noise colours. Asked simply for an enjoyable conversation, they produced dialogue that drifted and returned in the same measurable way.

The pattern also turned up beyond CANDOR, in a second, independent conversation dataset, and in two-person podcasts and speed-dating conversations.

## What this study cannot tell us

The authors are clear about the limits.

This is an observational, correlational study. Pink-noise structure and enjoyment go together, but the authors explicitly do not claim that pink noise causes enjoyment. Enjoying a conversation could lead people into this rhythm, or something else could produce both. The data cannot separate those possibilities.

Semantic similarity is also only one channel. The study measures the meanings of words people used. It does not measure tone of voice, eye contact or body language, all of which shape how a conversation feels.

The setting is narrow too. CANDOR is strangers on video calls. Whether the same pattern holds for old friends, family dinners or work meetings, where history and habits come into play, is untested here.

The language model result needs the same care. It concerns generated scripts, not live talk. That the scripts show stronger pink noise is a fact about the text. It is not proof that models understand conversation.

None of that empties the finding. It sets its proper size. Next time a conversation goes well, it may be worth noticing not just what was said, but the movement — the moments you drifted onto different ground, and the moments you came back and found you were, briefly, thinking together again.

## References

O'Nell, K. C., Finn, E. S., & Sanchez, K. L. "Pink noise in dyads' semantic similarity trajectories predicts conversation enjoyment." Science Advances (2026). DOI: [10.1126/sciadv.aeb2684](https://doi.org/10.1126/sciadv.aeb2684)
