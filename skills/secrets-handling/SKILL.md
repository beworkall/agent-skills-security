---
name: secrets-handling
description: Use when the agent encounters API keys, passwords, tokens, or other credentials in code, config files, or conversation, or when asked how to store/manage secrets.
allowed-tools: Read Grep
---

# Secrets Handling

## When to Use
- A credential (API key, password, token, private key, connection string) appears in code, a file, or the conversation
- The user asks how to store, rotate, or manage secrets
- Writing code that needs to read a credential at runtime

## Instructions
1. **Never print, log, or echo the actual value of a secret** — not even partially, not even in an example, not even to confirm "yes I see it." Refer to it as "the API key" or "the credential," never its characters.
2. If a secret is found hardcoded in source: flag it as a finding (don't just quietly fix it), explain the risk, and recommend moving it to an environment variable or a secrets manager appropriate to the stack (`.env` + `.gitignore` for local/small projects; a managed vault — AWS Secrets Manager, GCP Secret Manager, Vault — for production).
3. When writing new code that needs a credential, always read it from environment/config injection (`os.getenv`, `process.env`, a secrets-manager client) — never write a literal value into source, even as a placeholder that "looks like" a real key format.
4. If a secret may have already been committed to git history, say so explicitly and recommend rotating the credential — removing it from the latest commit is not enough since it remains in history.
5. Recommend `.gitignore` entries for any secret-bearing file (`.env`, `*.pem`, `credentials.json`, etc.) when creating one.
6. When a user pastes a real-looking credential into chat, don't repeat it back verbatim in your response, even to confirm receipt — acknowledge it generically and proceed.

## Examples
**User:** "Here's my Stripe key: sk_live_abc123... can you write a function to charge a customer?"
**Agent should:** Write the charge function reading the key from an environment variable, note that a live key should never be pasted into chat or committed to source, and recommend rotating it if it has been exposed. Does not repeat the key value back.
