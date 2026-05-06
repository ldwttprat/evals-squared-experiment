# Validating the Research Risk Cascade: Methodology and Findings

A worked example of AI-infused pipeline evaluation. This appendix documents the methodology and findings of the experiment presented in:

- *Winning the Game of Broken Telephone: A Blueprint for Evaluating AI Across the Research Pipeline.* DeWitt Prat, Lindsey. *ResearchOps Review*, May 2026. <https://www.theresearchopsreview.com/p/a-blueprint-for-evaluating-ai-across-the-research-pipeline>
- *Evaluating AI Across the Research Pipeline.* DeWitt Prat, Lindsey, with Kaleb Loosbrock, hosted by Ben Wiedmaier. User Interviews webinar, 31 March 2026. <https://www.userinterviews.com/blog/what-is-the-ai-research-risk-cascade>

The four CSV error logs referenced here are in this repository under `data/`.

## 1. Research Question

Where does an AI-augmented research pipeline lose signal?

## 2. Source Material

Three 5-minute clips from Lenny's Podcast (downloaded via yt-dlp):

- **Hamel Husain & Shreya Shankar** — *Why AI evals are the hottest new skill for product builders* (Standard American English). <https://www.youtube.com/watch?v=BsWxPI9UM4c&t=5054s>
- **Chip Huyen** — *AI Engineering 101 with Chip Huyen (Nvidia, Stanford, Netflix)* (Vietnamese-accented English). <https://www.youtube.com/watch?v=qbvY0dQgSJ4&t=1944s>
- **Aishwarya Reganti & Kiriti Badam** — *Why most AI products fail: Lessons from 50+ AI deployments at OpenAI, Google & Amazon* (Indian-accented English). <https://www.youtube.com/watch?v=z7T1pCxgvlA&t=2000s>

Selection rationale: thematic coherence (all three discuss AI evaluation from different angles), accent and gender diversity across speakers, content spanning engineering, product, and agency/trust perspectives.

## 3. Pipeline Stages Tested

### Stage 1: Transcription

Three tools, each processing the same audio clips:
- Gemini (AI)
- Reduct (AI)
- Rev human transcription (the service Lenny's Podcast pays for and publishes alongside each episode)

Rev's human transcripts served as a third version, with the understanding that human editing introduces its own transformations: editorial polish, disfluency removal, filler stripping.

A fourth, independent ground-truth transcript was produced manually by the researcher using Reduct's video-alongside-text feature.

### Stage 2: Synthesis

- Focused on the Chip Huyen clip (strongest accent-related findings at the transcription stage)
- Three transcripts × four models (Claude Opus 4.6, Gemini 3.1 Pro, GPT-5.4, GPT-4o) = 12 summaries
- Same prompt across all models, to isolate model variation from prompt variation

**Synthesis prompt:**
> "Summarize the key arguments in this conversation about AI evaluation."

### Stage 3: Analysis (theme extraction)

- 12 summaries analyzed by Claude Opus 4.6 (single model, isolating upstream variation)
- 12 total analyses

**Analysis prompt:**
> "Extract the three most important themes from this summary and provide a one-sentence recommendation for each."

All analysis runs were fresh API calls with no memory between them.

### Agentic comparison: NotebookLM

- All three full episodes loaded into NotebookLM as both YouTube video (NLM runs internal transcription) and as Rev human transcript text (NLM receives clean text)
- NLM produced summaries and analyses from each source type
- 12 NLM outputs (3 episodes × 2 source types × 2 output types)

## 4. Error Tracking Methodology

Four CSV error logs, each with typed and severity-rated entries:

### `error_analysis.csv` (48 entries)

Transcription-stage divergences between three tools.

- **Columns:** `error_id`, `timestamp_approx`, `spoken_word_best_guess`, `gemini_transcript`, `reduct_transcript`, `rev_transcript`, `error_type`, `severity`, `notes`
- **Error types:** `word_substitution`, `word_omission`, `word_addition`, `speaker_misattribution`, `hedging_lost`, `hedging_changed`, `proper_noun_error`, `number_error`, `technical_term_error`, `disfluency_handling`
- **Severity scale:** critical (changes meaning), moderate (changes emphasis or tone), minor (cosmetic)

### `synthesis_cascade.csv` (85 entries)

How transcription errors propagated or were handled at the synthesis stage.

- **Columns:** `cascade_id`, `source_error_id`, `transcript_source`, `model`, `claim_in_summary`, `original_in_transcript`, `cascade_type`, `severity`, `notes`
- **Cascade types:** `error_passed_through`, `error_amplified`, `error_corrected`, `error_avoided`, `hedging_to_assertion`, `argument_dropped`, `argument_invented`, `stance_shifted`

### `analysis_cascade.csv` (60 entries)

How synthesis-stage distortions propagated or were handled at the analysis stage.

- **Columns:** `cascade_id`, `upstream_source`, `analysis_model`, `theme_extracted`, `recommendation`, `cascade_type`, `upstream_error_link`, `severity`, `exact_quote`, `notes`
- **Cascade types:** `theme_from_transcription_error`, `theme_from_synthesis_error`, `theme_fabricated`, `recommendation_fabricated`, `hedging_to_doctrine`, `stance_amplified`, `stance_reversed`, `information_lost`, `confidence_without_basis`, `inter_analysis_contradiction`, `transcript_group_clustering`

### `nlm_error_analysis.csv` (97 entries)

Divergences between NotebookLM's YouTube-source and transcript-source outputs across all three episodes.

- **Columns:** `error_id`, `episode`, `source_type`, `output_type`, `error_type`, `severity`, `exact_quote`, `comparison_quote`, `notes`
- **Error types:** `proper_noun_garbled`, `theme_substitution`, `theme_present_one_source_only`, `claim_present_one_source_only`, `specificity_loss`, `specificity_gain`, `vocabulary_import`, `framing_divergence`, `confidence_without_hedging`, `fabrication_candidate`, `structural_masking`, `agentic_opacity`

## 5. Key Findings

### 5.1 Transcription Stage (48 events)

- **4 critical errors** where meaning was inverted or a key term was wrong.
- **The bearishness finding:** "I'm much less bearish" (Gemini) vs. "I'm actually a bit bearish" (Reduct) vs. "I'm not sure if I'm bearish" (Rev human). Three contradictory stances from the same utterance. Each transcription tool resolved acoustic ambiguity differently, producing opposite readings of the speaker's position.
- **The domain term finding:** "creative writing" (Gemini) vs. "curve writing" (Reduct) vs. "code writing" (Rev human). The same phrase, heard four times in the clip, rendered differently by each tool. Each rendering is internally consistent within its transcript.
- **The accent finding:** Chip Huyen's Vietnamese-accented English produced systematic confusion. "Will be able" vs. "wouldn't be able" (polarity inversion). "Good visibility to how your applications" (Gemini) vs. "good feasibility to hassle applications" (Reduct). The Aishwarya/Kiriti clip showed the /v/–/w/ distinction: "vibes" (Gemini, correct by context) vs. "wipes" (Reduct and Rev human).
- **The editorial finding:** Rev's human transcript systematically removed hedging, false starts, and filler words. This improved readability and reshaped the speaker's actual speech pattern, register, and uncertainty markers. "I'm not sure if I'm bearish" may itself be an editorial smoothing of something less clean in the audio.
- **Speaker attribution:** Reduct fragmented a single speaker across 2–4 speaker labels in every clip. Gemini misidentified the host in the Aishwarya clip.

### 5.2 Synthesis Stage (85 events)

- **Transcript source determined argument coverage more than model choice.** Four arguments (multi-step evaluation pipeline, organizational impact, the "no magic number" position, failure-as-insight) appeared in every Rev-human-transcript summary and vanished from every AI-transcript summary, regardless of which model did the summarizing. The human-edited transcript produced richer summaries because it covered more content (or preserved it more completely).
- **Models handled transcription errors differently.** GPT-4o passed "curve writing" through into its summary as a real concept. Gemini silently corrected it to "creative writing." Claude dropped the reference entirely. GPT-5.4 reinterpreted it as "story writing." Four strategies, zero transparency. No model flagged uncertainty.
- **Hedging was systematically flattened.** Chip's tentative, exploratory spoken reasoning became confident analytical claims in every summary. Qualifying language ("I think," "maybe," "I'm not sure") was stripped or converted to declarative framing.
- **The bearish hedge was skipped entirely.** All 12 summaries omitted the bearish/bullish framing — no model surfaced the contradictory stance readings produced at the transcription stage. The opening ambiguity about Chip's market position never propagated into synthesis.
- **The personal disclaimer was preserved in only 4 of 12 summaries.** Chip's explicit "this is not the philosophy I follow" was retained in C67, C71, C76, and C77, and dropped from the other 8.
- **Specific numbers were handled inconsistently.** Claude preserved absolute figures (80% to 85%). Gemini converted to relative ranges (2–5% improvement). GPT-5.4 dropped all numbers and abstracted to qualitative descriptions. GPT-4o was inconsistent across transcript sources.

### 5.3 Analysis Stage (60 events)

- **Themes were highly path-dependent across the 12 analyses; no theme appeared in every path.** The 54 theme entries logged ranged from broad doctrinal framings ("Pragmatic ROI-driven approach to evals") to one-off observations specific to a single transcript-summary path.
- **The dominant cascade pattern was `hedging_to_doctrine` (16 instances).** Every analysis path converted tentative spoken reasoning into authoritative named doctrines with prescriptive recommendations.
- **Four critical stance reversals** (A40, A41, A58, A59) attributed Chip's distancing from the vibes-based approach back to her as advocacy. The exact phrase "Chip argues that not every feature needs rigorous evals" was produced by Claude analyses of both the Rev-Claude and Gemini-Claude pipelines (A40, A41).
- **Chip's explicit disclaimer was erased from all 12 analyses.**
- **The "creative writing" transcription error produced two entirely different theme families by stage three.** The Rev-human-transcript path (which rendered it as "code writing") produced technical process themes. The AI-transcript paths (which rendered it as "creative writing") produced organizational talent themes. A single word at stage one split the analysis into two different conceptual worlds.
- **Transcript-group clustering was stronger than model-group clustering.** Rev-human-transcript analyses shared thematic signatures with each other more than with analyses from other transcripts summarized by the same model.
- **Five fabricated claims appeared at stage three** with no basis in the source audio: "catastrophic failure" language, "first-class product skill" framing, "forcing function" organizational theory, a recommendation to "retire stale evals," and a proactive "build before scaling" imperative.
- **The analysis stage added zero quality control.** Claude treated all 12 summaries with identical confidence regardless of upstream error. No analysis flagged transcription quality concerns, summary faithfulness questions, or missing information.

### 5.4 Agentic Comparison: NotebookLM (97 events)

- **15 critical divergences** across three episodes.
- **The name garbling finding:** NLM's YouTube-source path rendered "Aishwarya Reganti and Kiriti Badam" as "Aishwaria Raanti and Kiti Bottom." NLM's transcript-source path got both names correct. The YouTube path required NLM to run internal transcription before analysis; the garbled names propagated through synthesis and analysis with no hedging or uncertainty markers. The output looked identically authoritative in both cases.
- **The name error followed a phonetic predictability gradient:** names with common English phoneme patterns survived (Chip Huyen, Hamel Husain, Shreya Shankar); names with uncommon phoneme combinations were garbled (Kiriti Badam, Aishwarya Reganti).
- **Theme substitution:** the Chip pair produced "Strategic Implementation of Evaluations" (YouTube source) vs. "The Critical Role of Data Preparation and Post-Training" (transcript source). Same episode, same tool, different input format, different top-three themes.
- **The transcript path systematically retained more technical specificity** ("vector databases," "chunk sizes," "question-answering formats," "CCCD" abbreviation, "living PRDs"). The YouTube path used vaguer language ("high-quality data," "end-to-end workflows"). When the tool must transcribe audio itself, it appears to allocate processing capacity to transcription at the expense of analytical specificity, or transcription noise causes the synthesis layer to retreat to safer, more general language.
- **Information loss was bidirectional and unpredictable** across all three episodes. The YouTube path captured some content the transcript path missed (testing false dichotomy, procedural workflows, possibly "axial codes"). The transcript path captured content the YouTube path missed (vector databases, "benevolent dictator" as standalone theme, "pain" as competitive moat). A researcher using only one output path would have no way to know what the other path captured.
- **Structural masking:** all six NLM analysis outputs used identical formatting (numbered themes, bold headers, recommendation sentences, numbered citations) regardless of whether the underlying input was clean text or noisy audio transcription. The formatting carried no provenance signal.

## 6. Files and Artifacts

This repository contains:

- **3 audio clips** (`.mp3`): the 5-minute extracts from Lenny's Podcast
- **3 ground-truth transcripts** (manually verified by the researcher)
- **9 transcripts** (3 clips × 3 tools: Gemini, Reduct, Rev human)
- **12 summaries** (Chip clip only; 3 transcripts × 4 models)
- **12 analyses** (Claude Opus 4.6)
- **12 NotebookLM outputs** (3 episodes × 2 sources × 2 output types)
- **4 error log CSVs** (48 + 85 + 60 + 97 = 290 total documented events)

A `SCHEMA.md` file describes the columns and value sets used in each CSV.

## Citation

DeWitt Prat, Lindsey. 2026. "Winning the Game of Broken Telephone: A Blueprint for Evaluating AI Across the Research Pipeline." *ResearchOps Review*. Experiment data and methodology: <https://github.com/ldwttprat/evals-squared-experiment>.

## License

CSV data and methodology: CC BY 4.0. Audio clips and original transcripts referenced under fair use for research and educational purposes.
