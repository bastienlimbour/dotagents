# `/split`

## Objectif

Découper une spec ou un plan en tâches verticales, indépendantes et actionnables.

## À utiliser quand

- Une spec doit être transformée en tâches d'exécution.
- Un plan est trop large pour être implémenté directement.
- L'utilisateur veut créer des issues de tâches ou des fichiers locaux de tâches.
- Il faut préserver des tranches verticales plutôt qu'un découpage par couches techniques.

## Entrées

- Spec ou plan fourni.
- Issue de spec GitHub.
- `spec.md` local.
- Critères d'acceptation globaux.
- Contraintes, dépendances et décisions issues du contexte.

## Comportement

- Lire la spec ou tout autre contexte fourni.
- Conserver le principe de tracer bullets.
- Proposer des tâches sous forme de tranches verticales.
- Faire en sorte que chaque tâche soit independently-grabbable : un agent doit pouvoir la prendre avec peu ou pas de contexte oral supplémentaire.
- Inclure titre, objectif, critères d'acceptation, dépendances, notes, `Blocked by` et `User stories covered` lorsque pertinent.
- Annoter chaque tâche comme `AFK` ou `HITL` lorsque utile.
- Présenter le découpage complet pour validation.
- Demander un retour sur granularité, ordre, dépendances, tâches à fusionner ou séparer, et scope.
- Créer les issues ou fichiers locaux seulement après validation explicite.
- Avec GitHub, commenter l'issue de spec avec la liste des issues de tâches.
- Avec GitHub, ajouter le lien vers l'issue de spec en haut de chaque issue de tâche.

## Classification optionnelle

- `AFK` : la tâche semble pouvoir être prise par un agent sans interaction humaine supplémentaire, car le contrat d'exécution est suffisamment clair.
- `HITL` : la tâche nécessite probablement une décision, une review ou une intervention humaine.

Cette classification est informative en v1. Elle ne crée pas de label GitHub et ne déclenche pas de triage automatique.

## Sorties

Sortie par défaut :

```text
Issues GitHub de tâches
```

Fallback ou sortie locale explicite :

```text
.initiatives/<id>/tasks/<NNN-task-slug>.md
```

## Critères d'une bonne tâche

- Représenter une tranche verticale.
- Lier l'issue de spec parente en haut de l'issue.
- Inclure scope, critères d'acceptation, dépendances et notes.
- Être actionnable par un agent avec peu de contexte oral additionnel.
- Livrer un comportement observable ou une décision vérifiable lorsque possible.

Après création des tâches, l'agent commente l'issue de spec avec la liste des issues de tâches.

## Format

Les tâches locales sont le miroir des issues de tâches GitHub.

Chemin :

```text
.initiatives/<id>/tasks/<NNN-task-slug>.md
```

Template :

```markdown
# Task: <title>

Parent spec: ../spec.md

## What To Build

## Acceptance Criteria

## Scope

## Out Of Scope

## Dependencies

## Blocked By

## User Stories Covered

## Notes
```

## Règles de confirmation

- Présenter le découpage complet avant création.
- Demander validation explicite avant de créer des issues ou fichiers.
- Demander un retour sur granularité, ordre, dépendances, tâches à fusionner ou séparer, et scope.

## Vérification finale

- Chaque tâche est independently-grabbable.
- Le découpage évite les couches horizontales sauf nécessité explicite et justifiée.
- Les dépendances et blocages sont visibles.
- Les liens entre spec parente et tâches sont présents.

## Limites

- Ne pas implémenter les tâches.
- Ne pas créer d'issues avant validation.
- Ne pas découper en couches horizontales sauf nécessité explicite et justifiée.
