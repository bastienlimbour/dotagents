# `/brief`

## Objectif

Créer, initialiser ou mettre à jour un brief produit optionnel pour une initiative.

## À utiliser quand

- L'utilisateur a une idée vague et veut la cadrer.
- Un projet greenfield nécessite une première clarté produit.
- Une grosse feature nécessite un artefact d'exploration produit.
- L'utilisateur demande explicitement d'initialiser ou mettre à jour un brief.

## Entrées

- Conversation courante.
- Notes de brainstorming.
- Notes de recherche.
- Session de grilling.
- Contexte produit, business, domaine ou stratégique fourni par l'utilisateur.

## Comportement

- Si l'utilisateur veut seulement initialiser une initiative, créer un squelette de brief avec les sections canoniques.
- Si l'utilisateur fournit du contexte, l'analyser et identifier les manques critiques.
- Si des informations critiques manquent, poser des questions ciblées.
- Pour du contenu substantiel, proposer un draft en conversation.
- Écrire ou mettre à jour `brief.md` seulement après validation utilisateur.

## Sorties

```text
.initiatives/<id>/brief.md
```

## Format

`brief.md` est optionnel. Il est utile pour les projets greenfield, les grosses initiatives, les features substantielles et les situations où l'exploration produit compte.

S'il existe, il est l'artefact canonique d'exploration produit avant la spec.

Après publication d'une spec, le brief devient une archive locale non canonique.

Le brief est produit-first. Il peut conserver une trace légère de signaux techniques dans `Technical Notes`, mais les décisions techniques durables appartiennent à la spec ou aux ADRs.

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Brief: <title>

## Problem
Describe the user, product, business, or domain problem to solve.

## Users And Use Cases
Identify the target users and the main situations where the problem appears.

## Context
Capture relevant product, business, domain, strategic, or timing context.

## Solution Direction
Describe the current solution direction without over-specifying implementation details.

## Value Proposition
Explain why this direction creates value for users or the business.

## Scope
List what is included in the initiative at the product level.

## Out Of Scope
List what is intentionally excluded for now.

## Product Decisions
Record product or functional decisions already clarified.

## Technical Notes
Capture lightweight technical constraints, dependencies, or implementation signals mentioned during exploration.

## Constraints
List known business, UX, timing, budget, legal, operational, or technical constraints.

## Risks
List the main product, adoption, execution, business, or technical risks.

## Open Questions
List unresolved questions that should be answered before spec, validation, or implementation.

## References
Link to brainstorming notes, validation notes, research, issues, docs, or external references.
```

Règles de sections :

- `Problem` : required.
- `Users And Use Cases` : required.
- `Context` : required.
- `Solution Direction` : required.
- `Value Proposition` : required.
- `Scope` : required.
- `Out Of Scope` : required.
- `Product Decisions` : required.
- `Technical Notes` : optional.
- `Constraints` : required.
- `Risks` : required.
- `Open Questions` : required.
- `References` : optional.

## Règles de confirmation

- Pour une création ou une mise à jour substantielle, présenter un draft en conversation.
- Écrire seulement après validation utilisateur.
- Ne pas traiter le brief comme canonique après publication d'une spec.

## Limites

- Ne pas faire de brainstorming large.
- Ne pas faire de validation marché.
- Ne pas créer de spec technique.
- Ne pas mettre à jour `brief.md` automatiquement depuis d'autres skills.
