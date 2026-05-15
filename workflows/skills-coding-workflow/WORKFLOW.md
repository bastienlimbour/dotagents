# Spécification Du Skill-Based Coding Workflow

Ce document est la spécification interne du workflow de coding IA basé sur des Agent Skills. Il ne s'agit pas d'un fichier de règles runtime et il n'est pas destiné à être copié tel quel dans les projets utilisateurs.

Son rôle est de décrire les conventions stables, les artefacts et les invariants du workflow afin de créer les futurs `SKILL.md` et de garder les skills existants cohérents.

## Objectif

Ce workflow s'inspire du workflow de Matt Pocock, mais l'adapte au pilotage d'initiatives logicielles. Il n'est pas un framework agentique lourd : il fournit des routines ciblées pour que le développeur garde le contrôle en collaborant avec des agents IA.

Il vise surtout à transformer une idée, une intention ou un problème encore flou en contexte clair, puis en contrat d'exécution exploitable, puis en implémentation vérifiable.

La forme générale recherchée est :

```text
idée -> exploration -> validation -> décisions -> spec -> tâches verticales -> implémentation -> review/QA
```

Cette séquence n'est pas obligatoire. Chaque skill doit rester utilisable indépendamment avec le contexte fourni par l'utilisateur.

## Principes Fondamentaux

### Boîte À Outils Modulaire

Le workflow n'est pas un pipeline fixe. Chaque skill doit faire une chose claire et être utilisable indépendamment.

Le workflow doit pouvoir servir pour :

- Un projet greenfield.
- Une grosse initiative produit.
- Une feature importante.
- Une petite feature.
- Un bug fix.
- Une tâche triviale.

L'utilisateur ne doit pas avoir à choisir un mode formel comme `lightweight` ou `deep`. La profondeur du workflow s'adapte naturellement à l'intention, à l'incertitude et au risque.

### Real Engineering, Not Vibe Coding

Le workflow doit encoder des pratiques d'ingénierie réelles, pas encourager du vibe coding.

Concrètement, les agents doivent :

- Clarifier avant de construire.
- Explorer le codebase et la documentation avant de deviner.
- Produire des artefacts utiles lorsque cela réduit l'ambiguïté.
- Découper le travail en tranches verticales vérifiables.
- S'appuyer sur des feedback loops.
- Respecter l'architecture existante et les décisions documentées.
- Laisser l'humain trancher les décisions importantes.

### Autonomie Des Skills

Les skills ne doivent pas dépendre du fait qu'un autre skill ait été exécuté avant.

Un skill peut recevoir du contexte depuis :

- La conversation courante.
- Le prompt utilisateur.
- Un artefact local.
- Une issue GitHub/GitLab ou un fichier d'issue markdown local.
- Une spec.
- Une tâche.
- Des notes de recherche.
- La documentation projet.
- Les conventions projet déjà injectées dans le contexte agent par le setup.
- L'exploration du codebase.

Les skills ne doivent pas imposer de dépendances directes du type "lance `product-brief` avant" ou "lance `to-spec` après".

Ils peuvent dire qu'il manque du contexte, poser des questions ciblées, recommander de mieux cadrer la demande, ou proposer un artefact pertinent, mais chaque `SKILL.md` doit rester une routine autonome.

### Le Code Et Les Docs Priment Sur La Conversation

Si une réponse peut être trouvée dans le codebase ou dans la documentation projet, l'agent doit explorer ces sources au lieu de demander à l'utilisateur.

La conversation peut être incomplète, imprécise ou obsolète. Le code, les issues, `CONTEXT.md`, les ADRs, les specs et les docs projet doivent être utilisés pour vérifier les hypothèses.

Règle pratique :

```text
Si le repo peut répondre, explorer le repo.
Si le repo ne répond pas ou révèle une contradiction, questionner l'utilisateur.
```

### Questions Une Par Une

Dans les phases d'alignement, clarification, grilling, brainstorming ou validation, l'agent doit poser les questions une par une.

Cette règle réduit la surcharge cognitive et permet de résoudre les dépendances entre décisions dans le bon ordre.

Exception : l'agent peut présenter un court contexte, des options ou une recommandation avant la question, tant qu'il ne demande qu'une décision ou réponse à la fois.

### Contrôle Humain

L'agent propose, l'humain décide.

Les actions importantes demandent une confirmation explicite :

- Prendre une décision importante.
- Créer un artefact structurant.
- Publier une spec dans l'issue tracker.
- Créer des issues de tâches.
- Écrire de la documentation globale.
- Créer un ADR.
- Commenter une issue lorsque ce n'était pas explicitement demandé.
- Fermer une issue.
- Appliquer un refactor d'architecture.

### Source De Vérité Par Artefact

Chaque artefact doit avoir une seule source de vérité canonique.

Si un contenu équivalent existe ailleurs, la version non canonique doit être un résumé, un pointeur ou une archive.

Règle par défaut :

```text
docs/agents/*.md = artefacts sources des conventions du workflow pour le repo
.initiatives/<id>/ = mémoire locale d'exploration et d'artefacts locaux
issue tracker choisi = surface d'exécution et de collaboration
```

L'issue tracker choisi peut être GitHub Issues, GitLab Issues ou markdown local sous `.initiatives/`, selon la convention projet.

Règles par artefact :

- `product-brief.md`, `brainstorming.md`, `validation.md` et les recherches liées à une initiative restent en local dans `.initiatives/<id>/`.
- Si le tracker choisi est GitHub ou GitLab, `spec` et `tasks` vivent dans les issues du tracker.
- Si le tracker choisi est markdown local, `spec.md` et `tasks/*.md` vivent dans `.initiatives/<id>/` et suivent les conventions d'artefacts locaux du setup.
- `qa`, commentaires et résumés d'implémentation vivent avec l'issue ou le fichier markdown concerné.

### Documentation Durable Mais Légère

Le workflow doit créer des artefacts durables uniquement lorsqu'ils réduisent l'ambiguïté future.

Il faut éviter la documentation qui devient une corvée de maintenance :

- Pas de frontmatter dans les artefacts locaux.
- Pas d'index des initiatives.
- Pas de `decision-log.md`.
- Pas de machine à états de triage en v1.
- Pas de fermeture automatique d'issues en v1.

### Feedback Loops

L'implémentation, le diagnostic, le prototypage et la review doivent s'appuyer sur des signaux réels.

Exemples de feedback loops :

- Tests automatisés.
- Typecheck.
- Lint.
- Build.
- Script de reproduction.
- Vérification navigateur ou UI.
- Commande CLI.
- Benchmark.
- Checklist de QA manuelle.

L'agent ne doit pas coder, diagnostiquer ou reviewer uniquement à l'intuition lorsqu'une boucle de feedback utile existe.

### Tranches Verticales Et Tracer Bullets

Le travail doit être découpé en petites tranches verticales, indépendantes et actionnables.

À éviter :

```text
database -> API -> UI -> tests
```

À privilégier :

```text
petit comportement end-to-end -> vérification -> comportement suivant
```

Chaque tâche doit idéalement traverser les couches nécessaires pour livrer un comportement observable (principe de Tracer Bullets).

### Deep Modules

Lors de la rédaction des specs, du découpage, de l'implémentation ou de l'amélioration d'architecture, il faut privilégier les deep modules :

```text
Deep module = petite interface, comportement significatif caché derrière.
Shallow module = interface presque aussi complexe que l'implémentation.
```

Le workflow s'appuie sur les principes suivants : deep modules, seams, locality et deletion test.

## Skills (étapes du workflow)

Cette table sert d'inventaire de création des skills du workflow. Quand un skill existe dans `skills/`, son `SKILL.md` est la référence de comportement. Quand il n'existe pas encore, le fichier `steps/` correspondant est un brouillon d'authoring à réaligner avec cette spec et les skills existants avant création du `SKILL.md`.

| Skill | Rôle | Créé | Path |
| --- | --- | --- | --- |
| `setup-skills-workflow` | Configurer les conventions agent du repo | Oui | `skills/workflow/setup-skills-workflow/SKILL.md` |
| `brainstorm` | Explorer une idée largement et capturer l'exploration | Oui | `skills/workflow/brainstorm/SKILL.md` |
| `grill-me` | Stress-tester une idée ou décision, une question à la fois | Oui | `skills/workflow/grill-me/SKILL.md` |
| `product-brief` | Cadrer le problème, les utilisateurs et le scope produit | Oui | `skills/workflow/product-brief/SKILL.md` |
| `grill-with-docs` | Grilling appuyé sur code, docs, domaine et ADRs | Non | `workflows/skills-coding-workflow/steps/grill-with-docs.md` |
| `capture` | Extraire une longue session en note durable | Non | `workflows/skills-coding-workflow/steps/capture.md` |
| `validate` | Réduire l'incertitude par preuves, risques et prochain test | Non | `workflows/skills-coding-workflow/steps/validate.md` |
| `prototype` | Tester une hypothèse avec du code jetable | Non | `workflows/skills-coding-workflow/steps/prototype.md` |
| `to-spec` | Transformer le contexte en spec canonique | Non | `workflows/skills-coding-workflow/steps/to-spec.md` |
| `split` | Découper une spec en tâches verticales | Non | `workflows/skills-coding-workflow/steps/split.md` |
| `implement` | Implémenter un changement cadré avec feedback loop | Non | `workflows/skills-coding-workflow/steps/implement.md` |
| `implement-tdd` | Implémenter en red-green-refactor strict | Non | `workflows/skills-coding-workflow/steps/implement-tdd.md` |
| `review` | Relire les changements pour bugs, risques et tests manquants | Non | `workflows/skills-coding-workflow/steps/review.md` |
| `qa` | Générer une checklist de QA humaine | Non | `workflows/skills-coding-workflow/steps/qa.md` |
| `diagnose` | Reproduire, diagnostiquer et corriger bugs ou régressions | Non | `workflows/skills-coding-workflow/steps/diagnose.md` |
| `zoom-out` | Cartographier une zone du code à plus haut niveau | Non | `workflows/skills-coding-workflow/steps/zoom-out.md` |
| `improve-codebase-architecture` | Identifier des améliorations architecturales | Non | `workflows/skills-coding-workflow/steps/improve-codebase-architecture.md` |
| `handoff` | Créer un relais compact pour reprise de session | Non | `workflows/skills-coding-workflow/steps/handoff.md` |

Règles pour créer un futur skill :

- Décrire une routine claire, autonome et activable indépendamment.
- Ne pas imposer l'exécution préalable d'un autre skill.
- Respecter les conventions projet pertinentes déjà présentes dans le contexte agent avant toute opération d'issue, d'artefact local ou de documentation.
- Explorer le repo et la documentation avant de demander une information qui peut s'y trouver.
- Si le skill écrit un artefact local, confirmer d'abord l'initiative et le chemin cible.
- Si le skill écrit un artefact structurant, montrer un draft en conversation et attendre validation du contenu avant écriture.
- Si le skill écrit au fil de l'eau, documenter explicitement l'exception et la confirmation initiale qui l'autorise.
- Ne pas créer d'artefacts additionnels, d'issues, de commentaires tracker ou de documentation globale sans demande ou confirmation explicite.
- S'appuyer sur des feedback loops réelles lorsque le skill implémente, diagnostique, prototype ou review.

## Scope V1

### Inclus En V1

- GitHub Issues via `gh`, GitLab Issues via `glab`, ou markdown local sous `.initiatives/` comme issue tracker choisi.
- Artefacts d'exploration d'initiative.
- Specs et découpage en tâches.
- Implémentation avec ou sans TDD.
- Diagnostic.
- Prototypage.
- Review et génération de checklist QA.
- Documentation projet via `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/adr/` et `docs/research/`.
- Conventions agent propres à un projet via `CLAUDE.md` ou `AGENTS.md`, avec détails dans `docs/agents/`.

### Hors Scope En V1

- Système de triage d'issues.
- `docs/agents/triage-labels.md`.
- Boucles d'automatisation agent.
- Ralph Loop ou implémentation autonome continue.
- Fermeture automatique d'issues.
- Support officiel d'autres trackers comme Linear ou Jira.
- Skill `research` dédié.
- Index persistant des initiatives locales.
- Fichier local `decision-log.md`.

Ces éléments peuvent être mentionnés comme améliorations futures, mais ils ne doivent pas être implémentés en v1.

## Modèle D'Artefacts

### Synthèse Des Artefacts

| Artefact | Emplacement par défaut | Versionné | Canonique quand | Notes |
| --- | --- | --- | --- | --- |
| `product-brief.md` | `.initiatives/<id>/product-brief.md` | Non | Avant la spec, si un brief produit est utilisé | Source de vérité de l'exploration produit cadrée |
| `brainstorming.md` | `.initiatives/<id>/brainstorming.md` | Non | Pendant le brainstorming | Exploration divergente capturée au fil de l'eau |
| `validation.md` | `.initiatives/<id>/validation.md` | Non | Pendant la validation | Réduit l'incertitude, ne remplace pas une spec |
| Recherche d'initiative | `.initiatives/<id>/research/*.md` | Non | Pour une extraction liée à l'initiative | Longue conversation, recherche ou exploration |
| Recherche globale | `docs/research/*.md` | Oui | Pour une recherche réutilisable au niveau projet | Stack, architecture, fournisseur, réglementation, contrainte durable |
| Spec | Issue GitHub/GitLab ou `.initiatives/<id>/spec.md` | Selon tracker | Après publication ou création | Source de vérité de ce qui doit être construit |
| Issues de tâches | Issues GitHub/GitLab ou `.initiatives/<id>/tasks/*.md` | Selon tracker | Pendant l'implémentation | Tranches verticales liées à la spec parente |
| Checklist QA | Commentaire/checklist GitHub/GitLab ou fichier local | Selon emplacement | Pendant la validation manuelle | Support de QA humaine |
| `docs/agents/issue-tracker.md` | `docs/agents/issue-tracker.md` | Oui | Toujours pour les opérations d'issues | Décrit le tracker choisi et les commandes/conventions associées |
| `docs/agents/local-artifacts.md` | `docs/agents/local-artifacts.md` | Oui | Toujours pour les artefacts locaux | Décrit `.initiatives/`, chemins, noms et règles d'écriture |
| `docs/agents/documentation.md` | `docs/agents/documentation.md` | Oui | Toujours pour la consommation de docs projet | Indique quand lire `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs et docs associées |
| `CONTEXT.md` | Racine ou racine de contexte | Oui | Toujours pour le langage de domaine | Glossaire strict et langage partagé |
| `CONTEXT-MAP.md` | Racine du projet | Oui | Monorepos ou projets multi-contextes | Pointe les agents vers les contextes |
| ADR | `docs/adr/*.md` | Oui | Décisions globales durables | Critères ADR stricts |

### Dossier Local D'Initiative

Les initiatives locales vivent dans :

```text
.initiatives/<NNN-slug>/
```

Exemples :

```text
.initiatives/001-mvp/
.initiatives/002-dark-mode/
.initiatives/003-billing-redesign/
```

Règles :

- `.initiatives/` est gitignored par défaut.
- `.initiatives/` est local et semi-privé.
- `.initiatives/` n'est pas un coffre-fort à secrets.
- Le dossier utilise un ID à 3 chiffres et un slug en kebab-case.
- Si l'agent doit créer une initiative, il scanne les dossiers existants et propose le prochain ID.
- L'utilisateur peut aussi créer les dossiers manuellement.
- Pas de `.initiatives/index.md` en v1.
- Éviter de réutiliser un ID supprimé ou archivé.

Structure locale par défaut :

```text
.initiatives/
└── 001-initiative-slug/
    ├── product-brief.md
    ├── brainstorming.md
    ├── validation.md
    ├── research/
    │   ├── architecture-options.md
    │   └── market-signals.md
    ├── spec.md
    └── tasks/
        ├── 001-task-slug.md
        └── 002-task-slug.md
```

`spec.md` et `tasks/` ne sont présents que si le tracker choisi est markdown local, ou si l'utilisateur demande explicitement des artefacts locaux équivalents.

### Format Des Artefacts Locaux

Les artefacts markdown locaux doivent rester simples.

Règles :

- Pas de frontmatter.
- Un titre markdown classique suffit.
- Respecter le nom et le chemin fournis par l'utilisateur lorsqu'ils existent.
- Si aucun chemin n'est fourni, proposer un chemin selon les conventions d'artefacts locaux du setup.
- Noms par défaut pour les artefacts principaux : `brainstorming.md`, `product-brief.md`, `validation.md`, `spec.md`.
- Noms en kebab-case pour les fichiers `research/*.md`, `tasks/*.md` et les artefacts spécifiques.

Exception : les issues markdown locales peuvent avoir des lignes légères comme `Status:`, `Labels:` et `Parent issue:` ainsi qu'une section `## Comments`, si c'est la convention du tracker local.

### Conventions De `brainstorming.md`

`brainstorming.md` sert à capturer une exploration divergente, pas à produire une spec ou un plan.

Règles utiles aux futurs skills :

- Utiliser `## Starting Context` pour le contexte de départ et ne plus le réécrire une fois la session lancée.
- Garder les idées sous `## Ideas`, organisées par thèmes ou angles d'exploration adaptés au sujet.
- Utiliser des tags inline seulement quand ils clarifient le statut : `[Explore]`, `[Current scope]`, `[Later]`, `[Rejected]`.
- Ne pas dupliquer une idée dans plusieurs sections de type MVP, later, rejected, questions ou assumptions.
- Attacher les nuances, risques, raisons ou questions comme notes sous l'idée concernée.
- Ne pas ajouter de synthèse finale ou de convergence produit sauf demande explicite.

### Conventions De `product-brief.md`

`product-brief.md` est un brief produit léger. Il cadre le problème, les utilisateurs, les scénarios, la valeur, les horizons de scope, les règles produit, les risques et les questions ouvertes sans devenir une PRD complète, une spec technique ou une task list.

Règles utiles aux futurs skills :

- Distinguer clairement `Current Scope`, `Near-term follow-up`, `Future possibilities`, `Out Of Scope` et `Open Questions`.
- Capturer les exclusions explicites dans `Out Of Scope`, pas dans `Later Scope`.
- Marquer les inconnues importantes par `Not known yet` au lieu de les inventer.
- Marquer les sections non pertinentes par `Not relevant` avec une courte raison au lieu de les supprimer silencieusement.
- Garder `Technical / Architecture Handoff Notes` léger : contraintes, dépendances, implications ou questions, pas schémas détaillés ni contrats d'API.
- Ne pas transformer le brief en backlog, PRD exhaustive, plan d'implémentation, ADR ou spec.

### Confidentialité

`.initiatives/` est gitignored par défaut, mais ce n'est pas un coffre-fort sécurisé.

Autorisé :

- Réflexion produit.
- Notes d'exploration.
- Brouillons.
- Synthèses de recherche.
- Alternatives et pistes rejetées.
- Contexte local d'initiative.

Interdit :

- Secrets.
- Tokens.
- Credentials.
- Données personnelles brutes.
- Exports clients sensibles.
- Tout élément qui ne devrait pas être visible par quelqu'un ayant accès au repo.

### Cycle De Vie Après Publication De La Spec

Avant la spec :

```text
.initiatives/<id>/ = source de vérité de l'exploration
```

Après publication ou création d'une spec dans le tracker choisi :

```text
spec du tracker choisi = source de vérité de ce qui doit être construit
.initiatives/<id>/ = archive locale non canonique de l'exploration
```

L'agent ne doit plus traiter le `product-brief.md` local comme canonique après publication ou création de la spec.

Le dossier local d'initiative n'est pas supprimé automatiquement. L'utilisateur choisit de le conserver, l'archiver ou le supprimer.

## Règles De Confirmation

### Artefacts Structurants

Pour les artefacts structurants comme les specs ou les mises à jour substantielles du brief produit :

```text
confirmation de la cible -> draft en conversation -> validation du contenu -> écriture ou publication
```

Cela s'applique à :

- Création ou mise à jour substantielle de `product-brief.md`.
- Publication d'une spec dans l'issue tracker.
- Création d'une `spec.md` locale.
- Création d'issues de tâches depuis un split.
- Création de documentation globale.
- Création d'ADRs.

### Artefacts Mineurs Ou Extractifs

Pour les artefacts d'extraction comme les notes de capture :

```text
confirmation du chemin -> écriture du fichier -> résumé du résultat
```

L'agent n'a pas besoin de montrer tout le document en draft, sauf demande explicite de l'utilisateur.

### Exception De Capture Live Pour `brainstorm`

`brainstorm` peut écrire au fil de l'eau pendant la session après confirmation initiale de l'initiative et du chemin de l'artefact.

## Règles De Documentation

### `docs/agents/`

`docs/agents/` contient les conventions projet produites par le setup. Ces conventions sont ensuite exposées aux agents via `CLAUDE.md` ou `AGENTS.md`, donc les futurs skills doivent les considérer comme déjà disponibles dans le contexte agent après setup.

Fichiers attendus après setup :

- `docs/agents/issue-tracker.md` : tracker choisi, commandes et conventions pour créer, lire, commenter, lier ou fermer des issues.
- `docs/agents/local-artifacts.md` : conventions `.initiatives/`, noms de dossiers, chemins d'artefacts locaux et règles d'écriture.
- `docs/agents/documentation.md` : règles de consommation de `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs et documentation projet.

`CLAUDE.md` ou `AGENTS.md` doit rester court et fournir aux agents les conventions nécessaires, directement ou par référence aux fichiers de `docs/agents/`. Les détails ne doivent pas être dupliqués inutilement dans le fichier agent racine.

Les futurs skills doivent :

- Respecter les conventions d'issue tracker déjà présentes dans le contexte agent avant toute opération d'issue ou de tracker.
- Respecter les conventions d'artefacts locaux déjà présentes dans le contexte agent avant de créer, lire ou modifier un artefact local.
- Respecter les conventions de documentation déjà présentes dans le contexte agent lorsqu'une exploration ou un travail peut dépendre de la documentation projet.
- Procéder silencieusement si les fichiers optionnels comme `CONTEXT.md`, `CONTEXT-MAP.md` ou `docs/adr/` n'existent pas.
- Signaler explicitement une contradiction avec une convention ou un ADR existant au lieu de l'écraser silencieusement.

Le setup ne doit pas utiliser de marqueurs de blocs gérés. Il met à jour des sections Markdown naturelles, préserve les règles utilisateur non liées et évite les duplications.

### `CONTEXT.md`

`CONTEXT.md` est strictement un glossaire et un document de langage métier partagé.

Il contient :

- Termes canoniques du domaine.
- Termes à éviter.
- Relations entre concepts du domaine.
- Exemples de dialogue utilisant le bon vocabulaire.
- Ambiguïtés résolues.

Il ne doit pas contenir :

- État des initiatives.
- Briefs produit.
- Décisions locales d'une feature.
- Recherches détaillées.
- Notes de réunion.
- Todo lists.
- Specs techniques complètes.

Mettre à jour `CONTEXT.md` uniquement lorsqu'un terme, concept, lien de domaine ou modèle mental est clarifié et doit guider les futurs agents et développeurs.

### `CONTEXT-MAP.md`

Utiliser `CONTEXT-MAP.md` lorsqu'un repo contient plusieurs contextes, packages, domaines, apps ou sous-projets.

Il pointe les agents vers les bons fichiers `CONTEXT.md` et la documentation associée. Ce n'est pas une carte d'architecture générale.

### ADRs

`ADR` est le terme canonique.

ADR signifie Architecture Decision Record.

Les ADRs vivent par défaut dans :

```text
docs/adr/
```

Dans un repo multi-contextes, des ADRs spécifiques peuvent aussi vivre sous un contexte, par exemple `src/billing/docs/adr/`.

Convention de nommage :

```text
docs/adr/0001-short-slug.md
docs/adr/0002-short-slug.md
```

Le numéro est incrémental, sur 4 chiffres. Le slug est court, descriptif et en kebab-case.

Un ADR ne doit être créé que si les trois critères suivants sont vrais :

- La décision est difficile à inverser.
- La décision serait surprenante sans contexte.
- La décision implique un vrai compromis entre options.

Les ADRs concernent des décisions globales du projet, par exemple :

- Choix d'architecture.
- Choix de stack.
- Choix de dépendance majeure.
- Convention durable.
- Décision durable de modèle de domaine.

Les ADRs ne servent pas pour :

- Décisions locales d'initiative.
- Choix temporaires.
- Petits détails d'implémentation.
- Préférences subjectives à faible impact.
- Notes de recherche.

Format ADR minimal :

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

### Emplacements De Recherche

Il existe deux emplacements pour les recherches.

Recherche liée à une initiative :

```text
.initiatives/<id>/research/*.md
```

À utiliser pour :

- Un MVP spécifique.
- Une feature spécifique.
- Une exploration produit locale.
- L'extraction d'une longue session de grilling.
- Une synthèse de recherche qui ne sera plus canonique après la spec.

Recherche globale projet :

```text
docs/research/*.md
```

À utiliser pour :

- Décisions de stack.
- Comparaisons d'architecture.
- Analyse de fournisseur réutilisable.
- Contraintes réglementaires.
- Recherche qui impacte plusieurs initiatives.

Règle par défaut :

```text
Utiliser .initiatives/<id>/research/ sauf si la recherche est réutilisable au-delà de l'initiative courante ou peut être utile au projet dans son ensemble.
```

## Règles Issue Tracker

### Support V1

Support officiel v1 :

```text
GitHub Issues via gh
GitLab Issues via glab
Markdown local dans .initiatives/
```

La convention choisie est définie par le setup et exposée dans le contexte agent. Sa trace durable peut vivre dans `docs/agents/issue-tracker.md`. Le tracker recommandé suit le remote détecté : GitHub pour un remote GitHub, GitLab pour un remote GitLab, markdown local sinon. L'utilisateur peut choisir markdown local même lorsqu'un tracker distant existe.

Si `gh` ou `glab` est absent ou non authentifié, l'agent doit le signaler et recommander l'action concrète suivante. Il ne doit pas basculer silencieusement vers un autre tracker.

Les autres issue trackers, comme Linear ou Jira, peuvent être décrits manuellement dans `docs/agents/issue-tracker.md`, mais ils ne sont pas officiellement supportés en v1.

### Conventions Communes

Les futurs skills qui créent ou découpent des issues doivent respecter les conventions du tracker choisi.

Règles communes :

- Utiliser `gh` pour GitHub et `glab` pour GitLab.
- Utiliser les fichiers `.initiatives/<initiative>/spec.md` et `.initiatives/<initiative>/tasks/*.md` lorsque le tracker choisi est markdown local.
- Lier explicitement les tâches à leur spec parente, car les CLIs `gh` et `glab` ne fournissent pas une relation parent/enfant native fiable pour ce workflow.
- Ne jamais fermer une issue sauf instruction ou autorisation explicite de l'utilisateur.
- Ne jamais écrire de secrets, tokens, credentials, données personnelles brutes ou exports clients sensibles dans les issues, fichiers markdown locaux ou commentaires.

Pour markdown local, les issues peuvent utiliser :

- `Status:` près du haut du fichier.
- `Labels:` près du haut du fichier.
- `Parent issue:` près du haut du fichier pour les tâches issues d'une spec.
- Un séparateur `---` puis une section `## Comments` pour simuler les commentaires.

### Pas De Triage En V1

Pas de `docs/agents/triage-labels.md` en v1.

Aucun label obligatoire du type :

- `needs-triage`
- `needs-info`
- `ready-for-agent`
- `ready-for-human`
- `wontfix`

Si un projet utilise déjà des labels, `docs/agents/issue-tracker.md` peut les mentionner.

Les labels de triage et les boucles d'automatisation sont des améliorations futures.

## Execution Contract

Les skills d'implémentation nécessitent un execution contract clair.

L'execution contract n'est pas un document séparé. C'est l'ensemble minimal d'informations disponibles dans le contexte, quelle que soit leur source.

Éléments minimum :

- Goal : ce qui doit être obtenu.
- Scope : ce qui est inclus.
- Out of scope : ce qui ne doit pas être touché.
- Acceptance criteria : comment savoir que c'est terminé.
- Constraints : contraintes produit, UX, techniques, architecture, temps, légales ou business.
- Feedback loop : test, build, lint, repro, commande, check manuel ou autre vérification.
- Source of truth : issue, spec, product brief, prompt, fichier local ou autre contexte.

Si l'execution contract est incomplet, l'agent doit :

- Identifier les informations critiques manquantes.
- Proposer des hypothèses pour un execution contract minimal.
- Demander à l'utilisateur si ces hypothèses conviennent ou s'il veut fournir plus de contexte.

L'agent ne doit pas implémenter silencieusement à partir d'hypothèses floues.

## Exemples D'Utilisation

Ces exemples ne sont pas des flows obligatoires.

### Greenfield Ou Grosse Initiative

```text
setup-skills-workflow -> brainstorm -> grill-me/recherche -> capture -> product-brief -> validate -> prototype -> grill-me/recherche -> to-spec -> split -> implement -> review -> qa
```

### Feature Substantielle

```text
grill-me/exploration -> product-brief optionnel -> capture optionnel -> to-spec -> split -> implement -> review -> qa
```

### Petite Feature

```text
grill-me/exploration -> to-spec ou execution contract direct -> implement -> qa/review si utile
```

### Bug Ou Régression

```text
diagnose -> test de régression -> review si utile -> qa si visible utilisateur
```

### Sujet D'Architecture

```text
zoom-out -> improve-codebase-architecture -> prototype si besoin -> implement ou implement-tdd
```

## Skills Non Inclus En V1

### Pas De Skill `research` Dédié

La recherche peut se faire directement dans une session normale avec un prompt.

Utiliser :

- `capture` pour conserver le résultat.
- `validate` si la recherche sert une décision de validation.

### Pas De Skill `triage`

Pas de système de triage d'issues en v1.

Les futurs skills ne doivent pas créer :

- `docs/agents/triage-labels.md`.
- Labels obligatoires de triage.
- Workflow automatisé `ready-for-agent`.
- Agent briefs de triage.
- Fermeture automatique d'issues.

## Notes De Design Ouvertes

Le workflow est assez spécifié pour permettre la création progressive des futurs skills.

Les décisions restantes pourront être prises pendant l'authoring des skills :

- Formulation exacte de chaque futur `SKILL.md`.
- Templates précis des futurs artefacts non encore implémentés.
- Exceptions spécifiques qu'un futur skill devra documenter dans son propre `SKILL.md`.
