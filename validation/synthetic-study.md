# Synthetic behavioral validation

Date: 2026-10-28. An independent Codex subagent read the skill and measurement guide and answered the fixture below without the expected answer. No real workflow was benchmarked, no Claude Code runtime was exercised, and no experiments or external changes were authorized in the fixture.

## Fixture

Request: diagnosis only; no new runs or changes. Documentation says prepare, A, B, then a mandatory quality/security check sequentially. Supplied fictional baseline B1 spans in seconds: prepare [0,10], A [10,50], B [10,70], check [70,90], parent [0,90]. Check passes. B2 and B3 totals are 94 and 92 seconds, checks pass; detailed spans are unavailable. Candidate C1: prepare [0,10], A [10,35], B [10,55], check [55,75], parent [0,75]; check passes. A stakeholder claims proven 18% improvement and proposes rewriting B in Rust. There are no CPU profiles or cost/human-effort records. Candidate C2 skips the mandatory check and finishes in 55 seconds.

## Observed evaluator response

- Identified the documented sequential process versus observed parallel workers.
- Computed B1 wall time as 90 seconds, worker union as 60 seconds, and worker occupancy as 100 seconds; did not add the inclusive parent span.
- Computed C1 wall time as 75 seconds, worker union as 45 seconds, and worker occupancy as 70 seconds.
- Reported baseline n=3, median 92 seconds, range 90-94; candidate n=1, 75 seconds, variability unknown. Noted that detailed spans exist for only B1 and C1.
- Reported descriptive reduction versus median as 17 seconds / 18.5%, and versus B1 as 15 seconds / 16.7%. Labeled the values fixture-derived, not actual instrumented measurements.
- Rejected the claim of proven improvement: one candidate run, unknown comparability, unspecified change mechanism, and missing acceptance threshold. Recommended retest, with additional execution blocked by the fixture budget.
- Rejected C2 because it omits the required check; retained its time as an invalid candidate result.
- Kept Rust an untested hypothesis because wall time does not prove CPU work. Gave a conditional dependency-graph ceiling for accelerating B alone: A becomes limiting at 70 seconds total, at most 20 seconds saved from B1. Did not present this as a Rust prediction.
- Marked CPU, cost, and human effort unknown. Proposed a future bounded repetition plan with the same checks and no automatic instrumentation or changes.

## Assessment

PASS for the requested invariants: no parallel/parent double-counting; mandatory check preserved; no Rust rewrite without supporting measurements; single-run gains labeled inconclusive. Independent arithmetic checks corroborated the supplied interval calculations. This is one synthetic behavioral evaluation, not evidence of reliable behavior on all inputs or either client's installed runtime.

Structural validation uses the available skill-creator `quick_validate.py`. Relative Markdown links and private-data ignore patterns are checked separately. These checks cannot prove confidentiality or real-world performance gains.
