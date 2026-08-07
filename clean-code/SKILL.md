---
name: clean-code
description: "Apply Clean Code judgment in real time while writing or refactoring code — when to split a function, where to draw a class/file's SRP boundary, when a boolean flag argument means the function does two things, and when duplicated code should be merged versus left alone. Trigger while actively writing or modifying code (not for standalone bug-hunting review, security review, or whole-repo over-engineering audits — those belong to other review skills). Independent of any minimalism/YAGNI mode the user may also have active; this skill does not assume one."
---

# Clean Code

Judgment criteria for decisions that come up mid-write, not a principle summary —
skip anything a competent coder would already do without prompting.

## Trigger

Applies while actively writing new code or refactoring existing code. Does **not**
apply to:
- Pure bug-hunting / correctness review (defer to a bug-focused review skill)
- Security review
- Whole-codebase over-engineering audits
- Pure formatting/style passes with no structural judgment involved

## Core judgment: when to split a function

Don't split preemptively for symmetry or "just in case." Split when the function
already, in its current form, fails one of these:

- **Can't be named with a single verb phrase without "and"** — `validateAndSave`,
  `fetchAndParse` — the "and" is the tell, not the length.
- **Mixes abstraction levels** — one line manipulates a raw string/loop, the next
  calls a domain-level operation. Extract the low-level part.
- **Has a boolean/flag argument that forks its internal logic** — that's two
  functions wearing one name. Extract the branches into two named functions,
  unless the flag is genuine data (e.g. a config value passed straight through,
  not branched on to change control flow).

If none of these hold, a longer function is not automatically wrong — don't
manufacture a split just to hit an arbitrary line count.

## Core judgment: SRP / class & file boundaries

Draw the boundary at **"reason to change,"** not at line count or file count:

- A class with many small methods that all change together for the same reason
  (one actor, one concern) is cohesive — leave it, even if it's long.
- A class whose methods change for *different* reasons (e.g. one method changes
  when the DB schema changes, another when the UI copy changes) should split,
  even if it's short.
- Splitting one concern across multiple files/classes for the sake of "small
  files" without a distinct reason-to-change is the same mistake in reverse —
  don't do it just to look modular.

## DRY vs. coincidental similarity

Merge duplicated code only when it duplicates the same *reason to change*. If two
blocks look alike today but represent different concerns that could diverge
independently later, keep them separate — force-merging them creates a false
abstraction (a shared function with a flag/branch to handle the "coincidence"),
which is worse than the original duplication.

## Baseline (apply without discussion, don't narrate)

- Naming: intent-revealing, one word per concept, no abbreviations that need a
  comment to decode
- Comments: only "why," never "what"; delete stale/commented-out code on sight
- Errors: exceptions over sentinel/error-code returns; don't pass or return
  `null` where an explicit type/exception works

## Output

Apply silently — the code itself is the output. Don't narrate each principle
followed. Only surface a note when a trade-off is genuinely non-obvious from
the diff (e.g. "kept the flag arg here — the two branches share 90% of the
body, splitting would duplicate more than it clarifies").
