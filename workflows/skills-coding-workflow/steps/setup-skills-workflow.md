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
- Si le repo est hébergé sur GitHub ou GitLab.
- Si `gh` ou `glab` est disponible et authentifié lorsque possible.
- `CLAUDE.md` existant.
- `AGENTS.md` existant.
- `CONTEXT.md` et `CONTEXT-MAP.md` existants.
- `docs/adr/` existant.
- `docs/agents/` existant.
- `.initiatives/` existant.
- `.gitignore` existant.

## Séquence attendue

Le setup doit rester réexécutable et non destructif :

```text
explorer -> présenter les constats -> décider une convention à la fois -> prévisualiser les changements -> écrire en place -> vérifier
```

Après l'exploration, l'agent présente brièvement :

- Les règles agent déjà présentes.
- Les conventions de tracker détectées.
- Les artefacts locaux déjà présents.
- Les docs globales déjà présentes.
- Les éléments manquants qui peuvent être utiles.

Les éléments absents ne doivent pas être présentés comme des erreurs. Le setup propose seulement ce qui réduit une ambiguïté réelle pour les futurs agents.

## Questions à poser

Demander à l'utilisateur, une décision à la fois.

Avant chaque question, donner un court explainer : ce qu'est la convention, pourquoi le workflow en a besoin, et ce que le choix change concrètement.

Décisions à couvrir :

- Issue tracker : utiliser GitHub Issues via `gh`, GitLab Issues via `glab`, ou le fallback markdown local.
- Artefacts locaux : configurer ou non `.initiatives/`.
- `CONTEXT.md` : le créer seulement s'il est absent, utile et confirmé. Son absence n'est pas une erreur.
- `CONTEXT-MAP.md` : le créer seulement si le projet a plusieurs contextes, packages, domaines ou sous-projets.
- ADRs : confirmer que les décisions d'architecture durables vivent dans `docs/adr/`.
- Fichier routeur : utiliser `CLAUDE.md` ou `AGENTS.md` lorsqu'aucun des deux n'existe.

Pour le tracker, la recommandation par défaut suit le remote détecté : GitHub si le remote est GitHub, GitLab si le remote est GitLab, sinon fallback markdown local.

## Comportement

- Explorer le repo avant de proposer des changements.
- Présenter les constats avant de poser les décisions de setup.
- Préserver les règles agent existantes sauf si elles contredisent explicitement le workflow ou la demande utilisateur.
- Recommander une option par décision, expliquer brièvement pourquoi, puis demander confirmation.
- Prévisualiser le résumé des fichiers à créer ou modifier avant écriture.
- Écrire les fichiers seulement après confirmation des choix structurants.
- Mettre à jour les sections existantes en place au lieu d'ajouter des doublons.
- Ne pas écraser les sections utilisateur autour des blocs gérés par le workflow.
- Garder les fichiers routeurs courts et déplacer les règles détaillées dans `docs/agents/`.

## Sorties

Créer ou mettre à jour, selon les confirmations utilisateur :

- `CLAUDE.md` ou `AGENTS.md` comme routeur court, selon la convention choisie.
- `docs/agents/issue-tracker.md`.
- `docs/agents/local-artifacts.md`.
- `docs/agents/documentation.md`.
- `CONTEXT.md` si absent et confirmé.
- `CONTEXT-MAP.md` si nécessaire et confirmé.
- L'entrée `.initiatives/` dans `.gitignore`.
- Le dossier `.initiatives/` si l'utilisateur confirme.

Ne pas créer :

- `docs/agents/triage-labels.md` en v1.
- `.initiatives/index.md` en v1.
- `brief.md`, `brainstorming.md` ou `validation.md` sauf demande explicite dans une autre action.

## Format

Ce skill produit un bundle de templates, car il peut créer ou mettre à jour plusieurs fichiers durables.

Règles générales :

- `CLAUDE.md` ou `AGENTS.md` reste un routeur court.
- Les règles détaillées vivent dans `docs/agents/*`.
- Les templates des artefacts du workflow ne sont pas recopiés dans les fichiers routeurs.
- Les conventions projet doivent être concrètes et actionnables.

### `CLAUDE.md` ou `AGENTS.md`

Le fichier d'entrée agent doit rester un routeur court. Il ne doit pas dupliquer les règles détaillées.

Le setup suit cette règle : utiliser `CLAUDE.md` s'il existe, sinon `AGENTS.md` s'il existe, sinon demander à l'utilisateur quel fichier créer.

Si le fichier choisi contient déjà des sections équivalentes, le setup les met à jour en place. Il ne doit pas créer de second bloc `Issue Tracker`, `Local Artifacts` ou `Documentation`, ni supprimer des règles utilisateur non liées au workflow.

Template :

Les lignes de guidance dans les templates doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

```markdown
# Agent Instructions

## Issue Tracker

If you work with issues, read `docs/agents/issue-tracker.md`.

## Local Artifacts

If you create or use local workflow artifacts, read `docs/agents/local-artifacts.md`.

## Documentation

If you use or update project documentation, domain context, ADRs, or research docs, read `docs/agents/documentation.md`.
```

Règles de sections :

- `Issue Tracker` : required.
- `Local Artifacts` : required.
- `Documentation` : required.

### `docs/agents/issue-tracker.md`

Règles propres au projet pour interagir avec l'issue tracker.

En v1, le support officiel couvre :

- GitHub Issues via `gh`.
- GitLab Issues via `glab`.

Le fallback markdown local reste supporté dans `.initiatives/`.

Le setup choisit une seule variante de `docs/agents/issue-tracker.md` selon la convention confirmée : GitHub, GitLab ou markdown local.

Pour GitHub et GitLab, `issue-tracker.md` contient les commandes exactes à utiliser. Pour le markdown local, `issue-tracker.md` doit rester un pointeur court vers `docs/agents/local-artifacts.md` afin de ne pas dupliquer les règles `.initiatives/`, `spec.md` et `tasks/*.md`.

#### Template GitHub

Les lignes de guidance dans le template doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

```markdown
# Issue Tracker

## Tracker
GitHub Issues via `gh`.

## Conventions
- Read an issue: `gh issue view <number> --comments`
- List issues: `gh issue list`
- Create an issue: `gh issue create --title "<title>" --body-file <file>`
- Comment on an issue: `gh issue comment <number> --body-file <file>`
- Apply a label: `gh issue edit <number> --add-label "<label>"`
- Close an issue: `gh issue close <number> --comment "<reason>"`

## Spec And Task Links
The spec is a GitHub issue. Task issues link back to the spec issue.

## Labels
Document project labels agents may use, or state that no labels are required in v1.

## Closing Issues
Agents must not close issues unless explicitly instructed or allowed by this project.

## Security And Privacy
Never include secrets, tokens, credentials, raw personal data, or sensitive customer data in issues or comments.
```

#### Template GitLab

Les lignes de guidance dans le template doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

```markdown
# Issue Tracker

## Tracker
GitLab Issues via `glab`.

## Conventions
- Read an issue: `glab issue view <number> --comments`
- List issues: `glab issue list`
- Create an issue: `glab issue create --title "<title>" --description "<description>"`
- Comment on an issue: `glab issue note <number> --message "<message>"`
- Apply a label: `glab issue update <number> --label "<label>"`
- Close an issue: `glab issue close <number>`

## Spec And Task Links
The spec is a GitLab issue. Task issues link back to the spec issue.

## Labels
Document project labels agents may use, or state that no labels are required in v1.

## Closing Issues
Agents must not close issues unless explicitly instructed or allowed by this project. If a closing explanation is needed, comment before closing.

## Security And Privacy
Never include secrets, tokens, credentials, raw personal data, or sensitive customer data in issues or comments.
```

#### Template Markdown Local

Ce template est volontairement court. Les règles détaillées du mode local vivent dans `docs/agents/local-artifacts.md`.

```markdown
# Issue Tracker

## Tracker
Local markdown files under `.initiatives/`.

## Conventions
Use `docs/agents/local-artifacts.md` for local spec, task, initiative, naming, and gitignore conventions.

## Spec And Task Links
The local spec lives in `.initiatives/<id>/spec.md`. Local tasks live in `.initiatives/<id>/tasks/*.md`. Follow `docs/agents/local-artifacts.md` for the exact project convention.

## Labels
No labels are required in local markdown mode in v1.

## Closing Issues
Agents must not mark local tasks complete or closed unless explicitly instructed or allowed by this project.

## Security And Privacy
Never store secrets, tokens, credentials, raw personal data, or sensitive customer data in local workflow artifacts.
```

Dans le mode markdown local, `docs/agents/issue-tracker.md` ne doit pas recopier le contenu de `docs/agents/local-artifacts.md`. Il sert seulement de routeur pour les skills qui cherchent une convention d'issue tracker.

Règles de sections :

- `Tracker` : required.
- `Conventions` : required.
- `Spec And Task Links` : required.
- `Labels` : required, même pour dire qu'aucun label obligatoire n'existe en v1.
- `Closing Issues` : required. Valeur par défaut v1 : les agents ne ferment pas les issues sauf configuration explicite.
- `Security And Privacy` : required.

### `docs/agents/local-artifacts.md`

Règles propres au projet pour les artefacts locaux.

Ce fichier reste court et centré sur `.initiatives/`. Il ne doit pas redécrire tous les templates d'artefacts.

Template :

Les lignes de guidance dans le template doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

```markdown
# Local Artifacts

## Location
Describe where local workflow artifacts live, usually `.initiatives/<NNN-slug>/`.

## Initiative Naming
Describe the initiative folder naming convention and how to choose the next ID.

## Artifact Types
List supported local artifact types and their default paths.

## Creating An Initiative
Explain how agents should create or propose a new initiative folder.

## Creating Local Artifacts
Explain how agents should create local artifacts and when confirmation is required.

## Gitignore
State whether `.initiatives/` is gitignored and how to maintain that rule.

## Security And Privacy
State what must never be stored in local artifacts, such as secrets, tokens, credentials, and sensitive data.
```

Règles de sections :

- `Location` : required.
- `Initiative Naming` : required.
- `Artifact Types` : required.
- `Creating An Initiative` : required.
- `Creating Local Artifacts` : required.
- `Gitignore` : required.
- `Security And Privacy` : required.

### `docs/agents/documentation.md`

Règles propres au projet pour la documentation globale.

Ce fichier remplace le nom plus étroit `domain.md`, car il couvre toute la documentation globale du projet et pas seulement le domaine.

Il doit expliquer quand utiliser chaque type de documentation globale, sans recopier les templates complets de `CONTEXT.md`, `CONTEXT-MAP.md` ou ADR.

Template :

Les lignes de guidance dans le template doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

```markdown
# Documentation

## Before Working
Explain what agents should read before making domain, architecture, or documentation changes.

Read the relevant `CONTEXT.md` or `CONTEXT-MAP.md` first when domain language matters. Read relevant ADRs before changing architecture or contradicting an established design decision.

## Domain Context
Explain when agents should read or update `CONTEXT.md`.

Use `CONTEXT.md` for canonical domain language only.

When naming domain concepts in issues, specs, tests, implementation notes, or documentation, use the canonical vocabulary from `CONTEXT.md`. If a needed term is missing, note the gap instead of inventing durable project language silently.

If `CONTEXT.md` does not exist, proceed from the repo and conversation context. Propose creating it only when useful domain vocabulary has actually been clarified.

## Context Map
Explain when agents should read or update `CONTEXT-MAP.md`.

Use `CONTEXT-MAP.md` when the repo has multiple domains, packages, apps, or bounded contexts.

## ADRs
Explain when agents should propose or create ADRs.

Use `docs/adr/` for durable architecture decisions that meet the ADR criteria.

If a proposed change contradicts an existing ADR, flag the conflict explicitly instead of silently overriding the decision.

## Research Docs
Explain when reusable project-level research belongs in `docs/research/`.

Use `docs/research/` for reusable project-level research.

## Local Vs Global Documentation
Explain the boundary between versioned global docs and local initiative artifacts.

## Security And Privacy
State what must never be included in project documentation, such as secrets, tokens, credentials, and sensitive data.
```

Règles de sections :

- `Before Working` : required.
- `Domain Context` : required.
- `Context Map` : required.
- `ADRs` : required.
- `Research Docs` : required.
- `Local Vs Global Documentation` : required.
- `Security And Privacy` : required.

### `CONTEXT.md`

À créer seulement si le fichier est absent, utile au projet et confirmé par l'utilisateur.

`CONTEXT.md` est strictement un glossaire et un document de langage de domaine partagé. Il ne doit pas contenir l'état des initiatives, briefs produit, décisions locales de feature, recherches détaillées, notes de réunion, todo lists ou specs techniques complètes.

Son absence n'est pas une erreur. Le setup ne doit pas pousser à créer un `CONTEXT.md` vide ou spéculatif ; il le propose seulement si du vocabulaire de domaine utile est déjà connu ou confirmé.

Template :

Les lignes de guidance dans le template doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

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

### `CONTEXT-MAP.md`

À créer seulement si le repo contient plusieurs contextes, packages, domaines ou sous-projets, et après confirmation utilisateur.

`CONTEXT-MAP.md` est un routeur minimal. Il ne doit pas devenir une carte d'architecture complète.

Template :

Les lignes de guidance dans le template doivent être remplacées par les conventions du projet ; les commandes et règles déjà exactes peuvent être conservées telles quelles.

```markdown
# Context Map

## Purpose
Explain why this context map exists and how agents should use it.

## Contexts
List project contexts, packages, apps, domains, or sub-projects that need routing.

### <Context Name>
Name one context and describe the boundary briefly.

Path: `<path>`

Read first:
- `<path>/CONTEXT.md`
- `<path>/docs/...`

Use when:
- <When this context is relevant>

## Shared Documentation
List documentation shared across contexts.

## Notes
Add only routing notes that help agents choose the right context.
```

Règles de sections :

- `Purpose` : required.
- `Contexts` : required.
- Entrées de contexte : adaptable.
- `Shared Documentation` : required quand une documentation partagée existe.
- `Notes` : optional.

## Règles de confirmation

- Demander confirmation avant de créer ou modifier des fichiers structurants.
- Demander les décisions une par une lorsque plusieurs conventions sont possibles.
- Présenter un résumé des fichiers qui seront créés ou modifiés avant écriture.

## Vérification finale

- Les fichiers routeurs pointent vers les bons documents `docs/agents/`.
- Les sections routeur ne sont pas dupliquées après réexécution.
- Les règles utilisateur existantes non liées au workflow ont été préservées.
- Le tracker choisi correspond aux conventions écrites dans `docs/agents/issue-tracker.md`.
- Les règles détaillées ne sont pas dupliquées dans `CLAUDE.md` ou `AGENTS.md`.
- `.initiatives/` est dans `.gitignore` si le mode local est activé.
- `CONTEXT.md` n'a pas été créé vide ou sans utilité confirmée.
- Aucun artefact hors scope v1 n'a été créé.

## Limites

- Ne pas créer de système de triage en v1.
- Ne pas créer d'artefacts d'initiative sans demande explicite.
- Ne pas réécrire toute la documentation projet au-delà du setup agent.
