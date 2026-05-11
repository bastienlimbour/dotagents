# `/qa`

## Objectif

Générer une checklist de QA humaine pour une tâche, spec ou implémentation.

## À utiliser quand

- Une feature, tâche ou correction doit être validée manuellement.
- Les critères d'acceptation doivent être transformés en scénarios de vérification.
- Une implémentation touche des parcours utilisateur ou zones à risque.
- L'utilisateur veut un support de QA sans que l'agent prétende l'avoir exécutée.

## Entrées

- Source de vérité : issue, spec, task, brief ou prompt.
- Critères d'acceptation.
- Changements de code pertinents.
- Contexte produit ou parcours utilisateur.
- Vérifications techniques disponibles.

## Comportement

- Lire la source de vérité.
- Lire les critères d'acceptation.
- Inspecter les changements pertinents.
- Identifier les parcours utilisateur à valider.
- Mapper les checks aux critères d'acceptation.
- Inclure les préconditions et données de test.
- Inclure les checks de régression.
- Inclure les checks techniques : tests, build, lint ou typecheck lorsque pertinent.
- Inclure les risques ouverts.
- Proposer ensuite de créer un commentaire d'issue ou document local.

## Sorties

Checklist de QA en conversation par défaut.

Après confirmation, la checklist peut être créée comme commentaire d'issue ou document local.

## Format

La QA est orientée validation humaine du produit, pas seulement checks techniques.

Template :

```markdown
# QA Checklist: <task or spec>

## Context
Source de vérité relue, scope testé et limites.

## Preconditions
État initial, données requises, comptes, flags, environnement ou setup.

## User Flows To Validate
- [ ] Parcours principal.
- [ ] Parcours alternatif important.
- [ ] Erreur ou edge case important.

## Acceptance Criteria Mapping
- [ ] AC1: ...
- [ ] AC2: ...

## Regression Checks
- [ ] Zone existante qui pourrait avoir été cassée.

## Technical Checks
- [ ] Tests automatisés à lancer.
- [ ] Build, lint, typecheck ou autres commandes pertinentes.
- [ ] Logs, monitoring ou checks runtime si pertinent.

## Open Risks
Risques non entièrement couverts par cette checklist.
```

## Vérification finale

- Les checks couvrent les critères d'acceptation pertinents.
- Les préconditions et données de test nécessaires sont indiquées.
- Les risques ouverts sont explicites.
- L'agent ne prétend pas avoir exécuté la QA humaine.

## Limites

- Ne pas prétendre que la QA humaine a été faite.
- Ne pas modifier le code par défaut.
- Ne pas fermer d'issue automatiquement.
- Ne pas mettre à jour la spec automatiquement.
