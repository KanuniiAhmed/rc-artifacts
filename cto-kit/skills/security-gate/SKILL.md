---
description: Run the adversarial CSO security review on the current change before accepting/committing it. Use before merging or committing anything that touches auth, secrets, IAM, networking, external/user input, dependencies, or deployment — or whenever the user asks for a security gate / CSO review. $ARGUMENTS may name a scope (a path, "the diff", "the plan").
---

Run a binding security gate on the change under review.

1. Determine the scope from `$ARGUMENTS` (default: the current working-tree diff — `git diff` plus staged changes; if not a git repo, the files changed this session). If reviewing a plan rather than code, review the plan text.
2. Dispatch the **`security-gate`** agent (the CSO) with that scope. Give it the diff/plan and the project's `CLAUDE.md` context so it can calibrate to the project's stage and stack.
3. Relay its verdict verbatim structure — **PASS / PASS WITH CONDITIONS / BLOCK** — with the numbered required changes (each `file:line` + concrete fix).
4. If the verdict is **BLOCK** or **PASS WITH CONDITIONS**, do not consider the change accepted until the must-fix items are resolved or the user explicitly overrides. Surface any override to the user.
5. Record the verdict in your summary so it's captured (and, for meaningful changes, worth persisting via `/cto-kit:memory-sync`).
