# Evidence Rubric

## Source Strength

Prefer sources in this order:

1. Current local repo code, tests, docs, and configuration.
2. Official product, API, SDK, protocol, and release documentation.
3. Public source code, examples, demos, and issue trackers.
4. Customer or community evidence such as forums, reviews, support threads, and public discussions.
5. Analyst, media, blog, and secondary summaries.
6. Vendor marketing pages.

Vendor marketing can support positioning claims, but it should not carry
technical feasibility or customer-value claims by itself.

## Claim Rules

Each important claim should include:

- source IDs
- confidence
- claim kind
- thread origin
- contradictions or caveats
- verification status

Do not promote an unsourced note into a recommendation.

## Source Hygiene

- Use the smallest source set that answers the decision.
- Do not store raw chat transcripts, private records, secrets, full exported
  pages, or broad source dumps in the bundle.
- Prefer source IDs, paths, URLs, short notes, and relevant excerpts.
- Redact aggressively when a source contains credentials, tokens, user data, or
  private conversation content.
- Treat worker and model output as advisory until verified against primary
  sources, repo code, tests, docs, or live proof.

## Confidence Caps

- No customer/value evidence: max `medium`.
- No technical implementation evidence: max `low` for a build recommendation.
- No direct source for provider-specific facts: max `low`.
- Only vendor marketing sources: max `medium`.
- Only community or anecdotal sources: max `low`.
- No current repo inspection for implementation guidance: max `medium`.

## Closeout Failures

Closeout fails when:

- a required thread is missing
- source count is below the threshold needed for the decision
- important claims lack source IDs
- customer value is assumed
- implementation feasibility is asserted without repo, code, or docs evidence
- all sources come from one vendor or one source family
- skeptic findings remain open
- recommendation confidence exceeds the evidence cap
- there is no first implementation slice or validation plan

## Review Output Rules

The orchestrator output is a review result, not a report stack. It should:

- state the decision and verdict first
- list only accepted actionable findings that still matter
- explain rejected findings briefly enough that future review can audit the call
- defer work only with a concrete next-slice reason
- cite source IDs for important claims
- cap confidence when source families are thin
- include implementation surface, fit/cause, best fix, refactor tradeoff, proof,
  and residual risk when the decision is implementation-facing
- include the assurance commands and worker threads used

Closeout should fail when `review.md` still contains placeholders, lacks a
verdict, omits the evidence ledger, or leaves accepted actionable findings open.
