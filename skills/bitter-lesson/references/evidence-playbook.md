# Evidence, Evaluation, and Pilot Playbook

Use this playbook for consequential capability judgments, project reviews, benchmark audits, and pilot design. Do not treat benchmark or model names as frozen—always query for the current year's state of the art.

---

## 1. Search Both Sides of the Claim

Construct queries around the concrete operational task rather than generic "AI capabilities" terms. Include the current year.

### Positive-Capability Discovery (Underestimation Audit)
*Question: "What if the strongest current system, with proper tools and inference compute, already does this?"*
- `[task] frontier AI agent benchmark [year]`
- `[task] coding agent autonomous evaluation [year]`
- `[model] system card technical report agent harness`
- `[task] small open-weight model benchmark single GPU [year]`
- `[task] inference scaling parallel rollouts verifier selection`

### Failure, Harness Sensitivity, and Transfer Discovery (Overestimation Audit)
*Question: "What if the apparent success is benchmark contamination, vendor harness tuning, weak grading, or poor transfer?"*
- `[benchmark] limitations audit contamination saturation [year]`
- `[benchmark] independent evaluation standardized harness vs vendor`
- `[task] agent failure modes reliability pass@1 vs pass@k`
- `[task] reward hacking grading script exploitation`

A null search is not evidence of impossibility. Broaden terminology, check primary system cards, and if still unmeasured, recommend a 1-hour local probe or structured pilot.

---

## 2. Evidence Hierarchy & Extraction Schema

Prefer evidence in this order, weighing **task match, grading strictness, sample size, and harness transparency** together:

1. **Task-matched local trials:** Fresh representative tasks from the actual repo/workload, repeated runs, locked deterministic grading, strong frontier + small baselines, and logged human intervention time.
2. **Independent standardized evaluations:** Transparent harnesses, current models, multiple trials, and confidence intervals (e.g., METR, Epoch AI, Scale public standardized sets).
3. **Contamination-aware public benchmarks:** Held-out or post-cutoff tasks with execution-based graders (`Terminal-Bench`, `SWE-bench Pro`, `OSWorld 2.0`).
4. **Production telemetry & case studies:** Useful for workflow fit and real-world uplift; audit for selection bias and unmeasured human review labor.
5. **Vendor system cards & technical reports:** Essential for frontier upper bounds and elicitation recipes; treat unaudited headline numbers as claims requiring harness inspection.
6. **Demos and anecdotes:** Existence proofs (`pass@k > 0`), never reliability estimates.

### Comparable Evidence Table
Never compare two headline percentages without checking whether their setups match across these dimensions:

| Field | What to Capture |
| :--- | :--- |
| **Date & Status** | Publication/evaluation date; whether the leaderboard is still actively maintained or saturated |
| **System & Budget** | Exact model checkpoint, reasoning effort / thinking tokens, and total inference cost per task |
| **Harness / Scaffold** | Shell access, file tools, retries, parallel rollouts (`best-of-N`), verifier selection, context compaction |
| **Task Distribution** | Domain, repository scale, specification ambiguity, novelty, and human-time horizon |
| **Metric** | `pass@1` (unattended reliability) vs. `pass@k` / verifier-selected (discovery); partial credit rules |
| **Human Role** | Zero-shot autonomous vs. human-in-the-loop steering, environment setup, or output cherry-picking |
| **Validity & Transfer** | Contamination risk, grader edge-case error rate, reward-hacking susceptibility, and match to user workload |

---

## 3. Elicitation Ladder (Test Before Claiming a Capability Gap)

Do not declare a task beyond current models—or propose fine-tuning/complex scaffolding—until you have evaluated where it sits on the elicitation ladder:

1. **Clear specification & acceptance criteria:** Does the agent have the same context, conventions, and definition of done a human engineer would need?
2. **Frontier model + reasoning budget:** Was a current frontier model tested with an appropriate test-time compute budget?
3. **Minimalist execution harness:** Does the agent have raw shell access, filesystem tools, fast search (`ripgrep`), and the ability to run tests and inspect stack traces?
4. **Verifier & environment feedback loop:** Can the agent observe runtime errors, UI state, or compiler/linter output and self-correct iteratively?
5. **Inference-time scaling / parallel search:** Would running $N$ parallel trajectories (`rig` / `forge` workers) and selecting via a deterministic test suite or reward verifier solve it today?
6. **Context hygiene:** Is failure caused by reasoning limits, or simply by noisy tool dumps polluting the context window?
7. **Adaptation / Fine-Tuning (Last Resort for Capability, First Resort for Economics):** Only after steps 1–6 are characterized should you propose weight updates—either to distill the working pipeline into a cheap/fast model or to run online RL against the verifier from Step 4.

---

## 4. Designing the Smallest Decisive Pilot

When literature evidence doesn't cleanly transfer to the user's workload, propose a compact empirical pilot before committing to a multi-week architecture or training plan:

1. **Task Set (10–30 fresh tasks):** Draw directly from the real workload (easy, typical, and hard cases). Ensure zero overlap with public training data and hold out a test split.
2. **Locked Arms:**
   - *Arm A (Frontier Generalist Baseline):* Best current frontier model in a plain shell/tool harness (`rig` / Claude Code / Codex).
   - *Arm B (Small / Open-Weight Baseline):* Strongest small/local model (`Haiku`, `Qwen3-Coder`, `Devstral`) in the same harness to anchor unit economics.
   - *Arm C (Proposed Intervention):* Only if Arms A/B reveal a specific bottleneck.
3. **Pre-registered Grading & Full-Workload Metrics:**
   - Measure **first-attempt (`pass@1`)** and **verifier-selected (`pass@k`)** success.
   - Log **human review/cleanup minutes**, **wall-clock latency**, and **token/compute cost**.
   - Inspect failure transcripts for **reward hacking** or **missing environment observations** before blaming model intelligence.
4. **Decision Thresholds:** Define up front what result kills the need for custom scaffolding or fine-tuning (e.g., *"If Arm A hits >80% with a deterministic verifier, we invest in the verifier and distill to Arm B for cost, rather than building a custom RAG/SFT pipeline"*).

---

## 5. Language Discipline

| Avoid (Stale, Uncalibrated, or Vibe-Based) | Prefer (Dated, Operational, and Calibrated) |
| :--- | :--- |
| *"Models cannot work across large codebases."* | *"Commodity baseline in 2026: frontier models hit ~80–90% on SWE-bench Pro and 3B-active open models handle repo-level edits locally."* |
| *"We should fine-tune a model to do X."* | *"Frontier models already do X in a standard shell harness; test zero-shot + verifier first, and only fine-tune if we need to distill into a small model for latency/cost."* |
| *"This is solved."* | *"Demonstrated at ~60% `pass@1` on Terminal-Bench 4.0 under a standard CLI harness; unattended production reliability at 99% still requires a deterministic verifier."* |
| *"LLMs struggle with long-horizon planning."* | *"As of Oct 2026, METR 50% horizons reach ~16–17 human-hours, while 80% reliability sits near ~3 hours; tasks beyond that require milestone verification or human checkpoints."* |
