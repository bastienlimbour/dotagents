# Prototype UI

**Skill:** `prototype-ui`

**Status:** On-demand step.

**Role:** Quickly explore several disposable frontend directions before integrating UI cleanly into the product.

**When to use:** Uncertain UX, important screen, need to compare several visual directions, frontend AI-slop risk, product feature where user feel matters.

**Possible inputs:** brief, PRD, screenshots, design system, existing components, responsive constraints, user journey, visual references.

**Actions:**

- define what needs to be learned before prototyping
- create an isolated temporary area, prototype route, or local sandbox
- produce multiple clickable variants when useful
- use realistic data or lightweight fixtures
- avoid premature integration into product architecture
- document what works, what does not, and which elements to reuse
- clearly mark files as temporary or prepare their deletion

**Output:** disposable prototypes, options summary, UX recommendation, elements to reinject into `PRD`, `Tech Design`, `Build`, or an active artifact location.

**Artifact publication:** Prototypes stay local and disposable by default. If a parent issue exists, propose a summary comment with the selected option and elements to reinject; do not publish the raw prototype as product source of truth.

**Output contents:**

Required content:

- variants created
- recommended option and rationale
- UX trade-offs
- clean integration recommendation
- temporary files to delete or keep briefly

Conditional content:

- reusable components or patterns
- responsive and accessibility points to watch

Avoid:

- implicit promotion of prototype code to product code
- complete product plan
- exhaustive description of every visual detail

**Possible sizes:** micro-prototype of one component, or multi-screen exploration in an isolated route.

**Human gate:** choose the visual direction and validate what is worth integrating cleanly.

**Important:** A UI prototype is disposable. It must not accidentally become product code.
