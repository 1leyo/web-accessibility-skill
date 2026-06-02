# Framework Notes

Accessibility is the same across frameworks; the gotchas differ. Plain HTML/CSS/JS applies
everywhere. Below: the framework-specific traps.

## React (primary focus)

**IDs:** use `useId()` to generate stable unique IDs for `label`/`aria-describedby`/`aria-errormessage` associations, especially with SSR. Don't hand-roll IDs that can collide across instances.

**Focus management:** React does not move focus for you on route or view changes. After SPA navigation, programmatically move focus (via a `ref` and `.focus()`) to the new view's heading or main container, or screen-reader users won't know the page changed. For modals, trap focus inside while open and restore focus to the trigger on close.

**Refs for focus, not state:** use `useRef` + `element.focus()` for imperative focus. Don't try to drive focus through render state.

**Portals:** render modals/dialogs/tooltips via `createPortal` so they escape `overflow:hidden`/stacking contexts, but keep correct DOM/tab semantics and apply `inert` or focus-trapping to the background.

**Native first:** render `<button>`, not `<div onClick>`. If you must support keyboard on a non-native element, add `role`, `tabIndex={0}`, and `onKeyDown` for Enter/Space — but prefer the native element.

**`dangerouslySetInnerHTML`:** injected HTML bypasses JSX; verify it carries correct semantics and alt text.

**Libraries:** prefer headless accessible primitives (React Aria / Radix UI / Headless UI) for composite widgets over building ARIA from scratch — they implement APG keyboard patterns correctly.

**Linting:** `eslint-plugin-jsx-a11y` catches a useful subset statically. It is not a conformance check.

## Vue

- `v-html` mirrors React's `dangerouslySetInnerHTML` caveat.
- Use `nextTick` before moving focus after DOM updates.
- Vue Router `afterEach` is the hook for focus management on route change.
- Headless options: Headless UI (Vue), Reka UI (formerly Radix Vue).

## Svelte / SvelteKit

- Svelte's compiler emits a11y warnings at build time (missing alt, label associations, etc.) — heed them.
- SvelteKit: move focus after navigation in an `afterNavigate` hook; SvelteKit announces route changes via a live region by default, but verify focus placement.

## Angular

- Angular CDK `a11y` module: `FocusTrap`, `LiveAnnouncer`, `cdkTrapFocus` for modals and announcements.
- Router: move focus on `NavigationEnd`.
- Angular Material components are largely APG-compliant; still verify names and contrast.

## Plain HTML/CSS/JS

- The baseline. Native elements give you roles, names, and keyboard support for free.
- `:focus-visible` for focus rings; `inert` attribute for backgrounding content behind modals.
- No framework means no automatic focus management — handle it explicitly for any dynamic content.

## Universal reminders

- A component library being "accessible" covers the component, not your usage of it. You still own names, contrast, focus order, and content.
- Automated linters and scanners are a floor, not a ceiling. Keyboard + screen-reader + zoom testing remain mandatory.
