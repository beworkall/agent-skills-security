<div align="center">

# 🛡️ Security & Privacy Agent Skills

**Five sharp, single-purpose skills that make your AI coding agent actually security-aware.**

Built for Claude Code, Cursor, Codex, and anything else that reads `SKILL.md`.

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-6-5B8CFF)](skills)
[![Format](https://img.shields.io/badge/format-SKILL.md-black)](https://github.com/anthropics/skills)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

### [📦 Install in 10 seconds ↓](#install)

</div>

---

## Why this exists

Most agent-skills repos teach your agent to code faster. **None of them teach it to code safely.**

This pack fixes that — five focused skills covering the stuff that actually causes incidents:
leaking a secret, shipping an unaudited auth flow, an agent clicking "submit" on a form it
shouldn't have, or a feature quietly collecting data nobody consented to. Drop them in, and
your agent catches these automatically — you don't have to remember to ask.

## The skills

| Skill | What it catches |
|---|---|
| 🔍 [`security-audit`](skills/security-audit/SKILL.md) | Injection, auth flaws, unsafe deserialization — outputs a structured **Severity / Location / Recommendation** report, not vague "looks fine" |
| 🔐 [`secrets-handling`](skills/secrets-handling/SKILL.md) | API keys & passwords found in code — never logs real values, always routes to env vars / a secrets manager |
| 📴 [`offline-first-workflow`](skills/offline-first-workflow/SKILL.md) | Local-first storage design — pending-change logs, conflict resolution, no silent network dependency |
| 🌐 [`safe-browser-agent`](skills/safe-browser-agent/SKILL.md) | A browsing agent about to submit sensitive data — forces a confirmation step before anything irreversible |
| 🕵️ [`privacy-review`](skills/privacy-review/SKILL.md) | Over-collection, missing consent, silent trackers — fast ✅ / ⚠️ / ❌ checklist, not a 10-paragraph essay |
| ⚡ [`session-start`](skills/session-start/SKILL.md) | Say **"startsession"** (typos forgiven) and the agent switches to plain-language mode — act on vague requests directly, no need to name a skill or give exact commands |

Each skill's `description` is written as a concrete trigger, so your agent loads the right one
automatically — you never have to invoke anything by name.

## Install

**One-liner (any `npx skills`-compatible agent):**
```bash
npx skills@latest add beworkall/agent-skills-security
```

**Manual — Claude Code:**
```bash
git clone https://github.com/beworkall/agent-skills-security.git
cp -r agent-skills-security/skills/* ~/.claude/skills/
```

**Cursor / Codex / anything else:** copy whichever `skills/<name>/SKILL.md` you want into your
project's skills or rules directory — no Claude-specific syntax, fully portable.

## Try it

```
"Can you audit this login endpoint for security issues?"
"Here's my API key, write a function that uses it."
"I want this app to work offline and sync later."
"Log into my account and update my shipping address."
"Quick privacy pass on our signup flow before launch."
"startsession"
```
Each one triggers the matching skill automatically — see [`examples/prompts.md`](examples/prompts.md)
for the full list.

## How a skill is built

```yaml
---
name: kebab-case-name
description: The ONLY thing the agent reads before deciding to load this. Be specific about when to use it.
---
```
Numbered steps, not essays. A concrete output format. No skill here does anything your agent
couldn't already do — they just make it do it *consistently*, every time, without you having to ask.

## Contributing

PRs welcome, especially real-world refinements from actually using these day to day. Keep the
same shape: one clear trigger, numbered steps, a concrete output format. Open an issue first for
anything bigger than a tweak.

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, ship it in your own stack.

---

<div align="center">
<sub>Built by <a href="https://github.com/beworkall">@beworkall</a> — star it if it saved you a security review 🙌</sub>
</div>
