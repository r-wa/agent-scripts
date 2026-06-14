# Architecture

This repo has three layers.

## Rules

`AGENTS.MD` contains hard, always-on rules for work in this repository. It
should stay short. If instructions describe a reusable workflow, move them to a
skill.

## Skills

`skills/<name>/SKILL.md` is the workflow contract. It should tell Codex when to
use the skill, what inputs to collect, what loop to follow, and what output is
required.

Use this shape:

```text
skills/<name>/
  SKILL.md
  scripts/       # optional deterministic helpers
  references/    # optional rubrics, schemas, examples
  assets/        # optional templates/resources
  agents/        # optional Codex app metadata
```

## Scripts

Scripts exist only when deterministic behavior matters. A good script removes
repeated shell work, validates a contract, or creates a consistent artifact.

Avoid adding scripts just to make the repo look complete.

## Distribution

For local authoring, symlink individual skill folders into
`$HOME/.agents/skills`. Package this repo as a Codex plugin only after the
workflows stabilize and distribution needs are clear.
