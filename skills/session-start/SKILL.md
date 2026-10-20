---
name: session-start
description: Use when the user's message is, or closely resembles (including typos/variants), "startsession" — e.g. "start session", "startsesion", "satrtsession", "start the session". Triggers a plain-language working mode for the rest of the conversation.
allowed-tools: Read Bash(git:*) Grep
---

# Session Start

## When to Use
- The user's message is the single word/phrase "startsession" in any casing
- The user's message is a close typo or spaced variant of it (e.g. "start sesion", "startsesion", "satrt session") — match by intent, not exact spelling
- Do not match this skill for a message that merely mentions "session" in passing ("let's end this session") — only an explicit start-trigger counts

## Instructions
1. Treat this message as a mode switch, not a task — don't ask "what do you mean?" Acknowledge briefly that session mode is on, then wait for (or use, if already given) the user's actual request.
2. For the rest of this conversation, when the user describes a problem or goal in plain language (no explicit command name, no step-by-step instructions from them), do the work directly:
   - Pick the most reasonable interpretation and act — don't ask them to specify which skill, command, or exact syntax to use.
   - If a task matches one of the other installed skills (`security-audit`, `secrets-handling`, `offline-first-workflow`, `safe-browser-agent`, `privacy-review`), apply it automatically rather than asking the user to invoke it by name.
   - "Fix it" / "clear it" / "sort this out" are complete instructions — proceed using your best judgment on scope, then summarize what you changed.
3. Still surface anything that genuinely needs a decision only the user can make (a destructive action, an ambiguous choice with real consequences) — plain-language mode means fewer procedural questions, not skipping judgment calls that matter.
4. Don't re-explain this mode on every subsequent message in the same conversation — it stays active until the conversation ends or the user says otherwise.

## Examples
**User:** "startsesion"
**Agent should:** Respond briefly that it's ready, in plain-language mode — no need to specify exact commands from here.

**User (later in the same conversation):** "this login form feels off, clean it up"
**Agent should:** Investigate the form, identify issues (validation, security, UX), fix them directly, and summarize the changes — without first asking the user to name which skill or exact steps to run.
