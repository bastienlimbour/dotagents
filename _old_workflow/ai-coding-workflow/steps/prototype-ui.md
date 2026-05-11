# Prototype UI

**Skill name:** `prototype-ui`

**Step type:** On-demand.

**Role:** Explore disposable frontend directions so the product can choose a stronger UI path before clean implementation.

**When to use:** Uncertain UX, important screen, need to compare visual directions, frontend AI-slop risk, user-facing feature where feel matters, or unclear responsive behavior.

**Possible inputs:** Brief, Spec, screenshots, existing design system, components, user journey, responsive constraints, accessibility constraints, visual references, brand direction.

**Process:**

1. Define the learning goal before creating variants.
2. Identify evaluation criteria: usability, visual direction, information hierarchy, responsiveness, accessibility, and implementation risk.
3. Choose an isolated disposable location, route, or local sandbox, preferably gitignored or clearly excluded from normal product code.
4. Produce multiple variants when comparison will improve the decision.
5. Use realistic data or lightweight fixtures.
6. Check desktop and mobile behavior for promising variants.
7. Check basic accessibility for interactive elements when feasible.
8. Summarize what works, what fails, and which elements are worth clean integration.
9. Mark prototype files as temporary and identify cleanup needs.

**Rules:**

- Prototype UI code is disposable exploration; clean product implementation is out of scope.
- Preserve existing design-system patterns unless the goal is explicitly to challenge them.
- Do not promote prototype files into product architecture without clean integration.
- Do not commit prototype code by default. Commit only if the user explicitly accepts it and the code is cleaned or isolated as a deliberate artifact.

**Output:** Disposable prototype files plus a concise UX options summary, recommendation, and integration notes.

**Output location:** Recommended default: local disposable prototype files and session summary. If a parent issue exists, ask before publishing the selected option, rationale, and elements to reintegrate. If the user does not confirm publication, keep the summary in session only.

**Output template:**

```markdown
## Summary
<!-- Required. Paragraph, 1-3 sentences: what was prototyped and the headline recommendation. -->
<UI prototype summary.>

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

**Possible sizes:** lite (one component); standard (one important screen); full (multi-screen exploration for a critical flow or visual direction decision).

**Verification:** The selected direction was compared against the learning goal and can be reinjected into product or technical artifacts without promoting disposable code as architecture.

**Human gate:** Choose the visual direction and validate what is worth integrating cleanly.
