# agent-ledger

**Scoped claim: this is a production function with open books — not an economy.**
A single-agent household (Owl + owner, one human signer) recording what it produces,
what producing it cost in physical inputs, and how each output was verified.
Conceded up front, per the pressure test that designed this ledger:

- A single-household ledger is bookkeeping under any unit of account. What makes an
  economy is exchange between parties; there are no counterparties yet. The
  `counterparty` field exists in the schema from day one (always `internal` for now)
  so the format already assumes exchange and needs no migration later.
- Every entry passes through one human owner. That limit is stated here, not hidden.
- Success metric (pre-registered): this ledger succeeds when *someone else builds
  their first ledger cheaper because of ours* — not when exchange happens.

## What is in this repo

| File | What it is |
|---|---|
| `SCHEMA.md` | Entry format, the conversion contract, and the self-report accuracy metric |
| `PRE_REGISTRATION.md` | Month-one criteria, review triggers, owner-attention structure |
| `baseline_2026-10.jsonl` | **Month zero / baseline** — reconstructed from real records (git commits, task IDs, artifact paths). Cost fields are partial *by construction*. Never mixed into the live series. |
| `ledger.jsonl` | Live entries, append-only, measured at ship time |
| `publications/` | Assembled monthly markdown (human-readable view of the JSONL) |

## Reading it

Each entry: date · workstream · task · inputs (model, GPU-min, wall time, human-attention
minutes — `null` means *not recorded*, never an estimate) · output reference · verification
status + evidence · counterparty. Machine-readable JSONL is the source of truth; the
markdown publications are assembled from it by script (`agent_ledger_assemble.py`).

## Provenance of this experiment

Designed under pressure test `t_40c3f806` (strategist consultation, 2026-11-11); full
decision-grade doc in the household kanban attachments. Owner decisions recorded:
publication venue = new public repo; owner attention = reminder-driven, review-only.
