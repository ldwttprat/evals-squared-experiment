# evals-squared-experiment

Methodology, prompts, and divergence logs from the *evals²* experiment, which extends the cascade modeling first developed in [*The Research Risk Cascade: Why Even '90% Accurate' AI Tools Break Pipelines*](https://lindseydewittprat.substack.com/p/the-research-risk-cascade-why-even) (DeWitt Prat, January 2026). The experiment was presented at the [User Interviews webinar](https://www.userinterviews.com/blog/what-is-the-ai-research-risk-cascade) on 31 March 2026, and is published in [*Winning the Game of Broken Telephone: A Blueprint for Evaluating AI Across the Research Pipeline*](https://www.theresearchopsreview.com/p/a-blueprint-for-evaluating-ai-across-the-research-pipeline) (*ResearchOps Review*, May 2026).

The experiment runs three five-minute podcast clips through three transcription tools, four summarization models, and one analysis model, and tracks every place the outputs diverge from the source and from each other. The goal is to show how errors compound across an AI-augmented research pipeline, and to provide a reproducible method any researcher can run on their own source material in an afternoon.

## What's in here

- [`EXPERIMENT.md`](EXPERIMENT.md): full methodology, source material, prompts, and findings by stage
- [`SCHEMA.md`](SCHEMA.md): column definitions and value sets for the four CSV error logs
- [`SOURCES.md`](SOURCES.md): practitioner work the blueprint draws on
- [`data/`](data/): four CSV error logs (290 documented divergences across the pipeline)
  - `transcription_divergences.csv`: 48 transcription divergences
  - `synthesis_cascade.csv`: 85 synthesis divergences
  - `analysis_cascade.csv`: 60 analysis divergences
  - `nlm_error_analysis.csv`: 97 NotebookLM divergences (agentic comparison)
- [`audio/`](audio/): the three five-minute source clips (`.mp3`)
- [`transcripts/`](transcripts/): all transcripts and AI outputs used in the experiment
  - `ground-truth/`: three manually verified ground-truth transcripts
  - `tool-outputs/`: nine raw transcripts (3 clips × 3 tools: Gemini, Reduct, Rev human)
  - `summaries/`: twelve summaries (Chip clip; 3 transcripts × 4 LLMs)
  - `analyses/`: twelve Claude analyses
  - `nlm/`: twelve NotebookLM outputs (3 episodes × 2 sources × 2 output types)

## Running this yourself

The methodology in `EXPERIMENT.md` is designed to be portable. Pick one source (e.g., a recorded interview, a focus group, a podcast clip) and run it through whatever combination of tools your pipeline uses. Compare the outputs against each other and against the source. The shape of your cascade will come into view.

## Acknowledgment

Source audio and Rev human transcripts are from *Lenny's Podcast*, which has released its full data archive at <https://www.lennysdata.com/>. Re-shared here for research and educational use.

## Citation

DeWitt Prat, Lindsey. 2026. *evals² Experiment.* <https://github.com/ldwttprat/evals-squared-experiment>.

## License

CSV data and methodology: [CC BY 4.0](LICENSE). Source audio and Rev human transcripts from *Lenny's Podcast* (<https://www.lennysdata.com/>); AI-generated outputs (Claude, Gemini, GPT-4o, GPT-5.4) included for research and educational purposes.
