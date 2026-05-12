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

Pas de template canonique.

La structure doit être choisie par l'agent selon ce qui est capturé : session de grilling, recherche, exploration codebase, longue discussion, comparaison d'options ou autre contexte durable.

Règles :

- Garder un titre clair.
- Structurer le document selon le sujet, pas selon un template rigide.
- Lorsque c'est utile (après une session de gilling par exemple), extraire et séparer faits, hypothèses, interprétations, décisions, options, raisons des choix, et questions ouvertes
- Citer les sources ou références importantes lorsqu'elles existent.
- Ne pas créer automatiquement d'ADR, de spec ou de brief depuis une capture.

## Règles de confirmation

```text
confirmation du chemin -> écriture du fichier -> résumé du résultat
```

L'agent n'a pas besoin de montrer tout le document en draft, sauf demande explicite de l'utilisateur.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas créer d'ADR automatiquement.
- Ne pas publier dans l'issue tracker distant par défaut.
