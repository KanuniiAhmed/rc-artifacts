---
description: Run a WCAG 2.2 AA accessibility gate on a page or component — keyboard operability, focus management, semantics/ARIA, dark-mode contrast, reduced-motion, live-region announcements, and RTL/bidi. Use as a release gate on UI changes. $ARGUMENTS may name a component, page, or live URL.
---

Run the accessibility release gate.

1. Take the target (component/page/live URL) from `$ARGUMENTS` or the current UI diff.
2. Dispatch the **`a11y-gate`** agent. Verify against WCAG 2.2 AA: keyboard (focus, tab order, no traps, skip links), semantics-first (real tables, labeled forms, ARIA only to fill gaps), live/async regions (polite `aria-live`, no color-only state, no layout shift), contrast in dark mode, reduced-motion, and RTL reading/focus order.
3. Prefer automated (axe/Lighthouse) **plus** a manual keyboard + screen-reader reasoning pass of the key flow.
4. Report **PASS / PASS WITH CONDITIONS / BLOCK** with each finding tied to a specific WCAG success criterion and the minimal semantic fix. Escalate a11y-security overlaps to the security-gate.
