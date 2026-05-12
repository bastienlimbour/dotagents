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
- Lire `CONTEXT-MAP.md` s'il existe pour identifier le bon contexte, sinon lire le `CONTEXT.md` disponible.
- Lire les ADRs et la documentation utile avant de challenger une décision déjà documentée.
- Si plusieurs contextes existent et que le contexte cible est ambigu, poser une seule question pour le choisir.
- Challenger les termes flous ou ambigus.
- Aligner les termes avec le glossaire existant et signaler immédiatement les conflits.
- Proposer un terme canonique précis lorsqu'un mot est vague, surchargé ou utilisé pour plusieurs concepts.
- Tester les relations de domaine avec des scénarios concrets et des edge cases.
- Vérifier les contradictions entre conversation, documentation et code.
- Formuler les contradictions comme des décisions à trancher, pas comme des corrections silencieuses.
- Mettre à jour `CONTEXT.md` lorsqu'un langage de domaine est clarifié.
- Mettre à jour `CONTEXT.md` au fil de l'eau, sans attendre la fin de la session, lorsque la clarification est suffisamment stable.
- Si aucun `CONTEXT.md` pertinent n'existe, proposer sa création seulement lorsqu'un premier terme durable est clarifié.
- Proposer un ADR lorsqu'une décision globale durable satisfait les critères ADR.
- Demander confirmation avant de créer un ADR.

## Sorties

- Clarifications en conversation.
- Mise à jour de `CONTEXT.md` si un langage de domaine durable est clarifié.
- Proposition d'ADR si les critères ADR sont remplis.
- ADR créé seulement après confirmation.

## Format

### `CONTEXT.md`

`CONTEXT.md` est strictement un glossaire et un document de langage de domaine partagé. Il ne doit pas être utilisé comme mémoire générale du projet.

Il doit contenir uniquement des concepts métier ou de domaine utiles aux experts du projet. Les détails d'implémentation, concepts génériques de programmation, patterns techniques et notes temporaires n'y appartiennent pas.

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Context

## Canonical Terms
List approved domain terms and their concise meanings.

## Terms To Avoid
List ambiguous, deprecated, or misleading terms and what to use instead.

## Domain Relationships
Describe important relationships between domain concepts.

## Examples
Show short examples of correct domain language in realistic usage.

## Resolved Ambiguities
Record domain ambiguities that have been clarified and the chosen interpretation.
```

Règles de sections :

- `Canonical Terms` : required.
- `Terms To Avoid` : required.
- `Domain Relationships` : required.
- `Examples` : required.
- `Resolved Ambiguities` : required.

Règles de rédaction :

- Définir chaque terme en une phrase courte.
- Décrire ce que le concept est, pas son implémentation ni toutes ses actions.
- Être opinionated : choisir un terme canonique et lister les synonymes ou termes trompeurs à éviter.
- Exprimer les relations et cardinalités lorsqu'elles sont claires.
- Ajouter ou modifier seulement les éléments stables et réutilisables au-delà de la session courante.

### ADR

Créer un ADR seulement si les critères stricts sont remplis : décision difficile à inverser, surprenante sans contexte, et impliquant un vrai compromis entre options.

Les ADRs vivent dans `docs/adr/` avec une numérotation séquentielle `0001-short-slug.md`, `0002-short-slug.md`, etc. Pour créer un nouvel ADR, scanner les ADRs existants et incrémenter le plus grand numéro.

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# ADR: <short decision title>

## Context
Explain the situation, forces, constraints, and why a decision is needed.

## Decision
State the chosen decision clearly.

## Consequences
Describe expected benefits, costs, risks, and follow-up implications.

## Alternatives Considered
List the serious alternatives considered and why they were not chosen.
```

Règles de sections :

- `Context` : required.
- `Decision` : required.
- `Consequences` : required.
- `Alternatives Considered` : required.

Exemples de décisions qui peuvent qualifier :

- Choix de stack ou dépendance structurante difficile à remplacer.
- Pattern d'intégration entre contextes ou systèmes.
- Frontière durable de responsabilité entre domaines.
- Contrainte business, légale ou opérationnelle non visible dans le code.
- Déviation volontaire d'un choix évident qu'un futur développeur pourrait vouloir "corriger".

## Règles de confirmation

- Mettre à jour `CONTEXT.md` seulement pour des clarifications stables et durables.
- Demander confirmation avant de créer un nouveau `CONTEXT.md` ou de choisir un emplacement ambigu.
- Demander confirmation avant de créer un ADR.
- Ne pas commenter d'issue ni créer de note de recherche sans demande ou confirmation.

## Vérification finale

- Les termes clarifiés sont documentés au bon endroit.
- Les termes documentés sont des concepts de domaine, pas des détails techniques génériques.
- Les contradictions importantes entre conversation, documentation et code sont signalées.
- Les décisions qui ne satisfont pas les critères ADR ne sont pas promues en ADR.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas créer de notes de recherche automatiquement.
- Ne pas traiter `CONTEXT.md` comme une mémoire générale du projet.
- Ne pas documenter les concepts génériques de programmation dans `CONTEXT.md`.
- Ne pas promouvoir une préférence locale ou facilement réversible en ADR.
- Ne pas transformer la session en analyse d'architecture complète.
