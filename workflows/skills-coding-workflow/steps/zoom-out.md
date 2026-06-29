# `/zoom-out`

## Objectif

Remonter d'un niveau d'abstraction et cartographier les modules, concepts, flux et callers pertinents.

## À utiliser quand

- L'utilisateur ou l'agent manque de vue d'ensemble sur une zone du codebase.
- Une implémentation, review ou analyse d'architecture nécessite une carte des relations.
- Il faut comprendre les concepts de domaine, modules, flux ou callers avant d'agir.
- Le risque principal est de modifier localement sans comprendre les dépendances.

## Entrées

- Question ou zone du codebase à cartographier.
- `CONTEXT.md` si disponible.
- `CONTEXT-MAP.md` si disponible.
- Code pertinent.
- Documentation, ADRs ou issues liées lorsque disponibles.

## Comportement

- Lire `CONTEXT.md` si disponible.
- Explorer le code pertinent.
- Produire une carte concise des modules et relations.
- Utiliser le vocabulaire de domaine lorsque disponible.
- Aider l'utilisateur ou l'agent à retrouver une vue d'ensemble.

## Sorties

Carte concise en conversation par défaut.

La carte peut couvrir :

- Modules pertinents.
- Callers et callees importants.
- Concepts de domaine.
- Flux de données ou d'événements.
- Seams utiles pour tester ou modifier.
- Risques de dépendance ou de couplage.

## Prompt mental de référence

```
Go up a layer of abstraction.
Give me a map of relevant modules and callers,
using the project domain glossary vocabulary.
```

## Vérification finale

- La carte reste concise.
- Les relations importantes sont explicites.
- Le vocabulaire de domaine est utilisé lorsqu'il existe.
- Aucune modification de code ou d'artefact n'est faite sans demande explicite.

## Limites

- Ne pas refactorer.
- Ne pas implémenter.
- Ne pas créer d'artefact sauf demande explicite.
