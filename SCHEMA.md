# Schema

Column definitions and value sets for the four CSV error logs in [`data/`](data/).

---

## `transcription_divergences.csv` — transcription-stage divergences (48 rows)

Divergences between three transcription sources on the same source audio.

| Column | Description |
|---|---|
| `error_id` | Unique identifier (E01, E02, …) |
| `timestamp_approx` | Approximate timestamp in the audio clip |
| `manual_audit_ground_truth` | The researcher's manually audited reading of what was actually said in the audio, produced using Reduct's video-alongside-text feature. For 8 of 48 rows the audio is acoustically ambiguous and multiple candidate readings are listed instead of a single resolved one (these cases are flagged in the `notes` column) |
| `gemini_transcript` | What Gemini's ASR returned |
| `reduct_transcript` | What Reduct's ASR returned |
| `rev_transcript` | What Rev's human transcription returned (the version Lenny's Podcast publishes) |
| `error_type` | See enum below |
| `severity` | `critical`, `moderate`, or `minor` |
| `notes` | Researcher's interpretation of the divergence |

**`error_type` values:**
`word_substitution`, `word_omission`, `word_addition`, `speaker_misattribution`, `hedging_lost`, `hedging_changed`, `proper_noun_error`, `number_error`, `technical_term_error`, `disfluency_handling`

**`severity` scale:**
- `critical` — changes the meaning of the utterance
- `moderate` — changes emphasis or tone
- `minor` — cosmetic difference (e.g., punctuation, capitalization, filler removal)

---

## `synthesis_cascade.csv` — synthesis-stage divergences (85 rows)

How transcription errors propagated or were transformed at the synthesis stage. One row per observed cascade event.

| Column | Description |
|---|---|
| `cascade_id` | Unique identifier (C01, C02, …) |
| `source_error_id` | Linked `error_id` from `error_analysis.csv`, or blank if originating at synthesis |
| `transcript_source` | `gemini`, `reduct`, `rev`, or `all_transcripts` |
| `model` | `claude`, `gemini`, `openai` (GPT-5.4), or `openai_4o` (GPT-4o) |
| `claim_in_summary` | The text from the AI-generated summary |
| `original_in_transcript` | The corresponding text from the source transcript |
| `cascade_type` | See enum below |
| `severity` | `critical`, `moderate`, or `minor` |
| `notes` | Researcher's interpretation |

**`cascade_type` values:**
- `error_passed_through` — transcription error reproduced as-is
- `error_amplified` — transcription error made worse (e.g., elaborated into false detail)
- `error_corrected` — transcription error silently fixed by the model
- `error_avoided` — content omitted from summary, sidestepping the error
- `hedging_to_assertion` — hedged spoken language rendered as confident claim
- `argument_dropped` — speaker's argument or qualification absent from summary
- `argument_invented` — claim in summary not present in transcript
- `stance_shifted` — speaker's stance subtly reframed

---

## `analysis_cascade.csv` — analysis-stage divergences (60 rows)

How synthesis-stage distortions propagated or were transformed at the analysis (theme extraction) stage. One row per observed cascade event.

| Column | Description |
|---|---|
| `cascade_id` | Unique identifier (A01, A02, …) |
| `upstream_source` | The transcript-summary path that fed this analysis (e.g., `rev_claude`, `gemini_openai_4o`) |
| `analysis_model` | `claude` (Claude Opus 4.6) — the only analysis model in the final dataset |
| `theme_extracted` | The theme name produced by the analysis |
| `recommendation` | The recommendation produced alongside the theme |
| `cascade_type` | See enum below |
| `upstream_error_link` | Linked cascade IDs from `synthesis_cascade.csv` (semicolon-separated) |
| `severity` | `critical`, `moderate`, or `minor` |
| `exact_quote` | Verbatim quote from the analysis output |
| `notes` | Researcher's interpretation |

**`cascade_type` values:**
- `theme_from_transcription_error` — theme derived from a transcription error
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

## `nlm_error_analysis.csv` — NotebookLM divergences (97 rows)

Divergences between NotebookLM's YouTube-source and transcript-source outputs across all three episodes. Documents how an agentic platform behaves when fed the same source in two different formats.

| Column | Description |
|---|---|
| `error_id` | Unique identifier |
| `episode` | `chip`, `hamel_shreya`, or `aishwarya_kiriti` |
| `source_type` | `youtube_video` or `rev_transcript` |
| `output_type` | `summary` or `analysis` |
| `error_type` | See enum below |
| `severity` | `critical`, `moderate`, or `minor` |
| `exact_quote` | Verbatim quote from the NLM output |
| `comparison_quote` | Corresponding text from the other source path (or source audio) |
| `notes` | Researcher's interpretation |

**`error_type` values:**
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
