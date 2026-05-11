# `/capture`

## Objectif

Extraire une longue conversation, une session de recherche, une session de grilling ou une exploration dans une note markdown durable.

## À utiliser quand

- Une session a produit des conclusions utiles.
- Une recherche doit être conservée.
- Une longue discussion doit être condensée.
- L'utilisateur veut éviter de garder uniquement le contexte conversationnel brut.

## Entrées

- Conversation courante.
- Notes ou résultats de recherche.
- Session de grilling.
- Exploration du codebase ou de documentation.
- Chemin cible fourni explicitement par l'utilisateur, s'il existe.

## Comportement

- Si l'utilisateur donne un chemin, l'utiliser après avoir vérifié qu'il correspond au workflow.
- Si aucun chemin n'est donné, recommander `.initiatives/<id>/research/` ou `docs/research/` selon le scope.
- Demander à l'utilisateur de confirmer le chemin cible.
- Après confirmation du chemin, écrire directement sans draft complet en conversation.
- Résumer ce qui a été créé.

## Sorties

```text
.initiatives/<id>/research/<slug>.md
docs/research/<slug>.md
```

## Format

Pour une session de grilling, extraire :

- Faits.
- Hypothèses.
- Décisions clarifiées.
- Options comparées.
- Raisons des choix.
- Questions ouvertes.

Pour une session de recherche, structurer la sortie selon le sujet et les preuves, pas selon un template rigide de décisions.

Template adaptable :

```markdown
# <title>

## Context

## Key Findings

## Decisions Or Strong Signals

## Options Considered

## Open Questions

## Sources Or References
```

## Règles de confirmation

```text
confirmation du chemin -> écriture du fichier -> résumé du résultat
```

L'agent n'a pas besoin de montrer tout le document en draft, sauf demande explicite de l'utilisateur.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas créer d'ADR automatiquement.
- Ne pas publier dans GitHub par défaut.
