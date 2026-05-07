# Schema

Column definitions and value sets for the six CSV divergence logs in [`data/`](data/).

## Terminology

- **Divergence**: a single observed difference between outputs (between tools, between source paths, or between an output and the manually verified ground truth). One row per divergence.
- **Cascade**: how a divergence at one stage propagates or is transformed at the next stage. The synthesis and analysis files log cascade events because they track what happened to upstream divergences as the pipeline ran.

## What the headline counts mean

- **193 = 48 + 85 + 60.** Divergences from the Chip Huyen 5-minute clip pipeline: 48 transcription + 85 synthesis + 60 analysis. The figure cited in the article as "193 divergences from a single 5-minute clip."
- **45 = 25 + 20.** Transcription divergences from the other two 5-minute clips (Hamel/Shreya and Aishwarya/Kiriti). Transcription was performed on all three clips; synthesis and analysis were run only on the Chip clip.
- **97.** NotebookLM divergences from full-episode comparisons across all three episodes (full episodes, not 5-minute clips).
- **335 total** documented divergences across the experiment (193 + 45 + 97).

The pipeline-stage scope is different across files. 193 is one clip, three pipeline stages, four LLMs. The 45 additional transcription divergences cover only the transcription stage on the other two 5-min clips. The 97 NLM divergences come from a separate agentic-platform comparison run on full episodes.

---

## `transcription_divergences_chip.csv` — Chip Huyen clip transcription (48 rows)

Plus two parallel files with identical schema: `transcription_divergences_hamel_shreya.csv` (25 rows) and `transcription_divergences_aishwarya_kiriti.csv` (20 rows).

Divergences between three transcription sources on each 5-min clip.

| Column | Description |
|---|---|
| `divergence_id` | Unique identifier (E01, E02, …) |
| `timestamp_approx` | Approximate timestamp in the audio clip |
| `manual_audit_ground_truth` | The researcher's manually audited reading of what was actually said in the audio, produced using Reduct's video-alongside-text feature. A single ground-truth phrase per row, with a brief descriptor where the divergence is structural (speaker attribution, segment boundary). Full analytical context, alternate candidate readings, and divergence patterns across tools are documented in the `notes` column |
| `gemini_transcript` | What Gemini's ASR returned |
| `reduct_transcript` | What Reduct's ASR returned |
| `rev_transcript` | What Rev's human transcription returned (the version Lenny's Podcast publishes) |
| `divergence_type` | See enum below |
| `severity` | `critical`, `moderate`, or `minor` |
| `notes` | Researcher's interpretation of the divergence |

**`divergence_type` values:**
`word_substitution`, `word_omission`, `word_addition`, `speaker_misattribution`, `hedging_lost`, `hedging_changed`, `proper_noun_error`, `number_error`, `technical_term_error`, `disfluency_handling`

**`severity` scale:**
- `critical` — changes the meaning of the utterance
- `moderate` — changes emphasis or tone
- `minor` — cosmetic difference (e.g., punctuation, capitalization, filler removal)

---

## `synthesis_cascade_chip.csv` — synthesis-stage cascade events on Chip clip (85 rows)

How transcription divergences propagated or were transformed at the synthesis stage. One row per observed cascade event.

| Column | Description |
|---|---|
| `cascade_id` | Unique identifier (C01, C02, …) |
| `source_error_id` | Linked `divergence_id` from `transcription_divergences_chip.csv`, or blank if originating at synthesis |
| `transcript_source` | `gemini`, `reduct`, `rev`, or `all_transcripts` |
| `model` | `claude`, `gemini`, `openai` (GPT-5.4), or `openai_4o` (GPT-4o) |
| `claim_in_summary` | The text from the AI-generated summary |
| `original_in_transcript` | The corresponding text from the source transcript |
| `cascade_type` | See enum below |
| `severity` | `critical`, `moderate`, or `minor` |
| `notes` | Researcher's interpretation |

**`cascade_type` values:**
- `error_passed_through` — transcription divergence reproduced as-is
- `error_amplified` — transcription divergence made worse (e.g., elaborated into false detail)
- `error_corrected` — transcription divergence silently fixed by the model
- `error_avoided` — content omitted from summary, sidestepping the divergence
- `hedging_to_assertion` — hedged spoken language rendered as confident claim
- `argument_dropped` — speaker's argument or qualification absent from summary
- `argument_invented` — claim in summary not present in transcript
- `stance_shifted` — speaker's stance subtly reframed

---

## `analysis_cascade_chip.csv` — analysis-stage cascade events on Chip clip (60 rows)

How synthesis-stage distortions propagated or were transformed at the analysis (theme extraction) stage. One row per observed cascade event.

| Column | Description |
|---|---|
| `cascade_id` | Unique identifier (A01, A02, …) |
| `upstream_source` | The transcript-summary path that fed this analysis (e.g., `rev_claude`, `gemini_openai_4o`) |
| `analysis_model` | `claude` (Claude Opus 4.6) — the only analysis model in the final dataset |
| `theme_extracted` | The theme name produced by the analysis |
| `recommendation` | The recommendation produced alongside the theme |
| `cascade_type` | See enum below |
| `upstream_error_link` | Linked cascade IDs from `synthesis_cascade_chip.csv` (semicolon-separated) |
| `severity` | `critical`, `moderate`, or `minor` |
| `exact_quote` | Verbatim quote from the analysis output |
| `notes` | Researcher's interpretation |

**`cascade_type` values:**
- `theme_from_transcription_error` — theme derived from a transcription divergence
- `theme_from_synthesis_error` — theme derived from a synthesis-stage distortion
- `theme_fabricated` — theme has no basis in the upstream summary
- `recommendation_fabricated` — recommendation has no basis in the upstream summary
- `hedging_to_doctrine` — speaker's tentative framing converted to authoritative doctrine
- `stance_amplified` — speaker's stance presented more strongly than in the source
- `stance_reversed` — speaker's stance inverted
- `information_lost` — content present upstream is absent from the analysis
- `confidence_without_basis` — confident claim with weak or absent upstream support
- `inter_analysis_contradiction` — analyses from different paths contradict each other
- `transcript_group_clustering` — analyses from the same transcript share thematic signatures more than analyses from the same model

---

## `nlm_divergences.csv` — NotebookLM divergences (97 rows)

Divergences between NotebookLM's YouTube-source and transcript-source outputs across all three episodes (full-episode comparisons, not 5-minute clips). Documents how an agentic platform behaves when fed the same source in two different formats.

| Column | Description |
|---|---|
| `divergence_id` | Unique identifier |
| `episode` | `chip`, `hamel_shreya`, or `aishwarya_kiriti` |
| `source_type` | `youtube_video` or `rev_transcript` |
| `output_type` | `summary` or `analysis` |
| `divergence_type` | See enum below |
| `severity` | `critical`, `moderate`, or `minor` |
| `exact_quote` | Verbatim quote from the NLM output |
| `comparison_quote` | Corresponding text from the other source path (or source audio) |
| `notes` | Researcher's interpretation |

**`divergence_type` values:**
- `proper_noun_garbled` — name or term mistranscribed
- `theme_substitution` — same episode, different top theme by source path
- `theme_present_one_source_only` — theme appears in only one of the two source paths
- `claim_present_one_source_only` — claim appears in only one of the two source paths
- `specificity_loss` — content present upstream became vaguer in output
- `specificity_gain` — content present upstream became more specific in output
- `vocabulary_import` — output uses terminology not in the source
- `framing_divergence` — same content framed differently across source paths
- `confidence_without_hedging` — confident claim with no uncertainty markers
- `fabrication_candidate` — claim with weak or absent source support
- `structural_masking` — output formatting hides provenance differences
- `agentic_opacity` — failure mode specific to agentic orchestration (chained transcription + synthesis + analysis with no intermediate visibility)
