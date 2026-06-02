# Review Output Template

Use this structure for review output. Keep it in the chat unless the user asks for a file.
Adapt length to the input: a small snippet gets a short report, a full page gets the complete structure.

---

## Accessibility Review: [component/page name]

**Scope reviewed:** [what was given — file, component, snippet] · **Framework:** [detected] · **Target:** WCAG 2.2 AA

### Summary

[1–3 sentences: overall state, number of blockers/AA issues/enhancements found.]

### Findings

Ordered by severity (blockers → AA → enhancements). For each:

#### [n]. [Short title] — [Blocker / AA / Enhancement]

- **Problem:** [plain-language description of what's wrong and who it affects]
- **Criterion:** [e.g. 2.1.1 Keyboard (A) — [Required]]
- **Fix:**

```[lang]
// corrected code
```

[Repeat per finding.]

### Could not verify from static code

[List checks that require manual testing: screen-reader behaviour across browser/SR combos,
real 200%/400% zoom rendering, actual focus visibility, AT announcements. State that these
remain open and require keyboard + screen-reader + zoom testing by a human.]

### Conformance note

[Plain statement of legal relevance: which failures are [Required] (WCAG 2.1 → EN 301 549 →
BFSG/EAA legal minimum) vs [Recommended, soon required] (new in 2.2). Remind that static review
is not a conformance guarantee and this is not legal advice.]
