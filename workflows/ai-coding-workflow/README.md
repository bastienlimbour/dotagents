# Workflow AI pour le développement de projets logiciels

> [!NOTE]
> Ce workflow n'est pas fait pour le Vibe Coding. Si vous ne maîtrisez pas les fondamentaux du développement logiciel, ce workflow n'est pas fait pour vous.

Workflow AI coding léger, modulaire et humain-au-centre. Il couvre le cadrage, le découpage, l'implémentation, la review et la validation d'un projet logiciel, sans chercher à automatiser tout le cycle. Il s'appuie sur des skills spécialisés et une mémoire de travail versionnée, dans le repo ou dans un tracker.

---

## Principes

- **Cadrage-first :** cadrer avant de coder, avec un niveau de formalisation proportionné au scope.
- **Intention-driven :** activer les étapes selon le besoin, pas mécaniquement.
- **Produit / technique / exécution séparés :** `prd.md` décrit le quoi, `tech-design.md` le comment, `tasks/` l'ordre de build.
- **PRD fonctionnel, pas technique :** le PRD contient comportements, règles, edge cases et acceptance criteria, pas de détails d'implémentation.
- **Preflight proportionné :** le plan d'implémentation immédiat vit dans le `Build Preflight`, parfois en quelques lignes.
- **Une source de vérité par sujet :** éviter la double saisie concurrente entre Markdown, issues et tracker.
- **Vertical slices par défaut :** découper en tranches vérifiables, pas en couches `DB -> API -> UI`.
- **Doc utile seulement :** conserver les décisions durables et les documents utiles ; jeter les artefacts temporaires une fois consolidés.

---

## Vue d'ensemble

Le workflow distingue le flux principal et les skills transverses.

- **Core workflow :** progression normale d'une initiative vers le build.
- **On-demand skills :** skills activables hors séquence, selon contexte.

```text
Discovery : [brief] -> [validate]
Product   : prd
Technical : [tech-design]
Execution : [slice] -> build -> review -> qa -> capitalize
```

### Core workflow

| Étape | Skill | Statut | Artefact |
| ----- | ----- | ------ | -------- |
| Brief | `brief` | Optionnel | `brief.md` optionnel |
| Validate | `validate` | Optionnel | `validation.md` optionnel |
| PRD | `prd` | Requis sauf trivial | `prd.md` |
| Tech Design | `tech-design` | Si impact technique non trivial | `tech-design.md` |
| Slice | `slice` | Si multi-tâches | `tasks/*.md` |
| Build | `implement` / `implement-tdd` | Requis | Code + compte rendu |
| Review | `review` | Recommandé | Feedback |
| QA | `qa` | À la demande | `qa.md` optionnel |
| Capitalize | `capitalize` | Si décision durable ou doc à maintenir | Docs / ADRs / follow-ups |

### On-demand skills

| Skill | Rôle | Artefact |
| ----- | ---- | -------- |
| `brainstorm` | Ouvrir l'espace des options | `brainstorming.md` optionnel |
| `grill-me` | Interview décisionnelle persistante | Synthèse ou intégration dans l'étape suivante |
| `project-baseline` | Établir la baseline d'un projet existant | Docs projet mises à jour |
| `ship-readiness` | Gate optionnel avant livraison importante | Checklist ou verdict `Go / No-Go` |

### Règle mentale

```text
Brainstorm ouvre les options.
Brief converge vers une direction.
Grill Me rend les décisions explicites.
Validate réduit le risque externe.
PRD fixe ce qu'on construit.
Tech Design fixe comment on le construit.
Slice transforme PRD + Tech Design en tâches vérifiables.
Build commence par un Preflight puis implémente.
```

---

## Entrées rapides selon l'intention

| Intention | Chemin recommandé |
| --------- | ----------------- |
| Exploration d'idées | `Brainstorm -> Brief -> [Grill Me] -> [Validate]` |
| Gros projet / MVP from scratch | `[Brainstorm] -> Brief -> [Grill Me] -> [Validate] -> PRD -> Tech Design -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]` |
| Grosse feature sur projet existant | `[Brief] -> PRD -> [Grill Me] -> [Tech Design] -> Slice -> per-task(Build -> Review -> [QA]) -> [Capitalize]` |
| Feature moyenne multi-tâches | `PRD -> [Grill Me] -> [Tech Design Lite] -> Slice -> per-task(Build -> Review) -> [QA] -> [Capitalize]` |
| Petite feature | `PRD minimal -> [Grill Me] -> Build -> [Review] -> [QA]` |
| Fix / hotfix | `Build -> [Review] -> [QA]` |
| Refactoring structurel | `Tech Design -> [Grill Me] -> Slice -> per-task(Build -> Review) -> [QA] -> Capitalize` |
| Projet legacy / abandonné | `Project Baseline -> [PRD] ou [Tech Design]` |
| Livraison importante | `... -> Review -> [QA] -> Ship Readiness` |

---

## Documentation et artefacts

### Source de vérité

Le workflow est **storage-agnostic**. Une initiative a un support actif principal. Les supports secondaires pointent, commentent ou automatisent, mais ne dupliquent pas le contenu.

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

### Structure recommandée

Ici le support principal est le Markdown versionné dans le repo, mais il peut être remplacé par un tracker (Github issues, Linear, Jira, etc.)

```text
/
├─ AGENTS.md, README.md, etc.
│
├─ docs/
│  ├─ architecture.md
│  ├─ conventions.md
│  ├─ testing-strategy.md
│  ├─ decisions/
│  │  └─ 001-*.md
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

- `prd.md` : produit, comportement, règles fonctionnelles, acceptance criteria
- `tech-design.md` : architecture, décisions techniques, compromis, risques
- `tasks/*.md` : tranches exécutables et vérifiables
- `Build Preflight` : plan d'implémentation immédiat

### Execution Contract

`Build` démarre depuis un `Execution Contract` suffisant. Ce n'est pas un nouveau document : il vit dans un PRD minimal ou dans chaque task spec.

Contenu minimal :

- scope
- behavior
- acceptance criteria
- edge cases
- non-goals
- verification

---

## Étapes détaillées du core workflow

### 1. Brief

**Skill :** `brief`

**Statut :** Core optionnel.

**Rôle :** Transformer une ou plusieurs idées en direction produit claire. Le brief est une note d'opportunité légère avant d'investir dans un PRD.

**Quand l'utiliser :** Après brainstorming, nouveau produit, grosse feature, idée encore floue, besoin de cadrer l'opportunité. À sauter pour une feature claire et limitée.

**Inputs possibles :** Idée brute, notes, transcript, `brainstorming.md`, signaux utilisateurs, contexte business ou produit.

**Actions :**

- sélectionne et fait converger les idées/pistes prometteuses
- clarifie problème, cible, proposition de valeur
- décrit la solution envisagée dans les grandes lignes, sans détails techniques
- cadre le scope pressenti : MVP, V1, Later, Excluded
- explicite hypothèses, risques, contraintes, non-goals et questions ouvertes

**Output :** `brief.md` ou équivalent tracker.

**Contenu de l'output :**

- problème
- cible / utilisateurs
- proposition de valeur
- direction de solution
- cas d'usage principaux
- fonctionnalités importantes
- scope pressenti
- scope framing `MVP / V1 / Later / Excluded` si utile
- non-goals
- hypothèses
- risques
- contraintes
- questions ouvertes

**Tailles possibles :** brief léger, ou brief complet pour nouveau produit / grosse initiative.

**Gate humain :** confirmer la direction et le scope initial avant `Grill Me`, `Validate` ou `PRD`.

**Important :** Le brief converge vers une direction produit claire, mais ne remplace pas le PRD, la validation externe ou le Tech Design.

---

### 2. Validate

**Skill :** `validate`

**Statut :** Core optionnel.

**Rôle :** Réduire l'incertitude externe avant d'investir dans un PRD complet, un Tech Design ou une implémentation coûteuse.

**Quand l'utiliser :** Doute sur marché, concurrence, utilisateurs, dépendances externes, business model, faisabilité ou risque produit. À sauter si l'idée est sûre ou l'enjeu faible.

**Inputs possibles :** `brief.md`, synthèse `grill-me`, hypothèses à tester, questions ouvertes, contraintes business ou utilisateur.

**Actions :**

- recherches web approfondies et collecte de signaux externes
- analyse concurrence, alternatives, marché, utilisateurs ou business model si pertinent
- challenge les hypothèses du brief
- identifie risques, dépendances externes et contraintes majeures
- produit un verdict motivé `Go / No-Go / Pivot`

**Output :** `validation.md` ou équivalent tracker.

**Contenu de l'output :**

- hypothèses testées
- méthode et sources consultées
- analyse marché / concurrence / alternatives
- signaux utilisateurs ou business
- faisabilité
- dépendances externes
- risques et contraintes
- recommandations
- verdict `Go / No-Go / Pivot`

**Tailles possibles :** validation rapide sur quelques hypothèses, ou validation complète pour initiative stratégique.

**Gate humain :** continuer, pivoter ou abandonner.

**Important :** `Validate` teste une direction convergée. Il ne remplace ni `Brief` ni `PRD`.

---

### 3. PRD

**Skill :** `prd`

**Statut :** Core requis sauf changement trivial.

**Rôle :** Source de vérité produit et fonctionnelle. Le PRD fixe ce qu'on construit, pourquoi, pour qui, et le comportement observable attendu.

**Quand l'utiliser :** Avant toute implémentation non triviale. Niveau de détail proportionné au scope.

**Inputs possibles :** Idée claire, `brainstorming.md`, `brief.md`, `validation.md`, synthèse `grill-me`, retours utilisateurs, contraintes produit, contexte projet, doc existante.

**Actions :**

- consolide problème, objectifs, cible et valeur
- décrit solution produit et comportements attendus
- fixe scope, non-goals et success criteria
- détaille flows, règles, états, erreurs et edge cases si nécessaire
- formalise acceptance criteria et vérification fonctionnelle
- fournit un Execution Contract si single-task, ou une base pour `Slice` si multi-tâches

**Output :** `prd.md` ou équivalent tracker.

**Contenu de l'output :**

- problème et objectifs
- cible, personas ou utilisateurs concernés
- proposition de valeur
- solution côté produit
- user stories ou flows fonctionnels
- exigences fonctionnelles
- règles métier
- comportements attendus
- états UI ou états système attendus
- messages d'erreur attendus si pertinent
- edge cases fonctionnels
- scope `In Scope`
- `Out of Scope`
- `Future Candidates`
- assumptions
- acceptance criteria testables
- success criteria
- vérification fonctionnelle
- definition of done fonctionnelle si grosse initiative
- boundaries `Always do / Ask first / Never do` si utile

**Tailles possibles :** PRD minimal, PRD standard, ou PRD complet MVP.

**Gate humain :** valider scope, comportements ambigus, acceptance criteria et décisions produit importantes.

**Important :** Le PRD ne contient pas choix de stack, architecture, data model, endpoints, librairies, noms de fichiers, migrations ou détails d'implémentation.

---

### 4. Tech Design

**Skill :** `tech-design`

**Statut :** Core si impact technique non trivial.

**Rôle :** Source de vérité technique. Le Tech Design définit comment construire le produit et formalise les décisions structurantes.

**Quand l'utiliser :** Impact technique non trivial : architecture, data model, intégration, migration, sécurité, performance, scalabilité, observabilité, refactor structurel, choix de stack ou librairie durable.

**Inputs possibles :** `prd.md`, synthèse `grill-me`, contexte repo, architecture existante, docs techniques existantes, ADRs, conventions, services externes, contraintes stack, exigences non fonctionnelles.

**Actions :**

- explore le repo et les patterns existants
- collecte contraintes et exigences techniques
- propose architecture, modules et patterns
- arbitre stack, librairies, services, data model, interfaces/API, migrations et stratégie de tests
- identifie impacts sur l'existant, risques, rollback et dette éventuelle
- compare alternatives et formalise compromis
- crée ou référence des ADR si nécessaire

**Output :** `tech-design.md` ou équivalent tracker, avec ADRs si nécessaire.

**Contenu de l'output :**

- contexte technique
- contraintes et exigences non fonctionnelles
- architecture cible
- modules touchés ou créés
- intégrations et services externes
- data model
- interfaces/API
- migrations et compatibilité
- sécurité
- performance et scalabilité
- accessibilité si impact technique
- observabilité, monitoring, logs
- stratégie de testing technique
- plan de rollback si pertinent
- alternatives étudiées
- compromis retenus
- risques techniques
- questions ouvertes
- ADRs à créer ou mettre à jour

**Tailles possibles :** Tech Design Lite pour changement limité, Tech Design complet pour architecture, migration ou initiative structurante.

**Gate humain :** valider les arbitrages techniques avant `Slice` ou `Build`.

**Important :** Par défaut, Tech Design vient après PRD. Si la faisabilité technique est l'incertitude principale, faire un spike léger avant PRD, puis le Tech Design complet après PRD.

---

### 5. Slice

**Skill :** `slice`

**Statut :** Core si initiative multi-tâches.

**Rôle :** Transformer `PRD + Tech Design optionnel + contexte repo` en tâches petites, verticales et vérifiables.

**Quand l'utiliser :** Initiative multi-tâches. À sauter pour PRD minimal single-task avec Execution Contract suffisant.

**Inputs possibles :** `prd.md`, `tech-design.md`, ADRs, contexte repo, priorités produit, contraintes d'équipe.

**Actions :**

- découpe en vertical slices
- ordonne selon dépendances réelles
- garde chaque tâche auto-suffisante côté comportement
- associe tâches aux acceptance criteria correspondants
- référence le Tech Design quand utile

**Output :** une task spec par tâche dans `tasks/`, ou équivalent tracker.

**Contenu de l'output :**

- id et titre
- contexte
- objectif
- comportement attendu
- acceptance criteria testables
- edge cases utiles
- non-goals locaux si utile
- références au PRD
- références au Tech Design si utile
- vérification attendue
- dépendances `blocked-by` si applicable
- type `AFK | HITL` si utile

**Tailles possibles :** task spec minimale pour tâche simple, task spec détaillée pour tâche critique ou ambiguë.

**Gate humain :** valider granularité, verticalité, ordre, dépendances et vérifiabilité.

**Important :** Une task spec n'est pas un plan d'implémentation détaillé. Fichiers précis, commandes et séquence de code restent dans le `Build Preflight`.

---

### 6. Build

**Skills :** `implement`, `implement-tdd`

**Statut :** Core requis.

**Rôle :** Implémenter une tâche en restant dans le scope et en planifiant l'exécution avant le code.

**Quand l'utiliser :** Pour chaque task spec, ou directement depuis un PRD minimal single-task ou tout input avec un Execution Contract suffisant.

**Inputs possibles :** PRD minimal, task spec, `tech-design.md`, ADRs, contexte repo, instructions projet.

**Actions :**

- prépare un plan d'implémentation proportionné (Plan mode / Read only)
- implémente le plan en restant dans le scope
- debug si nécessaire
- exécute les vérifications nécessaires
- vérifie la conformité à l'Execution Contract

**Output :** code implémenté + compte rendu en session.

**Contenu de l'output :**

- approche retenue
- modules et fichiers créés ou impactés
- changements effectués
- tests et checks exécutés
- résultat des vérifications
- statut final
- ambiguïtés ou blocages restants

**Tailles possibles :** plan très court pour tâche évidente, plan détaillé pour tâche sensible ou HITL.

**Plan d'implémentation :** toujours présent mais adapté au scope et à la tâche. Il peut nécessiter une validation humaine (HITL) ou être auto-approuvé (AFK).

**Choix du skill :** `implement` pour intégration, UI, glue code, configuration. `implement-tdd` pour bug fix, logique métier, comportement sensible ou fort risque de régression.

**Gate humain :** validation du plan d'implémentation pour tâche `HITL`. Auto-approbation possible pour tâche `AFK` claire.

**Important :** Si l'Execution Contract est insuffisant, revenir vers `PRD`, `Tech Design`, `Slice` ou `Grill Me`.

---

### 7. Review

**Skill :** `review`

**Statut :** Core recommandé.

**Rôle :** Revue de code à froid, distincte de l'implémentation.

**Quand l'utiliser :** Toute tâche non triviale, logique complexe, changement sensible, architecture, sécurité, performance, ou besoin de regard frais.

**Inputs possibles :** diff, commits, PRD, task spec, Tech Design, tests, résultats de vérification.

**Actions :**

- compare code, PRD/task spec, Tech Design et acceptance criteria
- relit tests et vérifications
- cherche divergences, oublis, bugs, régressions
- évalue correctness, readability, architecture, security, performance
- signale dead code et simplifications évidentes

**Output :** feedback en session, ou commentaire de review dans le tracker/PR.

**Contenu de l'output :**

- verdict
- findings par sévérité
- références fichiers/lignes si possible
- écarts au PRD, task spec ou Tech Design
- couverture de tests et vérification
- risques de régression
- suggestions de correction

**Tailles possibles :** review courte pour changement simple, review complète pour changement sensible.

**Gate humain :** accepter la tâche ou la renvoyer en correction.

**Important :** `Review` évalue le code. Ce n'est pas une checklist de validation fonctionnelle manuelle.

---

### 8. QA

**Skill :** `qa`

**Statut :** Core à la demande.

**Rôle :** Produire un plan de test manuel pour valider le comportement en conditions réelles.

**Quand l'utiliser :** Après tâche conséquente, avant release importante, flow critique, impact utilisateur, ou besoin de validation manuelle explicite.

**Inputs possibles :** PRD, task specs, diff, commits, contexte du chat, initiative complète ou groupe de tâches.

**Actions :**

- produit une checklist ordonnée de tests manuels
- couvre cas nominaux, edge cases et régressions prioritaires
- propose un pas-à-pas d'exécution si utile

**Output :** checklist en session, `qa.md` optionnel ou équivalent tracker.

**Contenu de l'output :**

- périmètre testé
- prérequis
- données ou comptes nécessaires
- ordre d'exécution
- cas nominaux
- edge cases
- régressions à surveiller
- résultats observés
- anomalies relevées
- verdict manuel si applicable

**Tailles possibles :** checklist courte, ou plan QA complet pour release / flow critique.

**Gate humain :** exécuter ou superviser le test réel et statuer sur les anomalies.

**Important :** QA ne remplace pas Review.

---

### 9. Capitalize

**Skill :** `capitalize`

**Statut :** Core si décision durable ou doc à maintenir.

**Rôle :** Aligner la doc projet et la doc IA/agents avec ce qui a vraiment été construit.

**Quand l'utiliser :** Après changement durable de convention, architecture, API, comportement documenté, ADR, artefact futur ou règle agent.

**Inputs possibles :** code livré, diff, commits, PRD, task specs, Tech Design, ADRs, docs existantes.

**Actions :**

- met à jour docs obsolètes
- crée ou ajuste ADRs
- met à jour doc IA/agents si une règle doit persister
- réaligne PRD, Tech Design ou artefacts futurs invalidés
- ouvre follow-up de dette ou refactoring si nécessaire

**Output :** docs mises à jour, ADRs, règles agent, follow-ups, ou note indiquant qu'aucune capitalisation n'est utile.

**Contenu de l'output :**

- fichiers docs modifiés
- ADRs créées ou ajustées
- règles agent modifiées
- artefacts futurs réalignés
- follow-ups ouverts
- décisions devenues durables

**Tailles possibles :** note courte si rien à capitaliser, mise à jour complète si décision durable.

**Gate humain :** valider ce qui devient source de vérité durable.

**Important :** Capitalize ne documente pas pour le plaisir ; il maintient ce qui doit rester utile et vrai.

---

## Détail des on-demand skills

Ces skills sont hors core workflow. Ils s'invoquent quand le contexte l'exige.

### Brainstorm

**Skill :** `brainstorm`

**Statut :** On-demand skill.

**Rôle :** Ouvrir largement l'espace d'idées, générer des options, structurer les pistes sans converger.

**Quand l'utiliser :** Idée floue, nouveau produit, nouvelle direction, feature majeure, exploration produit/technique, manque d'options.

**Inputs possibles :** Objectif du brainstorming, intuition, notes, transcript vocal, idées existantes, directions à explorer, données, code ou doc projet.

**Actions :**

- pose des questions ouvertes sans relâche pour stimuler la réflexion et générer des pistes
- explore problèmes, opportunités, personas, solutions, proposition de valeur, cas d'usage, fonctionnalités, hypothèses, contraintes, risques
- structure les idées au fil du brainstorming
- continue jusqu'à demande d'arrêt explicite

**Output :** `brainstorming.md` ou équivalent tracker.

**Contenu de l'output :**

- contexte / objectif du brainstorming
- synthèse par thèmes
- problèmes et opportunités
- utilisateurs/personas possibles
- propositions de valeur
- solutions et variantes
- cas d'usage
- fonctionnalités candidates
- hypothèses
- contraintes et risques
- questions ouvertes

**Tailles possibles :** micro-brainstorm ciblé, ou brainstorm complet 30 à 120 minutes.

**Gate humain :** choisir les pistes à filtrer dans `Brief`, `PRD`, `Tech Design` ou une décision explicite.

**Important :** `Brainstorm` diverge volontairement. Il ne tranche pas.

---

### Grill Me

**Skill :** `grill-me`

**Statut :** On-demand skill.

**Rôle :** Interviewer l'utilisateur, une question à la fois, jusqu'à compréhension partagée et résolution des branches importantes de l'arbre de décision.

**Quand l'utiliser :** Idée claire mais décisions implicites, plan/design à challenger, dépendances entre décisions, Execution Contract ambigu, demande explicite de "grill me".

**Inputs possibles :** brief, PRD, Tech Design, task spec, plan, intention, contexte repo.

**Actions :**

- pose des questions une par une
- propose une recommandation à chaque question
- explore le repo au lieu de demander si la réponse est trouvable
- résout les dépendances dans le bon ordre
- arrête quand les décisions importantes sont résolues ou laissées ouvertes explicitement, ou quand l'utilisateur demande de stopper

**Output :** synthèse en session, ou intégration dans `brief.md`, `prd.md`, `tech-design.md` ou task specs.

**Contenu de l'output :**

- décisions clarifiées
- recommandations retenues
- questions résolues
- branches laissées ouvertes
- hypothèses à intégrer dans l'étape suivante
- ambiguïtés restantes

**Tailles possibles :** micro-interview sur une décision, ou interview complète sur une intention.

**Gate humain :** répondre aux questions et valider les décisions retenues.

**Important :** Utiliser `Grill Me` en général une seule fois par intention, au point d'ambiguïté le plus utile :

- après `Brief` : clarifier la direction avant validation ou PRD
- après `PRD` : challenger scope, comportements et acceptance criteria
- après `Tech Design` : challenger les arbitrages techniques
- avant `Build` : seulement si l'Execution Contract est ambigu

---

### Project Baseline

**Skill :** `project-baseline`

**Statut :** On-demand skill.

**Rôle :** Établir une base fiable du projet existant : doc produit, doc projet, architecture, conventions, stratégie de testing, zones à risque.

**Quand l'utiliser :** Onboarding legacy, projet abandonné, codebase peu documentée, reprise d'un projet existant.

**Inputs possibles :** repo existant, docs existantes, README, scripts, tests, architecture, tickets, contexte utilisateur.

**Actions :**

- explore le repo et la doc existante
- identifie architecture, conventions et stratégie de testing réelles
- repère zones à risque et incohérences
- met à jour la documentation durable utile

**Output :** mises à jour directes dans la doc projet.

**Contenu de l'output :**

- architecture actuelle
- conventions observées
- stratégie de testing réelle
- zones à risque
- incohérences
- fichiers docs mis à jour

**Tailles possibles :** baseline rapide pour onboarding, baseline complète pour repo legacy.

**Gate humain :** valider ce qui devient source de vérité projet.

**Important :** Ne produit pas forcément un artefact isolé type `current-state.md`. Il met à jour la documentation durable du projet.

---

### Ship Readiness

**Skill :** `ship-readiness`

**Statut :** On-demand skill, gate optionnel de livraison.

**Rôle :** Vérifier qu'un changement est prêt à être livré dans de bonnes conditions.

**Quand l'utiliser :** Release sensible, flow critique, changement utilisateur ou infra, migration, risque sécurité/performance.

**Inputs possibles :** diff, commits, PRD, task specs, QA, review, CI, logs, contexte release.

**Actions :**

- vérifie qualité, sécurité, performance et accessibilité si pertinent
- vérifie migrations, variables d'env, monitoring et rollback plan
- identifie blockers, risques acceptés et recommandations avant livraison

**Output :** verdict `Go / No-Go`, checklist de pré-livraison, ou équivalent tracker.

**Contenu de l'output :**

- blockers
- risques acceptés
- checks qualité
- checks sécurité
- performance
- accessibilité si pertinent
- migrations et variables d'env
- monitoring / alerting
- rollback plan
- recommandations avant livraison

**Tailles possibles :** checklist courte, ou gate complet de release.

**Gate humain :** accepter les risques ou bloquer la livraison.

**Important :** Ce n'est pas une étape normale de toutes les initiatives.

---

## Règles transverses

### Product / Technical / Execution boundaries

- PRD : comportement observable, règles fonctionnelles, acceptance criteria.
- Tech Design : décisions techniques, interfaces, data model, migrations, risques.
- Task specs : tranches exécutables avec Execution Contract.
- Build Preflight : plan immédiat d'implémentation.

### Vertical slices

- Construire une tranche complète et vérifiable.
- Éviter les tâches horizontales par couche.

### Source-driven decisions

- Vérifier la doc officielle quand une décision dépend d'un framework ou d'une lib.
- Signaler tout conflit entre doc officielle et patterns du repo avant de trancher.

### Context engineering

- Charger le contexte utile, pas tout le repo.
- Garder artefacts, fichiers et patterns pertinents pour la tâche.

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
