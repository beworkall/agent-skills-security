---
name: offline-first-workflow
description: Use when designing or reviewing a feature/app that should work without a network connection, or when the user asks for offline support, local-first storage, or sync-later behavior.
allowed-tools: Read
---

# Offline-First Workflow

## When to Use
- The user asks for an app/feature to "work offline" or be "local-first"
- Designing data storage for a mobile/desktop app that may lose connectivity
- Reviewing an architecture that currently assumes constant network access

## Instructions
1. Identify the source of truth: for offline-first, the **local store is authoritative for the user's immediate experience** — the network is a sync target, not a dependency for reads/writes to work.
2. Design storage choice by data shape: structured relational data → embedded SQL (SQLite/Room/Core Data); simple key-value → local key-value store; large blobs/files → local filesystem with a manifest.
3. For anything that will eventually sync to a server, record a local **pending-change log** (operation + timestamp + entity id) rather than only the current state — this is what makes later sync and conflict resolution possible.
4. Conflict resolution: pick and state one explicit strategy up front — last-write-wins (simplest, acceptable for single-user data), or field-level merge (needed for multi-device/multi-user). Don't leave it undecided.
5. Network calls must be wrapped so failure is a normal, handled path, not an exception that breaks the feature — queue the action locally and retry when connectivity returns, rather than blocking the user.
6. Never require a network round-trip for an action the user expects to be instant (saving a note, marking something done). Write locally first, sync in the background.
7. State explicitly which features (if any) genuinely cannot work offline (e.g., real-time collaboration, payment processing) rather than implying everything can.

## Examples
**User:** "I want my notes app to work without internet and sync when it's back online."
**Agent should:** Recommend SQLite as local source of truth, a pending-change log for edits made offline, last-write-wins for single-user sync, and background retry on reconnect — not a design that treats the server as required for basic save/load.
