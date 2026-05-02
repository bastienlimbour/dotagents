# Project Baseline

**Skill :** `project-baseline`

**Statut :** On-demand step.

**Rôle :** Établir une base fiable du projet existant : doc produit, doc projet, architecture, conventions, stratégie de testing, zones à risque.

**Quand l'utiliser :** Onboarding legacy, projet abandonné, codebase peu documentée, reprise d'un projet existant.

**Inputs possibles :** repo existant, docs existantes, README, scripts, tests, architecture, tickets, contexte utilisateur.

**Actions :**

- borne le scope de baseline avant exploration
- explore le repo et la doc existante
- identifie architecture, conventions et stratégie de testing réelles
- repère zones à risque et incohérences
- met à jour la documentation durable utile plutôt que créer un méga-document

**Output :** mises à jour directes dans la doc projet.

**Publication de l'artefact :** `Project Baseline` met à jour la documentation durable plutôt que créer un artefact temporaire. Proposer explicitement les fichiers durables à modifier avant édition. Si une issue ou tracker d'onboarding existe, proposer un commentaire de synthèse avec les docs mises à jour et les follow-ups.

**Contenu de l'output :**

Contenu obligatoire :

- fichiers docs mis à jour
- architecture actuelle
- conventions observées
- stratégie de testing réelle
- zones à risque
- incohérences

Contenu conditionnel :

- sources inspectées
- zones inconnues ou non couvertes
- follow-ups proposés

À éviter :

- artefact isolé type `current-state.md` sans usage durable
- arbre de fichiers exhaustif
- création de docs durables sans information réelle à maintenir

**Tailles possibles :** baseline rapide pour onboarding, baseline complète pour repo legacy.

**Gate humain :** valider ce qui devient source de vérité projet.

**Important :** Ne produit pas forcément un artefact isolé type `current-state.md`. Il met à jour la documentation durable du projet.
