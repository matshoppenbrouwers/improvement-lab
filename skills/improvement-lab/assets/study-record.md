# Study record

Copy this blank template to an approved private location. Fill fields or mark unknown/not applicable; never turn missing data into zero. Do not commit completed private studies or raw evidence.

## Scope and authorization

- Study ID / date / owner:
- Process and intended outcome:
- Trigger / exact start event / exact end event / exclusions:
- Representative inputs and private evidence IDs:
- Mode: diagnosis or authorized experiments; scope of existing authorization:
- Acceptance checks, security invariants, quality rubric and improvement threshold:
- Budget: runs / wall time / human effort / money; stopping conditions:
- Private evidence storage, access, retention and sanitization plan:

## Process evidence

| Step / dependency / actor | Documented behavior and source | Observed behavior and source | Missing evidence / assumptions |
| --- | --- | --- | --- |
| | | | |

## Baseline and measurement protocol

- Baseline revision/snapshot and rollback reference:
- Input IDs, environment, tool/model versions/settings, concurrency:
- Instruments, timestamp semantics, clock uncertainty and coverage:
- Parallel/nested attribution rule and cost deduplication:
- Repetitions, order, warmups, cache state and exclusions fixed in advance:

| Run / variant / input ID | Wall seconds | Human person-seconds | CPU seconds | Model/tool wait coverage and overlap | Retries / status | Cost / currency / measured or estimated | Quality checks / evidence ID |
| --- | --- | --- | --- | --- | --- | --- | --- |
| | | | | | | | |

## Bottlenecks and experiment plan

| Rank / bottleneck | Evidence / completion-path contribution | Proposed change and mechanism | Estimated benefit and assumptions | Risk / implementation cost |
| --- | --- | --- | --- | --- |
| | | | | |

- Candidate ID/revision, single hypothesis, authorization:
- Comparable input and check set; confounders:
- Reversible change, rollback and stop triggers:
- Rust proposal if relevant: measured CPU share, ceiling, integration/maintenance costs:

## Results and decision

| Metric / units / direction | Baseline n / median / range / IQR | Candidate n / median / range / IQR | Absolute change | Percentage change | Evidence label / source / uncertainty |
| --- | --- | --- | --- | --- | --- |
| | | | | | |

- Paired deltas, all failures/retries, excluded runs and reasons:
- Quality/security results and missing checks:
- Trade-offs, instrumentation overhead and threats to comparability:
- Observed / measured / estimated / inconclusive / rejected claims:
- Decision: adopt / retest / reject / blocked, with rationale:
- Next bounded action, owner, required evidence or authorization:
