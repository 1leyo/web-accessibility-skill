# Knowledge Base

Deep reference per topic. Each topic lists: requirements, implementation, common failures,
testing, mapped WCAG criteria, and edge cases. Use in both Development and Review mode.

Annotation legend: **[Required]** = WCAG 2.1 (legal minimum) · **[Recommended, soon required]** = new in WCAG 2.2 · **[Optional/AAA]** = AAA.

## Table of contents

1. Accessibility Principles
2. Keyboard Accessibility
3. Focus Management
4. Forms
5. Semantic HTML
6. ARIA
7. Color & Contrast
8. Images & Media
9. Zoom & Responsive
10. Testing
11. Content Hiding
12. Legal & WCAG Mapping

---

## 1. Accessibility Principles

**Requirements**
- POUR framework: Perceivable, Operable, Understandable, Robust.
- Target WCAG 2.2 AA (legal minimum currently 2.1 AA; see topic 12).
- Consider accessibility from the concept phase, not as an afterthought.
- Test regularly and document decisions.

**Implementation:** semantic HTML structure; relative CSS units for zoom; respect `prefers-reduced-motion`.

**Common failures:** accessibility treated as afterthought; relying solely on automated tools; no testing with assistive-technology users.

**Testing:** keyboard-only navigation; multiple screen-reader combinations; axe, WAVE, ARC, Lighthouse.

**WCAG structure:** 4 principles → 13 guidelines, levels A, AA, AAA. For conformance the load-bearing number is **Level AA = 56 cumulative criteria** (32 Level A + 24 Level AA). The total-count figure is cited inconsistently across sources (often 86 or 87) due to differing sub-criterion counting; do not assert a single total. What matters for review is the AA set of 56.

**Edge cases:** WCAG 2.2 added 9 criteria (focus, input, cognitive) and removed 4.1.1 Parsing as obsolete. WCAG 3.0 is in early development.

---

## 2. Keyboard Accessibility

**Requirements:** all interactive elements Tab-reachable; logical tab order; complete keyboard operation; no keyboard traps.

**Implementation:** use natively focusable HTML elements; never remove `outline` without a replacement; handle Enter/Space for custom controls; provide a documented arrow-key pattern for composite widgets.

**Common failures:** `<div onclick>` instead of `<button>`; keyboard traps; removed focus indicator; positive `tabindex` values that fight the natural order.

**Testing:** full keyboard navigation; Tab + Enter/Space activation; screen-reader keyboard test.

**WCAG:** 2.1.1 Keyboard (A) [Required] · 2.1.2 No Keyboard Trap (A) [Required].

**Edge cases:** custom widgets need documented keyboard patterns (follow APG); focus must remain visible at 200% zoom.

---

## 3. Focus Management

**Requirements:** focus always visible; indicator ≥ 2px and ≥ 3:1 contrast; focused element not fully obscured; meaningful focus placement after state changes (modal open, route change).

**Implementation:** keep logical DOM order equal to visual order; `:focus-visible { outline: 2px solid; outline-offset: 2px; }`; trap focus inside modals and restore it on close.

**Common failures:** removed outline; focus disappears at zoom; focus order ≠ visual order; focus lost after SPA navigation.

**Testing:** DevTools accessibility tree; 200% zoom focus visibility; screen-reader focus tracking.

**WCAG:** 2.4.7 Focus Visible (AA) [Required] · 2.4.11 Focus Not Obscured Minimum (AA) [Recommended, soon required] · 2.4.12 Focus Not Obscured Enhanced (AAA) [Optional/AAA] · 2.4.13 Focus Appearance (AAA) [Optional/AAA].

**Edge cases:** modal focus trapping; SPA route-change focus management (move focus to the new view's heading or container).

---

## 4. Forms

**Requirements:** visible labels on all fields; native controls stay in the DOM; errors concrete, solution-oriented, and linked; `aria-errormessage` paired with `aria-invalid="true"`.

**Implementation:** `<label for="id">` pattern; for custom checkboxes/radios hide the input visually but keep it in the DOM; provide an error summary plus inline messages; `aria-describedby` for hints.

**Common failures:** hidden/absent labels; disabled submit button; validation on every keystroke; placeholder used as the only label.

**Testing:** multiple browser/screen-reader combos; verify error announcement; reflect validation state in the page title where appropriate.

**WCAG:** 3.3.1 Error Identification (A) [Required] · 3.3.2 Labels or Instructions (A) [Required] · 3.3.3 Error Suggestion (AA) [Required] · 4.1.2 Name, Role, Value (A) [Required].

**Edge cases:** an error summary at the top is the most robust pattern; inline messages supplement it; `aria-errormessage` requires `aria-invalid="true"` to be honored.

---

## 5. Semantic HTML

**Requirements:** native elements provide roles automatically; prefer HTML over ARIA; logical heading hierarchy; landmark regions defined.

**Implementation:** `<button> <nav> <main> <header> <footer> <article> <aside>`; `<section aria-labelledby>` for custom landmarks.

**Common failures:** `<div class="btn">` (no role, no keyboard, no name); missing or skipped heading levels; no landmarks.

**Testing:** DevTools accessibility tree; screen-reader heading navigation; screen-reader landmark navigation.

**WCAG:** 4.1.2 Name, Role, Value (A) [Required] · 1.3.1 Info and Relationships (A) [Required] · 2.4.6 Headings and Labels (AA) [Required].

**Edge cases:** custom landmarks via `<section>` + `aria-labelledby`. Information flow: HTML → DOM → accessibility tree → platform accessibility API → OS → assistive technology.

---

## 6. ARIA

**Requirements:** native HTML first; consult the ARIA Authoring Practices Guide (APG); never `aria-hidden` on interactive elements; all interactive elements need an accessible name.

**Implementation:** `aria-label` / `aria-labelledby` for naming; `aria-errormessage` for errors; `aria-live` for dynamic content; `aria-expanded` for disclosure/accordion triggers.

**Common failures:** ARIA used where HTML works; `aria-hidden="true"` on interactive content; missing accessible names; ARIA widget with no keyboard support.

**Testing:** accessibility-tree inspection; multiple screen-reader combos; real-user testing.

**WCAG:** 4.1.2 Name, Role, Value (A) [Required] · 4.1.3 Status Messages (AA) [Required].

**Edge cases:** `aria-errormessage` requires `aria-invalid="true"`; `role="none"` is preferred over `role="presentation"`. ARIA roles are grouped into categories (landmark, widget, structure, live region, abstract); abstract roles must never be used in authored content.

**First rule of ARIA:** no ARIA is better than bad ARIA.

---

## 7. Color & Contrast

**Requirements:** normal text → 4.5:1; **large text** → 3:1; UI components and focus indicators → 3:1; color is never the sole distinguishing feature. "Large text" per WCAG = ≥ 18pt (typically 24px) at any weight, **or** ≥ 14pt bold (typically 18.66px). Below those sizes, 4.5:1 applies.

**Implementation:** underline links in addition to color; pair status icons with color; ensure focus indicator meets 3:1.

**Common failures:** color-only error indication; light gray on white; ghost buttons with insufficient border contrast.

**Testing tools:** contrast-grid.eightshapes.com; contrast.report; whocanuse.com; Figma plugins (Color Contrast, Stark).

**WCAG:** 1.4.1 Use of Color (A) [Required] · 1.4.3 Contrast Minimum (AA) [Required] · 1.4.11 Non-text Contrast (AA) [Required] · 1.4.6 Contrast Enhanced (AAA) [Optional/AAA].

**Edge cases:** AAA requires 7:1 for normal text; context affects perceived readability; thin fonts effectively need higher contrast.

---

## 8. Images & Media

**Requirements:** alt describes function, not appearance; text must be real text; animations pausable; `prefers-reduced-motion` supported; 200% zoom without loss.

**Implementation:** `<img alt="Suche">` not `<img alt="Lupe">`; decorative images `alt=""`; `@media (prefers-reduced-motion: reduce) { ... }`.

**Common failures:** alt describes appearance; text baked into images; auto-rotating carousels with no pause; content lost at zoom.

**Testing:** alt-text screen-reader check; 200%/400% zoom test; animation pause test.

**WCAG:** 1.1.1 Non-text Content (A) [Required] · 1.4.5 Images of Text (AA) [Required] · 1.4.4 Resize Text (AA) [Required] · 1.4.10 Reflow (AA) [Required] · 2.3.3 Animation from Interactions (AAA) [Optional/AAA].

**Edge cases:** decorative → empty alt; functional → describe the action; complex (charts) → provide an extended description nearby.

---

## 9. Zoom & Responsive

**Requirements:** 200% zoom without content loss; 400% usable; relative units; no horizontal scroll at 200%; pointer targets ≥ 24×24px (2.2 AA minimum), 44×44px recommended.

**Implementation:** `font-size: 1rem; padding: 1em`; `max-width: 100%` on images; flexbox/grid for reflow.

**Common failures:** fixed pixel widths; text in images; targets < 24×24px; drag-and-drop with no alternative.

**Testing:** 200%/400% zoom; target-size measurement; horizontal-scroll check.

**WCAG:** 1.4.4 Resize Text (AA) [Required] · 1.4.10 Reflow (AA) [Required] · 2.5.7 Dragging Movements (AA) [Recommended, soon required] · 2.5.8 Target Size Minimum (AA) [Recommended, soon required].

**Edge cases:** 2.5.8 minimum is 24×24px with a spacing exception (a 24px circle centered on the target must not overlap neighbors); inline text links are exempt. 44×44px is the 2.5.5 Target Size (Enhanced) AAA bar. Relative units are essential.

---

## 10. Testing

**Requirements:** combine automated tools, keyboard-only testing, multiple screen-reader combos, real-user testing, and zoom at 200%/400%.

**Implementation tools:** axe DevTools; WAVE; ARC Toolkit; Lighthouse; browser DevTools accessibility panel.

**Common failures:** relying only on automated tools; testing a single screen reader; skipping keyboard testing; no testing with disabled users.

**Process:** design checklist (contrast, focus, labels, errors, hierarchy, zoom, targets, animations, states); BITV-Test / EN 301 549 procedure; WCAG-EM Report Tool for formal conformance.

**Edge cases:** automated tools fully automate only ~30% of success criteria (axe-core surfaces ~57% of real issues by volume) — a green Lighthouse score is not conformance. Different assistive technologies behave differently; user testing is necessary for true accessibility.

---

## 11. Content Hiding

**Requirements:** invisible ≠ inaccessible; visual, semantic, and interactive hiding differ; focusable content must stay visible; no `aria-hidden` on interactive content.

**Hiding mechanisms:**

| Mechanism | Effect |
|---|---|
| `hidden` attribute | equivalent to `display:none`; removed from layout and tree |
| `disabled` | element locked but still in the accessibility tree |
| `inert` | completely non-interactive and removed from tab/AT |
| `tabindex="-1"` | removes from Tab order only (still focusable via script) |
| `aria-hidden="true"` | removes from the accessibility tree (must not wrap interactive content) |
| CSS `opacity:0` / `clip-path` / off-screen positioning | visual hiding only; content remains in the tree and keyboard-reachable |

**Common failures:** `aria-hidden` on interactive content; `role="presentation"` on interactive content; CSS-only hiding that leaves elements keyboard-reachable.

**Decision questions:** Who should NOT see/operate it? Who should still perceive it? Is it static or interactive? Then verify with browser + keyboard + screen reader.

**WCAG:** 4.1.2 Name, Role, Value (A) [Required] · 1.3.1 Info and Relationships (A) [Required].

**Edge cases:** `role="none"` preferred over `role="presentation"`; for a custom checkbox the decorative SVG gets `aria-hidden`, the real `<input>` stays; CSS hiding never removes from the accessibility tree.

---

## 12. Legal & WCAG Mapping

**Framework (DE/EU):**
- EN 301 549 / WCAG 2.1 AA is the current legal-minimum bar.
- EU: Directive 2016/2102 (public sector, WAD), Directive 2019/882 (EAA, private sector).
- Germany: BGG / BITV 2.0 (public sector), BFSG / BFSGV (private sector, in force 28.06.2025).
- An accessibility statement (Erklärung zur Barrierefreiheit) is required for covered offerings.

**Conformance:** Level A + AA mandatory. Tools: WCAG-EM Report Tool; BITV self-assessment; FFG Report Generator.

**Common failures:** non-compliance fines (up to €100,000 under BFSG); missing accessibility statement; claiming Level A where AA is required.

**WCAG 2.2 additions relevant to law:** 2.4.11 Focus Not Obscured Minimum (AA); 2.5.8 Target Size Minimum (AA); 2.5.7 Dragging Movements (AA); 3.2.6 Consistent Help (A); 3.3.7 Redundant Entry (A); 3.3.8 Accessible Authentication Minimum (AA).

**Edge cases:** German WCAG 2.1 translation is unofficial (Aktion Mensch); no official German WCAG 2.2 yet; 4.1.1 Parsing is obsolete; target size 24×24px is the pragmatic 2.2 AA bar, 44×44px is AAA (2.5.5 Enhanced). German Länder have their own public-sector laws. BITV weighting in assessment: concept 20%, implementation 45%, testing 30%, documentation 5%.

**Not legal advice.** For binding assessment, refer to the Bundesfachstelle Barrierefreiheit or a qualified lawyer.
