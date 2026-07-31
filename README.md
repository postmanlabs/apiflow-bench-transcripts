# APIFlow-Bench 1.0 — Raw Trial Transcripts

Complete raw transcripts for every trial behind the
[APIFlow-Bench 1.0 leaderboard](https://www.postman.com/ai/apiflow-leaderboard/):
**56,037 trials** — 24 models × 467 tasks × 5 trials (a handful of pairs have
fewer than 5 completed runs; see `_export_manifest.json`). The 2026-07-31 board
update added kimi-k3, claude-fable-5, gpt-5.6-luna, gpt-5.6-sol and minimax-m3
to the 19 launch models.

Benchmark code + task bank:
[APIFlow-Bench (code + task bank)](https://github.com/postmanlabs/APIFlow-Bench).

## AI-generated content notice

Every transcript in this repository is **AI-generated**: the complete,
unedited output of a large language model evaluated on APIFlow-Bench 1.0.
Model outputs may contain errors, hallucinated claims, or statements that do
not reflect the views of Postman, Inc. or of the model providers. Transcripts
were reviewed as part of the benchmark's publication process.

Published by [Postman](https://www.postman.com) as part of the APIFlow-Bench
1.0 release. Task prompts and benchmark materials are © 2026 Postman, Inc.;
model outputs remain subject to the usage terms of their respective providers.

## Layout

```
<model-slug>/<task_id>-t<N>.json
```

- `model-slug` — the model exactly as slugged on the leaderboard
  (e.g. `claude-sonnet-5`, `gpt-5.6-terra`, `minimax-m2p7`).
- `task_id` — the benchmark task (e.g. `v56-w01-sub01`, `v56-w03-chain-1to20`).
- `N` — trial number 1..5, matching the leaderboard's per-task trial numbering
  (`#trial-N` on the task drill-down pages).

Fetch a single transcript raw:

```
https://github.com/postmanlabs/apiflow-bench-transcripts/raw/main/<model-slug>/<task_id>-t<N>.json
```

Per-model bulk downloads (`transcripts-<model-slug>.tar.gz`) are attached to
the releases of the main benchmark repo.

## File contents

Each JSON is researcher-grade raw data for one trial (`schema_version: "1.0"`):

- `messages` — the real conversation: roles, message content, reasoning
  blocks, tool calls (name + arguments), and tool results, as recorded.
- `verifier` — the verifier output as stored (deterministic predicate groups
  and the LLM verifier payload where present).
- `verdict` / `passed` / `failure_reason` — trial outcome summary. `verdict` is
  `"C"` (correct = pass) or `"I"` (incorrect = fail); it is empty (`""`, with
  `passed: null`) for the 19 unscored trials listed below.
- `tokens` (input / output / cache / total), `duration_s`.
- `provenance` — bench label, run/eval identifiers, source log file, epoch.

Transcripts are published **unredacted** (including expected answers): the
benchmark's canary-based provenance grading replaces answer hiding.
`_export_manifest.json` carries per-model counts and size stats.

## Unscored trials

19 trials (all `qwen3p7-plus`) completed but carry no verifier verdict —
`verdict: ""`, `passed: null`, `verifier: null`. The published leaderboard
counts them in per-model trial totals (denominators) but not as passes; their
trial rows render as NO-SCORE. They are listed under `unscored_trials` in
`_export_manifest.json`:

```
v56-w02-chain-1to03-t3   v56-w02-chain-1to06-t2   v56-w03-chain-1to02-t4
v56-w03-chain-1to16-t2   v56-w03-sub15-t1         v56-w04-chain-1to12-t2
v56-w04-chain-1to17-t4   v56-w04-sub10-t3         v56-w05-chain-1to17-t1
v56-w05-chain-1to19-t5   v56-w06-sub04-t4         v56-w08-chain-1to03-t1
v56-w11-sub01-t2         v56-w11-sub01-t3         v56-w14-chain-1to07-t3
v56-w16-chain-1to04-t4   v56-w16-chain-1to15-t1   v56-w16-sub02-t3
v56-w18-chain-1to09-t1
```

## License

[Apache-2.0](LICENSE), same as the benchmark itself — this covers the
repository's compilation, structure, and metadata. The transcripts are model
outputs published for research transparency; model names identify the
providers whose APIs produced each output, and use of those outputs may
additionally be subject to the respective provider's terms.
