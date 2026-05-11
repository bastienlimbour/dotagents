# `/implement`

## Objectif

Implémenter une tâche, petite feature, correction de bug ou changement clairement cadré avec un workflow pragmatique non TDD strict.

## À utiliser quand

- L'utilisateur demande de construire ou modifier du code à partir d'un contexte suffisamment clair.
- Une issue, spec, tâche ou conversation fournit un execution contract exploitable.
- Le travail ne requiert pas explicitement un cycle TDD strict.
- Le changement peut être réalisé en une ou plusieurs tranches verticales raisonnables.

## Entrées

- Prompt utilisateur.
- Issue de tâche ou spec.
- Brief ou notes locales si elles sont la source de contexte disponible.
- Codebase et documentation projet.
- Critères d'acceptation.
- Feedback loop attendue ou inférable.

## Execution contract

Établir le contrat minimal avant de coder :

- Goal.
- Scope.
- Out of scope.
- Acceptance criteria.
- Constraints.
- Feedback loop.
- Source of truth.

Si le contexte critique manque, lister les manques, proposer des hypothèses et questionner l'utilisateur.

## Comportement

- Établir l'execution contract à partir du contexte.
- Explorer le codebase avant modification.
- Faire le plus petit changement correct.
- Identifier ou créer une feedback loop adaptée.
- Ajouter ou modifier des tests lorsque pertinent.
- Lancer les vérifications pertinentes lorsque possible.
- Résumer les changements et vérifications.
- Si une issue de tâche a servi de contexte, proposer un commentaire d'issue avec résumé, tests et points restants.

## Vérification finale

- Le changement respecte l'execution contract.
- Les critères d'acceptation pertinents sont couverts ou les écarts sont explicités.
- Les vérifications pertinentes ont été lancées, ou l'impossibilité de les lancer est documentée.
- Les changements sont résumés avec les fichiers importants et les risques restants.

## Limites

- Ne pas coder silencieusement à partir d'hypothèses floues.
- Ne pas fermer d'issue automatiquement en v1.
- Ne pas transformer une grosse spec en implémentation incontrôlée.
- Si l'entrée est trop large, proposer une première tranche verticale minimale et demander confirmation.
