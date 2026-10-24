---
lng_pair: id_20261024_block-dessa
title: "The Model That Learned to Talk Without Ever Reading a Word"
author: OpenSI-Labs
category: research
tags: [Block, Dessa, speech-to-speech, full-duplex, voice AI, audio-only training]
date: 2026-10-24 07:00:00 -0700
img: /assets/img/posts/2026-10-24-block-dessa.png
meta_description: "Block's Dessa is a full-duplex speech-to-speech model trained from scratch on human conversation audio alone — no text, no pretrained backbone. The demos are striking; the evidence so far is demos only."
---

On October 23, Jack Dorsey's Block unveiled Dessa, a voice model with a claim that sounds almost heretical after a decade of text-trained AI: it learned to hold a conversation without ever reading a single word. No text corpus, no pretrained language model underneath — just recordings of people talking, from scratch. Block calls it "the most authentic full-duplex speech model ever built," and its research lead, Ragavan Thurairatnam, frames it as a possible ["GPT-3 moment for speech"](https://panews.io/articles/01a16adb-b868-71d2-9020-e852cb11f62c).

To see why that matters, start with how today's voice assistants actually work. You speak; a transcriber turns your speech into text; a language model reads the text and writes a reply; a synthesizer reads the reply aloud. It is a relay race with three handoffs, and every handoff throws something away. The transcript keeps the words but drops the hesitation before them, the laugh inside them, the rising pitch that turns a statement into a question, the sarcasm that inverts the meaning entirely. It also imposes turn-taking by committee: the system waits until you stop talking, then starts, so conversations feel like walkie-talkie exchanges rather than talk.

Dessa collapses the relay into a single runner. Audio goes in, audio comes out, with no transcription step in between — a "true speech-to-speech model" in [Block's own description](https://aicoder.com/news/news-20261024-block-dessa-full-duplex-speech-model-trained-only-on-speech). And it is full-duplex: it listens while it speaks, the way people do. It can be interrupted mid-sentence, cut in itself, and slip in the small backchannel noises — "yeah," "got it," a soft laugh — that signal it is following you. Because it learned from real conversations rather than written scripts, Block says, it knows when to jump in and when to hold back. The demos on Block's page show it laughing mid-sentence, finishing a forgotten movie title, and answering a surprise trip to Paris with what sounds like teary gratitude. In one demo it talks with OpenAI's GPT-Live-1 voice model, and comes across as the more natural conversationalist of the two.

<figure>
<div style="text-align:center">
<svg width="680" height="340" viewBox="0 0 680 340" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">The relay race vs. the single runner</text>
<text x="170" y="58" font-size="14" font-weight="bold" text-anchor="middle">Today: speech → text → speech</text>
<rect x="20" y="80" width="90" height="54" rx="8" fill="#2b6cb0"/>
<text x="65" y="111" font-size="14" fill="#fff" text-anchor="middle">Your voice</text>
<rect x="135" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="180" y="111" font-size="14" fill="#fff" text-anchor="middle">Transcript</text>
<rect x="250" y="80" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="295" y="111" font-size="14" fill="#fff" text-anchor="middle">Text LLM</text>
<rect x="140" y="160" width="90" height="54" rx="8" fill="#6b46c1"/>
<text x="185" y="191" font-size="14" fill="#fff" text-anchor="middle">Speech out</text>
<text x="170" y="240" font-size="14" fill="#c53030" text-anchor="middle">Tone, timing, laughter: lost at each handoff</text>
<text x="510" y="58" font-size="14" font-weight="bold" text-anchor="middle">Dessa: audio in, audio out</text>
<rect x="400" y="80" width="110" height="54" rx="8" fill="#2b6cb0"/>
<text x="455" y="111" font-size="14" fill="#fff" text-anchor="middle">Your voice</text>
<rect x="535" y="80" width="110" height="54" rx="8" fill="#276749"/>
<text x="590" y="111" font-size="14" fill="#fff" text-anchor="middle">Dessa</text>
<rect x="455" y="160" width="110" height="54" rx="8" fill="#276749"/>
<text x="510" y="191" font-size="14" fill="#fff" text-anchor="middle">Spoken reply</text>
<text x="510" y="240" font-size="14" fill="#276749" text-anchor="middle">Listens while speaking: interruptible</text>
<line x1="110" y1="107" x2="135" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="225" y1="107" x2="250" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="295" y1="134" x2="230" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="535" y2="107" stroke="#a0aec0" stroke-width="2"/>
<line x1="590" y1="134" x2="510" y2="160" stroke="#a0aec0" stroke-width="2"/>
<line x1="510" y1="107" x2="510" y2="160" stroke="#a0aec0" stroke-width="2" stroke-dasharray="5,4"/>
</svg>
</div>
<figcaption style="text-align:center">Left: today's voice assistants flatten speech into text and back, losing everything that is not a word. Right: Dessa keeps the whole signal in one model — and keeps listening while it talks.</figcaption>
</figure>

The deeper claim is not about voice quality. It is about what language competence is made of. For years, the working assumption of the field has been that text corpora are the necessary scaffold: models learn language by reading the internet, and speech is a coat hung on top afterward. Dessa is a direct challenge to that assumption. Block says it learned language from ["hundreds of times fewer words"](https://www.aichatdaily.com/ai-models/block-unveils-dessa-full-duplex-voice-model-trained-only) than text LLMs see — because a minute of conversation carries far more information than its transcript: timing, emphasis, emotion, the social choreography of who speaks when. A child, Block's team notes, learns to talk years before learning to read; they wanted to see if a model could too. The efficiency claim extends to compute: training ran on a single NVIDIA GB200 NVL72 rack — one rack, not a data-center-scale cluster — and inference runs faster than real time locally on a MacBook Pro M4 Max or better, with no cloud round trip.

Block also frames the work as safety research, not just product craft. Today's voice AI, the team argues, is nearly deaf to emotion: it cannot hear distress in a caller's voice, and so cannot respond to it. Dessa's stated motivations are "curiosity (aka fun), better understanding between humans and AI, and safety." Early access goes first to a small group of AI safety researchers, precisely because, as Block puts it, a model that learned to talk from sound alone is new territory — the risks are not yet mapped. A public waitlist is open, but there is no release date, no API, and no price.

<figure>
<div style="text-align:center">
<svg width="680" height="300" viewBox="0 0 680 300" xmlns="http://www.w3.org/2000/svg" font-family="system-ui, sans-serif">
<text x="340" y="28" font-size="17" font-weight="bold" text-anchor="middle">What a transcript throws away</text>
<text x="340" y="58" font-size="14" text-anchor="middle">Same words, different meanings — carried only by sound</text>
<rect x="40" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="130" y="108" font-size="14" text-anchor="middle">“Really?” — flat</text>
<text x="130" y="130" font-size="14" text-anchor="middle">A question</text>
<rect x="250" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="340" y="108" font-size="14" text-anchor="middle">“Really?!” — rising</text>
<text x="340" y="130" font-size="14" text-anchor="middle">Disbelief, delight</text>
<rect x="460" y="80" width="180" height="70" rx="8" fill="#ebf4ff"/>
<text x="550" y="108" font-size="14" text-anchor="middle">“Really.” — dry</text>
<text x="550" y="130" font-size="14" text-anchor="middle">Sarcasm</text>
<text x="340" y="185" font-size="14" text-anchor="middle">Plus: pauses, laughter, sighs, interruptions, backchannels —</text>
<text x="340" y="210" font-size="14" text-anchor="middle">the social layer of conversation that text never records.</text>
<text x="340" y="250" font-size="14" font-weight="bold" text-anchor="middle">Dessa trains on the sound itself, so none of this is discarded.</text>
</svg>
</div>
<figcaption style="text-align:center">A transcript records words. Conversation runs on everything around the words — and that is exactly what an audio-only model gets to learn from.</figcaption>
</figure>

Now the honesty ledger, because it matters more here than usual. Everything above that sounds impressive rests, so far, on Block's own word and its own demo recordings. No parameter count, dataset size, latency figure, or formal benchmark has been published. "No text at all" is Block's description of its training, not an independently verified fact. And the demos themselves are not flawless: [The Verge](https://dealroom.co/news/165548-jack-dorseys-block-unveils-dessa-a-full-duplex-voice-ai-trained-only-on/) found them mostly natural but occasionally awkward — in one, Dessa mistakes its conversation partner for someone named "Ronaldo." A demo is a performance the maker chose to show you; it is not an evaluation. The right way to read Dessa today is as a existence proof with an asterisk: it appears possible to get this far on speech alone, and the asterisk says "someone independent still needs to check."

That asterisk is also the fresh angle. If Dessa's claim survives scrutiny, the field's data economics shift. Text corpora are finite, litigated, and increasingly expensive; human conversation is abundant, renewable, and mostly untranscribed. A model that learns from sound could keep improving from sources text models cannot touch — phone calls, meetings, bedtime stories, every spoken exchange that never becomes a document. And if it does not survive scrutiny — if "no text" turns out to mean "a little text, quietly" — the correction itself will be informative, because it will tell us where the boundary of speech-only learning actually lies. Either way, the question Dessa forces is one the field has been avoiding: how much of language is in the words, and how much is in the voice?

*Discussion: if a model can learn language from sound alone, what does "knowing a language" actually consist of — the words, or everything around them?*
