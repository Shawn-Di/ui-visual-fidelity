# UI Visual Fidelity

> A disciplined agent skill for fixing and refactoring existing web UIs without losing the design.

UI changes rarely fail because a single CSS property is hard to write. They fail when a “small fix” silently changes a theme, stacking layer, hover state, component boundary, or visual rhythm elsewhere.

**UI Visual Fidelity** gives coding agents a practical visual contract for high-risk UI work:

- reproduce the issue in the real browser before editing;
- trace DOM ownership, computed styles, pseudo-elements, clipping, and stacking;
- change the smallest responsible component or token;
- preserve layout, interaction, animation, and theme behavior;
- verify with both automated regression checks and real screenshots.

## What it covers

| Problem | Guardrail |
| --- | --- |
| CSS override drift | Fix the owning selector instead of adding global patches |
| Dark/light theme leakage | Verify each theme independently |
| “Centered” elements that still look wrong | Trust the rendered pixels, not only `text-align` or `align-items` |
| Refactors that change the design | Preserve cascade order, specificity, geometry, and states |
| Bloated visual layers | Extract semantic tokens and reusable surface/control templates |
| Visual regressions | Combine format checks, architecture checks, and screenshot comparison |

## The workflow

1. Lock the requested scope and identify the exact visual baseline.
2. Reproduce the target page, state, theme, and viewport.
3. Inspect the element, parent layers, computed styles, pseudo-elements, and cascade.
4. Write a regression check, then make the smallest causal change.
5. Compare dark and light screenshots before calling the work complete.
6. Refactor only after visual parity is stable.

## When to use it

Use it for UI bug fixes, screenshot matching, CSS override cleanup, design-system extraction, theme work, modal/drawer styling, responsive alignment, and visual refactors where “functionally correct” is not enough.

This is not a component library and does not invent a visual style. It protects an existing design system and makes its rules reusable.

## Install

Copy the `ui-visual-fidelity` directory into the skills directory supported by your coding agent. The package is intentionally small:

```text
ui-visual-fidelity/
├── SKILL.md
└── agents/openai.yaml
```

Then invoke it by name when working on an existing UI:

```text
Use $ui-visual-fidelity to fix this UI regression without changing unrelated states.
```

## Quality promise

This skill treats “tests pass” and “the UI is visually faithful” as separate acceptance gates. A stable refactor can still have hard-coded colors, long selectors, excessive `!important`, or small baseline mismatches; those remain explicit follow-up work instead of being hidden behind a lower line count.

## Contributing

Please include the original visual constraint, the smallest reproducible state, screenshots before and after, and the regression check that prevents the issue from returning. Keep changes scoped and avoid adding a new global override for a local problem.

## License

MIT © Shawn-Di
