# Research Threads

## Market Scout

Purpose: map existing products, adjacent solutions, feature patterns, and
implementation assets.

Expected evidence:

- product docs
- changelogs and release notes
- demos, screenshots, and videos where available
- public help docs
- open-source implementations or SDK examples

Output:

- competitors and adjacent products
- feature matrix
- observed implementation patterns
- asset links
- gaps and non-obvious alternatives

## Technical Investigator

Purpose: understand how to build or integrate the capability.

Expected evidence:

- current repo code paths
- official docs and SDKs
- open-source code
- examples
- protocols and data models
- release notes affecting implementation

Output:

- viable implementation approaches
- codebase impact
- complexity and risk
- proof path
- first implementation slice

## Customer/Value Researcher

Purpose: challenge whether the feature is worth building and how customers
would use it.

Expected evidence:

- support/community/user reports
- public reviews
- forum discussions
- workflow examples
- issue trackers
- testimonials and case studies treated cautiously

Output:

- user jobs
- pain evidence
- expected workflow
- willingness/value indicators
- objections
- adoption risk
- validation gaps

## Architect

Purpose: convert evidence into a repo-aware build strategy.

Expected evidence:

- current code structure
- active agent/project instructions
- tests and build commands
- existing architecture boundaries
- technical thread findings

Output:

- recommended architecture
- boundaries and adapters
- data model changes
- sequence of work
- tests or live proof
- rollback path

## Skeptic / Research Autoreviewer

Purpose: adversarially review the durable goal bundle and closeout evidence.

Finding categories:

- unsupported claim
- weak source
- stale source
- one-sided evidence
- missing direct provider/source evidence
- missing competitor or adjacent example
- missing customer value proof
- overconfident recommendation
- repo impact gap
- implementation feasibility gap
- better alternative ignored
- scope drift

Output:

- structured findings
- readiness: `ready`, `not_ready`, or `blocked`
- consensus blockers
