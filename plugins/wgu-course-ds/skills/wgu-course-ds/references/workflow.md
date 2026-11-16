# Workflow

## A. Building a page or block from a design

1. **Read the DS** (SKILL.md, "Every session") and the guides of every component the design uses.
2. **Read the design.** For Figma, use the Figma MCP: load its design-to-code skill, call `create_session`, then use `get_metadata` for structure, `get_design_context` for a reference implementation and a screenshot, and `get_variable_defs` for the variables used. The design is a reference; the DS decides.
3. **Ask before building** about anything the design doesn't settle: interactions, missing mobile frames, states not in the component guide, content that may vary in length.
4. **Map every value to a DS token.**
   - colours → context tokens (never primitives or `palette-*`)
   - text → type styles
   - spacing → the 4px scale
   - corners → radii (plus the asymmetric-corner rule)
   - durations → motion tokens

   For each value with no DS match, follow `requests.md`. Don't round to the nearest token silently.
5. **Reuse components.** Use the project's implementation of each DS component. If the project lacks one the DS documents, build it from its guide as a shared component, not inside the block.
6. **Lay out with flex/grid and max-widths**, not the design tool's absolute positions. Figma frames are 1280px wide; content sits at `content-width-wide` or `content-width-reading`.
7. **Make it responsive with container queries**: mobile-first, tablet at 36rem, desktop (the Figma values) at 48rem. Mobile type uses the `-mobile` sizes.
8. **Apply context.** Navy sections get `data-theme="pilot-inverse"` and set their own background and colour; check every child flips correctly.
9. **Add motion** only where the DS defines it, with the motion tokens, and turn everything off under reduced motion.
10. **Verify** against "Before saying it's done" in SKILL.md and run the `wgu-course-ds-review` skill.

## B. Syncing a project to a new DS version

1. Read `project/CHANGELOG.md` and `project/tokens.json`, and note the project's recorded `ds-version`.
2. For each entry since that version:
   - **Breaking**: find every use (search the codebase) and list it.
   - **Changed**: list where it's used, for a visual check.
   - **Added**: note it.
3. Update the project's token layer from `tokens.json`, keeping the three layers and the DS names. Prefer a script over hand edits when the project has one, and never hand-edit generated files.
4. Fix the uses of renamed or removed names. The DS announces breaking changes one version ahead and keeps the old name meanwhile, so move to the new name now.
5. Update the recorded `ds-version` only once the tokens match.
6. Report what changed and what needs a visual check.

## C. Reviewing someone else's work

Use the `wgu-course-ds-review` skill.
