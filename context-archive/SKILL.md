---
name: context-archive
description: Summarizes the current conversation into a compact, token-efficient context snapshot. Use when the user asks to "save context", "summarize for a new session", or wants to carry key decisions and progress into a fresh chat.
---

When the user asks to "save context" or "summarize for a new session," ALWAYS output the response strictly in the following Markdown format.

## Constraints

1. Language: English (for token efficiency).
2. Style: Noun-phrase endings only. No full sentences. No fluff.
3. Goal: Minimize token count while preserving core logic and decisions.

## Output Structure

```
# Context Summary: [Project Name]
## 1. Core Objective: [Main goal]
## 2. Key Decisions: [Bullet points of finalized items]
## 3. Constraints & Rules: [Preferences, tech stack, tone rules]
## 4. Current Status: [Current progress + Next immediate task]
## 5. Key References: [Vital data/values]
## 6. Glossary & Inferences: [Custom terms + "~It seems" deductions]
```


