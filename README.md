# bitter-lesson

An agent skill that recalibrates coding and research agents to where AI actually is—correcting **stale, low-biased pretraining priors** and **anti-Bitter-Lesson scaffolding** whenever scoping, architecting, evaluating, or forecasting AI/LLM projects.

## Why This Exists

Models systematically underestimate current AI capabilities and propose obsolete project goals because three biases stack inside their weights:

1. **Cutoff Lag:** On METR's long-task horizon measure, the length of software tasks frontier agents complete has been doubling every **~3 to 4.5 months** since 2023–2024. A six-month-old cutoff is 1.5 to 2 doublings behind.
2. **Corpus Lag:** Most tokens in a model's training distribution discussing "what LLMs can't do" were written about 2020–2024 models. Fluency with claims like *"LLMs struggle with long-horizon tasks"* or *"models need custom RAG/AST graphs for large codebases"* is an artifact of training data volume, not current reality.
3. **Inherited Forecaster Bias:** Human experts and superforecasters have repeatedly underestimated benchmark progress (FRI XPT and LEAP studies—e.g., the spring 2026 expert end-of-year median for METR's 80% horizon was nearly met by May). Models inherited that conservatism.

Without an explicit calibration gate, models propose goals that are already commodity baselines (e.g., *"fine-tune a model so it goes from fixing small bugs to working on large codebases"*) and recommend hand-built scaffolding that the next checkpoint release will render pointless.

## What the Skill Enforces

- **[`skills/bitter-lesson/SKILL.md`](skills/bitter-lesson/SKILL.md)** — Core workflow:
  1. **Refresh Before You Assess:** Treat internal knowledge as a floor, never a reading. Search current frontier releases, METR horizons, discriminating leaderboards (`SWE-bench Pro`, `Terminal-Bench 4.0`, `FrontierSWE v2`, `OSWorld 2.0`), and small/open-weight models (`Qwen3-Coder-Next`, `Devstral Small 2`, `Haiku 5.5`).
  2. **The "Already Solved?" & Elicitation Test:** Verify whether a current frontier or small/open-weight model already solves the goal in a plain agent harness (shell, files, tests, search) before accepting it as a milestone. Use the **1-Hour Rule** (test the strongest model on the real task) when in doubt.
  3. **Project the Trend ($2^{T/d}$):** Stress-test 3-, 6-, 12-, and 18-month plans against ~3.5–4.3 month capability doublings (~1.7×, ~2.8×, ~8×, ~22×).
  4. **Apply Rich Sutton's Bitter Lesson:** Sort system components into **Appreciating** (verifiers, deterministic sandboxes, true workload evals, proprietary feedback loops, inference-time search) vs. **Depreciating** (rigid DAG decompositions, prompt tricks, narrow capability SFT, context-limit hacks).
  5. **Catch Stale Language & Classify Narrowly:** Separate `Commodity baseline`, `Feasible with engineering`, `Frontier / variable`, `Unproven for this workload`, and `Blocked under stated constraints`.
  6. **Stay Calibrated, Not Credulous:** Account for the 5–10× gap between 50% and 80% reliability horizons, spec messiness, missing graders, research judgment/taste, vendor vs. independent harness gaps, and reward hacking.
- **[`skills/bitter-lesson/references/frontier-baseline.md`](skills/bitter-lesson/references/frontier-baseline.md)** — Dated empirical snapshot (`2026-10-27`) covering METR horizons, SWE-bench Pro / Terminal-Bench 4.0, small/open-weight models, saturated vs. discriminating benchmarks, production authorship data, and primary refresh sources.
- **[`skills/bitter-lesson/references/evidence-playbook.md`](skills/bitter-lesson/references/evidence-playbook.md)** — Operational playbook for bidirectional search (underestimation vs. overestimation audits), evidence grading, the 7-step elicitation ladder, and designing 10–30 task decisive pilots.

## Installation

```bash
git clone https://github.com/3xC1ibR/bitter-lesson.git
ln -sfn "$(pwd)/bitter-lesson/skills/bitter-lesson" ~/.agents/skills/bitter-lesson
```

## License

MIT
