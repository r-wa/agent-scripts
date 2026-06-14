# Product Researcher Self Review - 2026-06-14

This is the orchestrator-owned review output from using `product-researcher`
against its own updated skill and helper behavior.

Bundle used locally:
`work/autoreview/product-researcher-self-validation-20260614-230057`

## Decision

Ship the updated product-researcher skill and helper changes in agent-scripts.

## Verdict

verdict: ready

## Accepted Findings

- [autoreview-heading] Findings heading validation accepted longer review-style headings. Fixed with exact Markdown heading matching and regression-covered by [ci-exact-headings].
- [worker-skeptic] Worker prompt ownership omitted review.md. Fixed in [helper-prompt] and regression-covered by [ci-smoke].
- [worker-skeptic] The contract overclaimed a frozen bundle. Fixed by changing the contract to a durable goal bundle in [skill-contract] and related references.
- [worker-skeptic] not_ready completion attempts were too easy to miss in status. Fixed in [helper-status] and [helper-complete-review], with [ci-smoke] asserting status becomes not_ready.

## Rejected Findings

- [worker-skeptic] Requiring review.md in validate was rejected. validate remains a structural gate for in-progress and legacy bundles; [helper-assurance] is the closeout gate and fails missing review.md.
- [worker-skeptic] Semantic proof inside assurance was rejected for this slice. The helper gates structure and evidence hygiene; the orchestrator and autoreview handle judgment.

## Deferred Findings

- [worker-skeptic] A true immutable freeze/snapshot command is deferred until the workflow shows real drift pain. The current contract no longer claims enforced freezing.
- [worker-skeptic] Rich source metadata and claim graphs are deferred beyond the small agent-scripts helper.

## Evidence Ledger

- [skill-contract] `skills/product-researcher/SKILL.md` defines the durable goal bundle, bounded workers, validation gates, findings triage, and orchestrator-owned review output.
- [helper-prompt] `skills/product-researcher/scripts/product-research` worker prompts explicitly forbid edits to `brief.md`, `findings.md`, `review.md`, and `state.json`.
- [helper-assurance] `skills/product-researcher/scripts/product-research` closeout fails on placeholders, missing review shape, missing source IDs, missing verdicts, non-ready verdicts, and missing required worker reports.
- [helper-complete-review] `skills/product-researcher/scripts/product-research` records `not_ready` or `blocked` status for non-ready verdicts; `review` prints the curated record while returning nonzero unless ready.
- [ci-smoke] `.github/workflows/validate.yml` covers worker prompt ownership, missing `review.md` closeout failure, source ledger failure, `not_ready`, `blocked`, `complete`, and ready review output.
- [helper-exact-headings] Exact Markdown heading checks prevent copied review-style findings headings from passing assurance.
- [ci-exact-headings] CI covers malformed findings headings as an assurance failure.
- [local-validation] Local CI-equivalent validation passed after the accepted fixes.
- [autoreview-clean] Installed autoreview skill reported no accepted/actionable findings after the fixes.

## Confidence

high; confidence is based on current repo inspection, one real skeptic worker
report, local CI-equivalent validation, and a clean installed autoreview run. It
does not claim semantic perfection for every future research domain.

## Assurance

Commands/workers used:

- `product-research init` and `product-research validate` created the self-validation goal bundle.
- Worker thread: `skeptic` was executed by a sub-agent and imported with `product-research worker-import`.
- Worker-style `technical-investigator` and `architect` reports were imported as supporting evidence.
- `product-research assure`, `product-research complete`, and `product-research review` passed against the self-validation bundle.
- Local CI-equivalent validation passed.
- Installed autoreview skill returned clean after accepted fixes, including the exact-heading regression.

Remaining blockers: None for this slice.
