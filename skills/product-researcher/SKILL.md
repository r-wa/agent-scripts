---
name: product-researcher
description: "Evidence-led product and implementation research with market, customer, technical, architecture, and review threads."
---

# Product Researcher

Use this skill for product discovery, implementation research, competitor or
adjacent-product analysis, market options, customer workflow research, and
codebase-fit research.

Do not use it for quick factual lookups, generic web summaries, or questions
that only need a direct answer.

## Contract

Produce a decision-ready evidence bundle and brief. Do not treat the user's
initial direction as proven. Research alternatives, contradictions, and better
adjacent approaches.

Work like `autoreview`: one explicit goal, one durable goal bundle, bounded
worker threads, validation gates, accepted/rejected/deferred findings, and
closeout only after the assurance pass is clean or the blockers are explicit.

Workers are inputs. The orchestrator owns the review output. Do not concatenate
worker reports into the final answer. Triage them into a single decision record.

Treat worker and second-model output as advisory. Verify accepted claims against
primary sources, current repo code, tests, or live proof before promoting them
into findings or recommendations.

Keep context tight. Do not preserve raw chat transcripts, secrets, private
records, whole-page dumps, or broad source captures in the bundle. Store source
IDs, paths, URLs, concise notes, and relevant excerpts only. Keep transient
research bundles out of public repos unless the user explicitly asks to publish
that artifact.

## Helper Path

Set the helper once, then use `$PRODUCT_RESEARCH`:

```bash
export AGENTS_HOME="${AGENTS_HOME:-$HOME/.agents}"
export PRODUCT_RESEARCH="$AGENTS_HOME/skills/product-researcher/scripts/product-research"
```

## Inputs

Collect or infer:

- research question
- target mode
- current repo or product context, if any
- decision the research should support
- time or source constraints
- whether implementation handoff is needed

## Modes

- `build-what`: decide what should be built and why
- `build-how`: compare implementation approaches
- `market-map`: map products, adjacent tools, and feature patterns
- `implementation-map`: inspect code, docs, SDKs, examples, demos, and release notes
- `customer-value`: validate jobs, pain, workflow fit, alternatives, and objections
- `architecture`: propose a codebase-aware build shape
- `provider-specific`: inspect named provider/API/platform facts only when explicit

## Workflow

1. Establish the goal in a bundle:
   `$PRODUCT_RESEARCH init --goal "..." --mode build-what --decision "..." --context "$PWD"`
2. Validate the bundle:
   `$PRODUCT_RESEARCH validate <bundle>`
3. Select the smallest mode set that answers the decision.
4. Inspect repo or product truth before making implementation claims.
5. Split work into research threads:
   - market/products
   - technical implementation
   - customer workflow/value
   - architecture/codebase fit
   - evidence verification
6. Use a worker for each independent thread when useful:
   `$PRODUCT_RESEARCH worker-start <bundle> --thread technical-investigator`
7. Gather evidence from primary sources first.
8. Import worker reports:
   `$PRODUCT_RESEARCH worker-import <bundle> --thread technical-investigator --file /tmp/report.md`
9. Record important claims with source IDs.
10. Compare options and adjacent alternatives.
11. Run a skeptic review against the evidence bundle.
12. Triage worker claims into `findings.md`: accepted, rejected, deferred.
13. Write `review.md` as the orchestrator closeout record.
14. Fix accepted actionable findings.
15. Run assurance:
    `$PRODUCT_RESEARCH assure <bundle>`
16. Print the closeout review:
    `$PRODUCT_RESEARCH review <bundle>`
17. Repeat until assurance passes or blockers are explicit.
18. Use the review output as the final brief, plus implementation handoff only when useful.

## Evidence Rules

- Every important claim needs source IDs.
- Prefer the smallest source set that contains the truth.
- Direct provider evidence can stand alone for provider-specific facts.
- Otherwise prefer multiple independent source families.
- Mark uncertainty and contradictions.
- Do not invent pricing, API limits, platform behavior, or customer value.
- Do not recommend implementation until repo impact and validation are inspected.
- Research does not authorize push, PR updates, merges, releases, or public
  comments. Stop at the last authorized boundary unless the user grants that
  mutation separately.

See `references/evidence-rubric.md`.

## Output

The final output is `review.md` printed by `$PRODUCT_RESEARCH review <bundle>`.
It is not a transcript, not a pile of worker notes, and not a brainstorming dump.
It must contain:

- decision
- verdict: `ready`, `blocked`, or `not_ready`
- accepted findings, or `None.`
- rejected findings with reasons
- deferred findings with next-slice rationale
- evidence ledger with source IDs
- confidence level and cap reason
- assurance proof: commands, workers, and remaining blockers

For implementation recommendations, also answer the Peter-style review shape:
affected surface, cause or fit rationale, best fix, refactor tradeoff, proof,
and residual risk. Say `unknown` or `not proven` when evidence is insufficient.

`$PRODUCT_RESEARCH assure <bundle>` and `complete` exit clean only for
`verdict: ready`. Blocked and not-ready completion attempts remain non-ready in
bundle status. `$PRODUCT_RESEARCH review <bundle>` can print blocked or
not-ready reviews, but exits nonzero for them.

Keep the supporting `brief.md` decision-ready with:

- recommendation
- evidence summary
- validation
- next slice

## Closeout

Close out only when required evidence has been gathered, actionable skeptic
findings are fixed or explicitly rejected with reasons, and the recommendation
confidence does not exceed the evidence quality.

The assurance gate must pass and `$PRODUCT_RESEARCH review <bundle>` must print
the curated closeout record. `complete` may mark the bundle ready only when
`review.md` says `verdict: ready`; blocked or not-ready bundles must remain
non-ready and the final answer must say why.
