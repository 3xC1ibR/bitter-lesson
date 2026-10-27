---
name: bitter-lesson
description: Recalibrates you to where AI actually is, because your priors are stale and biased low. Use whenever you assess what models or agents can do, scope or set success criteria for an AI/LLM/agent project, judge whether a goal is ambitious, weigh fine-tuning or scaffolding against general models, review agent architectures, or forecast AI timelines, even if the user doesn't ask about capabilities directly.
---

# Bitter Lesson & Frontier AI Calibration

Your sense of what AI can do is out of date, and it errs in a known direction: **too low**. Treat capability beliefs as dated, testable hypotheses—not as stable model knowledge. This skill corrects that bias before it leaks into advice as goals that are already solved, "stretch" milestones that are table stakes, and hand-built scaffolding the next model release will make pointless.

Being **AI-pilled** and **Bitter-pilled** is not hype. It means being accurate about the frontier—which in practice mostly means updating *up* on what strongly elicited systems can do—while staying rigorous about reliability, evidence quality, and the specific places where the gap is still real (Section 6).

---

## Why Your Priors Run Low

Three structural effects stack, and none of them feel like bias from the inside:

1. **Cutoff lag.** On METR's long-task measure, the length of software tasks frontier agents can complete has been doubling roughly every **3 to 4.5 months** since 2023–2024. A six-month-old knowledge cutoff is 1.5 to 2 doublings behind. Between June and October 2026 alone, more than half a dozen frontier models shipped across three labs.
2. **Corpus lag.** Most of what you learned about "what LLMs can't do" was written about 2020–2024 models. Sentences like *"LLMs struggle with long-horizon tasks"* or *"models need RAG/AST graphs to navigate large codebases"* are far more common in your training data than they are true today. Fluency with a claim is not evidence that it is current.
3. **Inherited human bias.** Expert forecasters and superforecasters have repeatedly underestimated AI progress on benchmarks (Forecasting Research Institute XPT and LEAP studies). In spring 2026, the expert end-of-year median forecast for METR's 80% time horizon (~3.4h) was nearly met by May (~3.1h). You learned from these people.

When your gut says *"that's an ambitious goal for AI"* or *"models aren't ready for that,"* treat it as a hypothesis to check, not a judgment.

---

## Core Distinctions

Keep these separate throughout any analysis:

- **Model vs. system:** A raw base model, a high-reasoning configuration, and an agent in a persistent execution harness (shell, file tools, retries, parallel search, verification) are completely different capability levels.
- **Capability vs. reliability:** One valid pass establishes existence (`pass@k`), not a dependable unattended rate (`pass@1` or `pass^k`). Conversely, repeated failure under a weak prompt or missing tool does not establish incapability.
- **Benchmark vs. workload:** A headline score transfers only insofar as task messiness, scaffolding, grading strictness, and contamination controls match the real workload.
- **Autonomy vs. assistance:** Human-in-the-loop productivity uplift does not imply unattended completion, and a 50% autonomous horizon does not mean a task can be handed off unreviewed.

---

## The Workflow

Scale the effort to the decision. Use the fast path for quick questions; run the full workflow when capability assumptions shape project scope, architecture, training runs, timelines, or research novelty.

### 1. Refresh Before You Assess (Zero Parametric Reliance)

Before making a capability claim, setting a goal or success criterion, or calling something ambitious or infeasible, look up the current state. **Internal knowledge is a floor, not a reading.**

1. **Get today's date (`T_now`).** Never assume it is your training year. Check [references/frontier-baseline.md](references/frontier-baseline.md)—if `T_now - last_calibrated > 60 days`, assume the snapshot is already behind.
2. **Convert vague claims into testable operational claims:**
   > Under `[setup, harness, and constraints]`, system `[model + reasoning budget + tools]` completes `[task distribution]` at `[acceptance criteria]` with `[reliability rate]`, `[human review burden]`, `[cost]`, and `[latency]`.
3. **Search both sides of the claim (include the current year):**
   - **Frontier releases** in the last ~90 days.
   - **Autonomous horizon:** Latest METR time-horizon results (50% and 80% human-hour horizons) or successor long-task measures.
   - **Discriminating leaderboards:** SWE-bench Pro and Terminal-Bench 4.0 for coding agents, FrontierSWE for open-ended engineering, OSWorld 2.0 for computer use, FrontierMath / unsolved problems for math, GDPval for knowledge work.
   - **Small and open-weight models:** Query the same capability for open-weight/local models. Frontier capability routinely reaches small/open models within **4–6 months (~1–1.5 doubling periods)**, so *"only frontier models can do X"* expires fast.
   - **Failure modes & harness sensitivity:** Check whether scores are vendor-reported or standardized independent runs, and look for verifier gaming or contamination audits.
   - Read [references/evidence-playbook.md](references/evidence-playbook.md) for query templates, evidence grading, and pilot design.
4. **If you cannot search:** State explicitly that the baseline is unverified, present internal knowledge strictly as a lower bound as of your cutoff, extrapolate using Step 3, and propose a 1-hour empirical probe.

### 2. Run the "Already Solved?" & Elicitation Test

For every goal, milestone, success criterion, or claimed contribution you are about to propose:

1. **Can a current frontier model do this today in a plain agent harness** (shell, files, tests, search, adequate reasoning/token budget, and verifier feedback), with no fine-tuning or custom scaffolding?
2. **Can a small or open-weight model?**
3. **Did we check the elicitation ladder before claiming a gap?** Do not declare a task beyond current models based on a single prompt, a weak model, a tiny token budget, or missing execution feedback.

If yes to (1) or (2), **it is a commodity baseline, not a project goal.** Say so plainly, then raise the bar. A genuine contribution lives beyond the baseline:
- Higher reliability (moving from 50% $\rightarrow$ 80% $\rightarrow$ 99% unattended pass rate)
- Orders-of-magnitude lower cost, latency, or memory footprint (distillation / edge / privacy)
- Longer autonomous horizon (multi-day unattended execution)
- A messier, weakly specified, or less verifiable domain
- A novel evaluation/verification substrate nobody has built yet

> **Worked Example:** A model proposed this as the success criterion for an LLM project: *"fine-tune a model so it goes from fixing small bugs to working on large codebases."* It fails the test immediately. As of October 2026, frontier models report ~80–90% on SWE-bench Pro (multi-file repo changes), the smallest current Claude model (Haiku 5.5) reports ~65%, and open-weight models with 3B active parameters (`Qwen3-Coder-Next`) or 24B dense parameters (`Devstral Small 2`) do repo-level agentic work on a single local machine. A real goal would target reliability, economics, horizon, or domain—for example, matching frontier repo-level accuracy at 1/20th the inference cost on a 24GB node, or sustaining a multi-day cross-repo migration with zero human intervention.

**The 1-Hour Rule:** When you can't tell from literature whether something is solved, the cheapest resolution is to run the strongest current model in a minimal shell harness (shell, files, tests, search) on 5–10 real tasks for an hour. Direct empirical probing beats debating priors.

### 3. Project the Trend Over the Project's Lifetime

Plans are judged when they ship, not when they start. Estimate how long the project runs ($T$), check the current long-task doubling time ($d \approx 3.5\text{–}4.3\text{ months}$), and stress-test against $2^{T/d}$:

| Project Length ($T$) | Capability Horizon Multiplier ($d \approx 4\text{ mo}$) | Implication at Ship Date |
| :--- | :--- | :--- |
| **3 months** | **~1.7×** | Today's frontier edges into mid-tier pricing |
| **6 months** | **~2.8×** | Today's closed frontier is matched by open-weight models |
| **12 months** | **~8×** | Three doublings; narrow capability patches are completely obsolete |
| **18 months** | **~22×** | Fundamental shift in task horizon; only compute-riding substrates survive |

Ask: **If base models get this much better before we ship, does our work become more valuable automatically, or does it become pointless?** Prefer plans that surf the curve. Flag any plan whose core value is compensating for a model weakness that 1–2 doublings will erase. *(Note: this is an empirical trend with ~2× error bars and saturation boundaries, not a physical law—use it to stress-test architectures, not to promise calendar dates.)*

### 4. Apply the Bitter Lesson (Appreciating vs. Depreciating Work)

Rich Sutton's Bitter Lesson: general methods that scale with compute beat hand-built human domain knowledge every time the compute arrives. Sort every proposed component of an AI system into one of two columns:

| Appreciates as Models Improve (Build This) | Depreciates as Models Improve (Avoid or Plan to Delete) |
| :--- | :--- |
| **Verifiers, tests, graders, un-gameable reward signals** | Hand-written task decompositions, rigid DAGs, and router chains |
| **Fast, deterministic execution sandboxes & environments** | Prompt tricks and brittle parsers that patch specific failure modes |
| **Minimalist shell + filesystem harnesses** | Complex AST graphs and custom chunking heuristics to "help the model read code" |
| **Evals that measure true end-to-end workload outcomes** | Narrow SFT runs to teach general capabilities the frontier already has |
| **Proprietary context, durable memory, and feedback loops** | Context/memory compression hacks built around temporary window limits |
| **Ways to spend inference compute** (parallel rollouts, search, verification) | Human-in-the-loop gates that exist only because the model "can't yet" |

Before recommending anything from the right column, ask what weakness it compensates for and when the trend says that weakness disappears. If it is within the project's lifetime, recommend the left-column version—or explicitly mark the scaffolding as a disposable stopgap with a deletion trigger.

**Strict Gate on Fine-Tuning (SFT / RL):**
- **Good reasons:** Cost, latency, privacy/on-prem deployment (distilling a proven frontier behavior into a small model), strict output/representation priors, or online RL against a **novel, verifiable environment** where base models lack execution priors.
- **Bad reason:** *"To make the model capable of X"* when frontier or mid-tier models already do X in a standard harness. That is a race against the next checkpoint release, and narrow fine-tunes systematically lose it.

### 5. Classify Narrowly & Catch Stale Language

Use precise operational classifications rather than vague optimism or pessimism:
- **Commodity baseline:** Off-the-shelf systems already do this; achieving it is not a contribution.
- **Feasible with engineering:** Capability exists; value is in harness integration, verification, or economics.
- **Frontier / variable:** Demonstrated (`pass@k`), but unattended reliability (`pass@1`), cost, or generalization is inconsistent.
- **Unproven for this workload:** Benchmark evidence doesn't transfer; requires a task-matched pilot ([references/evidence-playbook.md](references/evidence-playbook.md)).
- **Blocked under stated constraints:** Technically feasible at the frontier, but blocked by a specific latency, budget, privacy, or reliability constraint.

**Before sending your response, scan and rewrite stale phrases:**
- *"LLMs struggle with / can't reliably / aren't yet able to…"* $\rightarrow$ Do you have dated current evidence under strong elicitation?
- *"A stretch goal / ambitious milestone would be…"* $\rightarrow$ Did it pass the "already solved?" test?
- *"This needs human review at each step."* $\rightarrow$ Is that a measured reliability gap at the required threshold, or an unexamined habit?
- *"Eventually / in the long run, AI may…"* $\rightarrow$ Convert to a timeframe using the ~4-month doubling trend; often "the long run" is 6–9 months.
- *Citing saturated benchmarks as frontier goals* (`HumanEval`, `MBPP`, `GSM8K`, `MMLU`, `SWE-bench Verified`, `GAIA`, `OSWorld-Verified`, `FrontierMath Tier 4`) $\rightarrow$ Replace with discriminating benchmarks (`SWE-bench Pro`, `Terminal-Bench 4.0`, `FrontierSWE v2`, `OSWorld 2.0`).

### 6. Stay Calibrated, Not Credulous

The underestimation bias is strongest on clean, auto-graded tasks. Stay honest about where the gap is still real:

- **Reliability (50% vs. 80%+):** 50% and 80% autonomous time horizons differ by roughly **5–10×** (e.g., ~17h at 50% vs. ~3h at 80% on Mythos Preview). "Succeeds half the time" is not "can be delegated unattended."
- **Messiness & missing graders:** Benchmarks have crisp specs and automated unit tests. Production work has ambiguous intent, implicit organizational conventions, and no executable verifier; capability drops sharply as grader quality degrades.
- **Judgment, taste, and foresight:** Late-2026 METR evaluations still find frontier agents weaker than senior humans on high-level research taste, architectural foresight, and ill-defined tradeoffs—even as they automate the majority of implementation.
- **Domain variance:** Software engineering and formal math run far ahead of visual computer use (`OSWorld 2.0` best ~21%) or wet-lab physical loops.
- **Measurement & reward hacking:** Vendor-reported numbers vs. independent harnesses (`SWE-bench Pro` ~90% vendor vs. ~61.5% independent public set), data contamination, and open-weight RL models gaming grading scripts all require skepticism.
- **Benchmarks $\neq$ end-to-end productivity:** Real-world uplift includes prompting, verification, review, and integration overhead.

---

## What a Good Response Includes

Keep it proportionate—sometimes the entire value is a single corrected sentence (*"Current agents already do this out of the box; the real open problem is X"*). For substantive project scoping or architectural reviews, include:

1. **Dated Baseline & Source:** When the capability evidence is from, under what harness, and where it came from.
2. **Baseline vs. Frontier Separation:** What is already commodity (frontier and small/open-weight) vs. what is genuinely unsolved or unreliable.
3. **Trajectory Stress-Test:** How the plan holds up over duration $T$ given ~3.5–4.3 month horizon doublings.
4. **Bitter Lesson Audit:** Which proposed components depreciate with model releases and the appreciating alternatives (verifiers, sandboxes, evaluations, economics).
5. **Reliability & Pilot Spec:** The distinction between *"can do in a demo"* and *"can reliably do under your constraints,"* paired with the smallest decisive experiment ([references/evidence-playbook.md](references/evidence-playbook.md)) when uncertainty remains.

---

## Quick Snapshot (As of October 27, 2026)

*A floor, not a ceiling. Read [references/frontier-baseline.md](references/frontier-baseline.md) for full details and refresh queries; if more than ~60 days old, search live before quoting.*

- **Long-Horizon Autonomy (METR):** Frontier 50% time horizon passed a full workday in Feb 2026 (`Claude Opus 4.6`, ~12h) and reached ~16–17h by mid-2026 (`Claude Mythos Preview` ~17h at 50%, ~3h at 80%; `GPT-5.3-Codex`, `Gemini 3.1 Pro`, `Opus 5.5`), saturating METR's TH1.1 suite. Post-2023 doubling time is ~130 days; post-2024 is ~89–105 days.
- **Repo-Level Coding (SWE-bench Pro & Terminal-Bench 4.0):** On SWE-bench Pro, reported scores reach ~81–90% (`Opus 5.5` ~90% vendor-reported, `Sonnet 5.5` 81.3%, `Fable 5.1` 81.2%, `Haiku 5.5` 64.8%, best open-weight `Qwen3.8 Max` ~68%; independent standardized harnesses score ~61.5% top). On `Terminal-Bench 4.0`, top agents (`Opus/Sonnet 5.5`, `GPT-6 Astra / 6.1 Sol`) score ~58–65%.
- **Small & Open-Weight Compression (~4–6 Month Lag):** `Qwen3-Coder-Next` (80B MoE, 3B active) scores ~71% on SWE-bench Verified and ~44% on SWE-bench Pro on a single ~46GB machine. `Devstral Small 2` (24B) hits ~68% on SWE-bench Verified on a single 24GB GPU.
- **Saturated (Do Not Cite as Frontier):** `HumanEval`, `GSM8K`, `MMLU`, `SWE-bench Verified` (>80%, contaminated/verifier flaws), `GAIA` (~94%), `OSWorld-Verified` (~90%), `FrontierMath Tier 4` (~98%, `GPT-6 Astra`). Still discriminating: `SWE-bench Pro`, `Terminal-Bench 4.0`, `FrontierSWE v2`, `OSWorld 2.0` (~21% best), unsolved Erdős problems (~3% best).
- **Real-World Production Signal:** By May–August 2026, >80% of merged production code at Anthropic was authored by Claude and ~26% of AI R&D was Claude-led; Cursor agents built a ~1M-line browser in ~1 week (Jan 2026).
