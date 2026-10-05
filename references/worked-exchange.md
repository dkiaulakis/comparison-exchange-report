# Synthetic worked exchange: retries after an unknown outcome

This fictional package is a worked interface, not an installed product command or a description of a private system. Its records, roles and identifiers are synthetic. It needs no sender service, credentials or network.

## Before and comparison

Donor supplied revision D1 proposes an operation identifier for safe retries but gives no evidence of payload conflict checks. Receiver R0 already validates syntax; its retry design assigns a new identifier on every attempt. Donor runtime quality is UNKNOWN. Receiver behavior below is a synthetic reproduction, not a production measurement.

| Idea | Donor advantage / limit | Receiver before → current | Adoption / reason | Proof to obtain / limit | Reciprocal offer |
| --- | --- | --- | --- | --- | --- |
| Stable identifier for one intent | Makes retries comparable / differing payload under same identifier unspecified | New identifier on retry → reuse identifier for same intent | Adapt stable identity, retain existing syntax validation | Execute normal, duplicate and conflict cases below offline; integration remains unverified | Offer payload-binding rejection as a proposal to D1 |
| Input validation | Not described in supplied D1 / private capability unknown | Already satisfied → retained | Decline copying; equivalent outcome exists | Invalid synthetic input rejected before an effect; not an absence claim about donor | Offer portable required-field documentation |

## Architecture and terms

Requester → input validation → operation record → synthetic effect → outcome record → requester.

“Operation record” means a durable association of **one identifier + one exact payload + its known outcome**. A request is untrusted input. Receiver authority decides whether effects are allowed. A receipt records evidence of an outcome; it does not grant permission.

The illustrative effect appends one synthetic message to an in-memory outbox (a list), with no actual recipient or send. The receiver's eventual real persistence/effect boundary is intentionally unspecified and needs its own integration decision.

## Self-contained logical contract, version 1

`apply_intent(request, state) -> result` is an illustrative interface name, not an installed CLI, SDK or endpoint. State is a caller-owned object with exactly two fields: `operations` (object mapping intent identifiers to `{ "message": string, "outcome": "completed" | "uncertain" }`) and `outbox` (array of `{ "intent_id": string, "message": string }`). It starts as `{ "operations": {}, "outbox": [] }`. Authorization is a caller precondition outside this retry interface: call it only after the receiver separately authorizes the synthetic operation; an unauthorized request must not reach it. This interface neither grants consent nor models the receiver's authorization API. This example assumes well-formed state and sequential calls; `apply_intent` updates that state in place and returns a separate result. Requests are JSON objects; unknown fields are rejected in this example. A blank string is empty or whitespace-only; accepted strings retain their exact bytes.

| Field | Type / semantics |
| --- | --- |
| request.intent_id | Required nonempty string, stable across retries of the same intent |
| request.message | Required nonempty string, exact payload; this example uses literal equality, no normalization |
| result.status | One of `applied`, `replayed`, `rejected`, `unknown` |
| result.code | `ok`, `invalid_input`, `payload_conflict`, `outcome_unknown` |
| result.effect_count | Nonnegative integer: observable total synthetic outbox length |
| result.retry | `none` or `inspect_outcome`; never “new identifier” for an unknown existing effect |

Rules/oracle (derive expected outputs from these rules, not from an implementation): apply the first matching rule in the numbered order below. Payload conflicts reject before outcome inspection; an uncertain outcome does not permit changing the bound payload. Every result includes the current outbox length as effect_count.

1. Invalid object/type/fields/blank string: return `rejected/invalid_input`, retry `none`, append nothing.
2. Known identifier with a different exact message: return `rejected/payload_conflict`, retry `none`, append nothing (even if the stored outcome is uncertain).
3. Known identifier with same message and completed outcome: return `replayed/ok`, retry `none`, append nothing.
4. Known identifier with same message whose outcome is uncertain: return `unknown/outcome_unknown`, retry `inspect_outcome`, append nothing; request outcome inspection, not another effect.
5. New valid intent: associate identifier with exact message, append once to the synthetic outbox, record completion, return `applied/ok`, retry `none`.

These rules define the complete permitted `(status, code, retry)` triples: `(applied, ok, none)`, `(replayed, ok, none)`, `(rejected, invalid_input, none)`, `(rejected, payload_conflict, none)` and `(unknown, outcome_unknown, inspect_outcome)`. Any other combination violates this illustrative contract.

For offline execution a receiving agent can implement this logical interface using its own standard library in a temporary directory. It must state that it implemented the example rather than discovered an installed product command. Inspect any generated code before running it; keep it offline and synthetic. Preserve actual outputs and any implementation mistakes. No helper supplied by this skill is required.

## Control, counterexample, repair and valid exception

Use a fresh state for each independently labelled scenario. Within a scenario retain state between steps.

| Scenario | Input sequence / precondition | Sender-specified expected result, defined before implementation |
| --- | --- | --- |
| Control | `{ "intent_id": "sample-1", "message": "hello" }` | `applied/ok`, effect_count 1, retry none |
| R0 counterexample | Same logical message retried as `sample-2` after `sample-1` applied | Step 1: `applied/ok`, effect_count 1, retry none; step 2: `applied/ok`, effect_count 2, retry none. Identifier alone cannot detect that two identifiers mean the same intent |
| Repair | Reuse `sample-1` with exact `hello` after first success | `replayed/ok`, effect_count remains 1, retry none |
| Payload conflict | Reuse `sample-1` with `different` | `rejected/payload_conflict`, effect_count remains 1, retry none |
| Outcome uncertain | State: `{ "operations": { "sample-1": { "message": "hello", "outcome": "uncertain" } }, "outbox": [{ "intent_id": "sample-1", "message": "hello" }] }`; request: `{ "intent_id": "sample-1", "message": "hello" }` | `unknown/outcome_unknown`, effect_count remains 1, retry inspect_outcome |
| Conflict with uncertain outcome | Use the preceding uncertain state with request `{ "intent_id": "sample-1", "message": "different" }` | `rejected/payload_conflict`, effect_count 1, retry none; first-match rule 2 precedes rule 4 |
| Invalid | Blank intent_id with message hello, empty state | `rejected/invalid_input`, effect_count 0, retry none |
| Valid exception | A pure computation with no durable/external effect, such as summing two numbers | Repeating the computation causes no duplicate side effect; this operation record can be unnecessary overhead. No operation record or `apply_intent` result contract applies to this separate pure computation |

Counterexample is intentionally not cured by the repaired identifier contract: the requester must preserve intent identity. State loss and concurrent workers also need separate persistence/atomicity design. This in-memory example provides neither crash durability nor atomic protection across processes. A recipient who calls it production-safe has misunderstood its limits.

## Adoption, failure and recovery

1. Identify a real duplicate-effect risk and check the receiver's existing equivalent behavior; decline duplication where already satisfied.
2. Map requester, validator, operation storage and effect/outcome roles to receiver equivalents under its authority. Decide payload representation, retention, identity ownership and concurrent/crash behavior; do not copy sender-specific storage.
3. Execute the synthetic oracle scenarios offline; preserve before/after output. Reject conflicting identity; keep same-intent retries stable.
4. For real unknown outcomes, stop repeat effects until outcome is inspected through an authorized observable interface. Compensation is a new authorized operation, not deletion of history. If outcome cannot be known, retain UNKNOWN and escalate through the receiver's operational procedure.
5. Integrate in an isolated authorized environment, establish runtime verification/rollback and prove installed/enabled/executed states separately. Never infer exactly-once production behavior from this example.
6. Return proven increments and unresolved concurrency/durability questions to the bilateral matrix; offer the payload-binding contract back as a proposal unless donor implementation and delivery are separately proven.
