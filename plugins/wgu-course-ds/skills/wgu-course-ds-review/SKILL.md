---
name: wgu-course-ds-review
description: Review WGU course UI code (a diff, a branch, files or a folder) against the WGU Course Design System and report violations with file:line. Use when asked to review, audit or check WGU course / ELPS / Open edX course UI for design-system consistency, before handing work over, or as the last check of the wgu-course-ds build skill. Reports only; fixes nothing unless asked.
---

# WGU Course DS review

Audit code against the WGU Course Design System. The rules are in the `wgu-course-ds` skill's `references/rules.md`; read it first. Where a rule depends on a component guide, read that guide from the live DS (see the `wgu-course-ds` skill for how).

## Scope

- No target given: review the working-tree diff (`git diff` plus untracked UI files).
- Otherwise review what the user names. Skip generated files, vendored code, the token definition file itself (raw values belong there), and design-tool exports.
- Find out where the project keeps its tokens and DS components first, so you can tell "defines a token" from "uses a raw value".

## Checks

Use the search patterns as a starting point, then read each hit in context: a pattern match is a lead, not a finding. Adapt file globs to the project's stack.

| # | Check | Starting pattern (ripgrep) |
|---|---|---|
| 1 | Raw colours outside the token file | `#[0-9a-fA-F]{3,8}\b`, `\brgba?\(`, `\bhsla?\(`, `\boklch\(` |
| 2 | Raw font sizes / line heights / font families | `font-size:\s*\d`, `line-height:\s*\d`, `text-\[\d+px\]`, `leading-\[`, `font-family:` |
| 3 | Primitive or palette tokens in components | `--(gray|teal|blue|orange|green|red|amber)-\d`, `palette-` |
| 4 | Interactive palette outside interactive blocks | `interactive` (allowed only in interactive blocks and their components) |
| 5 | Hand-picked light/dark or "inverse" variants instead of `data-theme` | `inverse`, `dark:`, `light`, `prefers-color-scheme` |
| 6 | Viewport media queries for component layout | `@media` (width conditions), Tailwind `sm:` / `md:` / `lg:` on component layout |
| 7 | Legacy Material Icons or other icon sets | `material-icons`, `Material Icons`, `fa-`, `lucide`, `heroicons` |
| 8 | Focus removed or missing | `outline:\s*none`, `outline-none` without a `focus-visible` style on the same element |
| 9 | States not in the guide | `:hover` / `hover:` / `transition` / `transform` on DS components; compare with the component README |
| 10 | Motion without reduced-motion handling, or raw durations | `animation`, `transition`, `@keyframes`, `\d+ms`; check for `prefers-reduced-motion` |
| 11 | `data-theme` element without its own background and colour | `data-theme` |
| 12 | Hand-rolled buttons and links where a DS component exists | `<button`, `<a ` with custom styling |
| 13 | Icon accessibility | icon-only buttons without `aria-label`; decorative icons without `aria-hidden` |
| 14 | Temporary design-tool asset URLs | `figma.com/api`, `figma-alpha-api` |
| 15 | `TODO(ds)` inventory | `TODO\(ds\)` (list every one; not a violation if it has a request) |

## Report

One list, most severe first. For each finding:

- `path:line`: what's wrong, in one sentence
- the DS rule or component guide it breaks
- the fix: the token, style or component to use; or "no token fits → `TODO(ds)` + request" (see `requests.md`)

Severity:

1. **Blocking:** accessibility failures (contrast, focus, keyboard, colour alone), Breaking-changelog names still in use, primitives in components.
2. **Should fix:** raw values with an exact token, invented states, viewport media queries, legacy icons.
3. **Note:** approximations, missing `TODO(ds)` requests, candidates kept local.

End with the `TODO(ds)` inventory and anything you couldn't check (e.g. contrast needing a render, a guide you couldn't read). Don't change code unless the user asks.
