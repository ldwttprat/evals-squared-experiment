# Sources and Influences

Practitioner work, academic research, and institutional efforts that inform the *evals²* experiment and the five-step blueprint in *Winning the Game of Broken Telephone*.

---

## On error analysis and definitional work

**Hamel Husain and Shreya Shankar** — Their work on LLM evals has trained thousands of engineers and product builders. The blueprint's emphasis on open coding of real outputs, identifying failure patterns inductively until saturation, and treating error analysis as the most important activity in evals draws directly on their public guidance.
- Hamel Husain — *AI Evals FAQ*: <https://hamel.dev/blog/posts/evals-faq/>
- Shreya Shankar — *In Defense of AI Evals*: <https://www.sh-reya.com/blog/in-defense-ai-evals/>

## On benchmark validity

**Andrew Bean and colleagues** — Reviewed 445 language model benchmarks and found most lack basic construct validity (they don't reliably measure what they claim to measure). Anchors the blueprint's wariness of borrowed metrics.
- *Lingua Manga: A Comprehensive Survey of LLM Benchmarks*: <https://openreview.net/pdf?id=mdA5lVvNcU>

**Deborah Raji and colleagues** — Showed that common evaluation benchmarks are routinely treated as general measures of capability they were never designed to capture. Foundational for the "Maintain" step.
- *AI and the Everything in the Whole Wide World Benchmark* (2021): <https://arxiv.org/abs/2111.15366>

## On proportionate rigor

**Carl Pearson and Constantine Papas** — Their concept of "minimum viable rigor" (matching the depth of checking to the stakes of the decision the research informs) anchors the blueprint's approach to the "Check" step. The experiment extends this with a twin idea, "minimum viable context," about how much the system needs to know about a study for any amount of checking to be meaningful.
- Carl Pearson — *Minimum Viable Rigor*: <https://carljpearson.com/minimum-viable-rigor/>
- Constantine Papas — *From Theory to Practice: Making Minimum Viable Rigor Work for Real Teams*: <https://www.thevoiceofuser.com/from-theory-to-practice-making-minimum-viable-rigor-work-for-real-teams/>

## On qualitative AI failure modes

**Caitlin Sullivan** — Identified four failure modes for AI-assisted qualitative analysis (fabricated quotes, generic insights, unflagged contradictions, analysis disconnected from decisions), with a quote-verification prompt as a practical fix. Used in the "Check" step.
- *How to Do AI Analysis You Can Actually Trust*: <https://www.lennysnewsletter.com/p/how-to-do-ai-analysis-you-can-actually>

## On the instability of the evaluation infrastructure itself

**EvalEval Coalition** — Hosted by Hugging Face, the University of Edinburgh, and EleutherAI. Exists specifically because evaluation infrastructure is unstable and needs ongoing scrutiny.
- <https://evalevalai.com/>

## On compounded error in production AI systems

**Baptiste Jamin** (CEO, Crisp) — His "Real Problem: Compounded Error" presentation at Paris AI Day 2026 makes the structural insight visible: a single AI step at 85–90% accuracy chained five times drops to roughly 44% reliability. *"Agents don't fail loudly. They fail statistically."*
- Slide deck: <https://gamma.app/docs/AI-Days-2026-3cknaqig8i03kyo>

## Tools referenced

- **Promptfoo** (acquired by OpenAI) — open-source eval framework: <https://www.promptfoo.dev/>
- **Monica.im** — LLM output comparison: <http://monica.im>
- **Poe** — LLM output comparison: <http://poe.com>
- **Reduct** — video-alongside-text transcription, used to produce the ground-truth transcripts: <https://reduct.video/>
- **Rev** — human transcription service used by *Lenny's Podcast* for published transcripts: <https://www.rev.com/>
