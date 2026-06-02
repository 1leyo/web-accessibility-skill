# web-accessibility

A Claude skill for building and reviewing accessible web applications, targeting WCAG 2.2 AA
and the German/European legal framework (BFSG, EAA / EU Directive 2019/882, EN 301 549).

## What it does

The skill operates in two modes and picks the right one based on your request:

**Development mode** -- triggered by requests like "build an accessible modal", "how do I make this form accessible?", "implement a skip link":
- Writes accessible HTML/JSX/CSS from the start using correct semantics, ARIA, keyboard handling, and focus management
- Annotates each implementation decision with the relevant WCAG success criterion, its level (A/AA/AAA), and its legal relevance under the current EU/German framework

**Review mode** -- triggered by requests like "review this for accessibility", "check this component against WCAG", "is this BFSG-compliant?":
- Walks a structured 12-category audit checklist (keyboard, focus, forms, ARIA, screen reader, contrast, target size, zoom, media, validation, navigation, authentication)
- Reports each finding with the affected criterion, its level, and a concrete code fix
- Clearly marks what cannot be verified from static code alone and requires manual keyboard, screen reader, and zoom testing

Both modes apply the same conformance standard and annotation system.

## Conformance target

Default: **WCAG 2.2 Level AA**

Criteria are annotated to reflect the current legal situation in the EU/Germany:

| Annotation | Meaning |
|---|---|
| [Required] | Criterion exists in WCAG 2.1 -- current legal minimum via EN 301 549 v3.2.1 |
| [Recommended, soon required] | New in WCAG 2.2 -- recommended now, expected to become mandatory with EN 301 549 v4.1.1 |
| [Optional/AAA] | Level AAA -- not legally required |

## Scope

The skill is framework-agnostic with a React focus. It also covers Vue, Svelte, Angular, and plain HTML/CSS/JS. See `references/framework-notes.md`.

## Installation

**From a `.skill` file:**

```bash
claude skill install web-accessibility.skill
```

**From this repository:**

```bash
git clone https://github.com/1leyo/web-accessibility-skill
claude skill install ./web-accessibility
```

## Usage examples

```
"Review this LoginForm component for accessibility."
"Build an accessible modal dialog in React."
"Is using aria-hidden here correct?"
"What WCAG criteria apply to my error messages?"
"Does this form meet BFSG requirements?"
```

## File structure

```
accessibility/
+-- SKILL.md                        Entrypoint, workflow logic, legal context
+-- references/
|   +-- review-matrix.md            12-category audit checklist with WCAG mapping
|   +-- knowledge-base.md           Deep reference per topic
|   +-- wcag-criteria.md            Authoritative criteria list with level and annotation
|   +-- framework-notes.md          React-first, plus Vue/Svelte/Angular/plain HTML
+-- assets/
    +-- review-template.md          Output structure for review reports
```

## Legal context (brief)

The BFSG (Barrierefreiheitsstarkungsgesetz) has been in force in Germany since 28 June 2025.
It transposes the European Accessibility Act (EU Directive 2019/882). The technical standard
it references is EN 301 549 v3.2.1, which incorporates WCAG 2.1 AA. The next version of
EN 301 549 (v4.1.1) is expected to reference WCAG 2.2, but has not yet been cited in the
EU Official Journal as of the time of writing.

For public-sector organizations in Germany, BGG and BITV 2.0 continue to apply.

## Disclaimer

This skill is provided for informational and development-assistance purposes only.

It is not legal advice. The author is not a lawyer and makes no representations about
the legal sufficiency of any output produced with this skill.

Using this skill does not guarantee that your application will be legally compliant with
the BFSG, the European Accessibility Act, EN 301 549, WCAG, BITV 2.0, or any other
accessibility standard or regulation. True conformance requires:

- Manual testing by a qualified accessibility specialist
- Testing with real assistive technologies across multiple browser and screen reader combinations
- Keyboard-only and zoom testing
- Where applicable, testing with disabled users
- A formal conformance evaluation following the WCAG-EM methodology

Static code analysis and AI-assisted review, including this skill, catch only a subset of
accessibility issues. They are a development aid, not a substitute for professional
accessibility auditing or legal counsel.

If you require a binding assessment of your product's compliance with accessibility law,
consult a qualified lawyer or a certified accessibility auditor.

For general guidance on BFSG obligations, the [Bundesfachstelle Barrierefreiheit](https://www.bundesfachstelle-barrierefreiheit.de) is a good starting point.

## Contributing

Issues and pull requests are welcome. If you find a factual error in the WCAG criteria,
legal context, or code examples, please open an issue with a reference to the relevant
specification or source.

## License

MIT
