---
description: Review a frontend/UI change against the design-system discipline — token-only styling (no stray hex/px), reusable primitives, dark-mode-first contrast, CSS logical properties for RTL, zero CLS, and CSP-safe rendering. Use on any UI diff, or when the user asks for a design review. $ARGUMENTS may name files/components in scope.
---

Review the UI change for design-system compliance.

1. Read the project's own design contract first (`DESIGN.md` / tokens file / `CLAUDE.md`) so you enforce its palette and primitives, not generic taste.
2. Dispatch the **`design-steward`** agent (or review inline if small) over the changed UI files from `$ARGUMENTS` / the diff.
3. Check: tokens only (flag raw hex/px and one-off styles), reuse of primitives (flag re-implemented cards/badges/lists), loading + empty states present, dark-mode contrast, **CSS logical properties only** (flag hardcoded left/right), **zero CLS** (reserved space, transform/opacity motion, reduced-motion), and **CSP safety** (no `dangerouslySetInnerHTML` of untrusted content, JSON-LD built from escaped typed fields).
4. Report pass/fail per rule with `file:line` and the minimal fix; flag anything needing a new token or a design decision for the user.
