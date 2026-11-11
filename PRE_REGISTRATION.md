# Pre-registration — month one (live series starts 2026-11-11)

Month one measures **recording overhead + entry completeness**, not economic validity.
No window can test "is this an economy" while exchange does not exist; pre-registering
that avoids the experiment quietly becoming a diary with extra steps.

## Measured (month one)

1. **Entry completeness**: % of shipped artifacts in `ledger.jsonl` with complete
   structure (task, output.ref checkable, verification status + evidence present).
   Cost fields may be null; they must be *explicitly* null.
2. **Owner attention overhead**: actual minutes the owner spends reviewing/deciding per
   month, self-reported at review time and logged in the publication header.

## Review structure (owner-attention design)

The owner's attention is reminder-driven, not scheduled: a monthly assembly lands as a
short nudge with stats; the owner reviews one file (~15 min target) and gives one-word
approval to publish. No other standing obligation exists for this experiment.

## Triggers (pre-committed)

- **Design review** if either: owner review exceeds 60 minutes in any month, or entry
  completeness < 80% for two consecutive months.
- **Kill** only by explicit owner decision — the ledger is cheap to run; silence is not
  a kill signal (that would let it decay quietly, which is the failure mode this file
  exists to prevent).

## Baseline rule

`baseline_2026-10.jsonl` (month zero) is **reconstructed** from real records — git
commits, kanban task IDs, artifact paths. Its cost fields are partial by construction
(no historical GPU sampling existed). It appears only in the first publication, clearly
labeled, and is never merged into `ledger.jsonl`.

## Publication cadence

- First publication: 2026-11 (month zero + live entries to date) — pushed on owner green light.
- Thereafter: assembled on the 1st of each month for the previous calendar month;
  nudge → one-word approval → push. A trigger without a named runner dies quietly;
  the runner is Owl, the approver is the owner.

## Defaults (v1, revisable at the first checkpoint — early December)

- Completeness target: ≥95% of shipped artifacts carry complete entries.
- Review timebox target: ≤30 min/month.
These are measurement targets for month one, not commitments; month one's job is to say
whether they are sane.
