# Skill Authoring

## Front Matter

Every skill needs front matter with a kebab-case `name` matching its folder and
a short `description`.

```md
---
name: product-researcher
description: Evidence-led product and implementation research with market, customer, technical, architecture, and review threads.
---
```

The description is a routing trigger. Front-load the key use case and keep it
under 140 characters so it survives shortening.

## Body

The body should be operational:

- when to use the skill
- when not to use it
- required inputs
- workflow loop
- output contract
- closeout criteria

Avoid essays. Put long rubrics in `references/`.

## References

Use references for material that is useful but too long for the skill body:

- evidence rules
- source hierarchy
- output schemas
- review checklists
- examples

## Scripts

Add scripts after the workflow repeats. Scripts should be testable from the
repo root and should fail clearly when required inputs are missing.

## Validation

Run:

```bash
scripts/validate-skills
```

This checks that each `skills/<name>/SKILL.md` exists, has front matter, has a
matching `name`, and keeps `description` terse.
