# rc-artifacts — reusable Claude Code assets

A personal **plugin marketplace**: proven patterns from real projects, packaged so any current or future project can install them. It grows over time — each time a pattern proves itself across projects, it becomes an installable plugin here.

> Origin: two independent side projects — a web app and a media-processing service — evolved the same engineering roles: a CTO orchestrator, an adversarial security reviewer that can block, and a cost-disciplined DevOps guardian. That convergence is the signal that these belong in a shared, reusable place instead of being re-invented per project.

## Install (once, then usable everywhere)

```bash
# from any Claude Code session — from a local clone:
/plugin marketplace add <path-to-your-clone>/artifcats
# ...or straight from GitHub once published:
/plugin marketplace add <github-user>/rc-artifacts

/plugin install cto-kit@rc-artifacts
/plugin install qa-kit@rc-artifacts
/plugin install design-kit@rc-artifacts
```

Or, for a quick tryout without installing:

```bash
claude --plugin-dir <path-to-your-clone>/artifcats/cto-kit
```

After install, reload with `/reload-plugins` if needed. Skills are namespaced as `/<plugin>:<name>`.

## Plugins

### `cto-kit` — solo-founder engineering discipline
Portable versions of the roles/gates that emerged in both projects.

**Agents** (spawn via the Task tool or let `orchestrator` dispatch them):
- `security-gate` — adversarial CSO. Read-only. Returns a binding **PASS / PASS-WITH-CONDITIONS / BLOCK** verdict on anything touching auth, secrets, IAM, input trust, deps, or deploy.
- `cost-guardian` — cloud cost & infra-safety reviewer. Enforces budget alarms, auto-shutdown, least-privilege, tagging, one-command teardown; reports estimated + worst-case monthly cost.
- `orchestrator` — CTO-style lead. Decomposes work, dispatches specialists in parallel, enforces the security + cost gates, and persists learnings.

**Skills** (`/cto-kit:<name>`):
- `/cto-kit:security-gate [scope]` — run the CSO review on the current diff/plan.
- `/cto-kit:cost-check [scope]` — audit infra for cost runaway before apply.
- `/cto-kit:memory-sync` — capture durable, non-obvious knowledge into project memory (one fact per file + `MEMORY.md` index).

### `qa-kit` — test & QA discipline
Distilled from QA patterns proven across real projects.

**Agents:** `qa-verifier` (writes & RUNS tests, drives the real feature, never claims an unrun pass) · `live-sentinel` (strictly read-only production spot-check, cache-busted, adversarial cross-checks, severity-ranked findings).

**Skills:** `/qa-kit:verify [scope]` — verify the current change end-to-end · `/qa-kit:live-check <url>` — read-only live-production sentinel pass.

### `design-kit` — frontend design-system discipline
Brand-neutral method distilled from frontend + accessibility patterns proven on real products. Defers to each project's own `DESIGN.md`.

**Agents:** `design-steward` (token-only, dark-mode-first, RTL via logical properties, zero CLS, CSP-safe; defers to the project's own `DESIGN.md`) · `a11y-gate` (WCAG 2.2 AA release gate).

**Skills:** `/design-kit:design-review [scope]` — review a UI diff against the design system · `/design-kit:a11y-check [target]` — WCAG 2.2 AA gate on a page/component.

> Scope note: `design-kit` owns the *application* design system. For chart/dashboard color use the built-in `dataviz` skill; for standalone artifact pages use `artifact-design`.

## Adding a new artifact (the "keep doing it" process)
When a pattern proves useful across ≥2 projects (or the user asks to capture one):
1. Create `./<plugin-name>/.claude-plugin/plugin.json` + its `agents/`, `skills/`, `hooks/`.
2. Add an entry to `.claude-plugin/marketplace.json`.
3. Test it (load with `--plugin-dir`, invoke a skill/agent).
4. Bump versions and update this README.
5. Record it in memory so other sessions discover it (see `MEMORY.md` in this project's memory dir).
