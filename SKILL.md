---
name: web-accessibility
version: 1.0.0
description: >
  Build and review accessible web applications conforming to WCAG 2.2 AA and the
  German/European legal framework (BFSG, EAA / EU Directive 2019/882, EN 301 549).
  Use this skill WHENEVER the user works on web UI and any of these apply: they ask
  to make something "barrierefrei" / accessible / WCAG-conform / BFSG-conform; they
  ask for an accessibility review, audit, or check of HTML/JSX/CSS/components; they
  build forms, modals, dialogs, menus, tabs, accordions, custom widgets, navigation,
  focus handling, or color/contrast decisions; they mention screen readers, keyboard
  navigation, ARIA, semantic HTML, focus indicators, alt text, or touch target sizes;
  or they ask whether code meets WCAG / EN 301 549 / BFSG. Works framework-agnostic
  (plain HTML, React, Vue, Svelte, Angular) with a React focus. Trigger this even when
  the user does not say the word "accessibility" but is clearly building interactive
  web UI that needs to be operable by keyboard and assistive technology.
---

# Web Accessibility (DE/EU): Build & Review

This skill helps with two tasks, sharing one knowledge base:

1. **Development** — writing accessible web UI from the start (correct semantics, ARIA, focus, contrast, keyboard support).
2. **Review** — auditing existing HTML/JSX/CSS/components against WCAG 2.2 AA and flagging issues with concrete fixes.

The skill is framework-agnostic with a React focus. Output goes in the chat by default (no file is produced unless the user asks).

## Default conformance target

Use **WCAG 2.2 Level AA** as the default standard. Rationale and the precise legal status are below in "Legal context". Key rule for annotations:

- Criteria that exist in **WCAG 2.1** (i.e. carried into 2.2) are the current **legal minimum** in the EU/Germany, because EN 301 549 v3.2.1 (the harmonised standard referenced by the EAA/BFSG) incorporates WCAG 2.1 AA. Mark these **[Required]**.
- The **9 criteria new in WCAG 2.2** are **not yet legally mandated** (EN 301 549 v4.1.1, which will reference WCAG 2.2, is expected but not yet referenced in the EU Official Journal). Mark these **[Recommended, soon required]**.
- AAA criteria are always **[Optional/AAA]** unless the user explicitly targets AAA.

When in doubt about a criterion's level or legal weight, consult `references/wcag-criteria.md` rather than guessing.

## Choosing the mode

Read the user's request and pick the matching workflow. If the request mixes both (e.g. "build an accessible modal and tell me what to watch out for"), do both: build first, then summarise the conformance notes.

| Signal in the request | Mode |
|---|---|
| "review", "audit", "check", "prüfe", pasted code to evaluate, "is this accessible?" | Review |
| "build", "write", "create", "implement", "how do I make X accessible?", "baue" | Development |
| Both verbs, or "build X and review it" | Both |

## Workflow: Review

1. **Identify scope.** What was given: a component, a page, a snippet? Note the framework.
2. **Walk the review matrix.** Read `references/review-matrix.md` and check each relevant category against the code. Do not invent issues; only flag what the code actually shows. If a category cannot be judged from static code (e.g. screen-reader behaviour, real zoom rendering), say so explicitly and mark it as "needs manual/AT testing".
3. **For each finding, report:**
   - The problem, in plain language.
   - The affected WCAG success criterion with **level (A/AA/AAA)** and **annotation** ([Required] / [Recommended, soon required] / [Optional/AAA]).
   - A concrete fix with corrected code.
4. **Order findings by severity:** blockers (Level A failures, keyboard traps, missing names) first, then AA, then enhancements.
5. **State the limits.** Automated/static review catches only part of the picture (axe-core fully automates ~30% of criteria). Always note which checks still require keyboard, screen-reader, and zoom testing by a human.

Use `assets/review-template.md` as the output structure. Keep it in the chat unless the user asks for a file.

## Workflow: Development

1. **Prefer native HTML.** Use `<button>`, `<a href>`, `<nav>`, `<main>`, `<label for>`, native form controls. Reach for ARIA only when no native element fits. See `references/knowledge-base.md` → SEMANTIC_HTML and ARIA.
2. **Follow the established pattern.** For composite widgets (modal, combobox, tabs, accordion, menu), follow the ARIA Authoring Practices Guide (APG) keyboard and role conventions. Don't improvise keyboard handling.
3. **Bake in the essentials as you write:**
   - Every interactive element reachable and operable by keyboard, with a visible focus indicator (never remove `outline` without an equivalent replacement).
   - Every form field has a programmatically associated visible label; errors linked via `aria-describedby` / `aria-errormessage` with `aria-invalid`.
   - Text contrast ≥ 4.5:1 (≥ 3:1 for large text and UI components/focus).
   - Touch/pointer targets ≥ 24×24px (WCAG 2.2 AA minimum; 44×44px recommended).
   - Layout uses relative units and reflows at 200%/400% zoom without horizontal scroll.
   - `prefers-reduced-motion` respected for animation.
4. **Annotate the WCAG criteria** your implementation satisfies, with level and Required/Recommended annotation, so the user understands the legal relevance.
5. **Note what still needs verification** (screen-reader testing, real zoom, AT combinations).

For React specifically, read `references/framework-notes.md` (focus management on route change, `useId`, refs for focus, portals for modals, `dangerouslySetInnerHTML` caveats).

## Knowledge sources (read as needed)

- `references/review-matrix.md` — 12-category audit checklist with WCAG mapping. Primary tool for **Review** mode.
- `references/knowledge-base.md` — deep reference per topic: requirements, implementation, common failures, testing, edge cases. Use in **both** modes for detail.
- `references/wcag-criteria.md` — authoritative list of relevant success criteria with level + Required/Recommended annotation. Consult before annotating any criterion.
- `references/framework-notes.md` — React-first, plus Vue/Svelte/Angular and plain-HTML notes.
- `assets/review-template.md` — output structure for review reports.

## Legal context (DE/EU), briefly

- **BFSG** (Barrierefreiheitsstärkungsgesetz) is in force since **28 June 2025**. It transposes the **EAA** (EU Directive 2019/882). Source of the technical bar: **EN 301 549**, which the EAA references.
- Scope: B2C digital services and products (e-commerce/online shops, banking, e-books, telecommunications, passenger transport, computers, self-service terminals, etc.). **Kleinstunternehmen** (< 10 employees AND ≤ €2M annual turnover or balance sheet) are exempt **for services** — but not when they place covered products on the market.
- Enforcement: fines up to **€100,000**; market surveillance by the Länder; competitors/qualified bodies can issue warnings (Abmahnung).
- Standard status (as of mid-2026): EN 301 549 **v3.2.1** is the referenced version and incorporates **WCAG 2.1 AA** → that is the legal minimum. The next version (**v4.1.1**, expected 2026) will reference **WCAG 2.2**, but is not yet referenced in the Official Journal. WCAG 2.2 itself is also ISO/IEC 40500:2025.
- This is general information, **not legal advice**. For a binding assessment, point the user to the Bundesfachstelle Barrierefreiheit or a qualified lawyer.

## Hard rules

- Never claim code "is BFSG/WCAG compliant" from static inspection alone. Conformance requires manual + AT testing. State conformance as "meets criterion X in this code" or "no static violation found", not as a guarantee.
- Never remove a focus indicator without providing a visible replacement.
- Never use `aria-hidden="true"` on a focusable/interactive element.
- Prefer native HTML over ARIA every time a native element exists.
- Do not present AAA criteria as legally required.
