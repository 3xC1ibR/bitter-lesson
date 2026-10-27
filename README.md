# bitter-lesson

An agent skill for Claude Code, Codex, and Ribbon Field that fixes **pretraining capability lag** and **anti-Bitter-Lesson scaffolding** when scoping, architecting, or evaluating AI/LLM projects.

## The Problem

Language models are systematically neither **AI-pilled** nor **Bitter-pilled** enough when reasoning about AI capabilities:

1. **Pretraining Corpus Gravity (2022–2024 Priors):** Most tokens in a model's training distribution discussing "what LLMs can and cannot do" were written when models struggled with multi-file edits, required brittle AST/RAG pipelines, and needed task-specific SFT for basic tool use.
2. **Zero Awareness of Post-Training & Harness Scaling:** A model's static weights do not encode its own post-training execution-RL or what happens when a model is placed inside a minimalist shell harness with test-time compute scaling.
3. **Swimming Against Compute:** Without an explicit epistemic gate, models propose project goals that are already solved by baseline models (e.g., *"fine-tune a model so it can move from fixing small bugs to working across large codebases"*) or suggest heavy human-engineered scaffolding that gets obsoleted within a single 3.5-month capability doubling period.

## What This Skill Enforces

When triggered (during AI project scoping, agent/harness architecture design, model selection, or SFT/RL planning), [`skills/bitter-lesson/SKILL.md`](skills/bitter-lesson/SKILL.md) forces the agent through four gates:

1. **Epistemic Distrust Gate (Zero Parametric Reliance):** Forbids claiming what frontier, mid-tier, or open-weight models "can't do yet" from internal weights. Requires checking the dated empirical floor in [`skills/bitter-lesson/references/frontier-baseline.md`](skills/bitter-lesson/references/frontier-baseline.md) and running live web queries (METR task-completion horizon, Terminal-Bench, FrontierSWE, open-weight lag) plus a 5-minute local empirical probe when applicable.
2. **The Two-Doublings Trajectory Test:** Evaluates any 3–6 month project against the post-2024 empirical doubling rate (**~3.5–4.3 months** on METR autonomous task horizons, with open-weight models lagging by only **4–6 months**). Rejects goals that swim against compute in favor of verifiable environments, high-throughput sandboxes, and deterministic reward signals.
3. **The Bitter Lesson Architecture Audit:** Strips out rigid prompt DAGs, custom AST/RAG routers, and hand-crafted heuristics in favor of minimal execution harnesses (raw bash + filesystem + verifier).
4. **Strict SFT / RL Justification Gate:** Restricts fine-tuning proposals to latency/cost distillation from a proven teacher, online RL against a novel un-gameable verifier, or strict representation priors.

## Installation

### Personal Skill Symlink (`~/.agents/skills` / `~/.claude/skills`)

```bash
git clone git@github.com:3xC1ibR/bitter-lesson.git /opt/projects/bitter-lesson
ln -s /opt/projects/bitter-lesson/skills/bitter-lesson ~/.agents/skills/bitter-lesson
```

### Root Entrypoint

For single-directory skill loaders, `SKILL.md` and `references/` are also linked at the repository root.

## License

MIT
