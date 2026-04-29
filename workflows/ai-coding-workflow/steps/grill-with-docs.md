# Grill With Docs

**Skill :** `grill-with-docs`

**Statut :** On-demand step.

**Rôle :** Challenger une intention ou un plan contre le langage domaine, les docs durables, les ADRs et le code existant.

**Quand l'utiliser :** Projet existant, vocabulaire métier ambigu, plan touchant plusieurs modules, refactor structurel, besoin d'aligner produit et codebase avant `PRD` ou `Tech Design`.

**Inputs possibles :** intention, `brief.md`, synthèse `grill-me`, draft PRD, draft Tech Design, `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/decisions/`, architecture existante, code pertinent.

**Actions :**

- inspecte `CONTEXT.md`, `CONTEXT-MAP.md`, ADRs, docs projet et code pertinent
- limite l'analyse aux sources utiles pour l'intention donnée
- distingue faits observés, recommandations et décisions à valider
- challenge immédiatement les termes flous, surchargés ou incohérents
- pose des questions une par une quand le code ou les docs ne suffisent pas
- propose une recommandation à chaque question
- résout les conflits entre vocabulaire du plan, vocabulaire du code et décisions existantes
- met à jour inline le vocabulaire durable quand un terme est stabilisé, ou propose explicitement la mise à jour si elle nécessite validation
- crée `CONTEXT.md`, `CONTEXT-MAP.md` ou `docs/decisions/` seulement au premier besoin réel
- propose un ADR seulement pour une décision difficile à renverser, surprenante sans contexte, et issue d'un vrai compromis

**Output :** synthèse en session, mises à jour de `CONTEXT.md` ou `CONTEXT-MAP.md`, ADRs proposées ou créées, intégration dans `PRD` ou `Tech Design`.

**Contenu de l'output :**

Contenu obligatoire :

- décisions clarifiées
- termes domaine retenus
- conflits de vocabulaire résolus
- ambiguïtés restantes

Contenu conditionnel :

- sources code/docs citées quand elles justifient une décision
- docs durables mises à jour ou à mettre à jour
- ADRs proposées si nécessaire

À éviter :

- carte exhaustive du codebase
- création de docs durables sans terme ou décision stabilisée
- ADR proposé sans vrai compromis durable

**Tailles possibles :** micro-alignement sur un terme ou une interface, ou session complète avant PRD sur projet existant.

**Gate humain :** valider les termes, décisions durables et ADRs avant qu'ils deviennent source de vérité.

**Important :** `grill-with-docs` ne remplace pas `Review`. Il aligne le langage et les décisions avant construction. C'est le successeur de l'ancien skill `domain-model`.
