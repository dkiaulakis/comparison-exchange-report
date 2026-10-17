# Portable comparison records

These are illustrative logical schemas, not an installed service or validator. Use text tables if automation adds no value. Public records explain observations without sender-only paths; retain detailed private evidence separately.

## Corpus

Record each supplied item's safe `source_ref`, `revision`, `kind`, exact-byte `sha256` (64 hexadecimal characters or null when unavailable), `read_extent` (complete, partial, inaccessible), and `duplicate_of` (safe reference or null). Record unread/partial limits. Equal names do not imply equal content. Track file copies, distinct hashes, names and selected/read revisions with separate denominators. Describe hash scope and collector; original-byte hashes need not match redacted narrative text.

## Decision

Corpus coverage counts each unique body/revision once. A decision record below addresses one revision-and-idea pair; several idea decisions may reference the same source revision without increasing its inventory count. A body-level summary does not replace conflicting idea-level decisions.

```json
{
  "capability": "Stable identity for retries",
  "idea_ref": "stable-retry-identity",
  "source_ref": "synthetic-D1",
  "source_sha256": null,
  "source_hash_limit": "Synthetic narrative, not a supplied file",
  "source_state": "supplied-claim",
  "receiver_before": "New identifier on retry",
  "receiver_current": "Existing syntax validation",
  "decision": "adapt",
  "why": "Repeated effects need stable intent identity",
  "adoption_status": "proposal",
  "adaptation": "Reuse an identifier for the same intent; reject changed payload",
  "proof": "Offline scenarios specified in worked-exchange.md; execution not asserted",
  "limits": "Crash durability and concurrency unproven",
  "reciprocal": {
    "kind": "recommendation",
    "what": "Document payload-conflict rejection",
    "why": "D1 leaves this contract unspecified",
    "status": "proposal"
  },
  "smallest_check": "Same identifier and payload causes one synthetic effect",
  "valid_exception": "Pure computation with no durable effect"
}
```

Decision: `reuse`, `adapt`, `decline`, `defer`. `source_state`, `adoption_status` and `reciprocal.status` use exactly the nine evidence labels in [report-pattern.md](report-pattern.md): `supplied-claim`, `absent-in-material`, `verified-current-capability`, `implemented/source-only`, `installed`, `enabled`, `executed-output-quality`, `proposal`, `unknown`. The slash in `implemented/source-only` is part of one label. Use separate observations for coexisting states. Decision, evidence-state, reciprocal-kind and verdict fields are closed vocabularies; descriptive fields are free text and references must resolve. Selecting an idea is not installation. Unknown hashes stay null with a reason; compute actual complete-file hashes rather than copying placeholders. Reciprocal kind: `recommendation`, `documented-capability`, `none`. A recommendation remains a proposal. If a reverse cell says `none`, explain why; this does not invalidate a useful take-only decision.

## Adoption continuation

For a resumed implementation, retain one compact row per originally selected outcome. This is a continuation view of the existing decisions, not another task system or a requirement to implement every supplied idea. Recover the original selection from its records; distinguish the supplied corpus, selected outcomes and supporting work. Do not invent a denominator when selection records are unavailable.

| Outcome / source idea | Original acceptance and owner | Current observation / stage | Necessary prerequisite and why it blocks | Next authorized action / remaining proof |
| --- | --- | --- | --- | --- |
| Synthetic O1 / stable-retry-identity | Same authorized request has one effect; changed payload refuses; receiver integration owner | Guard committed; ordinary caller still uses old version | Normal release must load the changed guard; current caller probe identifies the old revision | Use the existing release path, then observe repeat and conflict through the caller |
| Synthetic O2 / input validation | Blank input refuses through the public function; library owner | Already-present behavior verified with the scoped positive/refusal results | None; this pure computation needs no service | Reuse the existing implementation; do not invent a deployment prerequisite |

An infrastructure repair may be necessary and complete within its own scope while O1 remains unfinished. Reference one shared prerequisite from several affected outcomes without multiplying the adopted-outcome count or test counts. A blocker names its actual governing phase, owner, observation and clearing evidence; retain unavailable evidence as unknown. On each resume, remeasure changed source/runtime and authority, reuse still-valid scoped receipts and preserve failures rather than restarting finished work. Report selected outcomes satisfied over the recovered selected denominator separately from prerequisite progress; reuse may satisfy an outcome without new code when its criteria are proved.

This record adds no permission: compare-only work records proposals without implementing them, and a no-send request keeps reports and reciprocal recommendations local. Public exports use safe logical roles and descriptions, not this host's private task identifiers, paths or raw receipts.

## Later review

```json
{
  "reviewer": "independent-reviewer-A",
  "checked_at": "2026-10-05T00:00:00Z",
  "source_ref": "synthetic-D1",
  "source_sha256": null,
  "idea_ref": "stable-retry-identity",
  "verdict": "disagree",
  "basis": "Explain the observed disagreement without replacing the original decision"
}
```

Dates and identities above are synthetic placeholders, not proof. Append only material actually read. Verdict: `agree`, `disagree`, `not-assessed`. A decision verdict resolves `source_ref` + `idea_ref` to one historical decision; include its revision identifier if the pair has multiple versions. A review with `idea_ref: null` is a revision-level observation, not agreement/disagreement with every source decision. Distinguish attempts; never impersonate reviewers. Retain previous decisions, reviews and chronology. Define reviewer labels and whether verdicts affirm or contest the historical decision. A disagreement does not supply its replacement direction; record that direction only when known and safe, otherwise mark it withheld/unknown rather than prompting adoption. Count overlapping reviewer populations separately.

## Local checks

- Every available unique body/revision has a decision; unread material is explicit.
- Known hashes match read bytes; reviews refer to inventoried revisions; each non-null review `idea_ref` resolves to a decision for that source and identified historical revision.
- Evidence states have dated observations of that particular state.
- Previous records remain intact and disagreements are appended.
- Every public field, filename, comment, link and attachment fits the disclosure scope.

Run checks with available receiver tools and record dated observed results, assessor, tested scope and named failed/unknown items; state the number passed and denominator. Reading this schema passes none of them.

## Private ledger versus recipient projection

The canonical private ledger may contain exact mappings and rationale. Its recipient projection must select safe fields; a validator for the private schema does not require publishing those private fields. Omit unsafe rationale/configuration entirely when generalization would still expose it. State omissions and whether the output is a method comparison, classification index or partial view. Keep safe, source-specific adaptation and a concrete reciprocal recommendation where offered; an omitted detail is not an offer or an adoption instruction.
