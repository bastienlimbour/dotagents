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
- Lire les critères d'acceptation, user stories, scope items ou exigences explicites selon la source.
- Inspecter les changements pertinents.
- Identifier les parcours utilisateur à valider.
- Mapper les checks à la source de vérité : user stories, critères d'acceptation, scope items ou exigences explicites selon le contexte.
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

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# QA Checklist: <task or spec>

Source: <issue, spec, task, PR, or local path>

## Scope
Describe what this checklist validates and any important limits.

## Preconditions
List required environment, data, accounts, flags, setup, or initial state.

## User Flows To Validate
Checklist of user-facing flows to verify manually.
- [ ] <Primary flow>
- [ ] <Important alternate flow>
- [ ] <Important error or edge case>

## Source Coverage
Map checks to the relevant user stories, acceptance criteria, scope items, or explicit requirements.
- [ ] <Source item covered>

## Regression Checks
Checklist of existing behavior or areas that could regress.
- [ ] <Existing behavior or area that could regress>

## Technical Checks
Checklist of automated tests, build, lint, typecheck, runtime, or monitoring checks to run.
- [ ] <Automated test, build, lint, typecheck, or runtime check>

## Open Risks
List risks not fully covered by this checklist.
```

Règles de sections :

- `Source` : required.
- `Scope` : required.
- `Preconditions` : required.
- `User Flows To Validate` : required quand un comportement utilisateur existe.
- `Source Coverage` : required.
- `Regression Checks` : required.
- `Technical Checks` : required.
- `Open Risks` : required.

## Vérification finale

- Les checks couvrent les éléments pertinents de la source de vérité.
- Les préconditions et données de test nécessaires sont indiquées.
- Les risques ouverts sont explicites.
- L'agent ne prétend pas avoir exécuté la QA humaine.

## Limites

- Ne pas prétendre que la QA humaine a été faite.
- Ne pas modifier le code par défaut.
- Ne pas fermer d'issue automatiquement.
- Ne pas mettre à jour la spec automatiquement.
