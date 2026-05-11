# `/grill-with-docs`

## Objectif

Mener une session de grilling tout en maintenant la documentation globale lorsque c'est pertinent.

Ce step est `/grill-me` avec une responsabilité supplémentaire : préserver ou améliorer les sources de vérité durables du projet.

## À utiliser quand

- L'utilisateur veut clarifier une décision, un design ou un plan avec impact durable sur le projet.
- Le vocabulaire de domaine, les concepts ou les frontières de contexte sont ambigus.
- La conversation peut révéler une contradiction entre code, documentation et intention.
- Une décision globale pourrait mériter un ADR.

## Entrées

- Conversation courante.
- Codebase pertinent.
- `CONTEXT.md`.
- `CONTEXT-MAP.md`.
- ADRs.
- Documentation projet utile.
- Brief, spec, notes de recherche ou issue lorsque disponibles.

## Comportement

- Poser une question à la fois.
- Fournir une recommandation.
- Explorer le codebase lorsque pertinent.
- Lire `CONTEXT.md`, `CONTEXT-MAP.md`, les ADRs et la documentation utile.
- Challenger les termes flous ou ambigus.
- Vérifier les contradictions entre conversation, documentation et code.
- Mettre à jour `CONTEXT.md` lorsqu'un langage de domaine est clarifié.
- Mettre à jour `CONTEXT.md` au fil de l'eau, sans attendre la fin de la session, lorsque la clarification est suffisamment stable.
- Proposer un ADR lorsqu'une décision globale durable satisfait les critères ADR.
- Demander confirmation avant de créer un ADR.

## Sorties

- Clarifications en conversation.
- Mise à jour de `CONTEXT.md` si un langage de domaine durable est clarifié.
- Proposition d'ADR si les critères ADR sont remplis.
- ADR créé seulement après confirmation.

## Règles de confirmation

- Mettre à jour `CONTEXT.md` seulement pour des clarifications stables et durables.
- Demander confirmation avant de créer un ADR.
- Ne pas commenter d'issue ni créer de note de recherche sans demande ou confirmation.

## Vérification finale

- Les termes clarifiés sont documentés au bon endroit.
- Les contradictions importantes entre conversation, documentation et code sont signalées.
- Les décisions qui ne satisfont pas les critères ADR ne sont pas promues en ADR.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas créer de notes de recherche automatiquement.
- Ne pas traiter `CONTEXT.md` comme une mémoire générale du projet.
