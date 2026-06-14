# Agent Scripts

Shared agent instructions, skills, and small portable helpers for Ryan's workspaces.

This repo is the canonical place for:

- `AGENTS.MD`: shared hard rules for Codex-style agents
- `skills/`: reusable workflow skills, including repo-owned skills exposed by symlink
- `scripts/`: dependency-light helpers used across projects
- `hooks/`: local guardrails such as skill validation
- `docs/`: longer notes, rubrics, and design records that should not live in README

## Skills

Skills are the main routing layer. Each `skills/<name>/SKILL.md` has YAML front matter:

```yaml
---
name: skill-name
description: "Short generic trigger phrase."
---
```

Rules:

- Keep descriptions short and generic; optimize for routing, not documentation.
- Quote `description` in front matter.
- Keep skill bodies terse and operational.
- Prefer helper scripts under `skills/<name>/scripts/` when a workflow has repeatable commands.
- Keep longer rubrics in `skills/<name>/references/`.
- Validate after edits: `scripts/validate-skills`.

Install selected skills with the helper:

```bash
scripts/install-skills product-researcher
```

By default it symlinks into `$HOME/.agents/skills`.

Repo-owned skills stay canonical in the repo they describe and can be exposed here with tracked relative symlinks. Do not duplicate canonical skill copies unless deliberately vendoring a snapshot.

## Agent Instructions

Shared hard rules live in `AGENTS.MD`.

Global setup:

```text
~/.codex/AGENTS.md -> ~/Projects/agent-scripts/AGENTS.MD
```

Downstream repos should use a pointer-style `AGENTS.MD`:

```text
READ ~/Projects/agent-scripts/AGENTS.MD BEFORE ANYTHING (skip if missing).
```

Repo-specific rules go below that pointer. Do not copy the shared blocks into downstream repos.

## Helpers

`scripts/committer`

- Stages exactly the listed files.
- Enforces a non-empty commit message.
- Runs skill validation before committing.

`scripts/install-skills`

- Validates skills.
- Symlinks selected skills, or all skills, into `$HOME/.agents/skills`.
- Refuses to overwrite non-symlink targets.

`scripts/validate-skills`

- Checks every `skills/*/SKILL.md`.
- Verifies YAML front matter plus required `name` and `description`.
- Enforces quoted, terse descriptions.
- Enable as a local hook with `git config core.hooksPath hooks`.

`skills/product-researcher/scripts/product-research`

- Creates explicit goal bundles.
- Validates and assures research closeout.
- Starts/imports bounded worker thread reports.
- Prints the orchestrator-owned review output from `review.md`.

## Syncing

Treat this repo as canonical for shared agent rules and portable helper scripts.

When syncing downstream repos:

- Pull latest here first.
- Ensure each target repo starts with the pointer-style `AGENTS.MD`.
- Preserve repo-local rules below the pointer.
- Copy helper changes both directions only when the helper is meant to stay byte-identical.
- Keep scripts dependency-free and portable; no repo-specific imports or path aliases.
