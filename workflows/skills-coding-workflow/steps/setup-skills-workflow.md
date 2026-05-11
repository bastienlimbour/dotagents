# `/setup-skills-workflow`

## Objectif

Préparer un projet à utiliser ce workflow en créant ou mettant à jour les règles agent spécifiques au projet.

Ce skill doit être prompt-driven plutôt qu'un script déterministe. Il observe le repo, propose les choix un par un, recommande une option, demande confirmation, puis écrit les fichiers.

## À utiliser quand

- Un projet doit être configuré pour utiliser ce workflow de coding assisté par IA.
- Le repo n'a pas encore de règles agent claires pour les issues, les artefacts locaux ou la documentation globale.
- L'utilisateur veut installer, auditer ou réaligner `CLAUDE.md`, `AGENTS.md`, `docs/agents/`, `.initiatives/`, `CONTEXT.md` ou les conventions ADR.

## Entrées à inspecter

L'agent doit inspecter ou inférer :

- Remotes Git.
- Si le repo est hébergé sur GitHub.
- Si `gh` est disponible et authentifié lorsque possible.
- `CLAUDE.md` existant.
- `AGENTS.md` existant.
- `CONTEXT.md` et `CONTEXT-MAP.md` existants.
- `docs/adr/` existant.
- `docs/agents/` existant.
- `.initiatives/` existant.
- `.gitignore` existant.

## Questions à poser

Demander à l'utilisateur, une décision à la fois :

- S'il veut utiliser GitHub Issues ou le fallback markdown local.
- S'il veut configurer `.initiatives/`.
- S'il faut créer `CONTEXT.md` s'il est absent.
- Si le projet a besoin de `CONTEXT-MAP.md`.
- Si les ADRs doivent vivre dans `docs/adr/`.
- S'il faut utiliser `CLAUDE.md` ou `AGENTS.md` lorsqu'aucun des deux n'existe.

## Comportement

- Explorer le repo avant de proposer des changements.
- Préserver les règles agent existantes sauf si elles contredisent explicitement le workflow ou la demande utilisateur.
- Recommander une option par décision, expliquer brièvement pourquoi, puis demander confirmation.
- Écrire les fichiers seulement après confirmation des choix structurants.
- Garder les fichiers routeurs courts et déplacer les règles détaillées dans `docs/agents/`.

## Sorties

Créer ou mettre à jour, selon les confirmations utilisateur :

- `CLAUDE.md` ou `AGENTS.md` comme routeur court, selon la convention choisie.
- `docs/agents/issue-tracker.md`.
- `docs/agents/local-artifacts.md`.
- `docs/agents/documentation.md`.
- L'entrée `.initiatives/` dans `.gitignore`.
- Le dossier `.initiatives/` si l'utilisateur confirme.

Ne pas créer :

- `docs/agents/triage-labels.md` en v1.
- `.initiatives/index.md` en v1.
- `brief.md`, `brainstorming.md` ou `validation.md` sauf demande explicite dans une autre action.

## Format

### `CLAUDE.md` ou `AGENTS.md`

Le fichier d'entrée agent doit rester un routeur court. Il ne doit pas dupliquer les règles détaillées.

Le setup suit cette règle : utiliser `CLAUDE.md` s'il existe, sinon `AGENTS.md` s'il existe, sinon demander à l'utilisateur quel fichier créer.

Exemple de rôle :

```markdown
## Issue Tracker
If you are working with issues, read `docs/agents/issue-tracker.md`.

## Local Artifacts
If you are working with local artifacts, read `docs/agents/local-artifacts.md`.

## Documentation
If you need to use project documentation, domain context, ADRs, or research docs, read `docs/agents/documentation.md`.
```

### `docs/agents/issue-tracker.md`

Règles propres au projet pour interagir avec l'issue tracker.

En v1, le support officiel est GitHub Issues via `gh`.

Ce fichier doit expliquer :

- Comment on utilise l'issue tracker globalement : CLI, MCP server ou autre.
- Comment créer une issue.
- Comment commenter une issue.
- Comment gérer les relations entre issues, étant donné que le CLI ne gère pas nativement les sub issues.
- Si le projet utilise des labels.
- Si les agents ont le droit de fermer des issues. Valeur par défaut en v1 : non, sauf configuration explicite.
- Les règles de confidentialité et sécurité : pas de secrets, tokens, credentials, etc.

### `docs/agents/local-artifacts.md`

Règles propres au projet pour les artefacts locaux.

Ce fichier doit expliquer :

- La convention de chemin `.initiatives/`.
- Les attentes liées à `.gitignore`.
- La convention de nommage des dossiers d'initiative.
- Comment créer un artefact local.
- Les règles de confidentialité et sécurité : pas de secrets, tokens, credentials, etc.

### `docs/agents/documentation.md`

Règles propres au projet pour la documentation globale.

Ce fichier remplace le nom plus étroit `domain.md`, car il couvre toute la documentation globale du projet et pas seulement le domaine.

Il doit expliquer :

- Comment utiliser `CONTEXT.md`.
- Comment utiliser `CONTEXT-MAP.md` dans les monorepos.
- Comment créer des ADRs dans `docs/adr/`.
- Comment utiliser `docs/research/`.
- La frontière entre documentation globale versionnée et artefacts locaux d'initiative.

## Règles de confirmation

- Demander confirmation avant de créer ou modifier des fichiers structurants.
- Demander les décisions une par une lorsque plusieurs conventions sont possibles.
- Présenter un résumé des fichiers qui seront créés ou modifiés avant écriture.

## Vérification finale

- Les fichiers routeurs pointent vers les bons documents `docs/agents/`.
- Les règles détaillées ne sont pas dupliquées dans `CLAUDE.md` ou `AGENTS.md`.
- `.initiatives/` est dans `.gitignore` si le mode local est activé.
- Aucun artefact hors scope v1 n'a été créé.

## Limites

- Ne pas créer de système de triage en v1.
- Ne pas créer d'artefacts d'initiative sans demande explicite.
- Ne pas réécrire toute la documentation projet au-delà du setup agent.
