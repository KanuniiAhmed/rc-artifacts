---
description: Read-only spot-check of the LIVE deployed site/API — verify a just-shipped feature works in production, then a short random regression sweep. Strictly read-only (no edits, deploys, or data mutation). Use after a deploy or on a cadence. $ARGUMENTS should give the live base URL and/or what just shipped.
---

Run a live-production sentinel pass.

1. Take the live base URL and the just-shipped change from `$ARGUMENTS` (infer the change from recent commits if not given).
2. Dispatch the **`live-sentinel`** agent. It stays STRICTLY READ-ONLY — GET/curl + read-only reads only, cache-busted, realistic user + crawler user-agents.
3. It first proves the just-shipped feature works end-to-end against production (exact cache-busted URLs, expected vs actual), then does a short rotating regression sweep with cross-checks.
4. Relay its report: run summary, findings ranked `BROKEN / REGRESSION / SUSPECT / COSMETIC` (each with exact URL + expected vs actual), and coverage gaps for next run. If all healthy, say so plainly.
