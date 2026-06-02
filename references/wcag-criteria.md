# WCAG Success Criteria Reference (DE/EU annotation)

Authoritative quick reference for annotating findings. Consult before assigning level or legal weight.

**Annotation rule:**
- A criterion present in **WCAG 2.1** → current legal minimum via EN 301 549 v3.2.1 → **[Required]**.
- A criterion **new in WCAG 2.2** → **[Recommended, soon required]** (EN 301 549 v4.1.1 expected to reference WCAG 2.2, not yet in the EU Official Journal).
- **AAA** → **[Optional/AAA]**, never present as legally required.

## The 9 criteria new in WCAG 2.2 (memorize these)

| Criterion | Level | Annotation |
|---|---|---|
| 2.4.11 Focus Not Obscured (Minimum) | AA | [Recommended, soon required] |
| 2.4.12 Focus Not Obscured (Enhanced) | AAA | [Optional/AAA] |
| 2.4.13 Focus Appearance | AAA | [Optional/AAA] |
| 2.5.7 Dragging Movements | AA | [Recommended, soon required] |
| 2.5.8 Target Size (Minimum) | AA | [Recommended, soon required] |
| 3.2.6 Consistent Help | A | [Recommended, soon required] |
| 3.3.7 Redundant Entry | A | [Recommended, soon required] |
| 3.3.8 Accessible Authentication (Minimum) | AA | [Recommended, soon required] |
| 3.3.9 Accessible Authentication (Enhanced) | AAA | [Optional/AAA] |

Removed in 2.2: **4.1.1 Parsing** (obsolete). Do not flag parsing/validation as a WCAG failure.
Renamed in 2.2: old 2.5.5 Target Size → **2.5.5 Target Size (Enhanced)** (AAA, 44×44px).

## Commonly cited 2.1/2.0 criteria (all [Required] at A/AA)

| Criterion | Level | Topic |
|---|---|---|
| 1.1.1 Non-text Content | A | images, icons, media |
| 1.3.1 Info and Relationships | A | semantic structure |
| 1.4.1 Use of Color | A | color not sole cue |
| 1.4.3 Contrast (Minimum) | AA | text contrast 4.5:1 / 3:1 |
| 1.4.4 Resize Text | AA | zoom to 200% |
| 1.4.5 Images of Text | AA | real text |
| 1.4.10 Reflow | AA | no horizontal scroll at 200% |
| 1.4.11 Non-text Contrast | AA | UI/focus 3:1 |
| 2.1.1 Keyboard | A | keyboard operability |
| 2.1.2 No Keyboard Trap | A | no trap |
| 2.4.1 Bypass Blocks | A | skip links/landmarks |
| 2.4.3 Focus Order | A | logical order |
| 2.4.6 Headings and Labels | AA | descriptive headings |
| 2.4.7 Focus Visible | AA | visible focus indicator |
| 3.3.1 Error Identification | A | errors identified |
| 3.3.2 Labels or Instructions | A | field labels |
| 3.3.3 Error Suggestion | AA | correction hints |
| 4.1.2 Name, Role, Value | A | accessible name/role/state |
| 4.1.3 Status Messages | AA | live announcements |

For 1.4.3 thresholds use the values in `knowledge-base.md` topic 7. For target-size exceptions use topic 9.

Authoritative source: W3C WCAG 2.2 Recommendation (also ISO/IEC 40500:2025).
