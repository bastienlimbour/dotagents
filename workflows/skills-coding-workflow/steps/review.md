# `/review`

## Objectif

Relire les changements de manière indépendante pour identifier bugs, régressions, risques de sécurité, risques de performance, tests manquants et écarts avec la source de vérité.

## À utiliser quand

- Une implémentation doit être relue avant merge, livraison ou suite de travail.
- L'utilisateur demande une review.
- Il faut vérifier l'alignement entre changements et critères d'acceptation.
- Le risque principal est bug, régression, sécurité, performance ou test manquant.

## Entrées

- Source de vérité : issue, spec, task, prompt ou brief.
- Critères d'acceptation.
- Diff ou fichiers modifiés.
- Tests et vérifications exécutés, si disponibles.
- Résumé d'implémentation, sans lui faire confiance aveuglément.

## Comportement

- Lire la source de vérité.
- Lire les critères d'acceptation.
- Inspecter les changements de code.
- Préférer une nouvelle session ou un sub-agent avec contexte frais lorsque possible.
- Ne pas faire confiance aveuglément au résumé de l'agent qui a implémenté.
- Produire les findings d'abord, triés par sévérité.
- Citer fichiers et lignes lorsque possible.
- Si aucun finding bloquant n'existe, le dire explicitement et lister les risques résiduels.
- Proposer ensuite de créer un commentaire d'issue ou un document local.

## Sorties

Findings de review en conversation par défaut.

Après confirmation, les findings peuvent être créés comme commentaire d'issue ou document local.

## Format

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Review: <title>

Source: <issue, spec, task, PR, diff, or local path>

## Findings
List findings first, sorted by severity. If there are no findings, write `No findings.`

### <Severity>: <title>

Location: <file and line if available>

What is wrong:
Why it matters:
Suggested fix:
Related source item:

## Residual Risks And Missing Tests
List residual risks, missing tests, or verification gaps even when there are no findings.

## Reviewed Scope
Describe what source material, diff, files, or behavior was reviewed.

## Checks Reviewed
List tests, builds, lint, typecheck, QA notes, or other checks considered during review.
```

S'il n'y a aucun finding, `## Findings` doit contenir explicitement :

```text
No findings.
```

Règles de sections :

- `Source` : required.
- `Findings` : required.
- Champs d'un finding : required lorsqu'un finding existe.
- `Residual Risks And Missing Tests` : required.
- `Reviewed Scope` : required.
- `Checks Reviewed` : required.

## Vérification finale

- Les findings sont triés par sévérité.
- Les fichiers et lignes sont cités lorsque possible.
- Les écarts avec la source de vérité sont explicités.
- Les risques résiduels et tests manquants sont mentionnés même sans finding bloquant.

## Limites

- Ne pas modifier le code par défaut.
- Ne pas corriger les bugs par défaut.
- Ne pas créer de commentaire ou document sans confirmation.
