---
description: Audit infrastructure for cost-runaway and safety before applying it (or to review already-running infra). Use before terraform/CDK/CLI apply, or when the user asks about cloud cost, budget guardrails, auto-shutdown, or teardown. $ARGUMENTS may name a scope (an IaC path, "the terraform", "running infra").
---

Run a cloud cost & infra-safety audit.

1. Determine the scope from `$ARGUMENTS` (default: infrastructure code in the repo — Terraform/CDK/CloudFormation/CLI scripts — plus any changed infra files this session).
2. Dispatch the **`cost-guardian`** agent with that scope and the project's stated budget cap if one is documented (check `CLAUDE.md` / memory).
3. Relay its verdict — **SAFE TO APPLY / APPLY WITH CHANGES / DO NOT APPLY** — with numbered required changes (`file:line` + fix), the **estimated monthly cost**, the **worst-case runaway cost** if a guardrail is missing, and the exact apply + destroy commands.
4. Do not apply infrastructure that gets DO NOT APPLY until the required changes land, or the user explicitly overrides.
