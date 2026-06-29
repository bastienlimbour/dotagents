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
- Issue de spec GitHub ou GitLab.
- `spec.md` local.
- Critères d'acceptation globaux.
- Contraintes, dépendances et décisions issues du contexte.

## Comportement

- Lire la spec ou tout autre contexte fourni.
- Conserver le principe de tracer bullets.
- Proposer des tâches sous forme de tranches verticales.
- Faire en sorte que chaque tâche soit independently-grabbable : un agent doit pouvoir la prendre avec peu ou pas de contexte oral supplémentaire.
- Inclure titre, type `AFK` ou `HITL`, comportement à construire, user stories couvertes, critères d'acceptation, blocages et notes lorsque pertinent.
- Annoter chaque tâche comme `AFK` ou `HITL`.
- Présenter le découpage complet pour validation.
- Demander un retour sur granularité, ordre, dépendances, tâches à fusionner ou séparer, et scope.
- Créer les issues ou fichiers locaux seulement après validation explicite.
- Avec un tracker distant, commenter l'issue de spec avec la liste des issues de tâches.
- Avec un tracker distant, ajouter le lien vers l'issue de spec en haut de chaque issue de tâche.

## Classification

- `AFK` : la tâche semble pouvoir être prise par un agent sans interaction humaine supplémentaire, car le contrat d'exécution est suffisamment clair.
- `HITL` : la tâche nécessite probablement une décision, une review ou une intervention humaine.

Cette classification est obligatoire dans le corps de chaque tâche, mais informative en v1. Elle ne crée pas de label d'issue tracker et ne déclenche pas de triage automatique.

## Critères d'une bonne tâche

- Représenter une tranche verticale.
- Lier l'issue de spec parente en haut de l'issue.
- Inclure le comportement end-to-end à construire, les user stories couvertes, les critères d'acceptation et les blocages.
- Être actionnable par un agent avec peu de contexte oral additionnel.
- Livrer un comportement observable ou une décision vérifiable lorsque possible.

Après création des tâches, l'agent commente l'issue de spec avec la liste des issues de tâches.

## Sorties

Sortie par défaut :

```
Issues GitHub/GitLab de tâches
```

Fallback ou sortie locale explicite :

```
.initiatives/<id>/tasks/<NNN-task-slug>.md
```

Les CLI des trackers distant (Github ou Gitlab) ne permettent pas de relation parent/enfant native entre issues. Les relations sont donc représentées par des liens explicites.

## Format

Les tâches locales sont le miroir des issues de tâches du tracker distant.

Chemin :

```
.initiatives/<id>/tasks/<NNN-task-slug>.md
```

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```md
# Task: <title>

Parent spec: <link or path>

Type: AFK | HITL

## What To Build
Describe the narrow end-to-end behavior this vertical slice must deliver, not a layer-by-layer implementation plan.

## User Stories Covered
Reference only stable user story IDs from the parent spec with short labels.

- US-001 - <short label>
- US-004 - <short label>

## Acceptance Criteria
Checklist of observable, verifiable outcomes for this task.

- [ ] <Observable behavior or outcome>
- [ ] <Important edge case or constraint>
- [ ] <Regression-sensitive behavior, if relevant>

## Blocked By
List blocking tasks or state that the task can start immediately.

None - can start immediately.

## Notes
Add only useful clarifications, constraints, prior art, or prototype-derived decision snippets that do not fit elsewhere.
```

Règles de sections :

- `Parent spec` : required.
- `Type` : required.
- `What To Build` : required. Décrire le comportement end-to-end de la tranche verticale, pas un plan fichier par fichier.
- `User Stories Covered` : required lorsque la spec parente contient des user stories. Référencer uniquement les IDs stables avec un short label.
- `Acceptance Criteria` : required. Utiliser une checklist de critères observables et vérifiables, sans limite stricte de nombre.
- `Blocked By` : required. Utiliser `None - can start immediately.` s'il n'y a aucun blocage.
- `Notes` : optional.

Ne pas ajouter de sections `Scope`, `Out Of Scope`, `Verification` ou `Feedback Loop` par défaut. Les feedback loops et commandes de vérification doivent venir des conventions du repo et du contexte agent.

## Règles de confirmation

- Présenter le découpage complet avant création.
- Demander validation explicite avant de créer des issues ou fichiers.
- Demander un retour sur granularité, ordre, dépendances, tâches à fusionner ou séparer, et scope.

## Vérification finale

- Chaque tâche est independently-grabbable.
- Le découpage évite les couches horizontales sauf nécessité explicite et justifiée.
- Les blocages sont visibles.
- Les liens entre spec parente et tâches sont présents.

## Limites

- Ne pas implémenter les tâches.
- Ne pas créer d'issues avant validation.
- Ne pas découper en couches horizontales sauf nécessité explicite et justifiée.
