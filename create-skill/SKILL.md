---
name: create-skill
description: "Guides the design and authoring of a new agent skill (a SKILL.md file) that conforms to the agentskills.io open standard. Use whenever the user asks to create, draft, or scaffold a new skill, or wants to turn a recurring task/workflow into a reusable skill — including phrases like \"make a skill\", \"create a skill for X\", \"write a SKILL.md\", \"turn this workflow into a skill\". Trigger this even if the user only describes a repeated task without using the word \"skill\" explicitly, as long as turning it into a skill is the clear intent. Not for using or invoking an existing skill — only for authoring a new one."
---

# Create-Skill

Creating a skill is itself a design task. Producing a finished SKILL.md quickly matters less than working out, together with the user, what should actually be encoded.

## What a skill actually is

A skill is not an instruction set (a list of steps) — it's a **thinking framework**. A good skill doesn't say "do it in this order," it says "in this situation, judge by this criterion." Procedure is something a capable model can already work out on its own; what actually adds value is **the reasoning and criteria behind why to judge a certain way**.

Judge every draft against this test:
- Is this something a competent agent would have figured out on its own even without it? → doesn't belong in the skill
- Is this reasoning, context, or a priority the agent would likely miss or get wrong without it? → worth including

## What not to do

- **Don't embed code or concrete file structure.** Sample code, directory trees, file paths, and snippets baked into the SKILL.md body drift out of sync the moment reality differs per project, and they pull the agent toward following a stale example instead of checking the actual codebase. Leave "read the codebase and find what actually fits" to the agent.
- **Match the level of procedural detail to how fragile the task is — don't default to over-specifying.** When multiple approaches are valid and judgment depends on context, give criteria and priorities and trust the agent to apply them; a rigid numbered script narrows the agent's judgment and breaks the moment the situation differs slightly. But some tasks genuinely are fragile — a fixed sequence where skipping or reordering a step corrupts the result (a migration that must run in exact order, for example). That's exactly when a precise, low-freedom procedure is the right call, not a violation of this principle. The question to ask is: does this task tolerate the agent adapting on the fly, or does deviation break it?
- **Don't state uncertain things as settled fact.** Baking wrong information into a skill means repeating the same mistake every time the skill loads. If you're not confident, leave it out and let the agent verify it in the moment instead.
- **Don't let the description stay vague.** The description is the only thing loaded (alongside the name) at the discovery stage — a weak one means the skill exists but never triggers. Write it in the third person ("Extracts...", "Guides...", never "I can help you..." or "You can use this to...") since it's injected as-is into the system prompt, where a mismatched point of view hurts discovery. Lean slightly assertive about the trigger conditions, too: agents have a measured tendency to under-trigger skills, so a description that undersells when it applies is functionally the same as the skill not existing.

## Design procedure

### Step 1 — Confirm what to encode

When the user asks for a skill, don't start writing right away — confirm first (one question at a time, waiting for each answer):

1. What task does this skill cover? Within that task, what judgment does the agent commonly miss or get wrong?
2. When should this skill trigger — on what phrasing or situation? And when should it explicitly not trigger? (Non-triggers are part of the description too.)
3. Does this skill need to encode a "procedure" or a "judgment criterion"? If procedure, double-check whether the agent could already do this without help.
4. If there's an output (a document, an answer, code, etc.), has the user already set rules for its format, language, or tone?

Skip this step if the answers are already clear from what the user provided.

### Step 2 — Write the body

Build the body from what Step 1 surfaced. A reference structure (not mandatory — include only what applies):

- **Trigger conditions** — when it fires and when it doesn't, stated plainly in the body even if it overlaps with the description
- **Judgment criteria / thinking framework** — the core of the skill. Leave the reasoning behind the judgment, not just the conclusion
- **Procedure** — only where genuinely needed, and only where order matters
- **Output shape** — if there's a deliverable, its structure (the skeleton, not the content)

Write densely, with no filler sentences. Omit any section that doesn't apply.

### Step 3 — Confirm compliance with the agentskills.io spec

The frontmatter must follow these rules:

- `name`: lowercase letters, numbers, and hyphens only. Cannot start or end with a hyphen, no consecutive hyphens, 64 characters max. **Must match the directory name exactly.**
- `description`: 1024 characters max, must not be empty. Cover both "what it does" and "when to use it," and include the concrete phrases or keywords that should trigger it — a vague description is functionally the same as the skill never loading.
- Add optional fields (`license`, `compatibility`, `metadata`, `allowed-tools`) only when actually needed. Most skills don't need any of them.
- Keep the body under 500 lines, ideally under 5000 tokens. If more detailed material (reference docs, templates) is genuinely needed, split it into separate files under `references/`, `assets/`, etc., and link to them by relative path from SKILL.md — this is the same progressive-disclosure principle: the agent only reads those files when it actually needs them.

### Step 4 — Align with existing skills in the same collection (if any)

This skill isn't tied to any specific repository — it might be used standalone, or alongside other skills in a shared collection. So don't hardcode conventions; **check in the moment**:

- If other skills already live in the same location, skim a few for recurring patterns (how language is specified, density, interview style, output format) and match the new skill to them. If there are none, skip this step.
- If an index document introducing the skill list already exists (a README, etc.), add the new skill's entry in the same format as the existing ones. Don't create one if it doesn't already exist.

## Language

Default to the language the user is making the request in — Korean if they write in Korean, English if they write in English, and so on. If the user explicitly specifies a different language (e.g. "write it in English"), follow that instead.

This same default applies to the "language" guidance of the skill being authored: when specifying what language a new skill's user-facing output should use, default to matching the user's request language and switching only on explicit request, unless there's a specific reason not to. A skill that must fix on one language for a deliberate reason (token efficiency, for example) is a legitimate exception — but state that reason in the body. That exception is a judgment call, not a reference to any particular skill.

## Post-draft check

Show the draft to the user and review together:
- Can you predict exactly when this skill will fire from the description alone?
- Did any code or project-specific file structure slip in?
- Is there anything written as procedure that should really be a judgment criterion — or anything written as loose judgment that's actually a fragile, order-sensitive task that deserves a tighter procedure?
- If other skills exist in the same collection, does this one match their conventions (language, density, interview pattern)?
