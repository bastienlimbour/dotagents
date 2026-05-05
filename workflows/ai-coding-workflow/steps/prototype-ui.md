# Prototype UI

**Skill name:** `prototype-ui`

**Step type:** On-demand step.

**Role:** Explore disposable frontend directions so the product can choose a stronger UI path before clean implementation.

**When to use:** Uncertain UX, important screen, need to compare visual directions, frontend AI-slop risk, user-facing feature where feel matters, or unclear responsive behavior.

**Possible inputs:** Brief, PRD, screenshots, existing design system, components, user journey, responsive constraints, accessibility constraints, visual references, brand direction.

**Process:**

1. Define the learning goal before creating variants.
2. Identify evaluation criteria: usability, visual direction, information hierarchy, responsiveness, accessibility, and implementation risk.
3. Choose an isolated disposable location, route, or local sandbox.
4. Produce multiple variants when comparison will improve the decision.
5. Use realistic data or lightweight fixtures.
6. Check desktop and mobile behavior for promising variants.
7. Check basic accessibility for interactive elements when feasible.
8. Summarize what works, what fails, and which elements are worth clean integration.
9. Mark prototype files as temporary and identify cleanup needs.

**Rules:**

- Prototype UI code is disposable exploration.
- Clean product implementation happens in `Build`.
- Preserve existing design-system patterns unless the goal is explicitly to challenge them.
- Do not promote prototype files into product architecture without clean integration.

**Output:** Disposable prototype files plus a concise UX options summary, recommendation, and integration notes.

**Output location:** Check `.agents/workflow/output-locations.md` when it exists. Recommended default: local disposable prototype files and session summary. If a parent issue exists, publish only the selected option, rationale, and elements to reintegrate.

**Output template:**

```markdown
## UI Prototype Summary

## Learning Goal
<!-- Required. Paragraph, 1-3 sentences: UX question or decision this prototype should answer. -->
<Learning goal.>

## Variants Created
<!-- Required. Bullet list: one variant per bullet. -->
- **Variant A:** <Direction and distinguishing idea.>
- **Variant B:** <Direction and distinguishing idea.>

## Evaluation Criteria
<!-- Required. Bullet list: criteria used to compare variants. -->
- <Usability, hierarchy, responsiveness, accessibility, visual direction, or implementation risk.>

## Recommendation
<!-- Required. Paragraph, 2-5 sentences: selected direction and rationale. -->
<Selected direction and rationale.>

## Reusable Elements
<!-- Conditional. Bullet list: elements worth reintegrating into product code. -->
- <Layout, copy, component pattern, interaction, or visual treatment.>

## Responsive & Accessibility Notes
<!-- Conditional. Bullet list: observed issue or requirement to carry forward. -->
- <Responsive or accessibility note.>

## Temporary Files
<!-- Required. Bullet list: prototype path and cleanup recommendation. -->
- `<path>` - delete / keep briefly / integrate cleanly: <reason.>
```

**Possible sizes:** Micro-prototype for one component; standard prototype for one important screen; multi-screen exploration for a critical flow or visual direction decision.

**Verification:** The selected direction was compared against the learning goal and can be reinjected into PRD, Tech Design, or Build without promoting disposable code as architecture.

**Human gate:** Choose the visual direction and validate what is worth integrating cleanly.
