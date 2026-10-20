---
name: privacy-review
description: Use when reviewing a codebase, feature, or data flow for privacy issues — unnecessary data collection, missing consent, third-party trackers, or logs that shouldn't exist.
allowed-tools: Read Grep
---

# Privacy Review

## When to Use
- The user asks for a privacy review before shipping a feature
- Reviewing code that collects, stores, logs, or transmits user data
- Auditing third-party SDKs/scripts added to a project

## Instructions
Run this as a short checklist — keep it fast, not exhaustive prose.

1. **Data minimization**: for each piece of user data collected, confirm it is actually used for a stated purpose. Flag anything collected "just in case."
2. **Logging**: check whether logs capture anything sensitive — emails, IPs tied to identity, auth tokens, full request/response bodies on user-data endpoints. Logs are a common accidental leak point.
3. **Consent**: if data collection falls into a category that typically needs consent (analytics, marketing, location, biometric, third-party sharing), confirm a consent step exists before collection, not after.
4. **Third parties**: list every third-party SDK/script/pixel present and what data each can access. Flag any with broad access (e.g., a full-page tracking script) relative to its stated purpose.
5. **Retention**: check whether there's any defined deletion/retention policy for collected data, or whether it's kept indefinitely by default.
6. **Sharing boundary**: confirm user data isn't sent to a third-party endpoint as a side effect of an unrelated feature (e.g., an analytics call that accidentally includes a full user object).
7. Output findings as a short checklist with ✅ / ⚠️ / ❌ per item — don't write paragraphs per point.

## Examples
**User:** "Can you do a quick privacy pass on our signup flow before we launch?"
**Agent should:** Check what fields are collected and whether all are necessary, whether the analytics call sends more than needed, whether a privacy policy/consent checkbox exists, and return a short ✅/⚠️/❌ checklist — not a long essay.
