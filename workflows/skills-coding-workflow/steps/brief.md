# `/brief`

## Objectif

Créer, initialiser ou mettre à jour un brief produit optionnel pour une initiative.

## À utiliser quand

- L'utilisateur a une idée vague et veut la cadrer.
- Un projet greenfield nécessite une première clarté produit.
- Une grosse feature nécessite un artefact d'exploration produit.
- L'utilisateur veut consolider un brainstorming, une recherche ou une exploration en source de vérité produit.
- L'utilisateur demande explicitement d'initialiser ou mettre à jour un brief.

## Entrées

- Conversation courante.
- Notes de brainstorming.
- Notes de recherche.
- Session de grilling.
- Contexte produit, business, domaine ou stratégique fourni par l'utilisateur.

## Comportement

- Si l'utilisateur veut seulement initialiser une initiative, préparer un squelette de brief avec les sections canoniques.
- Si aucun chemin ou initiative n'est fourni, scanner `.initiatives/`, proposer le prochain dossier `<NNN-slug>` en kebab-case et confirmer `.initiatives/<NNN-slug>/brief.md` avant écriture.
- Si l'utilisateur fournit du contexte, l'analyser et identifier les manques critiques.
- Explorer légèrement les sources disponibles du repo lorsque ces sources peuvent répondre au contexte produit ou domaine avant de questionner l'utilisateur.
- Si des informations critiques manquent, poser une seule question ciblée à la fois, sauf si l'utilisateur demande explicitement une liste de questions.
- Ne pas inventer. Si une section required manque d'information fiable mais n'est pas bloquante, utiliser `Not known yet`.
- Pour une initialisation squelettique, écrire après confirmation du chemin cible.
- Pour du contenu substantiel, proposer un draft en conversation.
- Écrire ou mettre à jour `brief.md` seulement après validation utilisateur.

## Sorties

```text
.initiatives/<id>/brief.md
```

## Format

`brief.md` est optionnel. Il est utile pour les projets greenfield, les grosses initiatives, les features substantielles et les situations où l'exploration produit compte.

S'il existe, il devient la source de vérité produit locale de l'initiative pour le contexte d'exploration.

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

## Success Measures
Describe the expected outcomes or lightweight signals that would indicate the initiative is valuable.

## Scope
List what is included in the initiative at the product level.

## Deferred / Future Scope
List what is not included now but might be considered later.

## Out Of Scope
List what is explicitly excluded from this initiative unless revisited by a later decision.

## Product Decisions
Record product or functional decisions already clarified.

## Assumptions To Validate
List important assumptions, bets, or kill risks already identified.

## Technical Notes
Capture lightweight technical constraints, dependencies, or implementation signals mentioned during exploration.

## Constraints
List known business, UX, timing, budget, legal, operational, or technical constraints.

## Risks
List the main product, adoption, execution, business, or technical risks.

## Open Questions
List unresolved questions that should be answered before spec, validation, or implementation.
```

Règles de sections :

- `Problem` : required.
- `Users And Use Cases` : required.
- `Context` : required.
- `Solution Direction` : required.
- `Value Proposition` : required.
- `Success Measures` : optional.
- `Scope` : required.
- `Deferred / Future Scope` : required.
- `Out Of Scope` : required.
- `Product Decisions` : required.
- `Assumptions To Validate` : optional.
- `Technical Notes` : optional.
- `Constraints` : required.
- `Risks` : required.
- `Open Questions` : required.

Les sections optional sont incluses seulement si elles apportent une information utile.

`Constraints` contient les contraintes qui bornent l'initiative, y compris produit, UX, business, timing, légal, opérationnel ou technique.

`Technical Notes` contient uniquement des signaux techniques légers observés pendant l'exploration, non encore transformés en décisions durables.

## Règles de confirmation

- Pour une initialisation squelettique, confirmer le chemin cible avant écriture.
- Pour une création ou une mise à jour substantielle, présenter un draft en conversation.
- Écrire seulement après validation utilisateur.

## Limites

- Ne pas faire de brainstorming large.
- Ne pas faire de validation marché.
- Ne pas créer de spec technique.
- Ne pas transformer l'exploration légère du repo en audit codebase lourd par défaut.
