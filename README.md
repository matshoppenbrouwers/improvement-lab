# Improvement Lab

A reusable lean time-and-motion study skill for software, agent workflows, and operational processes. It maps actual work, measures time/effort/cost and quality, ranks bottlenecks, and evaluates bounded improvements. Session-flow is an example, not a dependency.

## Install

Clone this private repository with an authorized GitHub account:

```sh
git clone https://github.com/matshoppenbrouwers/improvement-lab.git
```

Copy the entire `skills/improvement-lab` folder (including `references` and `assets`) into ONE appropriate location per tool. Do not overwrite an existing installation without reviewing it.

| Tool | Personal installation | Project installation | Explicit invocation |
| --- | --- | --- | --- |
| Claude Code | `~/.claude/skills/improvement-lab/` | `.claude/skills/improvement-lab/` | `/improvement-lab` |
| Codex | `~/.agents/skills/improvement-lab/` | `.agents/skills/improvement-lab/` | `$improvement-lab` |

On Windows, `~` is your user profile. Reload skills or restart the client if the skill does not appear. Installation locations follow the [Claude Code](https://code.claude.com/docs/en/skills) and [Codex](https://developers.openai.com/codex/skills) documentation; managed clients may restrict local skills. Nothing is installed automatically by this repository.

## Use

Invoke the skill with a process boundary and available evidence, for example:

> Diagnose our issue-to-reviewed-patch workflow. Use the supplied sanitized run records. Preserve tests and security review. Budget: 30 minutes of analysis; no implementation or new instrumentation. Identify unknowns and propose bounded experiments.

For implementation, state which reversible experiments are authorized, the runtime/cost budget, and required checks. Diagnosis is the default. The result recommends **adopt, retest, reject, or blocked**, with evidence and uncertainty.

- [Skill instructions](skills/improvement-lab/SKILL.md)
- [Measurement guidance](skills/improvement-lab/references/measurement.md)
- [Reusable study-record template](skills/improvement-lab/assets/study-record.md)
- [Synthetic validation](validation/synthetic-study.md)

## Limitations and privacy

This is an instruction-only skill, not a profiling platform. It cannot recover missing timings, establish causality from a single run, or guarantee agent compliance. It does not install profilers, export telemetry, change permissions, or deploy. Rust is considered only when measurement supports it.

Keep completed studies outside the repository by default. The included `.gitignore` excludes `private-studies/`, `study-data/`, `raw-traces/`, `traces/`, `telemetry/`, `private/`, `*.jsonl`, `*.log`, credentials and common profiler output. If using the skill in another project, these rules do not travel with it: choose private storage or add and verify equivalent ignore rules there. Never commit raw prompts, credentials, company information or sensitive traces. Ignore rules do not protect already tracked or force-added files; inspect staged diffs.

Recreated from the supplied brief; no previous draft was imported. Validation is synthetic and structural, not a real workflow benchmark or a Claude Code runtime test. References are optional and are linked in the measurement guide; no third-party implementation is bundled.
