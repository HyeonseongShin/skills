# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is a personal collection of [Agent Skills](https://agentskills.io) for AI coding agents (Claude Code, Cursor, OpenCode, Codex, etc.). There is no application code, build system, linter, or test suite — the repository consists entirely of `SKILL.md` files, each defining one skill.

## Structure

Each skill lives in its own top-level directory containing a single `SKILL.md`:

- `grill-me/SKILL.md` — interviews the user before non-trivial implementation/design tasks to surface blind spots and missing constraints, then synthesizes answers into an improved proposal.
- `retrospective/SKILL.md` — runs a post-task retrospective (skill gaps, decision log, next-task heads-up, context gap report) when a task is marked done or a `plan.md` is about to be removed.
- `context-snapshot/SKILL.md` — compresses the current conversation into a compact, English, noun-phrase Markdown summary for carrying into a fresh session.

## SKILL.md conventions

Every `SKILL.md` follows the agentskills.io spec:

```markdown
---
name: skill-name        # kebab-case, matches the directory name
description: "..."      # specific, trigger-oriented — this is what agents use to decide WHEN to load the skill
---

<instructions body>
```

When editing or adding a skill, keep these conventions consistent with the existing ones:

- **`description` is the trigger condition.** It must spell out concrete situations/phrases that should cause the skill to load (e.g. "save context", "summarize for a new session"), plus explicit non-triggers where relevant. This field is load-bearing — vague descriptions mean the skill silently never fires.
- **Language matching.** Skills that produce user-facing output (`grill-me`, `retrospective`) explicitly instruct the agent to match the user's language throughout. `context-snapshot` is the deliberate exception — it always outputs English for token efficiency.
- **Density over completeness.** Several skills explicitly instruct "don't pad", "write N/A rather than inventing entries", "keep it short and dense". New skills should follow the same bias toward terse, structured output over prose.
- **One-question-at-a-time interview pattern.** `grill-me` and `retrospective` both use a step-by-step probing protocol (ask one thing, wait for the answer, then proceed) rather than dumping a list of questions. Preserve this pattern if extending either skill.

## Adding or renaming a skill

- Create `<skill-name>/SKILL.md` with the frontmatter above.
- Add a corresponding entry to the "Skills" section of `README.md` (one subsection per skill: short description + trigger summary), matching the existing format.
- If renaming a skill directory, update both the directory name and any references in `README.md` (see commit `ba1d0ad` for the precedent of renaming `context-archive` → `context-snapshot`).
