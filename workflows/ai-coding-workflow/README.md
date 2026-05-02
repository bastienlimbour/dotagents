# Workflow AI pour le développement de projets logiciels

Workflow AI coding léger, modulaire et humain-au-centre. Il couvre le cadrage, le découpage, l'implémentation, la review et la validation d'un projet logiciel, sans chercher à automatiser tout le cycle. Il s'appuie sur des agent skills spécialisés et une mémoire de travail flexible.

> [!NOTE]
> Ce workflow n'est pas prévu pour faire du Vibe Coding. Vous devez maîtriser les fondamentaux du développement logiciel et l'architecture de vos projets pour l'utiliser efficacement.

---

## Glossaire

- **Initiative :** unité de travail suivie dans le workflow : ajouter une feature, refactor un module, corriger un bug, développer un MVP, reprendre un projet abandonné, planifier une livraison sensible, etc.
- **Step :** étape du workflow avec un rôle, des inputs, des outputs et parfois un gate humain. Chaque step est liée à un ou plusieurs skills.
- **Core workflow :** chemin principal que suit une initiative du brief jusqu'à la livraison.
- **On-demand step :** step activable hors séquence quand le contexte le justifie.
- **Skill (Agent skill) :** ressource réutilisable, basée sur le système de fichiers, qui fournit à des agents IA des connaissances spécifiques à un domaine : workflows, contexte, best practices, capacités. Voir [agentskills.io](https://agentskills.io/) pour plus de détails.
- **Artefact :** document, issue ou commentaire temporaire utile pendant l'initiative, comme PRD, Tech Design, task specs, QA ou prototype.
- **Documentation durable :** information qui doit rester vraie après l'initiative : code, tests, README, docs projet, conventions, `CONTEXT.md`, `CONTEXT-MAP.md` ou ADRs.
- **CONTEXT.md :** glossaire domaine durable : termes, définitions, synonymes à éviter et ambiguïtés résolues.
- **CONTEXT-MAP.md :** carte des bounded contexts quand un projet contient plusieurs domaines métier.
- **ADR :** Architecture Decision Record. Décision durable, difficile à renverser ou surprenante sans contexte.
- **PRD :** source de vérité produit et fonctionnelle : comportement attendu, règles, edge cases et acceptance criteria.
- **Tech Design :** source de vérité technique : architecture, interfaces, data model, migrations, risques et compromis.
- **Task spec :** tranche exécutable et vérifiable issue du slicing.
- **Execution Contract :** contenu minimal permettant à `Build` d'implémenter sans ambiguïté. Il vit dans un PRD minimal, une task spec, une issue ou un prompt.
- **Build Preflight :** plan d'implémentation immédiat produit au début de `Build` avant d'écrire le code.
- **AFK / HITL :** `AFK` désigne une tâche claire, testable et non bloquée ; `HITL` désigne une tâche qui nécessite un jugement humain.
- **Gate humain :** point de décision où l'humain valide, arbitre ou bloque la suite.
- **Vertical slice :** tranche end-to-end vérifiable, plutôt qu'un découpage horizontal par couches `DB -> API -> UI`.
- **Feedback loop :** signal fiable qui prouve l'état du changement : test, typecheck, lint, build, CI, repro de bug, dev server ou vérification navigateur.
- **Seam / adapter :** frontière où isoler une dépendance ou une variation réelle, surtout pour tester, remplacer ou intégrer un système externe.
- **MCP :** Model Context Protocol. Serveur utilisé par un agent pour accéder à un outil ou une source externe de façon structurée.

---

## Principes

- **Cadrer avant de coder :** formaliser juste assez selon le scope et le niveau d'incertitude.
- **Séparer produit, technique et exécution :** `prd.md`, `tech-design.md` et `tasks/*.md` n'ont pas le même rôle.
- **Construire par vertical slices vérifiables :** chaque tâche doit produire un signal utile de bout en bout.
- **Garder l'humain sur le jugement :** produit, UX, architecture, sécurité sensible, review, QA et validation finale restent `HITL` quand l'enjeu est réel.
- **S'appuyer sur des feedback loops fiables :** tests, typecheck, lint, build, CI ou repro déterminent le plafond de qualité atteignable.
- **Capitaliser seulement ce qui dure :** les artefacts temporaires ne doivent pas devenir une fausse source de vérité.

---

## Vue d'ensemble

Le workflow est intention-driven : on utilise les steps selon le besoin, pas mécaniquement. Le flux nominal ressemble à ceci :

```text
Discovery : [brainstorm] -> [brief] -> [grill-me | grill-with-docs] -> [validate]
Product   : prd
Technical : [tech-design]
Execution : [slice] -> build/tdd -> review -> qa -> capitalize
```

Les crochets indiquent des steps optionnelles ou contextuelles. Le détail opérationnel de chaque step vit dans `steps/` ; ce README sert surtout à comprendre le workflow, choisir un chemin et savoir où placer l'information.

Les core workflow steps progressent du cadrage vers l'exécution. Les on-demand steps sont contextuelles : ouvrir des options, réduire une ambiguïté, comprendre une zone de code, diagnostiquer un bug, prototyper une UI ou vérifier une livraison.

---

## Choisir son chemin

### Exploration et cadrage

- **Exploration d'idées :** `Brainstorm -> Brief -> [Grill Me] -> [Validate]`.
- **Gros projet ou MVP from scratch :** `[Brainstorm] -> Brief -> [Grill Me] -> [Validate] -> PRD -> Tech Design -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]`.
- **UI incertaine :** `[Prototype UI] -> Brief ou PRD -> Build propre -> [Review] -> [QA]`.

### Feature et build

- **Grosse feature sur projet existant :** `[Brief] -> [Grill Me ou Grill With Docs] -> PRD -> [Tech Design] -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]`.
- **Feature moyenne multi-tâches :** `[Grill Me ou Grill With Docs] -> PRD -> [Tech Design Lite] -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]`.
- **Petite feature :** `PRD minimal -> [Grill Me si ambigu] -> Build -> [Review] -> [QA]`.
- **Fix ou hotfix simple :** `Build -> [Review] -> [QA]`.

### Investigation, refactor et reprise

- **Bug complexe :** `Diagnose -> Build ou TDD -> Review -> [QA]`.
- **Zone de code inconnue :** `Zoom Out`.
- **Refactoring structurel :** `Zoom Out -> Improve Codebase Architecture -> [Grill With Docs] -> Tech Design -> Slice -> per-task(Build -> Review) -> [QA] -> Capitalize`.
- **Projet legacy ou abandonné :** `Project Baseline -> [PRD] ou [Tech Design]`.
- **Livraison importante :** `... -> Review -> [QA] -> Ship Readiness`.

---

## Liste des steps

Les définitions détaillées vivent dans `steps/`. Voici un résumé des steps et leurs rôles :

### Core workflow

- **[Brief](steps/001-brief.md)** - `brief` - optionnel. Transforme une idée en direction produit claire. Artefact : `brief.md` ou équivalent tracker.
- **[Validate](steps/002-validate.md)** - `validate` - optionnel. Réduit l'incertitude externe avant d'investir davantage. Artefact : `validation.md` ou équivalent tracker.
- **[PRD](steps/003-prd.md)** - `prd` - requis sauf changement trivial. Fixe le comportement produit attendu. Artefact : `prd.md` ou équivalent tracker.
- **[Tech Design](steps/004-tech-design.md)** - `tech-design` - requis si impact technique non trivial. Formalise architecture, interfaces et compromis. Artefact : `tech-design.md` et ADRs si nécessaire.
- **[Slice](steps/005-slice.md)** - `slice` - requis si initiative multi-tâches. Découpe en tasks verticales, vérifiables et ordonnées par dépendances. Artefact : `tasks/*.md` ou équivalent tracker.
- **[Build](steps/006-build.md)** - `implement` ou `implement-tdd` - requis. Implémente une tâche depuis un Execution Contract suffisant. Artefact : code + compte rendu en session.
- **[Review](steps/007-review.md)** - `review` - recommandé. Revue de code à froid centrée sur bugs, risques et écarts au contrat. Artefact : feedback en session ou commentaire de review.
- **[QA](steps/008-qa.md)** - `qa` - à la demande. Produit un plan de test manuel et peut consigner les résultats observés. Artefact : checklist ou `qa.md` optionnel.
- **[Capitalize](steps/009-capitalize.md)** - `capitalize` - si décision durable ou doc à maintenir. Met à jour la doc durable et nettoie les artefacts temporaires. Artefact : docs, ADRs, follow-ups ou note de non-capitalisation.

### On-demand steps

- **[Brainstorm](steps/brainstorm.md)** - `brainstorm`. Ouvre l'espace des options sans converger trop tôt. Artefact : `brainstorming.md` optionnel.
- **[Grill Me](steps/grill-me.md)** - `grill-me`. Interview décisionnelle une question à la fois. Artefact : decision log court ou intégration dans l'étape suivante.
- **[Grill With Docs](steps/grill-with-docs.md)** - `grill-with-docs`. Aligne l'intention avec langage domaine, docs, ADRs et code existant. Artefact : décisions clarifiées, vocabulaire durable ou ADRs si nécessaire.
- **[Prototype UI](steps/prototype-ui.md)** - `prototype-ui`. Explore des directions frontend jetables avant intégration propre. Artefact : prototypes isolés + synthèse.
- **[Diagnose](steps/diagnose.md)** - `diagnose`. Isole la cause racine d'un bug complexe avant correction. Artefact : cause racine, fix, test de régression et vérifications.
- **[Zoom Out](steps/zoom-out.md)** - `zoom-out`. Cartographie une zone de code inconnue avant modification. Artefact : carte synthétique modules, callers, seams et risques.
- **[Improve Codebase Architecture](steps/improve-codebase-architecture.md)** - `improve-codebase-architecture`. Identifie des opportunités de deepening et de refactor structurant. Artefact : candidats de refactor priorisés.
- **[Project Baseline](steps/project-baseline.md)** - `project-baseline`. Établit la baseline d'un projet existant. Artefact : docs projet mises à jour.
- **[Ship Readiness](steps/ship-readiness.md)** - `ship-readiness`. Gate optionnel avant livraison sensible. Artefact : checklist ou verdict `Go / No-Go`.

---

## Mémoire du workflow

### Documentation durable

La documentation durable est la mémoire du projet à long terme. Elle est versionnée dans le repository.

Exemples :

- `docs/*` : documentation projet, architecture, conventions, testing strategy, etc.
- `docs/decisions/*` : décisions durables (ADRs) dont le contexte est utile à long terme.
- `CONTEXT.md` (optionnel) : vocabulaire domaine durable et termes partagés.
- `CONTEXT-MAP.md` (optionnel) : carte des bounded contexts si le projet en a plusieurs.
- `AGENTS.md` (optionnel) : règles et instructions pour les agents IA.
- `README.md` (optionnel) : porte d'entrée et guide de référence du projet (utilité, installation, mode d'emploi pour les utilisateurs, les contributeurs et les agents IA).

Ne pas créer un fichier durable avant d'avoir une information réelle à y stocker.

### Artefacts

Les artefacts sont des supports temporaires liés à une initiative, générés par l'agent IA durant le workflow.

Exemples : brainstorming, brief, validation, PRD, Tech Design, task specs, QA, prototypes.

La stratégie par défaut est **GitHub Issues + sub-issues**, ou un tracker équivalent capable de représenter une initiative parente, des tâches enfants et des liens. Markdown local reste tout à fait acceptable, surtout en solo ou local-first, si le cycle de vie est respecté.

Avant PRD, les artefacts très exploratoires comme brainstorming, brief ou notes de validation peuvent rester en local ou dans le chat. À partir du PRD, le support principal doit être explicite : issue parente, tracker équivalent ou dossier Markdown local.

#### Support principal des artefacts

Une initiative doit avoir un support actif principal. Les supports secondaires peuvent pointer, commenter ou automatiser, mais ne doivent pas dupliquer le contenu principal.

Recommandation pratique :

- par défaut : GitHub Issues ou tracker équivalent
- travail collaboratif ou multi-agent : GitHub Issues ou tracker équivalent
- travail solo ou local-first : Markdown local gitignored dans `.initiatives/<initiative>/`

Si le support est externe au repo, l'agent doit y accéder via CLI officielle ou serveur MCP.

#### Mode GitHub Issues

Créer l'issue parente au moment du PRD. Le brainstorming, le brief et les notes de validation restent locaux ou dans le chat tant qu'ils ne sont pas consolidés. Seuls les éléments utiles à l'exécution ou à la décision sont intégrés dans l'issue parente.

Issue parente :

- source de vérité active de l'initiative
- créée quand le PRD est prêt à devenir support de travail
- body canonique maintenu à jour
- liens vers sub-issues, commentaires importants, docs durables et ADRs

Body canonique recommandé :

- contexte court issu du brief ou de la validation, sans transcript brut
- PRD courant : scope, behavior, edge cases, acceptance criteria, non-goals
- Tech Design summary si impact technique non trivial
- liens vers commentaire Tech Design détaillé si nécessaire
- liens vers sub-issues de vertical slices
- statut, questions ouvertes bloquantes et décisions acceptées

Commentaires recommandés :

- decision log et arbitrages datés
- validation summary si elle justifie `Go / No-Go / Pivot`
- Tech Design détaillé quand il serait trop long pour le body
- QA plan ou rapport QA
- changement de scope ou clarification importante

Règle de consolidation : un commentaire peut garder l'historique, mais il ne doit pas devenir une source de vérité concurrente. Si une décision en commentaire change la vérité courante, la consolider dans le body, une sub-issue, une doc durable ou un ADR.

Sub-issues :

- une sub-issue par vertical slice
- chaque sub-issue contient son propre Execution Contract
- chaque sub-issue pointe vers l'issue parente
- ne pas recopier tout le PRD ou tout le Tech Design dans chaque sub-issue
- fermer ou mettre à jour les sub-issues quand le scope parent change

Mapping recommandé :

- brainstorming : local/chat, jamais copié brut
- brief : local/chat, résumé utile intégré au PRD
- validation : local/chat ou commentaire si elle justifie une décision
- PRD : body de l'issue parente
- Tech Design lite : section courte dans le body
- Tech Design non trivial : résumé dans le body + commentaire détaillé lié depuis le body
- tasks : sub-issues, une par vertical slice
- QA : commentaire sur l'issue parente ou sur la sub-issue concernée
- capitalization : docs durables, ADRs, cleanup local et fermeture de l'initiative

#### Mode Markdown local

Markdown local est acceptable si le support principal n'est pas un tracker. Le chemin recommandé est `.initiatives/<initiative>/`, gitignored par défaut.

Les artefacts locaux ne sont pas versionnés par défaut. Les décisions ou informations utiles à long terme sont consolidées dans la documentation durable.

#### Cycle de vie des artefacts

À la clôture d'une initiative, les artefacts associés doivent être supprimés, archivés, fermés ou consolidés dans une documentation durable. Un vieux PRD ne doit pas redevenir source de vérité implicite pour un agent.

Règles d'évolution :

- si contraintes, scope ou tâches changent sans pivot majeur : modifier l'initiative active.
- si le travail devient indépendant, s'il y a pivot majeur, ou si l'initiative précédente est historique : ouvrir une nouvelle initiative.
- ne pas réécrire l'histoire d'une initiative terminée
- ne pas modifier rétroactivement une task spec déjà implémentée pour masquer une erreur
- si un comportement livré doit changer, créer une nouvelle tâche ou initiative
- si une implémentation invalide des tâches futures, mettre à jour PRD, Tech Design et task specs à venir immédiatement

#### Structure Markdown recommandée

Si le support principal est le Markdown local, cette structure sépare la documentation durable et les artefacts temporaires groupés par initiative. Le dossier `.initiatives/` est gitignored par défaut.

```text
/
├─ README.md
├─ AGENTS.md
├─ CONTEXT.md                    (glossaire domaine durable, optionnel)
├─ CONTEXT-MAP.md                (si plusieurs bounded contexts, optionnel)
├─ .agents/                      (configuration agent optionnelle)
│  ├─ issue-tracker.md
│  └─ domain.md
├─ .initiatives/                 (gitignored par défaut)
│  ├─ 001-<initiative>/
│  │  ├─ brainstorming.md     (optionnel)
│  │  ├─ brief.md             (optionnel)
│  │  ├─ validation.md        (optionnel)
│  │  ├─ prd.md
│  │  ├─ tech-design.md       (optionnel)
│  │  ├─ qa.md                (optionnel)
│  │  └─ tasks/
│  │     ├─ 001-<task>.md
│  │     └─ ...
│  └─ 002-<initiative>/
│     └─ prd.md
├─ docs/
│  ├─ architecture.md
│  ├─ conventions.md
│  ├─ testing-strategy.md
│  └─ decisions/
│     └─ 001-*.md                (ADRs / décisions durables)
└─ apps/, packages/, scripts/, ...
```

Règles de nommage :

- un dossier par initiative, en kebab-case, préfixé par `001-`, `002-`, etc.
- `tasks/` n'existe que si l'initiative a plusieurs tâches
- un fichier par tâche, en kebab-case, préfixé par `001-`, `002-`, etc.

#### Initiative Index (optionnel)

Un index est utile mais optionnel. Si les artefacts vivent en Markdown local, l'emplacement recommandé est `.initiatives/index.md`. Pour une vue durable ou collaborative, préférer GitHub Projects, Linear, Jira ou `docs/product/initiatives.md`. Sur un petit projet, l'index peut ne pas exister.

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

#### Execution Contract

L'Execution Contract n'est pas un nouveau document : c'est le contenu minimal qu'un agent doit avoir à sa disposition pour implémenter une tâche. Il peut vivre dans un prompt, un PRD, une task spec, une issue ou tout autre support.

L'étape `Build` ne doit démarrer que si un `Execution Contract` suffisant est disponible.

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

#### Format des outputs

Les listes de contenu des outputs de chaque step ou skill ne sont pas des checklists exhaustives. Chaque skill doit produire le plus petit artefact utile pour la décision, l'exécution ou la validation.

Règles :

- choisir le niveau `lite / standard / full` avant de rédiger
- inclure seulement les sections qui changent une décision, lèvent une ambiguïté ou servent directement l'exécution
- distinguer contenu obligatoire, contenu conditionnel et contenu à éviter quand l'output peut grossir
- omettre les sections sans signal réel
- éviter transcript brut, logs longs, inventaire exhaustif de fichiers, copier-coller de l'étape précédente, etc.
- finir par les décisions prises et les questions ouvertes bloquantes

### Configuration agent (optionnel)

Sur un projet multi-agent ou piloté par issues, une configuration peut être utile pour éviter les ambiguïtés. Elle est versionnée et vit généralement dans le repo dans un dossier `.agents/`.

Emplacements recommandés :

- `.agents/issue-tracker.md` : indique où lire et publier les PRDs, les task specs, etc.
- `.agents/domain.md` : indique comment lire la documentation durable, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, etc.
- `AGENTS.md` ou `CLAUDE.md` : pointe vers les fichiers de configuration ci-dessus

Si ces docs n'existent pas, les skills ou agents consommateurs continuent silencieusement. Ils ne doivent pas proposer de les créer upfront. Seul un besoin réel de configuration durable justifie leur création.

---

## Règles globales

### Feedback loops et stop-the-line

- Sans feedback fiable, l'agent code à l'aveugle.
- Documenter les commandes réelles du projet dans `README.md`, `AGENTS.md`, `docs/testing-strategy.md` ou équivalent.
- Feedback minimal utile : typecheck, tests automatisés, lint, formatage, build et CI rapide.
- Feedback avancé : dev server accessible, vérification navigateur, tests e2e ciblés, migrations vérifiables, seeds reproductibles.
- Si test, build, CI ou runtime casse, traiter le problème ou documenter le blocage avant d'élargir le scope.
- Pour un bug, le feedback loop est le produit principal du diagnostic : sans signal pass/fail fiable, ne pas élargir les hypothèses.

### Context engineering

- Charger le contexte utile, pas tout le repo.
- Garder artefacts, fichiers et patterns pertinents pour la tâche.
- Utiliser `Zoom Out` avant de modifier une zone inconnue ou difficile à situer.
- Préférer `/clear` plutôt que `/compact` entre grandes étapes ou avant review.
- Utiliser PRD, tasks, issues, docs et tests comme mémoire externe plutôt que l'historique complet du chat.
- Garder le system prompt et les instructions poussées aussi courts que possible.
- Si `CONTEXT.md`, `CONTEXT-MAP.md` ou `docs/decisions/` n'existent pas, continuer silencieusement et ne les créer que lorsqu'une décision ou un terme réel est stabilisé.

### Source-driven decisions

- Vérifier la doc officielle quand une décision dépend d'un framework ou d'une lib.
- Signaler tout conflit entre doc officielle et patterns du repo avant de trancher.
- Utiliser le vocabulaire de `CONTEXT.md` dans les titres d'issues, PRDs, tests, hypothèses et plans.
- Si un terme nécessaire manque ou contredit l'usage du code, c'est un signal pour `Grill With Docs`.
- Signaler explicitement tout conflit avec une décision durable au lieu de l'écraser silencieusement.

---

## Livraison

Ce workflow couvre cadrage, découpage, implémentation, revue et validation. La partie commit, PR, CI, release et déploiement reste une responsabilité d'équipe ou de projet, avec `ship-readiness` comme gate optionnel avant livraison sensible.

## Crédits

A huge thanks to [@mattpocock](https://github.com/mattpocock) for sharing his workflow and agent skills; it greatly inspired this one.
