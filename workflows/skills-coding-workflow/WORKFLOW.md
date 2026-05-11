# Spécification Du Skill-Based Coding Workflow

Ce document est la spécification interne du futur workflow de coding IA basé sur des Agent Skills. Il ne s'agit pas d'un fichier de règles runtime et il n'est pas destiné à être copié tel quel dans les projets utilisateurs.

Son rôle est de décrire précisément le workflow, les artefacts, les conventions et les futurs skills afin de pouvoir créer les `SKILL.md` plus tard.

## Objectif

Ce workflow s'inspire du workflow de Matt Pocock, mais l'adapte au pilotage d'initiatives logicielles. Il n'est pas un framework agentique lourd : il fournit des routines ciblées pour que le développeur garde le contrôle en collaborant avec des agents IA.

Il vise surtout à transformer une idée, une intention ou un problème encore flou en contexte clair, puis en contrat d'exécution exploitable, puis en implémentation vérifiable.

La forme générale recherchée est :

```text
idée -> exploration -> décisions -> spec -> tâches verticales -> implémentation -> review/QA
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

Les futurs skills ne doivent pas dépendre du fait qu'un autre skill ait été exécuté avant.

Un skill peut recevoir du contexte depuis :

- La conversation courante.
- Le prompt utilisateur.
- Un artefact local.
- Une issue GitHub.
- Une spec.
- Une tâche.
- Des notes de recherche.
- La documentation projet.
- L'exploration du codebase.

Les skills ne doivent pas imposer de dépendances directes du type "lance `/brief` avant" ou "lance `/to-spec` après".

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
- Publier une spec dans GitHub.
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
.initiatives/<id>/ = mémoire locale d'exploration
GitHub Issues = surface d'exécution et de collaboration
```

Dans le workflow GitHub par défaut :

- `brief.md`, `brainstorming.md`, `validation.md` et les recherches liées à une initiative restent en local dans `.initiatives/<id>/`.
- `spec` et `tasks` vivent dans GitHub Issues.
- `qa` et les résumés d'implémentation peuvent être des commentaires ou checklists sur les issues concernées.

Dans le fallback markdown local :

- `spec.md` et `tasks/*.md` vivent dans `.initiatives/<id>/`.
- Ces fichiers ne sont pas versionnés, sauf si l'utilisateur modifie explicitement la convention.

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

## Scope V1

### Inclus En V1

- GitHub Issues via `gh`.
- Fallback markdown local dans `.initiatives/`.
- Artefacts d'exploration d'initiative.
- Specs et découpage en tâches.
- Implémentation avec ou sans TDD.
- Diagnostic.
- Prototypage.
- Review et génération de checklist QA.
- Documentation projet via `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/adr/` et `docs/research/`.
- Setup des règles agent propres à un projet via `CLAUDE.md` ou `AGENTS.md`.

### Hors Scope En V1

- Système de triage d'issues.
- `docs/agents/triage-labels.md`.
- Boucles d'automatisation agent.
- Ralph Loop ou implémentation autonome continue.
- Fermeture automatique d'issues.
- Support officiel GitLab, Linear ou Jira.
- Skill `/research` dédié.
- Index persistant des initiatives locales.
- Fichier local `decision-log.md`.

Ces éléments peuvent être mentionnés comme améliorations futures, mais ils ne doivent pas être implémentés en v1.

## Modèle D'Artefacts

### Synthèse Des Artefacts

| Artefact | Emplacement par défaut | Versionné | Canonique quand | Notes |
| --- | --- | --- | --- | --- |
| `brief.md` | `.initiatives/<id>/brief.md` | Non | Avant la spec, si un brief est utilisé | Source de vérité de l'exploration produit |
| `brainstorming.md` | `.initiatives/<id>/brainstorming.md` | Non | Pendant le brainstorming | Exploration divergente capturée au fil de l'eau |
| `validation.md` | `.initiatives/<id>/validation.md` | Non | Pendant la validation | Réduit l'incertitude, ne remplace pas une spec |
| Recherche d'initiative | `.initiatives/<id>/research/*.md` | Non | Pour une extraction liée à l'initiative | Longue conversation, recherche ou exploration |
| Recherche globale | `docs/research/*.md` | Oui | Pour une recherche réutilisable au niveau projet | Stack, architecture, fournisseur, réglementation, contrainte durable |
| Spec | Issue GitHub par défaut | Oui via tracker | Après publication | Source de vérité de ce qui doit être construit |
| Spec locale fallback | `.initiatives/<id>/spec.md` | Non | Si pas de tracker ou choix local | Mode solo/local |
| Issues de tâches | Issues GitHub par défaut | Oui via tracker | Pendant l'implémentation | Tranches verticales liées à la spec parente |
| Tâches locales fallback | `.initiatives/<id>/tasks/*.md` | Non | Si pas de tracker ou choix local | Miroir de la structure des issues de tâches |
| Checklist QA | Commentaire/checklist GitHub ou fichier local | Selon emplacement | Pendant la validation manuelle | Support de QA humaine |
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
    ├── brief.md
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

`spec.md` et `tasks/` ne sont présents que si l'utilisateur choisit explicitement de créer des artefacts locaux en markdown à la place de GitHub Issues.

### Format Des Artefacts Locaux

Les artefacts markdown locaux doivent rester simples.

Règles :

- Pas de frontmatter.
- Pas d'en-tête de métadonnées.
- Un titre markdown classique suffit.
- Noms fixes pour les artefacts principaux.
- Noms en kebab-case pour les fichiers `research/*.md`.

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

Après publication d'une spec GitHub :

```text
issue GitHub de spec = source de vérité de ce qui doit être construit
.initiatives/<id>/ = archive locale non canonique de l'exploration
```

L'agent ne doit plus traiter le brief local comme canonique après publication de la spec.

Le dossier local d'initiative n'est pas supprimé automatiquement. L'utilisateur choisit de le conserver, l'archiver ou le supprimer.

## Règles De Confirmation

### Artefacts Structurants

Pour les artefacts structurants comme les specs ou les mises à jour substantielles du brief :

```text
draft en conversation -> validation utilisateur -> écriture ou publication
```

Cela s'applique à :

- Création ou mise à jour substantielle de `brief.md`.
- Publication d'une spec GitHub.
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

### Exception De Capture Live Pour `/brainstorm`

`/brainstorm` peut écrire au fil de l'eau pendant la session.

## Règles De Documentation

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

Utiliser `CONTEXT-MAP.md` lorsqu'un repo contient plusieurs contextes, packages, domaines ou sous-projets.

Il pointe les agents vers les bons fichiers `CONTEXT.md` et la documentation associée.

### ADRs

`ADR` est le terme canonique.

ADR signifie Architecture Decision Record.

Les ADRs vivent dans :

```text
docs/adr/
```

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
# Short Decision Title

1 à 3 courts paragraphes couvrant le contexte, la décision et la raison.
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
```

Fallback :

```text
Markdown local dans .initiatives/
```

Les autres issue trackers peuvent être décrits manuellement dans `docs/agents/issue-tracker.md`, mais ils ne sont pas officiellement supportés en v1.

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
- Source of truth : issue, spec, brief, prompt, fichier local ou autre contexte.

Si l'execution contract est incomplet, l'agent doit :

- Identifier les informations critiques manquantes.
- Proposer des hypothèses pour un execution contract minimal.
- Demander à l'utilisateur si ces hypothèses conviennent ou s'il veut fournir plus de contexte.

L'agent ne doit pas implémenter silencieusement à partir d'hypothèses floues.

## Skills (étapes du workflow)

Les steps actifs du workflow sont maintenant documentés dans `steps/`.

Chaque fichier de step reste une spécification autonome, pas une implémentation finale de `SKILL.md`.

- [`/setup-skills-workflow`](steps/setup-skills-workflow.md)
- [`/brainstorm`](steps/brainstorm.md)
- [`/grill-me`](steps/grill-me.md)
- [`/grill-with-docs`](steps/grill-with-docs.md)
- [`/capture`](steps/capture.md)
- [`/brief`](steps/brief.md)
- [`/validate`](steps/validate.md)
- [`/prototype`](steps/prototype.md)
- [`/to-spec`](steps/to-spec.md)
- [`/split`](steps/split.md)
- [`/implement`](steps/implement.md)
- [`/implement-tdd`](steps/implement-tdd.md)
- [`/review`](steps/review.md)
- [`/qa`](steps/qa.md)
- [`/diagnose`](steps/diagnose.md)
- [`/zoom-out`](steps/zoom-out.md)
- [`/improve-codebase-architecture`](steps/improve-codebase-architecture.md)

## Skills Non Inclus En V1

### Pas De `/research`

La recherche peut se faire directement dans une session normale avec un prompt.

Utiliser :

- `/capture` pour conserver le résultat.
- `/validate` si la recherche sert une décision de validation.

### Pas De `/triage`

Pas de système de triage d'issues en v1.

Concepts utiles à conserver pour une future version :

- Un triage peut distinguer au minimum les catégories `bug` et `enhancement`.
- Un triage peut utiliser des états comme `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human` et `wontfix`.
- Une issue triagée devrait idéalement avoir une seule catégorie et un seul état.
- `ready-for-agent` ne doit pas être un simple label. Cela signifie que l'issue contient un contrat d'exécution assez clair pour qu'un agent puisse travailler avec peu ou pas d'interaction humaine.
- `ready-for-human` signifie qu'une décision, review, validation ou action humaine est nécessaire avant de continuer.
- Un agent brief peut être généré lorsqu'une issue devient `ready-for-agent`.

Structure possible d'un futur agent brief :

```text
Category
Summary
Current behavior
Desired behavior
Key interfaces
Acceptance criteria
Out of scope
```

Principes d'un agent brief :

- Durable plutôt que trop précis.
- Comportemental plutôt que procédural.
- Pas de chemins de fichiers fragiles.
- Pas de numéros de lignes.
- Critères d'acceptation vérifiables.
- Frontières de scope explicites.

Les futures versions pourront aussi ajouter :

- Labels d'état.
- Workflow `ready-for-agent` automatisé.
- Boucles d'automatisation.
- Fermeture automatique d'issues.

## Exemples D'Utilisation

Ces exemples ne sont pas des flows obligatoires.

### Greenfield Ou Grosse Initiative

```text
setup -> brainstorm -> grill/recherche -> capture -> brief -> validate -> prototype -> grill/recherche -> to-spec -> split -> implement -> review -> qa
```

### Feature Substantielle

```text
grill/exploration -> brief optionnel -> capture optionnel -> to-spec -> split -> implement -> review -> qa
```

### Petite Feature

```text
grill/exploration -> to-spec ou execution contract direct -> implement -> qa/review si utile
```

### Bug Ou Régression

```text
diagnose -> test de régression -> review si utile -> qa si visible utilisateur
```

### Sujet D'Architecture

```text
zoom-out -> improve-codebase-architecture -> prototype si besoin -> implement ou implement-tdd
```

## Notes De Design Ouvertes

Le workflow est maintenant assez spécifié pour permettre la future création des skills.

Les décisions restantes pourront être prises pendant l'authoring des skills :

- Formulation exacte de chaque `SKILL.md`.
- Contenu exact généré dans `docs/agents/*.md`.
- Quantité de cette spécification à conserver une fois les vrais skills créés.
