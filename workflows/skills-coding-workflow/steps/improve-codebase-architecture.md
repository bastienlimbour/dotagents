# `/improve-codebase-architecture`

## Objectif

Identifier des opportunités pour rendre le codebase plus profond, plus testable, plus navigable et moins fragile pour le développement assisté par IA.

Ce skill est un outil d'analyse architecturale, pas un refactor automatique.

## À utiliser quand

- L'utilisateur veut améliorer la structure du codebase plutôt qu'ajouter une feature isolée.
- Le code montre des abstractions pass-through, duplication entre callers, mauvais seams ou faible locality.
- Une initiative requiert une analyse architecturale avant implémentation.
- Le développement assisté par IA est ralenti par une architecture difficile à explorer ou tester.

## Entrées

- `CONTEXT.md`.
- `CONTEXT-MAP.md` si disponible.
- ADRs.
- Codebase.
- Specs, issues ou zones problématiques fournies par l'utilisateur.
- Tests ou feedback loops existants.

## Concepts clés

- Module : unité de comportement avec une responsabilité identifiable.
- Interface : surface publique utilisée par les callers.
- Implementation : complexité interne cachée derrière l'interface.
- Depth : rapport entre simplicité de l'interface et valeur du comportement caché.
- Seam : frontière où l'on peut tester, remplacer ou adapter une partie du système.
- Adapter : couche qui traduit entre deux interfaces ou systèmes.
- Leverage : quantité de complexité ou duplication supprimée pour les callers.
- Locality : capacité à comprendre ou modifier un comportement dans une zone limitée du code.

## Comportement

- Lire `CONTEXT.md`.
- Lire les ADRs.
- Explorer le codebase.
- Identifier les modules superficiels, abstractions pass-through, mauvais seams et zones à faible locality.
- Appliquer le deletion test.
- Présenter des candidats d'amélioration architecturale.
- Demander à l'utilisateur de choisir.
- Utiliser une boucle de grilling pour les designs sélectionnés.
- Créer des ADRs seulement lorsque les critères stricts sont remplis.
- Implémenter des refactors uniquement après décision explicite de l'utilisateur.

## Sorties

- Carte ou synthèse des problèmes architecturaux pertinents.
- Candidats d'amélioration classés par impact, risque et effort.
- Recommandation sur le ou les candidats à traiter.
- ADR proposé seulement si les critères ADR sont remplis.
- Refactor implémenté seulement après décision explicite.

## Format

### ADR

Créer un ADR seulement si les critères stricts sont remplis : décision difficile à inverser, surprenante sans contexte, et impliquant un vrai compromis entre options.

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

## Deletion test

```text
Si je supprime ce module, est-ce que la complexité disparaît ?
Si oui, c'était probablement un pass-through.
Si la complexité réapparaît dans N callers, le module justifiait probablement son existence.
```

## Règles de confirmation

- Demander à l'utilisateur de choisir les candidats à approfondir.
- Demander confirmation avant tout ADR.
- Demander confirmation explicite avant tout refactor d'architecture.

## Vérification finale

- Les recommandations sont reliées à des observations concrètes du code.
- Les tradeoffs sont explicités.
- Les décisions locales ne sont pas promues en ADR.
- Aucun refactor n'est appliqué sans accord explicite.

## Limites

- Ne pas refactorer pour l'esthétique.
- Ne pas implémenter de changement d'architecture sans choix utilisateur.
- Ne pas créer d'ADR pour des décisions locales ou facilement réversibles.
