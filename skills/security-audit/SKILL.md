---
name: security-audit
description: Use when reviewing code for security issues, checking for injection/auth flaws, exposed secrets, unsafe deserialization, or when the user asks for a security audit or vulnerability review.
allowed-tools: Read Grep Bash(git:*)
---

# Security Audit

## When to Use
- The user asks for a security review, audit, or "check this for vulnerabilities"
- Before merging code that touches auth, input handling, file I/O, or external requests
- When reviewing a PR/diff that adds a new API endpoint, form, or data parser

## Instructions
1. Scope the review: identify every file that handles user input, auth, file paths, database queries, or external calls. Don't review the whole repo blindly — focus there first.
2. Check for these categories, in order:
   - **Injection**: SQL/NoSQL/command/template injection — any place user input reaches a query, shell command, or eval-like function without parameterization or sanitization.
   - **Auth & session flaws**: missing authorization checks, predictable tokens, session fixation, privilege escalation paths.
   - **Secrets exposure**: hardcoded keys/passwords, secrets in logs, secrets in client-side/bundled code.
   - **Unsafe deserialization**: `pickle`, `eval`, unchecked `JSON.parse` of untrusted data feeding into object construction.
   - **Input validation**: missing length/type/format checks on anything from a user, URL, or external API.
   - **Dependency risk**: flag outdated or known-vulnerable packages if a lockfile/manifest is visible.
3. For each finding, do not just say "looks risky" — confirm the actual code path: trace the input from its source to the vulnerable sink before reporting it.
4. Never attempt to exploit, run, or demonstrate the vulnerability. Describe it; don't weaponize it.
5. Output a structured report, not prose. Use this exact format per finding:
   ```
   ## [SEVERITY] <short title>
   **Location:** file:line
   **Issue:** what's wrong, in one or two sentences
   **Recommendation:** the specific fix
   ```
   Severity is one of: CRITICAL, HIGH, MEDIUM, LOW, INFO.
6. End with a one-line summary: total findings by severity, and whether the code is safe to merge as-is.

## Examples
**User:** "Can you audit this login endpoint for security issues?"
**Agent should:** Trace how the password/token flows from request to storage/comparison, check for timing-safe comparison, rate limiting, and SQL parameterization, then output the structured report format above — not a paragraph of general advice.
