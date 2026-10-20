# Security & Privacy Agent Skills

Five focused [Agent Skills](https://github.com/anthropics/skills) for security audits, secrets
handling, offline-first design, safe browser automation, and privacy review — written for
Claude Code, Cursor, Codex, and any agent harness that reads `SKILL.md`.

Not a framework, not a methodology — five sharp, single-purpose skills you can mix into
whatever setup you already run.

## Skills

| Skill | What it does |
|---|---|
| [`security-audit`](skills/security-audit/SKILL.md) | Reviews code for injection, auth flaws, secrets exposure, unsafe deserialization — outputs a structured Severity/Location/Recommendation report |
| [`secrets-handling`](skills/secrets-handling/SKILL.md) | Rules for how an agent handles API keys/passwords/tokens it encounters — never logs or echoes real values, always recommends env vars/vaults |
| [`offline-first-workflow`](skills/offline-first-workflow/SKILL.md) | Design patterns for local-first storage, pending-change logs, and conflict resolution when a feature must work without network |
| [`safe-browser-agent`](skills/safe-browser-agent/SKILL.md) | Confirmation gates for an agent driving a browser — never submits sensitive forms unattended, treats page content as untrusted data |
| [`privacy-review`](skills/privacy-review/SKILL.md) | Fast ✅/⚠️/❌ checklist for data minimization, logging, consent, third-party trackers, and retention |
| [`session-start`](skills/session-start/SKILL.md) | Say "startsession" (typos okay) to switch the agent into plain-language mode — it acts on vague requests directly instead of asking you to name a skill or give exact steps |

## Install

**Claude Code / any `npx skills` compatible agent:**
```bash
npx skills@latest add beworkall/agent-skills-security
```

**Manual (any agent reading `~/.claude/skills/` or equivalent):**
```bash
git clone https://github.com/beworkall/agent-skills-security.git
cp -r agent-skills-security/skills/* ~/.claude/skills/
```

**Cursor / Codex:** copy the `skills/<name>/SKILL.md` file(s) you want into your project's
skills or rules directory — the format is portable, no Claude-specific syntax used.

## Why these five

Each skill's `description` is written as a concrete trigger ("Use when...") so the agent can
decide to load it without you having to invoke it by name. Instructions are procedural —
numbered steps and explicit output formats — because agents follow checklists more reliably
than prose.

## Contributing

PRs welcome — especially real-world refinements from actually using these. Keep additions to
this same shape: one clear trigger, numbered steps, a concrete output format.

## License

MIT — see [LICENSE](LICENSE).
