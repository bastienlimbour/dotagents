# `/handoff`

## Objectif

Créer un document de passage de relais compact pour qu'une nouvelle session ou un autre agent puisse reprendre un travail en cours sans ambiguïté.

Le handoff n'est pas une source de vérité canonique. Il résume l'état de travail courant et pointe vers les artefacts canoniques existants.

## À utiliser quand

- L'utilisateur veut mettre une session en pause.
- Le contexte devient long et risque d'être perdu.
- Une session d'implémentation, diagnostic, review ou QA a produit un état de travail utile à reprendre.
- Un changement de tâche ou de session arrive après un progrès significatif.
- Un autre agent ou une future session doit savoir quoi lire et quoi faire en premier.

## Entrées

- Conversation courante.
- Prompt utilisateur décrivant l'objectif de la prochaine session, s'il existe.
- Source de vérité disponible : issue, spec, tâche, brief, ADR, doc ou fichier local.
- État du repo lorsque pertinent : branche, `git status`, diff, commits récents, fichiers modifiés.
- Résultats de vérification : tests, typecheck, lint, build, reproduction, QA manuelle.
- Blocages, questions ouvertes, décisions prises ou hypothèses acceptées pendant la session.

## Comportement

- Lire la conversation courante et les artefacts pertinents avant d'écrire le handoff.
- Explorer le repo lorsque l'état du travail peut être vérifié par le code, le git status, le diff ou les artefacts locaux.
- Capturer l'état utile de reprise, pas le transcript brut.
- Ne pas dupliquer le contenu déjà présent dans une spec, issue, ADR, brief, commit, diff ou doc ; résumer brièvement et pointer vers le chemin, l'URL ou la référence.
- Identifier clairement la source de vérité canonique du travail à reprendre.
- Distinguer ce qui est terminé, ce qui reste à faire, ce qui est bloqué, ce qui est incertain et ce qui a été vérifié.
- Vérifier avant écriture que le handoff ne contient pas de secret, token, credential, donnée personnelle brute, prompt brut ou sortie LLM complète inutile.
- Si aucun état significatif n'est à transmettre, le dire au lieu de créer un handoff vide.
- Résumer à l'utilisateur où le handoff a été écrit, son caractère temporaire ou durable, et la première action recommandée pour la prochaine session.

## Sorties

Sortie temporaire par défaut :

```text
<path returned by mktemp -t handoff-XXXXXX.md>
```

Sortie locale durable seulement si l'utilisateur la demande explicitement ou confirme cette option :

```text
.handoffs/YYYY-MM-DD-HHMM-<slug>.md
```

Règles de sortie :

- Par défaut, utiliser `mktemp -t handoff-XXXXXX.md` pour éviter de créer une nouvelle convention projet ou une source de vérité durable.
- Lire le fichier temporaire créé par `mktemp` avant de l'écrire, car `mktemp` crée déjà le fichier vide.
- Pour un handoff durable local, demander confirmation du chemin cible avant écriture.
- Si un fichier durable cible existe déjà, demander confirmation avant écrasement ou proposer un nouveau slug.
- `.handoffs/` est local et non canonique par convention. Le skill peut recommander de le gitignore, mais ne doit pas modifier `.gitignore` sans demande explicite.

## Format

Template léger :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Handoff: <topic>

## Current State
Summarize what is happening now, the current status, and why this handoff exists.

## Source Of Truth
Point to the canonical source for the work: issue, spec, task, brief, ADR, doc, prompt or local file.

## What Changed This Session
List meaningful changes, discoveries or progress. Reference files, commits, diffs or artifacts instead of duplicating them.

## Decisions And Rationale
Record decisions made during the session and why they were chosen.

## Verification
List checks run and their results. Mention useful checks that were not run and why.

## Open Questions And Blockers
List unresolved questions, blockers, risks or assumptions that matter for continuation.

## Next Session Contract
State the minimal contract for the next session: goal, scope, out of scope, acceptance criteria and feedback loop when known.

## Files To Read First
List the smallest useful set of paths the next agent should read first, with one short reason per path.

## References
List important issues, docs, ADRs, commits, branches, commands, logs, external sources or local artifacts.
```

Règles :

- Garder le document compact et directement actionnable.
- Privilégier les chemins, URLs et références vérifiables aux longues explications.
- Ne pas inclure un log exhaustif des commandes, un diff complet ou un plan fichier par fichier.
- Inclure les résultats de feedback loops réels lorsqu'ils existent.
- Si une section n'est pas pertinente, l'omettre ou écrire `Not relevant` avec une raison courte.

## Règles de confirmation

Pour un handoff temporaire demandé explicitement :

```text
mktemp -> lecture du fichier vide -> écriture du handoff -> résumé du résultat
```

Pour un handoff durable local :

```text
confirmation du chemin -> écriture du fichier -> résumé du résultat
```

L'agent n'a pas besoin de montrer tout le document en draft, sauf demande explicite de l'utilisateur.

## Vérification finale

- Le prochain agent peut comprendre quoi lire, quoi faire en premier et quel résultat viser.
- La source de vérité canonique est claire.
- Les décisions importantes ont une raison, pas seulement un résultat.
- Les vérifications lancées et non lancées sont explicites.
- Les questions ouvertes, blockers et risques restants sont visibles.
- Les artefacts canoniques existants ne sont pas dupliqués inutilement.
- Aucun secret, token, credential, donnée personnelle brute, prompt brut ou transcript LLM complet inutile n'est inclus.
- Le handoff n'a pas créé ou modifié implicitement de spec, issue, ADR, brief ou documentation globale.

## Limites

- Ne pas remplacer `/capture` pour conserver une recherche, une exploration ou une longue discussion comme note durable.
- Ne pas remplacer une spec, une issue de tâche, un brief, un ADR ou un commentaire de QA.
- Ne pas créer de mode `resume` autonome en v1. Si l'utilisateur fournit un handoff à lire, le traiter comme une entrée de contexte normale.
- Ne pas créer de continuation prompt séparé.
- Ne pas créer de handoff chain, index persistant, scaffold script, validation script ou système de score.
- Ne pas publier dans l'issue tracker distant par défaut.
- Ne pas mettre à jour `.gitignore`, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/` ou `docs/research/` sans demande explicite.
- Ne pas créer de post-mortem ou de retro automatiquement.
