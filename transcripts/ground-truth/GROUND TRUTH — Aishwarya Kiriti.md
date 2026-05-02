# Ground Truth Transcript — Aishwarya Naresh Reganti & Kiriti Badam
## VERIFIED against video — content confirmed

**Source clip:** ~5:03 from Lenny's Podcast (Aishwarya & Kiriti episode)
**Content:** Evals debate — false dichotomy, production monitoring, evaluation datasets
**Accent profile:** Indian-accented English (Aishwarya and Kiriti), Standard American English (Lenny)
**Cross-referenced:** Lenny's AI, Gemini, Reduct (all three sources)

---

**Aishwarya:** I was part of that group, so I kind of know about the questions that he comes up with.

**Lenny:** I love that. That's cool.

**Aishwarya:** It's pretty cool. I was like, "Why are you doing so much?" And then he says, "It trickles down into a bunch of decisions that we take."

**Lenny:** Okay. Let me talk about another topic that's very — it's been a hot topic on this podcast. It was a hot topic on Twitter for a while. Evals. A lot of people are obsessed with evals, think they're the solution to a lot of problems in AI. A lot of people think they're overrated, that you don't need evals. You can just feel the vibes and you'll be all right. What's your take on evals? How far does that take people in solving a lot of the problems that you talk about?

**Kiriti:** In terms of what is going on in the community, I feel there's just this false dichotomy of like — either evals is going to solve everything, or online monitoring or production monitoring is going to solve everything. And I find no reason to trust like one of the extremes, in the sense that I will entirely bank my application on this or like that to solve the thing. Right?

So if you take a step back, think of what are evals. Evals are basically your trusted product thinking, or your knowledge about the product, that is going into this set of datasets that you're going to build, in the sense that: this is what matters to me. Like this is the kind of problems that my agent should not do. And let me build a list of datasets so that I'm going to do well on those.

And in terms of production monitoring, what you're doing there is uh you're deploying your application and then you're having some sort of key metrics that actually communicate back to you on how customers are using your product. Like you could be deploying any agent, and if the customer is giving a thumbs up for your interaction, you better want to know that. So that is what production monitoring is going to do.

And this production monitoring has existed for products for a long time. Just that now with the AI agents, you need to be monitoring at a lot more granularity. It's not just the customer always giving you explicit feedback, but there is many implicit feedback that you can get. For example, in ChatGPT, right? If you are liking the answer, you can actually give a thumbs up. Or if you don't like the answer, sometimes customers don't give you a thumbs down, but actually regenerate the answer.

So that is a clear indication that the initial answer that you generated is not meeting the customer's expectation, right. So these are the kind of implicit signals you always need to think about. And that spectrum has been increasing in terms of production monitoring. Now, let's come back to the initial topic of like, okay, is it evals or is it production monitoring? What does it matter? So I feel, again, we go back to this problem-first approach of: what is it that you're trying to build? You're trying to build a reliable application for your customers that's not going to do a bad thing. It's always going to do the right thing. Or if it is doing a wrong thing, you're basically alerted very quickly. Right?

So I break this down into two parts. One is, nobody goes into deploying an application without actually just testing that. This testing could be vibes or this testing could be, "Okay, I have these 10 questions that it should not go wrong, no matter what changes I make." And let me build this, and let's call this an evaluation dataset.

Now, let's say you build this, you deploy this, and then you figured, "Okay, now I need to understand whether it's doing the right thing or not." So if you're a high-throughput or like a high-transaction customer, you cannot practically sit and evaluate all the traces. Right? You need some indication to understand what are the things that I should look at. And this is where production monitoring comes into the picture — that you cannot predict the ways in which your agent could be doing wrong.

But all of these other implicit signals and explicit signals, those are going to communicate back to you what are the traces that you need to look at. And that is where production monitoring helps. And once you get this kind of traces, you need to examine what are the failure patterns that you're seeing in these different types of interactions. And is there something that I really care about that should not happen? And if that kind of failure modes are happening, then I need to think about building an evaluation dataset for it.

And okay, let's say I built an evaluation dataset for my agent trying to offer refunds where explicitly I have configured it not to. So I built this evaluation dataset, and then I made my changes in tools or prompts or whatever, and then I deployed the second version of the product. Now, there is no guarantee that this is the only problem that you're going to see. You still need production monitoring to actually have like - to catch different kinds of problems that you might encounter.

So I feel evals are important, production monitoring is important, but this notion of only one of them is going to solve things for you — that is completely dismissible in my opinion.

**Lenny:** All right. A very reasonable answer. And the point here isn't — it's not just as simple as "do both." It's more that there are different things to catch, and one approach won't catch all the things you need to be paying attention to.

**Kiriti:** Exactly.

**Lenny:** Awesome.

**Aishwarya:** I want to take two steps back and kind of talk about how much weight the term evals has had to take...

[CLIP ENDS]

---

## Divergence log — VERIFIED

| Timestamp (approx) | Gemini | Reduct | Lenny's AI | Ground truth (verified) |
|---|---|---|---|---|
| 0:00–end (speaker) | Long passage = Aishwarya ✗; Host = "Kiriti" ✗ | Long passage = "Speaker 3" (unnamed) | Long passage = Kiriti ✓; Host = Lenny ✓ | **Kiriti** speaks the long evals/monitoring passage. Gemini got the speaker wrong AND misidentified Lenny as Kiriti. |
| 0:13 | Host = "Host (Kiriti)" ✗ | Host = "Speaker 2" | Host = Lenny ✓ | **Lenny** — Gemini confused host with guest |
| ~2:13 | "you generated" ✓ | "you generated" ✓ | "regenerator" ✗ | **"you generated"** — Lenny's AI is the outlier |
| ~2:41 | "vibes" ✓ | "wipes" ✗ | "vibes" ✓ | **"vibes"** — only Reduct got it wrong; /v/→/w/ substitution |
| ~3:12 | "the ways in which" ✓ | "the base in which" ✗ | "the base in which" ✗ | **"the ways in which"** — only Gemini got it right; both Reduct and Lenny's AI garbled it |
| ~4:35 | "actually have like - to catch" | similar | similar | Minor — low stakes |

## Critical notes for the presentation

1. **Speaker attribution** is itself a cascade event. Gemini misidentified the host as Kiriti and attributed Kiriti's long analytical passage to Aishwarya. If a researcher used only the Gemini transcript, any downstream analysis would credit the wrong person with the argument. Verified: the long passage is Kiriti, the host is Lenny.

2. **"Vibes" → "wipes"** — confirmed. Gemini and Lenny's AI both heard "vibes." Only Reduct substituted /v/ → /w/. Systematic phonemic pattern for Indian-accented English, not a random error.

3. **"Ways" → "base"** — confirmed as "ways." Both Reduct AND Lenny's AI heard "base." Only Gemini got it right. Lenny's AI — the transcript that ships with the episode, the version a researcher would default to — got it wrong. "The base in which" reads smoothly but isn't what was said.

4. **"Regenerator" in Lenny's AI** — confirmed as "you generated." Lenny's AI introduced a word that doesn't exist in context. Both Gemini and Reduct got it right.
