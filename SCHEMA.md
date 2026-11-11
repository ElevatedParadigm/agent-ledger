# Schema v1 (2026-11-11)

## Entry fields (JSONL, one object per line, append-only)

| Field | Type | Notes |
|---|---|---|
| `id` | str | `YYYY-MM-DD-NN`, unique within the file |
| `date` | str | ISO date of completion |
| `workstream` | enum | `stella` · `eit` · `gourmet-oracle` · `h2-research` · `coordination` · `ledger` |
| `task` | str | one line, what was produced |
| `inputs.model` | str/null | model used (`qwen3.8-27b local`, `ornith-1.5 local`, `none (python)`) |
| `inputs.gpu_min` | num/null | GPU-minutes by model+quant; `null` = not recorded (no historical sampling) |
| `inputs.energy_wh` | num/null | only if sampled by an existing cron; currently never — labeled, not estimated |
| `inputs.wall_time_min` | num/null | derivable from timestamps where they exist, else null |
| `inputs.owner_attention_min` | num/null | human review/decision time attributable to this entry |
| `output.type` | enum | `commit` · `artifact` · `publication` · `consultation` · `record` |
| `output.ref` | str | path, commit hash, task id, or URL — must be checkable by a stranger |
| `output.public` | bool | is the ref publicly reachable? |
| `verification.status` | enum | `live-verified` · `tests-passed` · `frozen-nulls` · `reconstructed` (baseline only) · `pending` |
| `verification.evidence` | str | one line: what a stranger would check |
| `counterparty` | str | always `internal` until rails exist; field exists from day one |
| `notes` | str | optional |

**Nulls are first-class.** A missing cost is recorded as `null`, never estimated.
Estimates would be synthetic data and violate the household's zero-synthetic-data policy.

## Cost structure (why two columns of cost)

Weights are local and **sunk** — capital already paid. The marginal cost of this
household is electricity + attention, while most agent households' dominant cost column
is per-token rent. Entries therefore separate:

- **marginal**: `gpu_min`, `energy_wh` (when sampled), `owner_attention_min`
- **amortized/capital**: model weights — recorded once in this file, never re-charged per entry

## Conversion contract

Entries are recorded in physical inputs. No monetary conversion is applied. When an
external unit of account becomes available for inter-agent exchange, entries convert via
a formula published here as a **dated amendment** to this section; history is never
re-recorded or re-based. Until then the ledger's claim scope stays: *production function
with open books*.

## Self-report accuracy metric

At each publication, every number cited in the accompanying summary is re-queried against
live state and match/mismatch counts are recorded below. First data point (2026-11-11):
the consultation brief that designed this ledger was checked live by a second agent —
**9 of 12 claims exact, 3 stale within hours** (Stella event count, observation count,
test-suite size; all three were undercounts because the systems are live and growing).
Self-reported accuracy at time of writing: **75%**. Measuring our own drift is on-thesis.

| Publication | Claims checked | Exact | Stale/wrong | Accuracy |
|---|---|---|---|---|
| 2026-11 (month zero) | 12 | 9 | 3 | 75% |
