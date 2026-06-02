# Review Matrix

The 12-category audit checklist. For each category: what to check, why it matters, and the
mapped WCAG success criteria with level and legal annotation.

Annotation legend:
- **[Required]** — in WCAG 2.1, therefore current EU/DE legal minimum via EN 301 549 v3.2.1.
- **[Recommended, soon required]** — new in WCAG 2.2, recommended now, expected to become mandatory with EN 301 549 v4.1.1.
- **[Optional/AAA]** — Level AAA, not legally required.

Cross-check every criterion's level against `wcag-criteria.md` before reporting.

## 1. Keyboard

**Check:** All interactive elements reachable and operable via keyboard (Tab/Shift+Tab, Enter/Space, arrows where applicable). Logical tab order. No keyboard traps.
**Why:** Motor-impairment and screen-reader users depend entirely on the keyboard.

| Criterion | Level | Annotation |
|---|---|---|
| 2.1.1 Keyboard | A | [Required] |
| 2.1.2 No Keyboard Trap | A | [Required] |

## 2. Focus

**Check:** Focus is always visible, indicator ≥ 2px with ≥ 3:1 contrast against adjacent colors, and the focused element is not fully hidden by other content (sticky headers, overlays).
**Why:** Low-vision and keyboard users must be able to track their position.

| Criterion | Level | Annotation |
|---|---|---|
| 2.4.7 Focus Visible | AA | [Required] |
| 2.4.11 Focus Not Obscured (Minimum) | AA | [Recommended, soon required] |
| 2.4.13 Focus Appearance | AAA | [Optional/AAA] |

## 3. Forms

**Check:** Every field has a visible, programmatically associated label. Errors are concrete, solution-oriented, and linked via `aria-describedby` / `aria-errormessage` with `aria-invalid="true"`. No placeholder-as-label.
**Why:** Labels provide context; linked errors enable correction.

| Criterion | Level | Annotation |
|---|---|---|
| 3.3.1 Error Identification | A | [Required] |
| 3.3.2 Labels or Instructions | A | [Required] |
| 3.3.3 Error Suggestion | AA | [Required] |
| 4.1.2 Name, Role, Value | A | [Required] |

## 4. ARIA

**Check:** Native HTML used wherever possible; ARIA only when no native element fits. All interactive elements have an accessible name. No `aria-hidden` on interactive elements. ARIA widgets follow APG keyboard patterns.
**Why:** Native elements have reliable built-in support; misused ARIA actively harms.

| Criterion | Level | Annotation |
|---|---|---|
| 4.1.2 Name, Role, Value | A | [Required] |
| 4.1.3 Status Messages | AA | [Required] |

## 5. Screen Reader

**Check:** Content is meaningful when linearised; non-text content has text alternatives; structure (headings, landmarks, lists) is conveyed. Verify with multiple browser/screen-reader combinations.
**Why:** Different browser/SR combinations behave differently; static code cannot confirm this — flag for manual AT testing.

| Criterion | Level | Annotation |
|---|---|---|
| 1.1.1 Non-text Content | A | [Required] |
| 2.4.1 Bypass Blocks | A | [Required] |
| 1.3.1 Info and Relationships | A | [Required] |

## 6. Contrast

**Check:** Body text ≥ 4.5:1; large text ≥ 3:1; UI components and focus indicators ≥ 3:1. Color is never the sole means of conveying information. "Large text" = ≥ 18pt (≈ 24px) any weight, or ≥ 14pt bold (≈ 18.66px).
**Why:** Low-vision and aging users need sufficient contrast.

| Criterion | Level | Annotation |
|---|---|---|
| 1.4.1 Use of Color | A | [Required] |
| 1.4.3 Contrast (Minimum) | AA | [Required] |
| 1.4.11 Non-text Contrast | AA | [Required] |

## 7. Target Size / Responsive

**Check:** Pointer targets ≥ 24×24px (or sufficient spacing per the 2.2 exception); 44×44px recommended. Drag-only interactions have a single-pointer alternative.
**Why:** Motor-impairment users need adequate, well-spaced targets.

| Criterion | Level | Annotation |
|---|---|---|
| 2.5.7 Dragging Movements | AA | [Recommended, soon required] |
| 2.5.8 Target Size (Minimum) | AA | [Recommended, soon required] |

## 8. Zoom

**Check:** Usable at 200% zoom with no loss of content/function and no horizontal scrolling (reflow); usable at 400%. Relative units (rem/em/%), not fixed pixel widths.
**Why:** Low-vision users depend on zoom and reflow.

| Criterion | Level | Annotation |
|---|---|---|
| 1.4.4 Resize Text | AA | [Required] |
| 1.4.10 Reflow | AA | [Required] |

## 9. Media

**Check:** Alt text describes function, not appearance; decorative images use `alt=""`. Real text instead of text-in-images. Animations are pausable; `prefers-reduced-motion` respected.
**Why:** Screen-reader users need text alternatives; motion can trigger vestibular disorders.

| Criterion | Level | Annotation |
|---|---|---|
| 1.1.1 Non-text Content | A | [Required] |
| 1.4.5 Images of Text | AA | [Required] |
| 2.3.3 Animation from Interactions | AAA | [Optional/AAA] |

## 10. Validation

**Check:** Error summary on submit; validate on blur/submit, not on every keystroke; submit button never disabled (disabled buttons aren't announced and give no feedback). Redundant entry avoided.
**Why:** Robust error handling; prevents screen-reader announcement fatigue.

| Criterion | Level | Annotation |
|---|---|---|
| 3.3.1 Error Identification | A | [Required] |
| 3.3.7 Redundant Entry | A | [Recommended, soon required] |

## 11. Navigation

**Check:** Complete heading hierarchy (no skipped levels, one logical `<h1>`); landmark regions defined (`<header> <nav> <main> <footer>`); skip link present; help mechanisms in a consistent location.
**Why:** Screen-reader users navigate by structure (headings and landmarks).

| Criterion | Level | Annotation |
|---|---|---|
| 2.4.1 Bypass Blocks | A | [Required] |
| 2.4.6 Headings and Labels | AA | [Required] |
| 3.2.6 Consistent Help | A | [Recommended, soon required] |

## 12. Authentication (WCAG 2.2)

**Check:** Login does not rely on a cognitive function test (remembering/transcribing) with no alternative. Allow paste, password managers, copy of one-time codes, or other non-cognitive methods.
**Why:** Users with cognitive disabilities are otherwise locked out.

| Criterion | Level | Annotation |
|---|---|---|
| 3.3.8 Accessible Authentication (Minimum) | AA | [Recommended, soon required] |
