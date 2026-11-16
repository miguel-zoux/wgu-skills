# Rules

Condensed from the DS README (v2.1) and the practice of the teams building with it. The live DS wins over this file. Exact values (colours, sizes, durations) are deliberately left out: read them from `project/tokens.json`.

## Tokens: three layers

1. **Primitives** (`gray-*`, `teal-*`, `blue-*`, `orange-*`, `green-*`, `red-*`, `amber-*`): raw values. Never used in components.
2. **Theme** (`palette-*`: `neutral`, `brand`, `accent`, `highlight`, `positive`, `negative`, `attention`, `info`): roles a course theme remaps. Never used in components.
3. **Context** (`bg-*`, `text-*`, `icon-*`, `border-*`, `action-*`, `focus-ring`, `input-*`): the **only** layer components use.

- Names are the DS names, lowercase, `category-role[-variant][-state]`, with no prefix. If a platform needs a namespace, add it to every token at build time; don't rename them by hand.
- Context tokens point at palette variables (`--text-heading: var(--palette-brand-600)`), so a new theme only changes the palette block.
- Tokens are never edited in code and never invented locally. No hand-written colour, font size, line height, spacing, radius, shadow or duration where a token exists.
- Use each type style's `--font-size-<style>` / `--line-height-<style>` variables (and `-mobile`), never pixel values.

## Theming and context

- Each theme has two ids: `pilot` (light surfaces) and `pilot-inverse` (navy sections). Set `data-theme="pilot"` on the course root and `data-theme="pilot-inverse"` on a dark section; every context token inside flips. A white card inside a navy section sets `data-theme="pilot"` again.
- **The element carrying `data-theme` sets its own `background: var(--bg-surface)` and `color: var(--text-body)`**, because inherited text colour is already computed.
- Never pick light or dark tokens by hand, and never create "inverse" component variants. Context does that (e.g. outline and ghost actions turn white on navy by themselves).
- Shadows aren't used on navy sections.

## Colour roles

- Surfaces: `bg-surface`, `bg-surface-emphasis` for a band or panel.
- Text: `text-heading`, `text-body`, `text-muted`. `text-heading` on `bg-surface-emphasis` is for heading sizes only.
- **The interactive palette (`*-interactive*`) is exclusive to interactive blocks** (Flashcards, Unfolding Scenario, …) and the components that build them (InteractiveHeader, LaunchCard, ActivityShell, ConfirmDialog, RadioCard). Content blocks use the context tokens, or a component's own fixed colours (Callout, Label).
- Feedback: a light `bg-feedback-*` with its `text-feedback-*`. For a solid fill with white text, use `bg-feedback-*-strong`; never use an icon token as a fill. There is no feedback component. Never signal state with colour alone; pair it with an icon or words.
- Actions: `action-fill-*` for filled buttons, `action-outline-*` for outline and ghost, `action-neutral-*` for icon buttons.

## Typography

- Two families: **Sora** (display, headings, callouts, statement, actions, captions) and **Lato** (body), both from Google Fonts. Weights **400 and 700 only**.
- Use the DS style names: `display-1/2`, `heading-1…6`, `callout-lg/md`, `statement`, `body-xl…xs-regular|bold`, `action-md/sm`, `caption-md/sm`.
- Reading prose is `body-lg-regular`. `body-xs-*` is only for brief secondary text.
- Write mobile-first with the style's mobile size, then switch at the desktop breakpoint.

## Layout, spacing and shape

- Spacing is a 4px scale (`space-1` = 4 … `space-20` = 80).
- Sections: `section-padding` on desktop, `section-padding-mobile-x` / `-y` on mobile. Content is centred at `content-width-wide`, or `content-width-reading` for reading text.
- Radii: `radius-xs/sm/md/lg/xl`, `radius-full` for pills. Buttons are pills; cards and inputs are evenly rounded.
- **Asymmetric corner:** one corner noticeably tighter, used only on images in cards, tab-like labels (Label, InteractiveHeader chip), the Callout and ProcessFlow steps, as each component guide specifies. Not on buttons, cards or inputs.
- Dividers are a 1px `border-default` border, never an image.
- One elevation only: `shadow-card` (and `shadow-card-soft` for the lower cards of a stack). Hierarchy comes from colour and space.

## Responsiveness

- Components respond to **their container, not the viewport**: use container queries. Mobile is below `breakpoint-sm` (576px / 36rem), tablet from 576px, desktop from `breakpoint-md` (768px / 48rem).
- CSS variables can't be used in query conditions, so write the literal values (36rem, 48rem).
- Don't use media queries for component layout. `prefers-reduced-motion` and similar user preferences are fine.

## Icons

- **Google Material Symbols, Outlined**, with fill 0, weight 400 and grade 0. Fill 1 only for a selected state a component defines. Never the legacy Material Icons set or another library.
- Optical size: 20 for icons up to 20px, 24 for 24px, 40 for 32px and up. Sizes are 16 / 20 / 24 / 32 on the icon's square box, fixed by the component.
- Colour is `currentColor` from `icon-*` tokens or the parent component (`action-*` in buttons). Never a primitive.
- An icon next to a label is `aria-hidden="true"`. An icon-only button has an `aria-label` on the button, with the icon hidden. Back arrows lead and forward arrows trail. Use each icon's established meaning.

## Components and states

- Before building anything a DS component covers, read its `components/<Component>/README.md` and reuse the project's implementation if one exists.
- **Implement exactly the states the guide lists** (default, hover, keyboard focus, disabled, …), including its "Differences from Figma" notes. Don't invent hover effects, icon movement, transitions or extra states. If something isn't covered, ask.
- Focus: every focusable element shows the `focus-ring`, 2px solid, offset 2px, on keyboard focus (`:focus-visible`). Never remove focus styles.
- Prefer inset outlines (e.g. an inset box-shadow) for hover and focus borders, so the 2–3px outline doesn't resize the control.
- **Candidates** listed in the DS README (e.g. progress indicator, carousel controls) aren't DS components. Keep them local to their block and say so.

## Motion

- Motion explains what changed; it never decorates.
- Durations: `motion-fast` (hover, focus, colour, small elements appearing), `motion-medium` (entrances: opening an activity, flipping a card), `motion-slow` (content revealed on scroll), `motion-exit` (always faster than entrances), `motion-stagger` (between items in sequence).
- Easing: `ease-enter` for entrances and state changes, `ease-exit` for exits.
- Entrances fade with a short rise from the spacing scale: `space-3` for dialogs, `space-4` for an activity opening, `space-6` for content revealed on scroll.
- **Reduced motion:** every animation and transition is off and content simply appears.

## Accessibility

- Contrast: text 4.5:1; large text (≥24px regular, ≥19px bold), icons, control borders and focus rings 3:1. Respect each token's usage-note limits (e.g. white on `bg-callout` is for large text only, through the Callout).
- Never colour alone; keyboard and screen-reader behaviour as each component guide describes.

## Assets

- Download every image into the project; never ship temporary design-tool URLs. Check the real file type (some ".png" files are JPEGs).
- Icons come from Material Symbols, not from Figma exports.
