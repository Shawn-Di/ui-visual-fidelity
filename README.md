# UI Visual Fidelity

> Turn chaotic AI-generated web UI into readable, maintainable, smaller code — without changing the UI structure.

AI-generated pages often work, but leave behind unreadable CSS, duplicated overrides, unclear ownership, broken themes, and fragile visual fixes. This skill helps an agent make that code understandable and maintainable while keeping the rendered product intact.

**UI Visual Fidelity** gives coding agents a practical visual contract for high-risk UI cleanup:

- reproduce the issue in the real browser before editing;
- trace DOM ownership, computed styles, pseudo-elements, clipping, and stacking;
- change the smallest responsible component or token;
- preserve layout, interaction, animation, and theme behavior;
- verify with both automated regression checks and real screenshots.

## What it promises

Each capability is both an instruction and an acceptance condition:

| Capability | Instruction | Must be true when finished |
| --- | --- | --- |
| Readable UI code | Group styles by visual responsibility and name ownership clearly | Another engineer can find the rule without tracing a wall of overrides |
| Maintainable UI | Extract semantic tokens and reusable surface, border, glass, button, and state templates | Repeated visual decisions have one reusable source |
| Smaller code | Remove duplication, merge equivalent rules, and reduce unnecessary late overrides | Code becomes smaller without deleting behavior or hiding differences |
| Structure preservation | Keep DOM structure, layout, spacing, states, interactions, and animation unchanged unless explicitly requested | Before/after screenshots and behavior checks show no unintended structural change |
| Theme safety | Verify dark and light modes independently | No theme leakage, unreadable text, or leftover dark/light surfaces |
| Visual correctness | Inspect computed styles, pseudo-elements, clipping, stacking, and actual pixels | “Tests pass” is not accepted as proof when the screenshot still differs |

The skill reduces UI/style code duplication. It does not rewrite business logic or change the product architecture unless the user explicitly asks for that.

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

## Install in Codex

Yes. A user can download this repository and use the Skill in Codex by copying the `ui-visual-fidelity` directory into a supported skills location. For a single project:

```bash
git clone https://github.com/Shawn-Di/ui-visual-fidelity.git
mkdir -p .agents/skills
cp -R ui-visual-fidelity .agents/skills/
```

For a user-level installation, copy the same directory into `~/.codex/skills/`. Start a new Codex task after installation so the Skill can be discovered.

The package is intentionally small:

```text
ui-visual-fidelity/
├── SKILL.md
└── agents/openai.yaml
```

Then invoke it by name when working on an existing AI-generated UI:

```text
Use $ui-visual-fidelity to fix this UI regression without changing unrelated states.
```

## Quality boundary

This skill treats “tests pass” and “the UI is visually faithful” as separate acceptance gates. A refactor can still have hard-coded colors, long selectors, excessive `!important`, or baseline mismatches; those remain explicit follow-up work instead of being hidden behind a lower line count.

It is for preserving an existing design, not inventing a replacement style. When the user provides a screenshot or an earlier accepted version, that reference is the visual contract.

## Contributing

Please include the original visual constraint, the smallest reproducible state, screenshots before and after, and the regression check that prevents the issue from returning. Keep changes scoped and avoid adding a new global override for a local problem.

## License

MIT © Shawn-Di
