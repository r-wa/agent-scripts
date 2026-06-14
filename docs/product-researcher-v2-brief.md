# Product Researcher v2 Brief

## Positioning

`product-researcher` is not a generic research assistant. It is a
script-backed, evidence-led investigation workflow for deciding:

- what to build
- how to build it
- what market options and adjacent products exist
- how existing products implement similar functionality
- whether the idea has customer value
- what implementation path is most defensible

The output is a decision-ready evidence bundle and brief, reviewed until clean.

## Modes

- `build-what`: understand what should be built and why
- `build-how`: understand implementation approaches and tradeoffs
- `market-map`: identify products, adjacent products, and feature patterns
- `implementation-map`: inspect code, SDKs, docs, demos, screenshots, release notes, and open-source implementations
- `customer-value`: validate jobs, willingness, workflow fit, pain, alternatives, and objections
- `architecture`: propose a build shape against the current codebase
- `provider-specific`: inspect a named provider/API/platform/pricing model only when explicit

Pricing, plan limits, and API constraints are optional facets, not default
assumptions.

## Autoreview Shape

```text
research bundle
-> durable goal context
-> independent thread reviews
-> structured findings
-> accept/reject with evidence
-> fix gaps
-> rerun
-> closeout only when clean
```

The helper should exit non-zero when evidence is weak, findings remain open,
or the review verdict is not ready.

## Thread Model

The orchestrator owns the bundle. Worker threads do not mutate final
conclusions directly. Each worker produces a thread report that the
orchestrator imports.

Required threads:

- Market Scout
- Technical Investigator
- Customer/Value Researcher
- Architect
- Skeptic / Research Autoreviewer

Optional threads:

- Provider/API Specialist
- Pricing/Packaging Specialist
- UX Asset Hunter
- Legal/Security/Privacy Reviewer
- Benchmark/Prototype Worker

## Evidence Model

Every source should record:

- source ID
- type
- title
- URL or path
- publisher
- fetched or accessed time
- content hash where practical
- excerpt or snippet
- source strength
- freshness or staleness
- whether it is primary, secondary, community, or marketing

Every claim should record:

- claim ID
- text
- source IDs
- claim kind
- confidence
- thread origin
- contradicting claims
- verification status

Every option should record:

- option name
- user value
- implementation shape
- market examples
- customer evidence
- technical evidence
- risks
- repo impact
- first slice
- rollback path

## Closeout Rules

Closeout fails when:

- a required thread is missing
- source count is below threshold
- claims lack source IDs
- direct provider/source evidence is missing for provider-specific claims
- customer value is assumed rather than evidenced
- implementation feasibility is asserted without repo, code, or docs evidence
- all sources come from one vendor or one source family
- skeptic has open actionable findings
- recommendation confidence exceeds evidence caps
- there is no first implementation slice or validation plan

Closeout passes when:

- consensus is reached
- all accepted findings are fixed
- rejected findings have concrete resolutions
- the brief is rendered
- implementation handoff is scoped to one slice

## Output Brief

The rendered brief should answer:

1. What are we trying to learn?
2. What exists in the market?
3. What adjacent approaches might be better?
4. What functionality matters?
5. How do customers use or value it?
6. How can we implement it?
7. What does the current codebase imply?
8. What evidence supports this?
9. What evidence contradicts it?
10. What should we build first, if anything?
11. What should we not build?
12. What remains unknown?
13. What is the implementation handoff?

## Build Order

1. Use the instruction-only skill manually.
2. Capture real evidence bundles from 3 to 5 runs.
3. Add thread prompt generation and report import.
4. Add source and asset capture.
5. Add consensus scoring with confidence caps.
6. Add skeptic review schema.
7. Add closeout gate.
8. Add rendered brief and implementation handoff.
9. Add worker launching only after the bundle format is stable.
