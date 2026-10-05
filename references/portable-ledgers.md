# Portable comparison records

These are illustrative logical schemas, not an installed service or validator. Use text tables if automation adds no value. Public records explain observations without sender-only paths; retain detailed private evidence separately.

## Corpus

Record each supplied item's safe `source_ref`, `revision`, `kind`, exact-byte `sha256` (64 hexadecimal characters or null when unavailable), `read_extent` (complete, partial, inaccessible), and `duplicate_of` (safe reference or null). Record unread/partial limits. Equal names do not imply equal content.

## Decision

One row per unique body/revision:

```json
{
  "capability": "Stable identity for retries",
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

Decision: `reuse`, `adapt`, `decline`, `defer`. Adoption status follows the evidence states in [report-pattern.md](report-pattern.md); selecting an idea is not installation. Unknown hashes stay null with a reason; compute actual complete-file hashes rather than copying placeholders. Reciprocal kind: `recommendation`, `documented-capability`, `none`. A recommendation remains a proposal. If a reverse cell says `none`, explain why; this does not invalidate a useful take-only decision.

## Later review

```json
{
  "reviewer": "independent-reviewer-A",
  "checked_at": "2026-10-05T00:00:00Z",
  "source_ref": "synthetic-D1",
  "source_sha256": null,
  "verdict": "disagree",
  "basis": "Explain the observed disagreement without replacing the original decision"
}
```

Dates and identities above are synthetic placeholders, not proof. Append only material actually read. Verdict: `agree`, `disagree`, `not-assessed`. Distinguish attempts; never impersonate reviewers. Retain previous decisions, reviews and chronology.

## Local checks

- Every available unique body/revision has a decision; unread material is explicit.
- Known hashes match read bytes; reviews refer to inventoried revisions.
- Evidence states have dated observations of that particular state.
- Previous records remain intact and disagreements are appended.
- Every public field, filename, comment, link and attachment fits the disclosure scope.

Run checks with available receiver tools and record actual results. Reading this schema passes none of them.
