# `/validate`

## Objectif

Réduire l'incertitude autour d'une idée, solution, feature, marché, direction technique ou hypothèse business.

## À utiliser quand

- L'utilisateur a besoin de confiance avant d'investir dans l'implémentation.
- Une direction produit est risquée.
- La faisabilité technique est incertaine.
- L'incertitude marché, concurrentielle, coût ou business model compte.

## Entrées

- Conversation courante.
- Brief, brainstorming ou notes de recherche.
- Hypothèse à valider.
- Codebase ou documentation si la validation est technique.
- Sources externes si une recherche est confirmée par l'utilisateur.

## Comportement

- Lire le contexte fourni.
- Identifier les incertitudes critiques.
- Proposer les axes de validation.
- Recommander une profondeur d'analyse.
- Demander confirmation avant recherche ou analyse approfondie.
- Distinguer faits, sources, hypothèses, signaux faibles, interprétations, inconnues et niveau de confiance.
- Produire un rapport léger en v1.
- Inclure un verdict lorsque utile : `Go`, `No-Go`, `Pivot` ou `Needs More Research`.

## Axes possibles

- Problème utilisateur.
- Marché et concurrents.
- Faisabilité technique.
- Coûts et business model.
- Distribution et acquisition.
- Risque légal ou réglementaire.
- UX et adoption.
- Différenciation.

## Sorties

Sortie par défaut :

```text
.initiatives/<id>/validation.md
```

Si la validation est utile globalement :

```text
docs/research/<slug>.md
```

## Format

Template adaptable :

```markdown
# Validation: <title>

## Question

## Context

## Critical Uncertainties

## Evidence

## Interpretation

## Confidence

## Verdict
Go | No-Go | Pivot | Needs More Research

## Open Questions
```

## Règles de confirmation

- Demander confirmation avant recherche ou analyse approfondie.
- Demander confirmation du chemin cible avant écriture.
- Ne pas transformer automatiquement le rapport en décision produit finale.

## Vérification finale

- Les faits, hypothèses et interprétations sont séparés.
- Le niveau de confiance est explicite.
- Les sources ou preuves importantes sont citées lorsque disponibles.
- Le verdict, s'il existe, reste proportionné aux preuves.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas présenter le verdict comme une certitude.
- Garder la v1 légère.
