# `/to-spec`

## Objectif

Synthétiser le contexte connu en spec canonique.

## À utiliser quand

- L'utilisateur est prêt à formaliser ce qui doit être construit.
- L'exploration a produit assez de clarté.
- Une petite feature peut passer directement de la conversation à une spec.

## Entrées

- Conversation.
- Brief.
- Notes de brainstorming.
- Notes de recherche.
- Recherche globale.
- `CONTEXT.md`.
- ADRs.
- Exploration du codebase.
- Issue existante.

## Comportement

- Lire le contexte fourni.
- Explorer le codebase lorsque nécessaire.
- Utiliser le langage de domaine du projet.
- Respecter les ADRs.
- Identifier les décisions produit et techniques durables.
- Chercher des opportunités de deep modules.
- Identifier les modules ou interfaces clés à créer, modifier ou préserver.
- Confirmer avec l'utilisateur les modules/interfaces clés et les zones principales à tester avant publication.
- Produire une liste longue mais non artificielle de user stories avec IDs stables et immuables.
- Si une information critique manque, poser des questions ciblées.
- Si une incertitude est acceptable, la documenter dans `Risks And Open Questions`.
- Produire un draft complet de spec en conversation.
- Demander validation explicite.
- Publier ou écrire seulement après validation.

## Sorties

Sortie par défaut :

```text
Issue de spec dans le tracker distant GitHub ou GitLab
```

Fallback ou sortie locale explicite :

```text
.initiatives/<id>/spec.md
```

## Issue de spec

La spec est une issue dans le tracker distant configuré par défaut : GitHub ou GitLab.

Elle est l'issue parente logique de l'initiative ou de la feature.

Les CLI des trackers distant (Github ou Gitlab) ne permettent pas de relation parent/enfant native entre issues. Les relations sont donc représentées par des liens explicites.

Responsabilités de l'issue de spec :

- Contenir la spec canonique.
- Lier les issues de tâches après création.
- Recevoir des commentaires ou checklists de QA globale si utile.
- Rester la source de vérité de ce qui doit être construit.

## Format

La spec est un document produit plus direction technique. Elle doit être assez précise pour être découpée en tâches verticales, mais assez durable pour survivre aux changements d'implémentation.

Ne pas inclure :

- Plan exhaustif fichier par fichier.
- Numéros de lignes.
- Snippets de code fragiles.
- Pseudo-code détaillé sauf nécessité forte.
- Micro-étapes que les implémenteurs de tâches pourront décider plus tard.

La spec ne contient pas de section `Acceptance Criteria` par défaut. Les acceptance criteria détaillés sont créés au niveau task pendant `/split`, à partir des user stories, du scope, des décisions et des contraintes pertinentes.

Règles des user stories :

- Utiliser des IDs stables et immuables : `US-001`, `US-002`, etc.
- Ne jamais renuméroter les IDs existants.
- Si une user story n'est plus valide, la marquer comme `Deprecated` ou `Replaced by US-0XX`.
- Les nouvelles user stories prennent le prochain ID disponible.
- Format : `US-001 - As a <actor>, I want <capability>, so that <benefit>.`
- La liste doit couvrir les acteurs, cas d'usage, variantes, edge cases produit et bénéfices importants, sans créer de stories artificielles.

Règle de durabilité :

- Ne pas inclure de plan fichier par fichier, numéros de lignes ou snippets de code fragiles.
- Exception : si un prototype a produit un snippet qui encode une décision plus précisément que la prose, par exemple state machine, reducer, schema ou type shape, l'inclure dans la section pertinente et noter brièvement qu'il vient d'un prototype.

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Spec: <title>

## Problem Statement
Describe the problem from the user's perspective, why it matters, and the relevant context.

## Solution
Describe the selected solution, expected behavior, and important tradeoffs.

## User Stories
Long list of stable user stories using: `US-001 - As a <actor>, I want <capability>, so that <benefit>.`

US-001 - As a <actor>, I want <capability>, so that <benefit>.
US-002 - As a <actor>, I want <capability>, so that <benefit>.

## Scope
List what is included in this spec.

## Out Of Scope
List what is explicitly excluded from this spec.

## Product Decisions
Record important product and functional decisions already clarified.

## Implementation Decisions
Record durable technical direction, key interfaces or modules, deep modules targeted, and architecture constraints.

## Testing Decisions
Record behaviors to test, testing strategy, regression risks, and important feedback loops.

## Risks And Open Questions
List remaining uncertainties, risks, assumptions, and questions that are acceptable to carry forward.

## Further Notes
Add only useful notes that do not fit elsewhere.
```

Règles de sections :

- `Problem Statement` : required.
- `Solution` : required.
- `User Stories` : required.
- `Scope` : required.
- `Out Of Scope` : required.
- `Product Decisions` : required.
- `Implementation Decisions` : required.
- `Testing Decisions` : required.
- `Risks And Open Questions` : required.
- `Further Notes` : optional.

## Règles de confirmation

- Produire un draft complet en conversation avant publication ou écriture.
- Demander validation explicite.
- Confirmer les modules/interfaces clés et les zones principales à tester avant publication.

## Vérification finale

- La spec a une source de vérité claire : issue GitHub/GitLab ou fichier local.
- Le scope et le out of scope sont explicites.
- Les user stories ont des IDs stables et couvrent les cas d'usage importants.
- Les risques et questions ouvertes acceptables sont documentés.

## Limites

- Ne pas faire une grosse interview par défaut.
- Ne pas inclure de plan d'implémentation fragile fichier par fichier.
- Ne pas créer de section `Acceptance Criteria` par défaut.
- Ne pas créer d'issues de tâches. C'est le rôle de `/split`.
