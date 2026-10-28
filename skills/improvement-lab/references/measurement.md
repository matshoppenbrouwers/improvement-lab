# Measurement guidance

## Capture only what is available

Prefer existing application logs, timestamps, CI records, runtime timing commands, billing records, and manual effort diaries. Check consent, coverage, timestamp semantics, and clock consistency first. Use monotonic clocks for durations when available. For cross-host events, record clock offsets/uncertainty; do not infer precise ordering from unsynchronized clocks. Never substitute transcript length or token count for elapsed time.

For each event record a sanitized run ID, span ID, parent ID, actor/resource, dependency IDs, start/end, units, source, and uncertainty. Missing starts, ends, or categories stay unknown. Record instrumentation overhead and dropped events. Separate time actually observed from time inferred from logs.

| Metric | Meaning and accounting |
| --- | --- |
| Wall-clock elapsed | End minus start for the declared boundary, including queues and required checks. |
| Human effort | Active person-time: union overlapping intervals per person, then sum across people. Approval queue time is not active effort. |
| CPU time | User/system CPU consumed, separately from elapsed time. Parallel CPU seconds can exceed wall seconds. |
| Model/tool waits | Explicitly sourced intervals waiting on model or tool completion; distinguish worker occupancy from caller wait and CPU execution. |
| Retries | Attempts, failures, causes, and time/cost including abandoned runs; report completion rate and success-conditioned timing separately. |
| Cost | Currency, pricing date, tokens/compute/fees and source. Label rate-based estimates; subscriptions are not known per-run charges. |
| Quality | Fixed checks, expected outputs, reviewer rubric, failure counts and security invariants per run. Unknown or omitted checks are not passes. |

## Parallel and nested work

Use the union of intervals to measure time covered by a category; retain overlap across categories explicitly. For an additive wall-time breakdown, partition the timeline into disjoint states (including overlap/mixed and unattributed time) with a declared attribution rule. Do not add independently computed category totals as if they were exclusive.

Keep inclusive parent spans for latency; use exclusive parent work plus children for additive resource accounting. If a parent cost/token total already includes child usage, choose that total or deduplicated children plus exclusive parent usage, never both.

Example: preparation [0,10], workers A [10,50] and B [10,70], required check [70,90]. Elapsed time is 90 seconds. Worker occupancy totals 100 seconds, but their union is 60 seconds. With the stated dependencies, the completion path is preparation -> B -> check. Shortening A alone does not shorten this run; shortening B can move the bottleneck to A. Parent [0,90] is not another 90 seconds of work to add.

## Comparability and uncertainty

Freeze input identity, revision, tool/model version and settings, hardware, concurrency, external service conditions, cache state, and checks. Record changes and confounders. Separate cold and warm cache comparisons; include cache creation and invalidation costs over the relevant workload. Do not mix setup-excluded candidate results with setup-included baselines.

Choose a bounded repetition plan before running. Three or more paired runs can be an exploratory starting point, not proof or a universal sample-size rule. Noisy systems require more observations; if the budget cannot support them, report inconclusive. Include every attempted run and explain any exclusions decided in advance. Alternate or randomize baseline/candidate order where feasible; separate warmups according to a fixed rule. Avoid rerunning only failures until a favorable sample appears.

Report n, median, min/max and preferably IQR for each metric; show paired deltas when inputs are paired. Use confidence intervals only with a stated defensible method and enough data. A single sample cannot estimate run-to-run variability. Avoid presenting tiny-sample percentiles or numerical precision as confidence.

For lower-is-better metrics, signed change = candidate - baseline; reduction = baseline - candidate; reduction percent = 100 * (baseline - candidate) / baseline. State the sign convention. If baseline is zero, percentage is undefined; report the absolute difference. If either value is missing, do not calculate it. For higher-is-better metrics, state the direction explicitly. Report quality separately; do not combine seconds, dollars, and quality scores without an agreed utility model.

For a measured serial fraction f sped up by factor s, the ideal elapsed-time speedup ceiling is 1 / ((1-f) + f/s), before new overhead. State the assumptions; this formula is not evidence that the change will achieve s, and parallel dependency graphs need their own path analysis.

## Optional references, not dependencies

These are starting points to inspect when relevant. Verify the installed version and coverage before using their output. Do not install or enable integrations automatically.

- [Anthropic process-optimization](https://github.com/anthropics/knowledge-work-plugins/blob/main/operations/skills/process-optimization/SKILL.md): process mapping and waste analysis; does not collect timings automatically.
- [agent-profiler](https://github.com/YeonwooSung/my-claude-code-mods/blob/main/agent-profiler/README.md): Claude Code event-based measurements and optional trace export. README reviewed 2026-10-28 lists Claude Code 2.1.287+ (desktop 2.1.286), but reports probes on a different version; verify locally. It cannot split model-server time, misses Bash-based file modifications in repeated-read detection, and can drop older in-memory turns. Async children can outlive parent tool calls. Trace exports can expose paths and text; redaction is not a privacy guarantee. Verify coverage and export destination before use.
- [time-blame](https://github.com/karanb192/time-blame): quick Claude/tool/approval diagnosis. README reviewed 2026-10-28 lists 2.1.302+; totals reset on clear/resume/reload and are not retained after the session. Successful retries are not separately observable, and managed installs can attribute approvals to tools. Verify installed behavior before relying on a baseline.
- [auto-optimize](https://github.com/bluuewhale/auto-optimize): code performance experiment loop. Its automation scope does not grant this skill permission to change infrastructure or run unbounded experiments.
- [Codex Goals](https://developers.openai.com/cookbook/examples/codex/using_goals_in_codex): measurable objectives, evidence, constraints, and stopping conditions. Goals are optional; create one only when requested and supported.
