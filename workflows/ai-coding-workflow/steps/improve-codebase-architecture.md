# Improve Codebase Architecture

**Skill :** `improve-codebase-architecture`

**Statut :** On-demand step.

**Rôle :** Identifier les frictions architecturales et les opportunités de deepening qui rendent le code plus testable, local et navigable par agents.

**Quand l'utiliser :** Ball of mud, modules shallow, tests difficiles, duplication de logique, refactor structurel, absence de seam de régression après `Diagnose`, ou entretien régulier d'un codebase qui évolue vite avec agents.

**Inputs possibles :** repo, zone de code, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, tests existants, bugs récents, douleurs de maintenance.

**Actions :**

- lit le langage domaine et les décisions pertinentes
- explore organiquement les zones où la compréhension demande trop de sauts entre modules
- applique le deletion test aux modules suspects
- cherche les modules shallow, seams mal placés, adapters inutiles, tests couplés aux détails et logique dispersée
- classe les dépendances : in-process, local-substitutable, remote-owned, true external
- propose seulement les 3 à 5 candidats de deepening les plus actionnables
- classe les candidats par impact, effort, risque et confiance
- lance une discussion de design sur le candidat choisi et documente termes ou décisions durables si nécessaire

**Output :** candidats de deepening avec fichiers/modules concernés, problème, solution proposée, bénéfices en leverage/locality, impact test, risques et prochaine étape.

**Contenu de l'output :**

Contenu obligatoire :

- candidats numérotés
- problème architectural observé
- solution en prose
- bénéfices de locality et leverage
- impact, effort, risque et confiance
- stratégie de test par interface
- conflits éventuels avec décisions existantes
- recommandation de `Tech Design`, ADR ou tâche de refactor

À éviter :

- inventaire exhaustif de toutes les imperfections
- interface finale imposée avant discussion de design
- lancement d'un gros refactor sans Execution Contract

**Gate humain :** choisir le candidat à explorer, valider l'interface structurante et décider si le refactor mérite une initiative.

**Important :** Ce skill propose d'abord. Il ne doit pas lancer un gros refactor sans gate humain et sans Execution Contract.
