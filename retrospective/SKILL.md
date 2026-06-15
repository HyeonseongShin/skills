---
name: retrospective
description: "Run a structured post-task retrospective to extract skill gaps, capture design decisions, identify context that was missing or discovered late, and generate improvement candidates for the skill system and AGENTS.md. Trigger when the user says a task or feature is complete, when a plan.md is about to be deleted, or when the user explicitly asks for a retrospective. Skip for trivial tasks (one-liners, minor fixes)."
---
 
# Retrospective Skill
 
Post-task debrief that turns completed work into a feedback signal — extracting what the skill system missed, what decisions should be preserved, and what the next task should know going in.
 
## When to Trigger
 
**Trigger when:**
- User signals task completion ("done", "finished", "merged", "shipped")
- A plan.md has been executed and is about to be deleted
- User explicitly asks for a retrospective
**Skip when:**
- Task was trivial (one-liner, quick lookup, minor fix)
- Task is still in progress
---
 
## Step 1: Acknowledge and Open
 
One sentence acknowledging completion. Signal you're running a retrospective. Keep it short.
 
Example:
> "Good work. Now that the task is done, want to do a quick retrospective and capture anything worth keeping for next time?"
 
---
 
## Step 2: Probe — One Question at a Time
 
Ask these in order. Skip any that clearly don't apply. Wait for each answer before continuing.
 
**Q1 — Skill hit rate**
> "Were there moments in this task where a skill was actually useful? Which skill, and in what context?"
 
Listen for: which skills were useful, which were loaded but ignored.
 
**Q2 — Skill gaps**
> "Were there things you had to reason through or look up yourself because no skill covered it?"
 
Listen for: missing conventions, undocumented patterns, implicit knowledge not written anywhere.
 
**Q3 — Decision capture**
> "Were there any decisions made that future readers couldn't infer from the code alone? Things where the *why* would be invisible without context?"
 
Listen for: architectural choices, rejected alternatives, trade-offs — things that belong in a decision record but never get written.
 
**Q4 — Friction**
> "Were there moments where the agent got stuck, or where you had to re-explain the same context more than once?"
 
Listen for: context that had to be re-explained, wrong assumptions, anything that slowed the loop.
 
**Q5 — Surprises**
> "Was anything more complex than expected — or unexpectedly simple?"
 
Listen for: scope misestimation, hidden dependencies, assumptions in the original plan that turned out wrong.
 
---
 
## Step 3: Four Outputs
 
Produce exactly four outputs. Concise. If there's nothing to say, say so — don't pad.
 
### Output 1: Skill Update Candidates
 
```
[update] <skill-name>: <what to add or change> — <why>
[new]    <skill-name>: <one-line summary of what it covers>
```
 
Only include items where the signal was clear. Max 5.
 
### Output 2: Decision Log
 
Per item:
```
- [decision] <what was decided>
  - context: <why this decision was needed>
  - reason: <why this direction was chosen>
  - tradeoff: <what was given up>
```
 
Skip entirely if there were no meaningful decisions. Max 3.
 
### Output 3: Next Task Heads-Up
 
Things that would have helped *this* task if known at the start.
 
```
- <one line, the essential point>
```
 
Max 3 items.
 
### Output 4: Context Gap Report
 
Context that was missing at the start, discovered mid-task, or would have shortened the loop if it had been available upfront. For each gap, recommend where it should live going forward.
 
Per item:
```
- [gap] <what context was missing or discovered late>
  - discovered: <when in the task this became clear — upfront / mid-task / near the end>
  - impact: <how it affected the task — wrong assumption, extra turns, rework, etc.>
  - suggested home:
      - AGENTS.md        — if it's a project-wide constraint or convention all agents should know
      - <skill-name>     — if it belongs in a specific skill's instructions or gotchas
      - plan.md (upfront) — if it should be surfaced during planning, not discovered mid-task
      - docs/decisions/  — if it's a one-off decision context, not a general rule
```
 
Only include gaps where the impact was real. Max 5.
 
**Classification guide:**
- Constraint that applies to every task in this repo → **AGENTS.md**
- Knowledge specific to a skill's domain → **skill gotchas**
- Information that should be gathered before coding starts → **plan.md (upfront)**
- One-time decision rationale → **docs/decisions/**
---
 
## Step 4: plan.md Disposition
 
End with a clear recommendation:
 
- **Archive** — If the Decision Log has entries and future reference is likely
  → recommend moving to `docs/decisions/JIRA-XXX-<slug>.md`
- **Discard** — If there were no meaningful decisions and the task was routine
  → state explicitly that deletion is fine
---
 
## Gotchas
 
- Don't fill in sections that have nothing to say. Write "N/A" explicitly rather than inventing entries.
- Skill Update Candidates should only reflect things the agent actually struggled with — no generic improvement suggestions.
- Decision Log is strictly for things that can't be inferred from the code alone. No implementation detail summaries.
- If the full retrospective runs long, it has failed its purpose. Keep it short and dense.
---
 
## Language
 
Match the user's language throughout. If the user speaks Korean, conduct the retrospective in Korean. If English, use English.
Format tags (`[update]`, `[new]`, etc.) may be translated to match the user's language.

