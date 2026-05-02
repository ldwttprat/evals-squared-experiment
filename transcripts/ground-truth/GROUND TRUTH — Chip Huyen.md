# Ground Truth Transcript — Chip Huyen
## VERIFIED against video — content confirmed, one word marked [inaudible]

**Source clip:** ~5:00 from Lenny's Podcast (Chip Huyen episode)
**Content:** Data labeling company economics, what evals are, vibes vs evals debate
**Accent profile:** Vietnamese-accented English (Chip), Standard American English (Lenny)
**Cross-referenced:** Lenny's AI transcript, Gemini transcript, Reduct transcript
**Status:** Content verified by Lindsey against video, March 20 2026

---

**Lenny:** ...as they have so few customers, and there's so many people getting into the space. So basically, even though they're some of the fastest-growing companies in the world, you're feeling like there's, there's a challenge up ahead.

**Chip:** I'm not sure if I'm bearish on it. Um, I think I'm curious because I think things has a way of work out in ways that I don't expect. So I think that maybe these companies, they have a lot of data. Maybe they would be able to use that to like have some insight that helps them like stay ahead of the curve, you know. So, so I don't know.

**Lenny:** A very fair answer. Okay, well while we're on this topic, I want to chat about evals, which is a very recurring topic in this podcast. This is the other piece of data content these companies share that AI labs really need. Can you just talk about what an eval is, the simplest way to understand it, and then how this helps models get smarter?

**Chip:** So I think that people approach eval, I think there's like two very different problems. One is an app builder, right, and like, can I say I have an app that do like maybe a chatbot. Very simple, it's the first thing that came to my mind. Um, and I want to know if this chatbot is good or bad, right? So so I need to come up with a way of like evaluating this chatbot.

Um, another thing is, uh, I think of this as a task-specific eval design. So let's say I'm a model developer and I want to make my model better at creative writing, right? And I was like, okay, but how, how do I even measure creative writing, right? So I need someone to like, okay, understand creative writing and think about like what makes good story or like what makes a story good and then design the whole dataset and then criteria to evaluate creative writing.

Um, so yeah, so so I think that's like — I think it's more like eval design that is very interesting. Uh, coming up with criteria, um, coming up with guidelines, how to do it, and then also like train people, like how to do it effectively.

Um, so I guess, uh, in a [inaudible] I think eval is really, really fun because it's extremely creative. Uh, I was looking at like different evals people built and I was like, wow, like — it's not dry at all. It's just like super, super, super fun.

**Lenny:** We had a whole podcast on evals with Hamel and Shreya, and that's exactly what they talked about is just, it's actually really fun to create evals for, for companies, especially. So let's still dig into that one a little bit more. There's this kind of debate online that I don't know how big of a deal this debate is, but it feels like people spend a lot of time thinking about this. This idea of, do we need evals for AI products? Some of the best companies say they don't really do evals. They just go on vibes. They're just like, is this working well, can I feel it or not? What's your take on just the importance of building evals and the skill of evals for AI apps, not the model companies?

**Chip:** You don't have to be like absolutely perfect at things to win. You just need to be like good enough and be consistent about it. Okay, this is not the philosophy I follow, but like I have worked with enough companies to see that play out. So what I say like why companies don't need eval, right?

Let's say you are like an executive, right, and you want to have a new use case. So here's a use case you started out and build and it's like it works well, right? The customers are somewhat happy, you don't have the exact metric for it, but like the traffic keeps increasing, like people seem happy, people keep buying stuff, right? And now here's your engineer coming like, okay, we need eval for it.

And the executive was like, okay, how much effort do we need to put into eval? And they were like, okay, maybe like two engineers, this much and this much, and it could maybe would improve, so I was like, okay, so how much expected gain can I get from it? And the engineer could be like, oh, maybe you can improve it from like 80% to like 82%, 85%, right? And I was like, okay, but it's going to take that two engineers and build and launch a new feature, then it could give me like so much more like improvement, right?

So so I think it's like one of them as they eval, sometimes people think of eval as like, okay, this is good enough, just don't touch it, like if you do spend a lot of energy on eval it would only incremental improvement whereas they spend the energy on like another use case and maybe let's get it to good enough that you can just vibe check it, right?

So so I do think like maybe that's the debate is about. I do think that like a lot of time people just like get things to the place when it's like, okay, good enough, people run. But and then but of course there's a lot of risk associated with it because if you don't have a clear metric, you don't have good visibility to how your application and the model is performing, it might do something very dumb or it can cause you like I don't know, something like crazy can happen.

So yeah so so I do think eval is very, very important if you have, if you operate at scale and where like failures can have like catastrophic consequences then you do need to be very tyrannical about like what you put in front of the users, understand different failure modes like what could go wrong and also maybe in the space when that like is a feature, as a product, as a competitive advantage, right? You want to be the best at it, so you want to have like a very strong understanding of like where you are and like where you are with your competitors. But it's just something that's like more like a learning curve.

---

## Divergence log — VERIFIED

| Timestamp (approx) | Gemini | Reduct | Lenny's AI | Ground truth (verified) |
|---|---|---|---|---|
| 0:09 | "I'm much less bearish" ✗ | "I'm actually a bit bearish" ✗ | "I'm not sure if I'm bearish" ✓ | **"I'm not sure if I'm bearish"** — Lenny's AI correct; both AI tools wrong in opposite directions |
| 0:13 | "things have had a way of work out" | "things have, has a way of work out" | "things has a way of work out" | **"things has a way of work out"** — Chip's actual grammar; all three smoothed differently |
| 0:24 | "maybe they will be able" (right direction, wrong modal) | "maybe they wouldn't be able" ✗ | "maybe they wouldn't be able" ✗ | **"maybe they would be able"** — Both Reduct AND Lenny's AI inverted the meaning. Only Gemini got the direction right. |
| 1:19–1:42 | "creative writing" (×4) ✓ | "curve writing" (×4) ✗ | "code writing" (×4) ✗ | **"creative writing"** — only Gemini correct; Reduct and Lenny's AI each substituted a different plausible term |
| ~1:57 | "in a way" | "in a quiz" | "[inaudible]" | **[inaudible]** — unresolvable even against video |
| ~3:43 | "it's going to take that two engineers and build and launch" | "if you're going to take that two engineers" | "[inaudible] that two engineers" | **"it's going to take that two engineers and build and launch"** |
| ~4:56 | "in the space when that like is a feature, as a product, as a competitive advantage" | similar | similar | Minor variance — low stakes |

## Critical notes for the presentation

1. **The bearishness divergence** — three transcripts, three opposite readings of Chip's stance. Verified: "I'm not sure if I'm bearish." The published Lenny's transcript got it right. Both AI tools got it wrong, each in a different direction — Gemini made her sound confident ("much less bearish"), Reduct made her sound like she agreed ("actually a bit bearish"). Neither captured her actual hedging.

2. **"Would" → "wouldn't" inversion** — verified as "maybe they would be able to use that." Both Reduct AND the published Lenny's transcript rendered this as "wouldn't be able" — inverting Chip's cautious optimism into pessimism. Only Gemini got the direction right ("will be able" — wrong modal verb but correct meaning). The published transcript, which a researcher would treat as the most authoritative source, inverted the speaker's argument.

3. **"Creative writing" vs "code writing" vs "curve writing"** — verified as "creative writing." Only Gemini got it right. The published Lenny's transcript substituted "code writing," sending downstream analysis in a completely different direction. Reduct substituted "curve writing," a nonexistent concept that appeared four times and reads like a real term.

4. **The disclaimer** ("this is not the philosophy I follow") is present in all three transcripts and confirmed in the ground truth. It was erased from all downstream summaries. This is a synthesis-layer cascade event — the transcription was correct at step one; the error entered at step two.

5. **No transcript passed all four blueprint checks** (preserve hedging/stance, get terms right, get names right, attribute correctly). Gemini passed 3/4 (failed stance). Lenny's AI passed 2/4 (failed terms + inverted a key meaning). Reduct passed 0/4.
