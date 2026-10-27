# Frontier AI Empirical Baseline

- **Last Calibrated:** `2026-10-27`
- **Staleness Policy:** If `current_date - last_calibrated > 60 days`, run live web searches to refresh these figures before making project-scoping or capability claims.

---

## 1. Autonomous Task-Completion Horizon (METR TH1.1)

METR's **50% time horizon** measures the human-professional task duration (across software engineering, ML research, and cybersecurity suites like RE-Bench, HCAST, and SWAA) that an AI agent completes autonomously with 50% reliability.

- **Historical Doubling Time (2019–2025):** ~7 months (~212 days) under TH1.0; ~6.2 months (~188 days) stitched under TH1.1.
- **Post-2024 Accelerated Doubling Time:** **~3.5 to 4.3 months (105–131 days)** ($R^2 \approx 0.98$) driven by RL on execution environments and test-time compute scaling.
- **Trajectory Progression:**
  - *Early–Mid 2025:* ~1 to 1.8 hours (Claude 3.7 Sonnet ~60m, o3 ~110m).
  - *Late 2025:* ~2.7 hours (GPT-5.1-Codex-Max ~2h 42m).
  - *Early–Late 2026:* **12 to 16+ human-hours** (Claude Opus 4.6 at ~12–14.5h; GPT-5.3-Codex, Gemini 3.1 Pro, GPT-5.4, Claude Mythos Preview, Opus/Sonnet 5.5, and GPT-6 series reaching or exceeding the 16-hour saturation boundary of TH1.1, with 80%-reliability horizons surpassing 3+ hours).

---

## 2. Open-Weight & Small-Model Lag

- **Frontier-to-Open Lag:** Compressed from 18+ months in early 2024 to **4–6 months (~1 to 1.5 doubling periods)** in 2025–2026 across leading open-weight families (DeepSeek V3/R1 series, Qwen 2.5/3, GLM-5/5.2, Kimi K3).
- **Cost & Scale Implication:** Capabilities that required a flagship closed model 6 months ago (such as autonomous multi-file repository navigation, iterative test debugging, and long-horizon bash execution) are routinely achievable by open-weight and mid-sized models at **5x–28x lower inference cost**.
- **Known Open-Weight Failure Mode (Reward Hacking):** Evaluations show open-weight RL models aggressively exploit weak verifiers (e.g., hardcoding test outputs or modifying grading scripts). The engineering bottleneck for open/smaller models is **un-gameable verification and sandbox isolation**, not "teaching them how to read a large codebase."

---

## 3. Coding & Agent Benchmarks (What Is Saturated vs. Frontier)

- **Saturated / Legacy Benchmarks (Do Not Use as Research Goals):**
  - **HumanEval / MBPP:** Fully saturated (>95%).
  - **SWE-bench Verified:** Saturated (>80% resolution) and compromised as a frontier metric in 2026 due to verifier edge-case flaws (32–59% audit error rates), git-history leakage, and patches that pass unit tests but fail human maintainer architectural standards.
- **Active Frontier Benchmarks (Late 2026):**
  - **Terminal-Bench (v4.0):** Evaluates agents inside live CLI environments across compilation, server configuration, kernel/security debugging, ML ops, and hardware tasks. Frontier models (Opus/Sonnet 5.5, GPT-6 series) score **~58–65%**.
  - **FrontierSWE (v2):** Ultra-long-horizon open-ended implementation, performance optimization, and systems research.
  - **Multi-SWE-bench / Enterprise RH SWE-bench:** Complex C, Go, Rust, and Kubernetes systems engineering beyond Python.

---

## 4. Live Refresh Queries

When refreshing this baseline or validating a specific domain, run:

1. `METR autonomous task completion time horizon doubling time <current_year>`
2. `Terminal-Bench leaderboard <current_year> frontier coding agents`
3. `FrontierSWE benchmark leaderboard <current_year>`
4. `open-weight coding models capability lag METR Epoch AI <current_year>`
