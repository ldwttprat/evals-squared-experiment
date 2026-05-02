# Ground Truth Transcript — Hamel Husain & Shreya Shankar
## VERIFIED against video — content confirmed

**Source clip:** ~4:50 from Lenny's Podcast (Hamel Husain & Shreya Shankar episode)
**Content:** Error analysis walkthrough, open coding, benevolent dictator concept
**Accent profile:** Standard American English (all speakers)
**Cross-referenced:** Lenny's AI transcript, Gemini transcript, Reduct transcript

---

**Hamel:** The channel through which the customer is communicating is through text message, and you're just getting like really garbled. And you can see here that it kind of doesn't make sense. You know, like the words are being cut off, like "in the meantime," and then the system doesn't know how to respond, because you know how people text message. They like write short phrases. They, you know, split their sentence across four or five different turns.

**Lenny:** Yeah, so what do you do with something like that?

**Hamel:** Yeah, so this is a different kind of error. This is more of "hey, we're not handling this interaction correctly." This is more of a technical problem rather than "hey, the AI is not doing exactly what we want."

**Lenny:** It's still really cool. Like, it's amazing you're catching that too here. Otherwise you'd have no idea this was happening.

**Hamel:** Yeah, you might not know this is happening, right? And so you would just say, okay, you'd write a note like, "conversation flow is janky because of text message."

**Lenny:** And I like — yeah, I like that you're using the word janky. It shows you just how informal this can be at this stage.

**Hamel:** Yeah, it's supposed to be chill. Like, just don't overthink it. And there's some — there's a way to do this. So the question always comes up: how do you do this? Do you look at — do you try to find all the different problems in this trace? What — what do you write a note about? And the answer is: just write down the first thing that you see that's wrong. The most upstream error. Don't worry about all the errors. Just capture the most — the first thing that you see that's wrong, and stop and move on. And you can get really good at this. The first two or three can be very painful, but you know, it doesn't — you can, you know, do a bunch of them really fast.

So here's another one. And let's skip the system prompt again. And the user asks, "Hey, I'm looking for a two-to-three bedroom with either one or two baths. Do you provide virtual tours?" And a bunch of tools are called. And it says, "Hi Sarah, currently we have a three-bedroom, two-and-a-half-bathroom apartment available for $2,175." "Unfortunately, we don't have any two-bedroom options at the moment. We do offer virtual tours. You can schedule a tour, blah blah blah."

It just so happens that there's no virtual tour, right?

**Lenny:** Nice.

**Hamel:** Right? So, you know, it is hallucinating something that doesn't exist, and you would kind of have to bring your context as an engineer, or even your product context, to say, "Hey, this is kind of weird. Like, you know, we shouldn't be telling a person about a virtual tour when it's not offered." So you would say, okay, "offered virtual tour," and you just — you just write the note.

So you can see there's a diversity of different kinds of errors that we're seeing. And we're actually learning a lot about your application in a very short amount of time.

**Shreya:** One common question that we get from people at this stage is, "Okay, I understand what's going on. Can I ask an LLM to do this process for me?"

**Lenny:** Mm, great question.

**Shreya:** And I loved Hamel's most recent example, because what we usually find when we try to ask an LLM to do this error analysis is it just says the trace looks good. Because it doesn't have the context needed to understand whether something might be, you know, bad product smell or not. For example, the hallucination about scheduling the tour, right? I can guarantee you — I would bet money on this — if I put that into ChatGPT and asked, "Is there an error?" it would say, "No, did a great job."

But Hamel had the context of knowing we don't actually have this virtual tour functionality, right?

So I think in these cases, it's so important to make sure you are manually doing this yourself. And we'll talk — we can talk a little bit more about when to use LLMs in the process later. But like, number one pitfall right here is people are like, "Let me automate this with an LLM."

**Lenny:** Do you think they'll — we'll get to a place where an agent can do this without — has that context?

**Shreya:** Oh, no no no. Sorry. There are parts of error analysis that an LLM is suited for, which we can talk about later in this podcast. But right now, in this stage of freeform note-taking, is not the place for an LLM.

**Lenny:** Got it. And this is something you call open coding, this step?

**Shreya:** Yes, absolutely.

**Lenny:** Cool. Um, another term that you used in your post that I love, and that fits into this step, is this idea of a benevolent dictator. Maybe just talk about what that is, and maybe Shreya cover that?

**Shreya:** Yeah, so Hamel actually came up with this term.

**Lenny:** Okay, maybe Hamel cover that.

**Hamel:** No problem. And we'll actually show the LLM automation in this example, because we're going to take this example, we're going to go all the way through.

**Lenny:** Amazing.

**Hamel:** And so — benevolent dictator is just a catchy term for the fact that when you're doing this open coding, a lot of teams get bogged down in having a committee do this. And for a lot of situations, that's wholly unnecessary.

---

## Divergence log — VERIFIED

| Timestamp (approx) | Gemini | Reduct | Lenny's AI | Ground truth (verified) |
|---|---|---|---|---|
| ~1:35 | "one or two baths" | "one or two bats" ✗ | "one or two baths" | **"baths"** — Reduct dropped the /θ/ |
| ~3:08 | "Hamel's most recent example" | "how most most recent example" ✗ | "Hamel's most recent example" | **"Hamel's most recent example"** — Reduct garbled the name |
| ~3:42 | "Hamel had the context" | "Hamill had the context" ✗ | "Hamel had the context" | **"Hamel"** — Reduct misspelled throughout |
| ~4:23 | "maybe Shreya cover that" | "maybe sure I cover that" ✗ | "maybe Shreya cover that" | **"Shreya"** — Reduct garbled the name |
| Throughout | 2 speakers (Host, Hamel) | 2 speakers (Speaker 1, Speaker 2) | 3 speakers (Lenny, Hamel, Shreya) | **3 speakers** — Lenny's AI has correct attribution; Reduct collapsed Shreya into Speaker 2; Gemini collapsed Shreya into Hamel |

## Critical notes for the presentation

1. **Lowest divergence of the three clips** — as expected for Standard American English speakers in a clean recording. The cascade still produced errors, but fewer and less consequential than the Chip or Aishwarya/Kiriti clips.

2. **Reduct's name garbling** is the main pattern: "Hamill" for Hamel, "sure I" for Shreya, "bats" for "baths." These are phonemic substitutions, not random — the tool is hearing plausible alternatives and committing to them.

3. **Speaker attribution varies across all three tools.** Gemini collapsed Shreya into Hamel's speaker block. Reduct used anonymous labels. Only Lenny's AI correctly distinguished all three speakers by name. This is the one dimension where Lenny's AI outperformed both other tools on this clip.

4. **Blueprint check (Chip criteria applied to this clip):** All three transcripts pass on hedging/stance (no significant stance changes in SAE clip), technical terms (no domain-specific terms misheard), and speaker attribution (all got the basic two-party structure right, though Shreya attribution varies). Reduct fails on names. This clip is the baseline — the low-complexity case where the cascade has less to destroy.
