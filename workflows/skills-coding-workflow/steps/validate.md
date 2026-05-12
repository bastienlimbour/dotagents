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
- Partir d'un brief ou contexte équivalent plutôt que d'une question unique.
- Identifier les incertitudes critiques.
- Choisir les axes de validation pertinents parmi les axes canoniques.
- Recommander une profondeur d'analyse.
- Demander confirmation avant recherche ou analyse approfondie.
- Sous-traiter les recherches par axe à des sub-agents lorsque cela aide à séparer les analyses.
- Condenser les recherches des sub-agents dans `validation.md` par défaut, sans créer de fichiers séparés par axe.
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

Le rapport affiche tous les axes canoniques. Pour un axe non couvert, remplacer les sous-sections par une ligne `Not covered: <short reason>`.

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Validation: <title>

## Context
Summarize the brief or equivalent context being validated.

## Validation Scope
State what is being validated, what is intentionally not covered, and the depth of research performed.

## Axis Findings
Summarize findings for every canonical axis. Use `Not covered: <short reason>` when an axis was not researched.

### User Problem

#### Why This Axis Matters
Explain why the user problem matters for this initiative.

#### Evidence
List facts, sources, observations, or signals related to the user problem.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### Market And Competitors

#### Why This Axis Matters
Explain why market and competitor dynamics matter for this initiative.

#### Evidence
List facts, sources, observations, or signals about the market and competitors.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### Technical Feasibility

#### Why This Axis Matters
Explain why technical feasibility matters for this initiative.

#### Evidence
List facts, repo observations, docs, experiments, or external signals about feasibility.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### Costs And Business Model

#### Why This Axis Matters
Explain why costs or business model considerations matter for this initiative.

#### Evidence
List facts, estimates, sources, or signals about cost, pricing, revenue, margin, or business model.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### Distribution And Acquisition

#### Why This Axis Matters
Explain why distribution or acquisition matters for this initiative.

#### Evidence
List facts, sources, observations, or signals about channels, adoption paths, or acquisition constraints.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### Legal Or Regulatory Risk

#### Why This Axis Matters
Explain why legal or regulatory risk matters for this initiative.

#### Evidence
List facts, sources, constraints, jurisdictions, data types, compliance obligations, or legal signals.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### UX And Adoption

#### Why This Axis Matters
Explain why UX and adoption risk matters for this initiative.

#### Evidence
List facts, sources, usability signals, user behavior, workflow constraints, or adoption signals.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

### Differentiation

#### Why This Axis Matters
Explain why differentiation matters for this initiative.

#### Evidence
List facts, sources, competitor comparisons, positioning signals, or uniqueness signals.

#### Interpretation
Explain what the evidence suggests and where it remains ambiguous.

#### Confidence
Use `High`, `Medium`, or `Low`, optionally followed by one short justification.

High | Medium | Low

#### Risks Or Unknowns
List risks, weak evidence, unresolved assumptions, or unknowns for this axis.

## Cross-Axis Synthesis
Synthesize convergences, contradictions, tradeoffs, and the strongest signals across axes.

## Verdict And Recommendations
Provide one standardized verdict and a short list of actionable recommendations.

Verdict: Go | No-Go | Pivot | Needs More Research

- <Recommendation>

## Open Questions
List unresolved questions that still matter after validation.

## Sources And References
List important sources, references, repos, docs, searches, or artifacts used.
```

Format d'un axe non couvert :

```markdown
### Legal Or Regulatory Risk

Not covered: <short reason>
```

Règles de sections :

- `Context` : required.
- `Validation Scope` : required.
- `Axis Findings` : required.
- Chaque axe canonique : required, contenu adaptable.
- Sous-sections d'un axe couvert : required.
- Axe non couvert : remplacer les sous-sections par `Not covered: <short reason>`.
- `Confidence` : required pour un axe couvert, valeur standardisée `High`, `Medium` ou `Low`, éventuellement suivie d'une phrase courte.
- `Cross-Axis Synthesis` : required.
- `Verdict And Recommendations` : required.
- `Open Questions` : required.
- `Sources And References` : required quand des sources existent ; sinon `Not known yet`.

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
- Ne pas créer automatiquement de fichiers de recherche séparés pour les axes sous-traités.
- Garder la v1 légère.
