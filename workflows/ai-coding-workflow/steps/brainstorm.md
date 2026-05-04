# Brainstorm

**Skill:** `brainstorm`

**Status:** On-demand step.

**Role:** Open the idea space broadly, generate options, and structure directions without converging.

**When to use:** Unclear idea, new product, new direction, major feature, product/technical exploration, lack of options.

**Possible inputs:** Brainstorming goal, context, intuition, notes, voice transcript, existing ideas, directions to explore, data, code, or project documentation.

**Actions:**

- create a local `brainstorming.md` file in `.initiatives/<NNN-initiative-name>/`
- define the brainstorming goal and context
- ask open-ended questions persistently to stimulate thinking and generate directions
- explore problems, opportunities, personas, solutions, value proposition, use cases, capabilities, assumptions, constraints, and risks
- cluster ideas during brainstorming to avoid a flat dump
- continue until an explicit stop request or the end of the timebox

**Output:** brainstorming summary in session, optional local `brainstorming.md`, or tracker comment only if an active artifact location already exists.

**Artifact publication:** By default, keep brainstorming in the session/chat or in gitignored `.initiatives/<initiative>/brainstorming.md`. Do not create a parent GitHub issue for divergent brainstorming unless explicitly requested; if a parent issue already exists, propose a summary comment without raw transcript.

**Output contents:**

Required content:

- brainstorming context / goal
- summary by themes
- promising directions to filter later
- open questions

Conditional content:

- problems and opportunities
- possible users/personas
- value propositions
- solutions and variants
- use cases
- candidate capabilities
- assumptions
- constraints and risks

Avoid:

- full session transcript
- premature product decision
- raw list of all ideas without grouping

**Possible sizes:** targeted micro-brainstorm, or full 30 to 120 minute brainstorm.

**Human gate:** choose directions to filter in `Brief`, `PRD`, `Tech Design`, or an explicit decision.

**Important:** `Brainstorm` intentionally diverges. It does not decide.
