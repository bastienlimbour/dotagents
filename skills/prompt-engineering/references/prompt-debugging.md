# Prompt Debugging, Evaluation, and Rewriting

## Contents

- Define success criteria first
- Failure taxonomy
- Rewriting heuristics
- Anti-patterns
- Building evaluation sets
- Prompt review checklist

## Define success criteria first

Do not optimize prompts blindly. First define what success means:

- Accuracy, completeness, structure compliance, tone fit, low hallucination rate.
- For agents: correct tool choice, correct stop conditions, safe handling of risky actions, successful verification.

## Failure taxonomy

When a prompt fails, locate the failure type before rewriting.

| Failure | Likely Cause | Fix |
| --- | --- | --- |
| Off-topic answer | Goal too vague | Sharpen the objective |
| Inconsistent format | Output contract too loose | Show the exact template or schema |
| Hallucinated details | No uncertainty rule | Require use of provided sources only |
| Skipped steps | Workflow not explicit | Add step list or status tracking |
| Wrong tool choice | Tool descriptions overlap | Clarify tool purposes and boundaries |
| Verbose preamble | Output rules too weak | Request direct output only |
| Brittle behavior | Conflicting constraints | Remove or reorder lower-priority rules |
| Silent guessing | No uncertainty policy | Add explicit uncertainty handling |
| Too many questions | Ask-vs-act rule missing | Add default: proceed with safe default, state assumption |
| Ignores constraints | Constraint buried in noise | Move constraint near the top; reduce total prompt length |

## Rewriting heuristics

When improving a weak prompt:

1. Replace vague goals (`make it better`) with concrete outcomes.
2. Replace soft adjectives (`short`, `good`, `detailed`) with measurable guidance.
3. Move key instructions to the top.
4. Turn implicit assumptions into explicit constraints.
5. Replace large "do not" blocks with positive alternatives.
6. Add an uncertainty rule when unsupported guesses would be harmful.
7. Split multi-goal prompts into stages if reliability is poor.
8. If a change does not improve measurable behavior, remove it.

Useful wording patterns:

- `Use only the provided source material.`
- `If the answer is not supported by the input, say so clearly.`
- `Return the result in the following structure:`
- `Preserve X, improve Y, avoid Z.`
- `Ask for clarification only if the missing information blocks a reliable answer.`

When in doubt: simplify the prompt, sharpen the objective, make the output contract more explicit.

## Anti-patterns

| Anti-Pattern | Problem |
| --- | --- |
| Too vague (`Improve this.`) | No actionable direction |
| Too broad (`Refactor the whole project.`) | Unbounded scope |
| Contradictory (`Be concise and fully exhaustive.`) | Impossible to satisfy |
| Too dense, no structure | No priorities or output contract |
| No definition of done | Model does not know when to stop |
| Too much irrelevant context | Noise reduces quality |
| Pure prohibitions without fallback | No actionable recovery |
| Too many goals, no priority | Model cannot rank trade-offs |
| Overlong examples | Crowd out the real task |
| Demanding certainty on incomplete inputs | Encourages hallucination |
| Micromanaging steps | Blocks better solutions, makes prompts brittle |
| Structure more complex than the task | Overhead without benefit |

## Building evaluation sets

Test prompts with structured cases:

1. **Positive cases**: Requests that should succeed.
2. **Near misses**: Similar requests that should not trigger the same behavior.
3. **Boundary cases**: Inputs that reveal scope ambiguity.
4. **Edge cases**: Missing context, malformed data, conflicting constraints.
5. **Adversarial cases**: Attempts to break format, override instructions, or inject malicious directions.

For skills or agent rules, add trigger evaluation: 3 prompts that should trigger, 2 that should not, 1 boundary case.

## Prompt review checklist

### Before sending a prompt

- [ ] Is the objective precise and in the first few lines?
- [ ] Is the context sufficient but not excessive?
- [ ] Are constraints explicit?
- [ ] Is the output format defined and testable?
- [ ] Is uncertainty handling specified?
- [ ] Is the completion criterion clear?
- [ ] Can the model admit uncertainty safely?
- [ ] Are examples helping rather than adding noise?

### Additional checks for agent instructions

- [ ] Is tool usage clearly defined?
- [ ] Are approval boundaries set for risky actions?
- [ ] Are stop conditions and escalation rules explicit?
- [ ] Is there conflicting or redundant guidance to remove?
- [ ] Is the best prompt the smallest one that reliably meets the success criteria?
