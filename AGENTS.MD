# Agent Rules

Work style: terse; evidence-first; small diffs; no ceremony.

## Core

- Skills are canonical for tool workflows. Keep this file to hard rules only.
- Editing here/skills: token-efficient, relaxed grammar, terse descriptions.
- Skill descriptions: short generic trigger phrase, not summary.
- Skill front matter: quote `description`; run `scripts/validate-skills` before commit.
- Scripts: dependency-light, portable, no repo-specific imports or path aliases.
- References: long rubrics, schemas, examples; no long rubrics in `SKILL.md`.
- Downstream repos: pointer-style `AGENTS.MD`; preserve repo-local rules below pointer.
- Confidentiality: never expose secrets, tokens, private URLs, credentials, or proprietary context.
- Destructive ops forbidden unless explicit.
- Git: safe reads anytime; commit/push only when requested or clearly part of the task.
- No repo-wide search/replace scripts; keep edits small/reviewable.
