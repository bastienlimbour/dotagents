# Workflow AI pour le développement de projets logiciels

> [!NOTE]
> Ce workflow n'est pas fait pour le Vibe Coding. Vous devez maitriser les fondamentaux du développement logiciel et maîtriser l'architecture de vos projets pour l'utiliser efficacement.

Workflow AI coding léger, modulaire et humain-au-centre. Il couvre le cadrage, le découpage, l'implémentation, la review et la validation d'un projet logiciel, sans chercher à automatiser tout le cycle. Il s'appuie sur des skills spécialisés et une mémoire de travail versionnée, dans le repo ou dans un tracker.

---

## Principes

- **Cadrage-first :** cadrer avant de coder, avec un niveau de formalisation proportionné au scope.
- **Alignement avant documentation :** clarifier les décisions implicites avec `grill-me` ou `grill-with-docs` avant de produire un PRD non trivial.
- **Intention-driven :** activer les étapes selon le besoin, pas mécaniquement.
- **Produit / technique / exécution séparés :** `prd.md` décrit le quoi, `tech-design.md` le comment, `tasks/` l'ordre de build.
- **PRD fonctionnel, pas technique :** le PRD contient comportements, règles, edge cases et acceptance criteria, pas de détails d'implémentation.
- **Preflight proportionné :** le plan d'implémentation immédiat vit dans le `Build Preflight`, parfois en quelques lignes.
- **Vertical slices par défaut :** découper en tranches vérifiables, pas en couches `DB -> API -> UI`.
- **Feedback loops-first :** tests, typecheck, lint, CI et environnement local stable définissent le plafond de qualité des agents.
- **Humain pour le jugement :** garder l'humain dans la boucle pour produit, UX, architecture, QA, review et validation finale.
- **Interfaces avant implémentation :** concevoir les frontières de modules et interfaces stables avant de déléguer l'intérieur à un agent.
- **Contexte propre :** préférer des tâches courtes, un contexte ciblé et un clear entre grandes étapes plutôt qu'une conversation infinie.
- **Une source de vérité par sujet :** éviter la double saisie concurrente entre Markdown, issues et tracker.
- **Doc utile seulement :** conserver les décisions durables et les documents utiles ; jeter les artefacts temporaires une fois consolidés.

---

## Vue d'ensemble

Le workflow distingue le flux principal et les étapes transverses.

- **Core workflow :** progression normale d'une initiative vers le build.
- **On-demand steps :** étapes activables hors séquence, selon contexte.

```text
Discovery : [brainstorm] -> [brief] -> [grill-me | grill-with-docs] -> [validate]
Product   : prd
Technical : [tech-design]
Execution : [slice] -> build/tdd -> review -> qa -> capitalize
```

### Core workflow steps

| Étape | Skill | Statut | Artefact |
| ----- | ----- | ------ | -------- |
| [Brief](steps/001-brief.md) | `brief` | Optionnel | `brief.md` optionnel |
| [Validate](steps/002-validate.md) | `validate` | Optionnel | `validation.md` optionnel |
| [PRD](steps/003-prd.md) | `prd` | Requis sauf trivial | `prd.md` |
| [Tech Design](steps/004-tech-design.md) | `tech-design` | Si impact technique non trivial | `tech-design.md` |
| [Slice](steps/005-slice.md) | `slice` | Si multi-tâches | `tasks/*.md` |
| [Build](steps/006-build.md) | `implement` / `implement-tdd` | Requis | Code + compte rendu |
| [Review](steps/007-review.md) | `review` | Recommandé | Feedback |
| [QA](steps/008-qa.md) | `qa` | À la demande | `qa.md` optionnel |
| [Capitalize](steps/009-capitalize.md) | `capitalize` | Si décision durable ou doc à maintenir | Docs / ADRs / follow-ups |

### On-demand steps

| Étape | Skill | Rôle | Artefact |
| ----- | ----- | ---- | -------- |
| [Brainstorm](steps/brainstorm.md) | `brainstorm` | Ouvrir l'espace des options | `brainstorming.md` optionnel |
| [Grill Me](steps/grill-me.md) | `grill-me` | Interview décisionnelle persistante | Synthèse ou intégration dans l'étape suivante |
| [Grill With Docs](steps/grill-with-docs.md) | `grill-with-docs` | Interview alignée avec langage domaine, docs et ADRs | `CONTEXT.md`, décisions ou ADRs |
| [Prototype UI](steps/prototype-ui.md) | `prototype-ui` | Explorer des directions frontend jetables | Prototypes isolés + synthèse |
| [Diagnose](steps/diagnose.md) | `diagnose` | Diagnostiquer un bug complexe ou une régression | Cause racine + fix + test de régression |
| [Zoom Out](steps/zoom-out.md) | `zoom-out` | Cartographier une zone de code inconnue | Carte modules / callers / seams |
| [Improve Codebase Architecture](steps/improve-codebase-architecture.md) | `improve-codebase-architecture` | Trouver des opportunités de deepening | Candidats de refactor structurants |
| [Project Baseline](steps/project-baseline.md) | `project-baseline` | Établir la baseline d'un projet existant | Docs projet mises à jour |
| [Ship Readiness](steps/ship-readiness.md) | `ship-readiness` | Gate optionnel avant livraison importante | Checklist ou verdict `Go / No-Go` |

---

## Entrées rapides selon l'intention

| Intention | Chemin recommandé |
| --------- | ----------------- |
| Exploration d'idées | `Brainstorm -> Brief -> [Grill Me] -> [Validate]` |
| Gros projet / MVP from scratch | `[Brainstorm] -> Brief -> [Grill Me] -> [Validate] -> PRD -> Tech Design -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]` |
| Grosse feature sur projet existant | `[Brief] -> [Grill Me ou Grill With Docs] -> PRD -> [Tech Design] -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]` |
| Feature moyenne multi-tâches | `[Grill Me ou Grill With Docs] -> PRD -> [Tech Design Lite] -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]` |
| Petite feature | `PRD minimal -> [Grill Me si ambigu] -> Build -> [Review] -> [QA]` |
| Fix / hotfix | `Build -> [Review] -> [QA]` |
| Bug complexe | `Diagnose -> Build ou TDD -> Review -> [QA]` |
| Zone de code inconnue | `Zoom Out` |
| UI incertaine | `[Prototype UI] -> Brief ou PRD -> Build propre -> [Review] -> [QA]` |
| Refactoring structurel | `Zoom Out -> Improve Codebase Architecture -> [Grill With Docs] -> Tech Design -> Slice -> per-task(Build -> Review) -> [QA] -> Capitalize` |
| Projet legacy / abandonné | `Project Baseline -> [PRD] ou [Tech Design]` |
| Livraison importante | `... -> Review -> [QA] -> Ship Readiness` |

---

## Documentation et artefacts

### Source de vérité

Le workflow est **storage-agnostic**. Une initiative a un support actif principal. Les supports secondaires pointent, commentent ou automatisent, mais ne dupliquent pas le contenu.

Les artefacts de travail (`prd.md`, `tech-design.md`, `tasks/`, `qa.md`, prototypes) servent pendant l'initiative. À la clôture, ils doivent être supprimés, archivés, fermés ou consolidés dans une documentation durable. Un vieux PRD ne doit pas redevenir source de vérité implicite pour un agent.

Les décisions durables vivent dans le code, les tests, les docs projet, les conventions, `CONTEXT.md` ou les ADRs. Les artefacts temporaires ne survivent pas par défaut.

Les fichiers durables sont créés **lazily** : ne pas créer `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/` ou `docs/agents/` avant d'avoir une information réelle à y stocker.

### Supports possibles

- fichiers Markdown dans le repo
- GitHub Issues / Sub-Issues
- tracker type Linear, Jira, GitHub Projects

Recommandation pratique :

- travail collaboratif ou multi-agent : GitHub Issues ou tracker équivalent
- travail solo ou local-first : Markdown dans le repo

Robustesse pour un agent :

1. Markdown versionné dans le repo
2. GitHub Issues / tracker du même écosystème que le repo
3. Outil externe séparé du repo

Si le support est externe au repo, l'agent doit y accéder via CLI officielle ou serveur MCP.

### Configuration agent optionnelle

Sur un projet multi-agent ou piloté par issues, une configuration repo-locale peut éviter les ambiguïtés répétées.

Emplacement recommandé :

- `AGENTS.md` ou `CLAUDE.md` : bloc `## Agent skills` qui pointe vers les docs ci-dessous
- `docs/agents/issue-tracker.md` : où lire et publier les issues ou PRDs
- `docs/agents/domain.md` : comment lire `CONTEXT.md`, `CONTEXT-MAP.md` et `docs/decisions/`

Options fréquentes de tracker :

- GitHub Issues via `gh`
- GitLab Issues via `glab`
- Markdown local, par exemple `.scratch/<feature>/`
- Linear, Jira ou autre tracker, décrit en prose avec le CLI ou MCP à utiliser

Si ces docs n'existent pas, les skills consommateurs continuent silencieusement. Ils ne doivent pas proposer de les créer upfront ; seul un besoin réel de configuration durable justifie leur création.

### Structure recommandée

Ici le support principal est le Markdown versionné dans le repo, mais il peut être remplacé par un tracker (GitHub Issues, Linear, Jira, etc.)

```text
/
├─ AGENTS.md, README.md, etc.
├─ CONTEXT.md                    (glossaire domaine durable, optionnel)
├─ CONTEXT-MAP.md                (si plusieurs bounded contexts, optionnel)
├─ docs/
│  ├─ agents/                    (configuration agent optionnelle)
│  │  ├─ issue-tracker.md
│  │  └─ domain.md
│  ├─ architecture.md
│  ├─ conventions.md
│  ├─ testing-strategy.md
│  ├─ decisions/
│  │  └─ 001-*.md                (ADRs / décisions durables)
│  ├─ product/
│  │  └─ initiatives.md          (optionnel)
│  └─ specs/
│     ├─ 001-<initiative>/
│     │  ├─ brainstorming.md     (optionnel)
│     │  ├─ brief.md             (optionnel)
│     │  ├─ validation.md        (optionnel)
│     │  ├─ prd.md
│     │  ├─ tech-design.md       (optionnel)
│     │  ├─ qa.md                (optionnel)
│     │  └─ tasks/
│     │     ├─ 001-<task>.md
│     │     └─ ...
│     └─ 002-<initiative>/
│        └─ prd.md
│
└─ apps/, packages/, scripts/, ...
```

Règles de nommage :

- un dossier par initiative, en kebab-case, préfixé par `001-`, `002-`, ...
- `tasks/` n'existe que si l'initiative a plusieurs tâches
- un fichier par tâche, préfixé par `001-`, `002-`, ...

### Initiative Index

Un index est utile mais optionnel. Il peut vivre dans `docs/product/initiatives.md`, `docs/specs/index.md`, GitHub Projects, Linear, Jira, ou ne pas exister sur un petit projet.

Son rôle :

- lister les initiatives
- indiquer leur statut
- pointer vers PRD, tâches ou tickets

Exemple minimal :

```text
En cours
- 003-team-collaboration - PRD validé, 2/5 tâches terminées

À venir
- 004-gamification - brainstorming uniquement

Terminées
- 001-mvp
- 002-dark-mode
```

### Boundaries documentaires

Le workflow ne crée pas d'étape `Spec` séparée.

- `CONTEXT.md` : vocabulaire domaine durable et termes partagés.
- `CONTEXT-MAP.md` : carte des bounded contexts si le projet en a plusieurs.
- `prd.md` : produit, comportement, règles fonctionnelles, acceptance criteria
- `tech-design.md` : architecture, décisions techniques, compromis, risques
- `tasks/*.md` : tranches exécutables et vérifiables
- `Build Preflight` : plan d'implémentation immédiat
- `docs/decisions/*.md` : ADRs ou décisions durables, seulement quand le contexte restera utile.
- `docs/agents/*.md` : configuration consommée par les agents, seulement si le repo en a besoin.

### Format `CONTEXT.md`

`CONTEXT.md` capture le langage métier durable. Il doit rester lisible par un domaine expert et ne pas devenir une doc technique.

Structure recommandée :

```md
# {Context Name}

Description courte du contexte.

## Language

**Order**:
Définition concise en une phrase.
_Avoid_: Purchase, transaction

## Relationships

- Un **Order** produit une ou plusieurs **Invoices**

## Example dialogue

> **Dev:** "Quand un **Customer** place un **Order**, crée-t-on l'**Invoice** immédiatement ?"
> **Domain expert:** "Non, l'**Invoice** est générée après confirmation du fulfilment."

## Flagged ambiguities

- "account" était utilisé pour **Customer** et **User** ; décision : concepts distincts.
```

Règles :

- choisir un terme canonique et lister les synonymes à éviter avec `_Avoid_:`
- garder les définitions courtes : ce que le concept est, pas comment il est implémenté
- inclure les relations et cardinalités évidentes
- documenter les ambiguïtés résolues
- exclure les concepts techniques génériques, même s'ils sont fréquents dans le code
- mettre à jour inline quand un terme est stabilisé, ne pas attendre la fin de session

### Format des décisions durables

Les décisions vivent dans `docs/decisions/` et utilisent un numéro séquentiel : `001-<slug>.md`, `002-<slug>.md`, etc.

Format minimal :

```md
# {Titre court de la décision}

1 à 3 phrases : contexte, décision, pourquoi.
```

Sections optionnelles, seulement si elles ajoutent une vraie valeur :

- `Status: proposed | accepted | deprecated | superseded by 00X`
- `Considered Options`
- `Consequences`

Créer une décision seulement si les trois critères sont vrais : difficile à renverser, surprenante sans contexte, issue d'un vrai compromis.

### Execution Contract

`Build` démarre depuis un `Execution Contract` suffisant. Ce n'est pas un nouveau document : il vit dans un PRD minimal ou dans chaque task spec.

Contenu minimal :

- scope
- behavior
- acceptance criteria
- edge cases
- non-goals
- verification
- verification commands ou feedback commands si connues
- dépendances `blocked-by` si applicable
- type `AFK | HITL` si la tâche est destinée à un agent
- touchpoints probables, sans plan d'implémentation détaillé

### Format des outputs

Les listes de contenu ne sont pas des checklists exhaustives. Chaque skill doit produire le plus petit artefact utile pour la décision, l'exécution ou la validation.

Règles :

- choisir le niveau `lite / standard / full` avant de rédiger
- inclure seulement les sections qui changent une décision, lèvent une ambiguïté ou servent directement l'exécution
- distinguer contenu obligatoire, contenu conditionnel et contenu à éviter quand l'output peut grossir
- omettre les sections sans signal réel
- éviter transcript brut, logs longs, inventaire exhaustif de fichiers, copier-coller de l'étape précédente
- finir par les décisions prises, questions ouvertes bloquantes

---

## Référence des étapes

Les définitions détaillées vivent dans `steps/`.

### Core workflow

| Ordre | Étape | Fichier |
| ----- | ----- | ------- |
| 001 | Brief | [steps/001-brief.md](steps/001-brief.md) |
| 002 | Validate | [steps/002-validate.md](steps/002-validate.md) |
| 003 | PRD | [steps/003-prd.md](steps/003-prd.md) |
| 004 | Tech Design | [steps/004-tech-design.md](steps/004-tech-design.md) |
| 005 | Slice | [steps/005-slice.md](steps/005-slice.md) |
| 006 | Build | [steps/006-build.md](steps/006-build.md) |
| 007 | Review | [steps/007-review.md](steps/007-review.md) |
| 008 | QA | [steps/008-qa.md](steps/008-qa.md) |
| 009 | Capitalize | [steps/009-capitalize.md](steps/009-capitalize.md) |

### On-demand steps

| Étape | Fichier |
| ----- | ------- |
| Brainstorm | [steps/brainstorm.md](steps/brainstorm.md) |
| Grill Me | [steps/grill-me.md](steps/grill-me.md) |
| Grill With Docs | [steps/grill-with-docs.md](steps/grill-with-docs.md) |
| Prototype UI | [steps/prototype-ui.md](steps/prototype-ui.md) |
| Diagnose | [steps/diagnose.md](steps/diagnose.md) |
| Zoom Out | [steps/zoom-out.md](steps/zoom-out.md) |
| Improve Codebase Architecture | [steps/improve-codebase-architecture.md](steps/improve-codebase-architecture.md) |
| Project Baseline | [steps/project-baseline.md](steps/project-baseline.md) |
| Ship Readiness | [steps/ship-readiness.md](steps/ship-readiness.md) |

---

## Règles transverses

### Product / Technical / Execution boundaries

- `CONTEXT.md` : vocabulaire domaine durable et termes partagés.
- Brief : direction produit claire, description de ce qu'on souhaite build.
- PRD : comportement observable, règles fonctionnelles, acceptance criteria.
- Tech Design : décisions techniques, interfaces, data model, migrations, risques.
- Task specs : tranches exécutables avec Execution Contract.
- Build Preflight : plan immédiat d'implémentation.
- `docs/agents/` : configuration de consommation par agents.

### Feedback loops

- Sans feedback fiable, l'agent code à l'aveugle.
- Documenter les commandes réelles du projet dans `README.md`, `AGENTS.md`, `docs/testing-strategy.md` ou équivalent.
- Feedback minimal utile : typecheck, tests automatisés, lint, formatage, build et CI rapide.
- Feedback avancé : dev server accessible, vérification navigateur, tests e2e ciblés, migrations vérifiables, seeds reproductibles.
- Les hooks de pre-commit peuvent bloquer formatage, lint, typecheck et tests critiques avant commit.
- Si un check échoue, corriger ou documenter le blocage avant d'élargir le scope.
- Pour un bug, le feedback loop est le produit principal du diagnostic : sans signal pass/fail fiable, ne pas élargir les hypothèses.

### AFK / HITL

- `AFK` : tâche claire, non bloquée, testable, avec Execution Contract suffisant.
- `HITL` : clarification produit, arbitrage métier, UX, architecture, sécurité sensible, QA, review ou validation finale.
- Une tâche `AFK` peut être auto-approuvée seulement si les dépendances, checks et critères de succès sont explicites.
- Une tâche bloquée ou ambiguë reste `HITL` jusqu'à résolution.

### Vertical slices

- Construire une tranche complète et vérifiable.
- Éviter les tâches horizontales par couche.
- Inclure les couches nécessaires à la slice : données, logique, API/routes, UI minimale et tests si pertinent.
- Obtenir du feedback de bout en bout tôt, même avec une version minimale.
- Préférer plusieurs petites slices reviewables à une grosse tâche qui ne devient testable qu'à la fin.
- Utiliser les tracer bullets : une slice fine qui traverse le système vaut mieux qu'un lot de tâches par couche.

### TDD

- Utiliser red-green-refactor pour bug fix, logique métier, comportement sensible ou risque de régression.
- Tester un comportement à la fois via les interfaces publiques.
- Vérifier que le test échoue pour la bonne raison avant d'implémenter.
- Éviter les tests qui figent les détails internes, les mocks inutiles ou les tests complaisants écrits après coup.
- Ne pas faire de TDD horizontal : éviter `tous les tests` puis `tout le code`.
- Préférer des tests integration-style via les vraies interfaces publiques.
- Mock uniquement aux frontières système ou quand un substitut local n'est pas pratique.
- Préférer des interfaces spécifiques pour les opérations externes plutôt qu'un fetcher générique difficile à tester.

### Deep modules

- Préférer des modules profonds : interface simple, comportement utile encapsulé, frontière de test claire.
- Éviter la multiplication de petits fichiers, helpers ou exports qui dispersent la compréhension.
- L'humain valide les interfaces structurantes ; l'agent peut implémenter l'intérieur du module.
- La depth est une propriété de l'interface : beaucoup de comportement utile pour peu de surface à apprendre.
- L'interface est la surface de test ; si le test doit passer derrière l'interface, la forme du module est probablement mauvaise.
- La locality concentre changements, bugs et connaissances à un endroit au lieu de les disperser chez les callers.
- Le deletion test révèle les pass-through : supprimer un module shallow fait souvent disparaître la complexité au lieu de la concentrer.
- Un adapter unique indique souvent un seam hypothétique ; deux adapters ou variantes réelles justifient mieux le seam.
- Les seams internes d'un module profond ne doivent pas forcément devenir son interface externe.
- Dépendance in-process : deepenable directement et testable par l'interface du module.
- Dépendance local-substitutable : préférer un substitut local en test plutôt qu'un mock fragile.
- Dépendance remote-owned : définir un port au seam, avec adapter production et adapter test.
- Dépendance true external : injecter un port et utiliser un mock adapter ciblé.

### Source-driven decisions

- Vérifier la doc officielle quand une décision dépend d'un framework ou d'une lib.
- Signaler tout conflit entre doc officielle et patterns du repo avant de trancher.
- Utiliser le vocabulaire de `CONTEXT.md` dans les titres d'issues, PRDs, tests, hypothèses et plans.
- Si un terme nécessaire manque ou contredit l'usage du code, c'est un signal pour `Grill With Docs`.
- Signaler explicitement tout conflit avec une décision durable au lieu de l'écraser silencieusement.

### Context engineering

- Charger le contexte utile, pas tout le repo.
- Garder artefacts, fichiers et patterns pertinents pour la tâche.
- Utiliser `Zoom Out` avant de modifier une zone inconnue ou difficile à situer.
- Préférer `clear` entre grandes étapes ou avant review à un historique compacté trop long.
- Utiliser PRD, tasks, issues, docs et tests comme mémoire externe plutôt que l'historique complet du chat.
- Garder le system prompt et les instructions poussées aussi courts que possible.
- Standards en pull pour l'implémenteur : docs et conventions disponibles si besoin.
- Standards en push pour le reviewer : règles pertinentes explicitement fournies pour comparaison.
- Si `CONTEXT.md`, `CONTEXT-MAP.md` ou `docs/decisions/` n'existent pas, continuer silencieusement et ne les créer que lorsqu'une décision ou un terme réel est stabilisé.

### Stop-the-line

- Si test, build ou runtime casse, traiter avant d'ajouter du scope.
- Ne pas empiler du nouveau travail sur un état instable.

### Faire évoluer une initiative

Modifier une initiative active si contrainte, scope ou tâches changent sans pivot majeur.

Ouvrir une nouvelle initiative si le travail devient indépendant, s'il y a pivot majeur, ou si l'initiative précédente est historique.

Règles :

- ne pas réécrire l'histoire d'une initiative terminée
- ne pas modifier rétroactivement une task spec déjà implémentée pour masquer une erreur
- si un comportement livré doit changer, créer une nouvelle tâche ou initiative
- si une implémentation invalide des tâches futures, mettre à jour PRD, Tech Design et task specs à venir immédiatement

---

## Livraison

Ce workflow couvre cadrage, découpage, implémentation, revue et validation. Commit, PR, CI, release et déploiement restent des pratiques d'équipe ou de projet, avec `ship-readiness` comme gate optionnel avant livraison sensible.

## Crédits

A huge thanks to [@mattpocock](https://github.com/mattpocock) for sharing his workflow and agent skills; it greatly inspired this one.
