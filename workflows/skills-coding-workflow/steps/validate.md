# `/validate`

## Objectif

Réduire l'incertitude autour d'une idée, solution, feature, marché, direction technique ou hypothèse business.

Le skill ne décide pas à la place de l'utilisateur. Il rend explicites les preuves, les risques, les inconnues et le prochain test utile avant d'investir davantage.

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
- Extraire la cible de validation : problème, utilisateur cible, alternative actuelle, solution proposée et hypothèse la plus risquée.
- Identifier les incertitudes critiques.
- Choisir les axes de validation pertinents parmi les axes canoniques.
- Recommander une profondeur d'analyse.
- Demander confirmation avant recherche ou analyse approfondie.
- Sous-traiter les recherches par axe à des sub-agents lorsque cela aide à séparer les analyses.
- Condenser les recherches des sub-agents dans `validation.md` par défaut, sans créer de fichiers séparés par axe.
- Distinguer faits, sources, hypothèses, signaux faibles, interprétations, inconnues et niveau de confiance.
- Évaluer la force des preuves sans confondre intérêt poli et engagement réel.
- Repérer les red flags qui doivent limiter la portée du verdict.
- Proposer l'expérience de validation la moins coûteuse pour tester l'hypothèse la plus risquée.
- Produire un rapport léger en v1.
- Inclure un verdict lorsque utile : `Go`, `No-Go`, `Pivot` ou `Needs More Research`.

## Axes possibles

- Problème utilisateur.
- Demande et engagement.
- Marché et concurrents.
- Faisabilité technique.
- Coûts et business model.
- Distribution et acquisition.
- Risque légal ou réglementaire.
- UX et adoption.
- Différenciation.

## Sorties

Sortie par défaut :

```
.initiatives/<id>/validation.md
```

Si la validation est utile globalement :

```
docs/research/<slug>.md
```

## Format

Le rapport affiche tous les axes canoniques dans `Axis Coverage`. Les détails ne sont développés que pour les axes `Covered` ou `Partial`.

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```md
# Validation: {{ title }}

## Context

{{ brief or equivalent context being validated }}

## Validation Target

- Problem: {{ problem to validate }}
- Target user: {{ specific target user or segment }}
- Current workaround or alternative: {{ current solution, workaround, competitor, manual process, or status quo }}
- Proposed solution or hypothesis: {{ proposed direction, solution, feature, or business hypothesis }}
- Riskiest assumption: {{ assumption that would most weaken or invalidate the idea if false }}

## Validation Scope

- Covered: {{ axes, questions, or risks covered by this validation }}
- Not covered: {{ intentionally excluded axes, questions, or risks }}
- Depth: {{ lightweight, focused, or deeper analysis actually performed; avoid formal modes }}
- Sources used: {{ conversation, brief, repo/docs, web research, interviews, benchmarks, or other inputs }}

## Evidence Quality

- Strongest evidence: {{ strongest behavior, commitment, source, repo signal, or external proof }}
- Weakest evidence: {{ weakest claim, assumption, analogy, or unsupported signal }}
- Main evidence gaps: {{ missing evidence that would materially affect the verdict }}
- Overall confidence: {{ High | Medium | Low }}

## Axis Coverage

| Axis | Status | Confidence | Short Reason |
| --- | --- | --- | --- |
| User Problem | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Demand And Commitment | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Market And Competitors | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Technical Feasibility | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Costs And Business Model | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Distribution And Acquisition | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Legal Or Regulatory Risk | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| UX And Adoption | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |
| Differentiation | {{ Covered/Partial/Not covered }} | {{ High/Medium/Low }} | {{ short reason }} |

## Detailed Findings

{{ repeat this section only for axes that were covered or partially covered }}

### {{ axis name }}

**Finding:** {{ main conclusion for this axis }}

**Evidence:**

- {{ fact, source, signal, repo observation, interview, user behavior, competitor data, or other evidence }}

**Interpretation:**

{{ what the evidence suggests, what remains ambiguous, and what would change the conclusion }}

**Confidence:** {{ High | Medium | Low }}

**Risks Or Unknowns:**

- {{ risk, weak evidence, unresolved assumption, contradiction, missing source, or unknown }}

**Next Signal To Seek:**

- {{ smallest useful signal that would increase or decrease confidence }}

## Cross-Axis Synthesis

{{ convergences, contradictions, tradeoffs, and strongest signals across axes }}

## Red Flags

{{ critical risks that should cap or weaken the verdict; use "None identified" when appropriate }}

## Recommended Validation Experiments

| Experiment | Tests Assumption | Expected Signal | Effort |
| --- | --- | --- | --- |
| {{ experiment }} | {{ assumption being tested }} | {{ measurable or observable pass/fail signal }} | {{ rough time, cost, or complexity }} |

## Verdict And Recommendations

Verdict: {{ Go | No-Go | Pivot | Needs More Research }}

- {{ actionable recommendation }}

## Open Questions

{{ unresolved questions that still matter after validation }}

## Sources And References

{{ important sources, references, repos, docs, searches, or artifacts used; use "Not known yet" when none exist }}
```

## Hiérarchie des preuves

L'agent doit privilégier les preuves de comportement réel plutôt que les opinions déclaratives.

Force indicative des preuves, de la plus forte à la plus faible :

1. Paiement réel, contrat, précommande, usage répété ou design partner engagé.
2. Conversations directes avec des clients potentiels centrées sur le comportement actuel, pas sur l'avis à propos de la solution.
3. Comportements observables : reviews, forums, recherche, plaintes publiques, job postings, workarounds visibles.
4. Données de marché, benchmarks, concurrents, observations repo/docs ou signaux externes vérifiables.
5. Affirmations du porteur d'idée, analogies, hypothèses ou intérêt poli.

`Evidence Quality` doit résumer brièvement quelles preuves dominent le rapport.

## Red flags possibles

Ces red flags ne déclenchent pas automatiquement une décision, mais ils doivent limiter la confiance ou le verdict :

- Utilisateur cible trop vague.
- Problème peu douloureux, peu fréquent ou non reconnu.
- Aucun workaround, budget, dépense de temps ou alternative actuelle identifiable.
- Différenciation marginale par rapport aux alternatives directes, indirectes ou au status quo.
- Adoption nécessitant un changement de workflow important sans bénéfice nettement supérieur.
- Business model ou unit economics manifestement faibles.
- Risque légal, réglementaire, éthique ou sécurité critique.
- Faisabilité technique non prouvée pour le cœur de la solution.
- Validation reposant surtout sur des avis amicaux ou de l'intérêt poli.

Règles de sections :

- `Context` : required.
- `Validation Target` : required.
- `Validation Scope` : required.
- `Evidence Quality` : required.
- `Axis Coverage` : required, avec tous les axes canoniques.
- Chaque axe canonique : required dans `Axis Coverage`, avec statut `Covered`, `Partial` ou `Not covered`.
- `Detailed Findings` : required uniquement pour les axes `Covered` ou `Partial`.
- `Confidence` : required pour chaque axe, valeur standardisée `High`, `Medium` ou `Low`.
- `Cross-Axis Synthesis` : required.
- `Red Flags` : required.
- `Recommended Validation Experiments` : required.
- `Verdict And Recommendations` : required.
- `Open Questions` : required.
- `Sources And References` : required quand des sources existent ; sinon `Not known yet`.

## Règles de confirmation

- Demander confirmation avant recherche ou analyse approfondie.
- Demander confirmation du chemin cible avant écriture.
- Ne pas transformer automatiquement le rapport en décision produit finale.
- Ne pas recommander de passer à la spec ou à l'implémentation si les preuves restent trop faibles ; utiliser `Needs More Research` et proposer le prochain test.

## Vérification finale

- Les faits, hypothèses et interprétations sont séparés.
- La cible de validation et l'hypothèse la plus risquée sont explicites.
- Le niveau de confiance est explicite.
- La force des preuves est proportionnée au verdict.
- Les sources ou preuves importantes sont citées lorsque disponibles.
- Les red flags importants sont visibles.
- Au moins une expérience de validation actionnable est proposée si l'incertitude reste significative.
- Le verdict, s'il existe, reste proportionné aux preuves.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas présenter le verdict comme une certitude.
- Ne pas créer automatiquement de fichiers de recherche séparés pour les axes sous-traités.
- Ne pas imposer Lean Canvas, SWOT, PESTLE, score pondéré ou interviews obligatoires en v1.
- Ne pas confondre `/validate` avec `/to-spec`, `/prototype` ou `/split` : le résultat principal reste une réduction d'incertitude.
- Garder la v1 légère.
