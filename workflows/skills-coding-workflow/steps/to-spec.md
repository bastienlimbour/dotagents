# `/to-spec`

## Objectif

Synthétiser le contexte connu en spec canonique.

## À utiliser quand

- L'utilisateur est prêt à formaliser ce qui doit être construit.
- L'exploration a produit assez de clarté.
- Une petite feature peut passer directement de la conversation à une spec.

## Entrées

- Conversation.
- Brief.
- Notes de brainstorming.
- Notes de recherche.
- Recherche globale.
- `CONTEXT.md`.
- ADRs.
- Exploration du codebase.
- Issue existante.

## Comportement

- Lire le contexte fourni.
- Explorer le codebase lorsque nécessaire.
- Utiliser le langage de domaine du projet.
- Respecter les ADRs.
- Identifier les décisions produit et techniques durables.
- Chercher des opportunités de deep modules.
- Identifier les modules ou interfaces clés à créer, modifier ou préserver.
- Confirmer avec l'utilisateur les modules/interfaces clés et les zones principales à tester avant publication.
- Si une information critique manque, poser des questions ciblées.
- Si une incertitude est acceptable, la documenter dans `Risks And Open Questions`.
- Produire un draft complet de spec en conversation.
- Demander validation explicite.
- Publier ou écrire seulement après validation.

## Sorties

Sortie par défaut :

```text
Issue GitHub de spec
```

Fallback ou sortie locale explicite :

```text
.initiatives/<id>/spec.md
```

## Issue de spec

La spec est une issue GitHub par défaut.

Elle est l'issue parente logique de l'initiative ou de la feature.

La GitHub CLI ne crée pas de relation parent/enfant native entre issues. Les relations sont donc représentées par des liens explicites.

Responsabilités de l'issue de spec :

- Contenir la spec canonique.
- Lier les issues de tâches après création.
- Recevoir des commentaires ou checklists de QA globale si utile.
- Rester la source de vérité de ce qui doit être construit.

## Format

La spec est un document produit plus direction technique. Elle doit être assez précise pour être découpée en tâches verticales, mais assez durable pour survivre aux changements d'implémentation.

Ne pas inclure :

- Plan exhaustif fichier par fichier.
- Numéros de lignes.
- Snippets de code fragiles.
- Pseudo-code détaillé sauf nécessité forte.
- Micro-étapes que les implémenteurs de tâches pourront décider plus tard.

Template :

```markdown
# Spec: <title>

## Problem
Quel problème est résolu, pourquoi il compte, et quel contexte est pertinent.

## Solution
Solution retenue, comportement attendu et compromis importants.

## Users And Use Cases
Utilisateurs, personas si utile, cas d'usage et user stories lorsque pertinent.

## Scope
Ce qui est inclus.

## Out Of Scope
Ce qui est explicitement exclu.

## Product Decisions
Décisions produit et fonctionnelles importantes déjà clarifiées.

## Implementation Decisions
Direction technique durable, interfaces ou modules importants, deep modules visés, contraintes d'architecture.

## Testing Decisions
Comportements à tester, stratégie de test, risques de régression et feedback loops importantes.

## Acceptance Criteria
Critères globaux vérifiables pour l'initiative ou la feature.

## Risks And Open Questions
Incertitudes restantes, risques et hypothèses.
```

## Règles de confirmation

- Produire un draft complet en conversation avant publication ou écriture.
- Demander validation explicite.
- Confirmer les modules/interfaces clés et les zones principales à tester avant publication.

## Vérification finale

- La spec a une source de vérité claire : issue GitHub ou fichier local.
- Le scope et le out of scope sont explicites.
- Les critères d'acceptation sont vérifiables.
- Les risques et questions ouvertes acceptables sont documentés.

## Limites

- Ne pas faire une grosse interview par défaut.
- Ne pas inclure de plan d'implémentation fragile fichier par fichier.
- Ne pas créer d'issues de tâches. C'est le rôle de `/split`.
