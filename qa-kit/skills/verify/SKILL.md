---
description: Verify the current change actually behaves correctly end-to-end before accepting/committing it — write and RUN the tests, drive the real feature, report actual output. Use before merging non-trivial work, or when the user asks to verify/QA a change. $ARGUMENTS may name what changed or a scope.
---

Verify the change under review really works.

1. Determine what changed and its intended behavior from `$ARGUMENTS`, the working-tree diff, and the spec / `CLAUDE.md`. If the expected behavior is ambiguous, surface that gap first.
2. Dispatch the **`qa-verifier`** agent (or do it inline if small): write/extend tests at the right levels and **run them**, and drive the actual feature end-to-end — confirm the specific thing that was supposed to change did change, and cross-check a related surface.
3. Report what was run, pass/fail with **actual output**, coverage gaps, and any injection/edge cases relevant to untrusted input. Never report a pass that wasn't executed.
4. If anything fails, treat the change as not-yet-accepted and say what must be fixed.
