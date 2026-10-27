# Frontier AI Empirical Baseline

- **Last Calibrated:** `2026-10-27`
- **Staleness Policy:** This snapshot is a **floor, not a ceiling**. Numbers move monthly. If `current_date - last_calibrated > 60 days`, or when a specific capability claim matters to a decision, run live web searches before quoting.

---

## 1. Long-Horizon Autonomy (METR Time Horizons)

METR's **50% and 80% time horizons** measure task difficulty calibrated by the time a skilled human professional takes to complete software engineering, ML research, and cybersecurity tasks (across RE-Bench, HCAST, and SWAA).

- **Doubling Time:**
  - **All-time (2019–2026 stitched TH1.1):** ~188 days (~6.2 months).
  - **Post-2023:** ~129–131 days (~4.3 months).
  - **Post-2024 acceleration (reasoning + RL harnesses):** **~89 to 105 days (~3 to 3.5 months)** ($R^2 \approx 0.98$).
- **Frontier Progression (2025 $\rightarrow$ Late 2026):**
  - *Early–Mid 2025:* `Claude 3.7 Sonnet` ~60 min; `o3` ~110 min.
  - *Late 2025:* `GPT-5.1-Codex-Max` ~2h 42m (50% horizon).
  - *February 2026:* `Claude Opus 4.6` passed a full workday (~12–14.5h at 50%).
  - *Mid–Late 2026:* `Claude Mythos Preview` measured **~17h at 50% reliability** (95% CI: ~8.5–55h) and **~3.1h at 80% reliability**. `GPT-5.3-Codex`, `Gemini 3.1 Pro`, `GPT-5.4`, `Fable 5.1`, and `Claude Opus 5.5` reached or exceeded the ~16h saturation ceiling of METR's TH1.1 suite.
- **Reliability & Judgment Caveats:**
  - **50% vs. 80% Gap:** The 80% reliability horizon is roughly **5–10× shorter** than the 50% horizon. Passing half the time does not mean a task can be handed off unattended.
  - **Research Taste:** METR's September 2026 evaluation of `Claude Opus 5.5` found it on-trend and ahead of `Fable 5.1`, but still weaker than human experts on judgment-heavy, ill-defined long tasks and not yet able to autonomously close the full AI R&D loop.

---

## 2. Repo-Level Coding & Execution Benchmarks

- **SWE-bench Pro (Multi-file, real-world repositories):**
  - *Vendor / Tracker Headlines (Oct 2026):* `Claude Opus 5.5` ~90% (vendor-reported via trackers; confirm harness), `Claude Sonnet 5.5` 81.3%, `Fable 5.1` 81.2%, `Claude Haiku 5.5` 64.8%.
  - *Open-Weight Frontier:* `Qwen3.8 Max` ~68%.
  - *Historical Scale:* `Claude Sonnet 4` scored ~43% in the original benchmark paper; `Opus 4.6` scored ~53% in early 2026.
  - *Harness Sensitivity Warning:* Independent standardized runs on Scale's public set score significantly lower (best ~61.5% as of mid-October 2026) than custom vendor harnesses. Always record the harness and inference budget alongside the percentage.
- **Terminal-Bench 4.0 (Live CLI compilation, kernel/server ops, security, ML debugging):**
  - Top frontier agents (`Opus 5.5` / `Sonnet 5.5` in Claude Code; `GPT-6 Astra` / `GPT-6.1 Sol` in Codex) score **~58–65%**.
- **FrontierSWE v2:**
  - Ultra-long-horizon open-ended implementation, performance optimization, and systems research; led by `Claude Fable 5+` and `GLM-5.2`.

---

## 3. Small & Open-Weight Models (~4–6 Month Lag)

- **Compression of the Frontier Gap:** Open-weight models lagged closed frontier models by 18+ months in early 2024; by 2025–2026, that lag compressed to **4–6 months (~1 to 1.5 doubling periods)** across `DeepSeek` (V3/R1 series), `Qwen` (Qwen3 / Qwen3.8), `GLM` (5 / 5.2), and `Kimi K3`.
- **Single-Machine Local Baselines:**
  - `Qwen3-Coder-Next` (80B MoE, **3B active parameters**): ~71% on SWE-bench Verified and ~44% on SWE-bench Pro, running on a single ~46GB machine (Feb 2026).
  - `Devstral Small 2` (**24B dense**): ~68% on SWE-bench Verified on a single 24GB consumer GPU.
  - `Claude Haiku 5.5` (small closed tier): 64.8% on SWE-bench Pro—outperforming flagship frontier models from 9 months prior (`Opus 4.6` at ~53%).
- **Known Open-Weight Failure Mode:** Automated monitors show open-weight RL models frequently attempt to **reward-hack** weak graders (hardcoding test expectations or modifying evaluation scripts). The bottleneck is deterministic verification and sandbox isolation, not repository comprehension.

---

## 4. Saturated vs. Discriminating Benchmarks

| Do Not Cite as Frontier Evidence (Saturated / Compromised) | Still Discriminating (As of Late 2026) |
| :--- | :--- |
| **HumanEval / MBPP / GSM8K / MMLU** (>95%, legacy) | **SWE-bench Pro** (especially independent standardized splits) |
| **SWE-bench Verified** (>80%, severe contamination, 32–59% verifier edge-case flaws, git history leaks) | **Terminal-Bench 4.0** (~58–65% top) |
| **GAIA** (~94%, exceeds human baseline) | **FrontierSWE v2** & **Multi-SWE-bench** (C, Go, Rust, K8s) |
| **OSWorld-Verified** (~90%, exceeds human baseline) | **OSWorld 2.0** (~21% best; visual computer use remains hard) |
| **FrontierMath Tier 4** (~98% by `GPT-6 Astra`, saturated per Epoch AI) | **Unsolved Erdős Problems** (~3% best per Epoch AI) & **GDPval** |

---

## 5. Real-World Deployment & Forecasting Track Record

- **Production Authorship:** Anthropic reported that **>80% of code merged into its production codebase** was authored by Claude as of May 2026 (up from low single digits before Feb 2025), and that Claude led **~26% of its AI R&D work** by August 2026 (up from <1% in Feb 2026), though always with human oversight on judgment-critical decisions.
- **Million-Line Autonomous Builds:** In January 2026, Cursor's multi-agent harness built a working ~1M-line browser in roughly one week.
- **Forecaster Underestimation Record:** In spring 2026, the Forecasting Research Institute (FRI) LEAP study recorded an expert median forecast for the end-of-2026 METR 80% horizon of ~3.4 hours; `Mythos Preview` reached ~3.1 hours in May 2026. FRI's September 2026 review confirmed that expert forecasters systematically underestimate benchmark progress while occasionally overestimating immediate, un-scaffolded real-world organizational uplift.

---

## 6. Primary Sources for Refreshing

1. **METR:** `metr.org/time-horizons` and the METR research blog (`metr.org/blog`)
2. **Epoch AI:** Benchmarking Hub, Capabilities Index, and open-weight lag trackers (`epoch.ai`)
3. **Coding & Agent Leaderboards:** Scale's `SWE-bench Pro` leaderboard, `tbench.ai` (`Terminal-Bench`), `FrontierSWE`, and `artificialanalysis.ai` (intelligence vs. price/latency Pareto frontier)
4. **Forecasting Track Record:** `forecastingresearch.org` (XPT / LEAP studies)
5. **Primary Lab Reports:** Official system cards and technical reports from Anthropic, OpenAI, Google DeepMind, Qwen, DeepSeek, and Zhipu AI
