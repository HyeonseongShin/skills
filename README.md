# Skills

A personal collection of [Agent Skills](https://agentskills.io) for AI coding agents (Claude Code, Cursor, OpenCode, Codex, and more).

Each skill lives in its own directory with a `SKILL.md` file describing when and how the agent should use it.

## Skills

### [grill-me](./grill-me/SKILL.md)

Proactively interviews you with focused, one-at-a-time questions before diving into implementation or design work. Surfaces blind spots, unstated assumptions, and missing constraints, then synthesizes the answers into an improved proposal.

Triggers automatically before non-trivial implementation, design, or decision-making tasks.

### [retrospective](./retrospective/SKILL.md)

Runs a structured post-task retrospective once a task is complete. Probes for skill gaps, decisions worth recording, friction points, and surprises, then produces skill update candidates, a decision log, next-task heads-up notes, and a context gap report.

Triggers when a task is marked done, a `plan.md` is about to be deleted, or on explicit request.

### [create-skill](./create-skill/SKILL.md)

Guides the design and authoring of a new agent skill that conforms to the agentskills.io spec. Treats skill-writing as a design task — confirms what judgment the skill should encode before drafting, and checks the result against spec and existing-collection conventions.

Triggers on requests like "make a skill", "create a skill for X", or "turn this workflow into a skill".

### [clean-code](./clean-code/SKILL.md)

Applies Clean Code judgment in real time while writing or refactoring: when to split a function, where to draw a class/file's SRP boundary, when a boolean flag argument means "two functions," and when duplicated code should be merged versus left alone.

Triggers while actively writing or modifying code — not for standalone bug-hunting, security, or whole-repo over-engineering review (those belong to other skills).

### [context-snapshot](./context-snapshot/SKILL.md)

Summarizes the current conversation into a compact, token-efficient context snapshot for carrying key decisions and progress into a fresh session. Outputs a structured Markdown summary (objective, decisions, constraints, status, references, glossary).

Triggers on requests like "save context" or "summarize for a new session".

## Usage

Install with the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
# Install all skills
npx skills add HyeonseongShin/skills

# Install a specific skill
npx skills add HyeonseongShin/skills --skill grill-me

# Install non-interactively to a specific agent
npx skills add HyeonseongShin/skills --skill grill-me -a claude-code -y
```

## License

[MIT](./LICENSE)
