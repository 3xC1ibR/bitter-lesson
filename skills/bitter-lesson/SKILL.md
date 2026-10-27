---
name: bitter-lesson
description: Calibrate AI/LLM capability assumptions, project scoping, agent architectures, and training/eval plans against live empirical frontier benchmarks and Rich Sutton's Bitter Lesson. Mandatory whenever discussing, designing, evaluating, or scoping LLM projects, coding agents, harnesses, fine-tuning/RL runs, or autonomous workflows. Never rely on static model weights to judge what models can or cannot do.
---

# Bitter Lesson & Frontier AI Calibration

Models systematically underestimate current AI capabilities and propose obsolete architectures because their pretraining corpora are dominated by 2022–2024 priors (when models struggled with multi-file edits, required rigid RAG/AST scaffolding, and needed narrow SFT for basic tasks) and their weights lack awareness of post-training execution-RL and test-time compute harnesses.

When scoping an AI project, designing an agent harness, proposing fine-tuning/RL, or evaluating feasibility, execute the four protocols below before making architectural or capability claims.

---

## 1. Epistemic Distrust Gate (Zero Parametric Reliance)

Never claim what frontier, mid-tier, or open-weight models "cannot do yet," "struggle with," or "require fine-tuning/scaffolding to achieve" based on internal parametric knowledge alone.

1. **Check the date (`T_now`) vs. baseline calibration:** Read [references/frontier-baseline.md](references/frontier-baseline.md) for the anchored empirical floor (`last_calibrated`).
2. **Run live empirical verification when:**
   - `T_now - last_calibrated > 60 days`, or
   - Scoping a project's technical thesis, model selection, or success criteria, or
   - Claiming a capability ceiling or proposing SFT/RL/scaffolding to bridge a perceived model limitation.
3. **Required live queries (use web search or live leaderboards):**
   - **Autonomous Task Horizon:** Query `METR autonomous task completion time horizon doubling time` (check 50% and 80% human-hour horizons and the open-weight lag).
   - **Execution Benchmarks:** Query `Terminal-Bench leaderboard`, `FrontierSWE`, `LiveCodeBench`, or `Artificial Analysis intelligence vs price pareto`. (Treat static Python patch benchmarks like SWE-bench Verified as saturated/legacy).
4. **Local Empirical Probe (5-Minute Rule):** When local execution is available (e.g., via `rig`, `forge`, or CLI), test whether a zero-shot prompt + minimal bash loop or a smaller/open-weight model already solves a representative sample before proposing a multi-week training or scaffolding effort.

---

## 2. The Two-Doublings Trajectory Test

Post-2024 autonomous agent task horizons double approximately every **3.5 to 4.3 months (105–131 days)** ($R^2 \approx 0.98$), and open-weight models trail the closed frontier by only **4 to 6 months (~1 to 1.5 doubling periods)** at a fraction of the cost.

Any project taking 3–6 months to build will ship into a world where:
- Autonomous task horizons have doubled **1 to 1.5x**.
- Today's closed-frontier capability is available in cheap, fast, or open-weight models.

### Project Goal Rubric: Surfing vs. Swimming Against Compute

Before endorsing a project goal or research milestone, apply this filter:

| Anti-Pattern (Swimming Against Compute — Reject) | Bitter-Pilled Target (Surfing Compute — Propose) |
| :--- | :--- |
| "Fine-tune a model so it can move from fixing small bugs to working across large codebases." *(Solved baseline in frontier & mid-size models via standard bash/grep harnesses)* | Build **high-throughput, deterministic execution sandboxes** (`forge`) and **verifiable reward environments** that turn raw compute into autonomous hill-climbing. |
| "Build a complex multi-stage AST graph parser, custom semantic chunker, and rigid router DAG so the agent finds the right files." | Strip scaffolding down to a **minimalist shell + filesystem harness** (`rig`); invest engineering in fast environment reset, tool reliability, and parallel trajectory verification. |
| "Collect static SFT trajectories to teach a model a multi-step workflow." | Build an **automated verifier / grading harness** and run online RL or inference-time search (best-of-$N$, verifier-guided tree/trajectory selection) against real execution feedback. |
| "Prompt-engineer 15 specialized sub-agent personas with rigid handoff schemas." | Give a single capable agent (or dynamically spawned general workers) direct access to the environment, clear objective metrics, and durable state/memory (`stoic`, `agent-coord`). |

---

## 3. The Bitter Lesson Architecture Audit

When reviewing or designing an AI system, actively strip out human-engineered domain heuristics that compensate for yesterday's model weaknesses:

1. **Minimalist Harness Default:** Start with raw bash, standard Unix tools (`ripgrep`, `git`, test runners), and direct file manipulation. Add specialized tools only when empirical traces prove the bottleneck is **environment I/O, latency, security isolation, or observability**—never to "help the model think."
2. **Environment & Verifier > SFT:** When an agent fails a long-horizon task, diagnose in this order:
   1. **Missing observation / feedback loop:** Can the agent actually see runtime errors, test output, logs, or UI state?
   2. **Weak or gameable verifier:** Can the agent verify its own work deterministically without reward-hacking?
   3. **Insufficient test-time compute / search:** Would parallel rollouts + verifier selection solve it today?
   4. **Context hygiene / harness ergonomics:** Is context polluted by noisy tool output or rigid truncation?
3. **Strict Justification Gate for Fine-Tuning (SFT / RL):** Only propose model weight training when the goal is one of:
   - **Latency / Cost / Privacy Distillation:** Compressing a proven frontier capability into a small model (e.g., 1B–32B) for high-frequency, low-latency, or on-device execution where the frontier teacher already demonstrates the behavior.
   - **RL on a Novel Verifiable Environment:** Training with execution feedback on a domain with a fast, un-gameable reward signal where zero-shot/test-time scaling hits a verified wall.
   - **Strict Behavioral / Representation Priors:** Specialized token/action spaces or calibrated probability estimation where in-context prompting is structurally insufficient.

---

## 4. Calibration Output Format

When advising on an AI/LLM project, research direction, or architecture:

1. **State the Empirical Floor:** Explicitly cite the current capability baseline (from live search + [references/frontier-baseline.md](references/frontier-baseline.md)) for both frontier and open-weight/small models on the relevant task class.
2. **Call Out Obsolete Assumptions:** If the user's or a prior model's framing assumes a 2023–2024 limitation (e.g., "models can't handle large repos," "we need RAG for codebase navigation," "we need SFT for basic tool use"), directly correct it with current empirical evidence.
3. **Formulate Compute-Compounding Milestones:** Frame success criteria around **verifiable environments, evaluation harnesses, latency/cost pareto shifts, or tasks beyond the current 16+ human-hour autonomous horizon**—ensuring the work gets *more* valuable as base models double every ~4 months.
