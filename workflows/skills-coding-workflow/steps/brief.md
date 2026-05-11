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

Template :

```markdown
# Brief: <title>

## Problem
Quel problème doit être résolu.

## Target Users
Pour qui le problème est résolu.

## Context
Contexte produit, business, domaine ou stratégique pertinent.

## Proposed Solution
Direction de solution actuelle.

## Value Proposition
Pourquoi cette solution crée de la valeur.

## Use Cases
Cas d'usage principaux.

## Product Decisions
Décisions produit déjà clarifiées.

## Constraints
Contraintes connues : business, UX, techniques, timing, budget, légales ou autres.

## Risks
Risques principaux.

## Open Questions
Questions non résolues.

## Out Of Scope
Ce qui est exclu pour le moment.

## References
Liens vers `brainstorming.md`, `research/*.md`, issues ou documents externes.
```

## Règles de confirmation

- Pour une création ou une mise à jour substantielle, présenter un draft en conversation.
- Écrire seulement après validation utilisateur.
- Ne pas traiter le brief comme canonique après publication d'une spec.

## Limites

- Ne pas faire de brainstorming large.
- Ne pas faire de validation marché.
- Ne pas créer de spec technique.
- Ne pas mettre à jour `brief.md` automatiquement depuis d'autres skills.
