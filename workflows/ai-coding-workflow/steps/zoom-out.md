# Zoom Out

**Skill :** `zoom-out`

**Statut :** On-demand step.

**Rôle :** Monter d'un niveau d'abstraction pour comprendre comment une zone de code s'insère dans le système avant de l'éditer.

**Quand l'utiliser :** Zone de code inconnue, stack trace traversant plusieurs modules, refactor imminent, onboarding sur un domaine, doute sur les callers ou les seams.

**Inputs possibles :** fichier, dossier, symbole, stack trace, issue, PRD, task spec, intention de modification, `CONTEXT.md`, décisions durables.

**Actions :**

- limite la carte à l'intention ou à la zone demandée
- lit le vocabulaire domaine et les décisions pertinentes si disponibles
- cartographie modules, callers, flux de données, seams et adapters pertinents
- explique les responsabilités en langage domaine plutôt qu'en noms de fichiers uniquement
- signale les zones de couplage, d'ambiguïté ou de risque
- indique le niveau de confiance et les inconnues restantes si nécessaire
- recommande la prochaine étape : `Build`, `Grill With Docs`, `Tech Design`, `Diagnose` ou `Improve Codebase Architecture`

**Output :** carte synthétique de la zone, modules et callers pertinents, seams à respecter, risques et prochaine étape recommandée.

**Contenu de l'output :**

Contenu obligatoire :

- zone étudiée
- responsabilités principales en langage domaine
- callers, callees ou flux pertinents
- seams, adapters ou interfaces à respecter
- risques, zones de couplage ou ambiguïtés
- prochaine étape recommandée

Contenu conditionnel :

- termes domaine ou décisions durables applicables
- dépendances externes ou ownership connu
- niveau de confiance et inconnues restantes

À éviter :

- carte complète du repo sans lien avec l'intention
- plan d'implémentation détaillé
- refactor proposé sans gate humain

**Gate humain :** confirmer que la carte correspond à l'intention avant une modification sensible.

**Important :** `Zoom Out` n'implémente pas. Il réduit le risque de modifier une zone sans comprendre son contexte système.
