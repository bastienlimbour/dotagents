# 005 - Slice

**Skill :** `slice`

**Statut :** Core si initiative multi-tâches.

**Rôle :** Transformer `PRD + Tech Design optionnel + contexte repo` en tâches petites, verticales et vérifiables.

**Quand l'utiliser :** Initiative multi-tâches. À sauter pour PRD minimal single-task avec Execution Contract suffisant.

**Inputs possibles :** `prd.md`, `tech-design.md`, ADRs, contexte repo, priorités produit, contraintes d'équipe.

**Actions :**

- découpe en vertical slices
- ordonne selon dépendances réelles, comme un graphe plutôt qu'un plan linéaire
- garde chaque tâche auto-suffisante côté comportement
- rend chaque tâche independently grabbable par un agent
- évite de recopier le PRD ou le Tech Design dans chaque tâche
- classe chaque tâche en `AFK` ou `HITL` quand cela aide l'exécution
- associe tâches aux acceptance criteria correspondants
- référence le PRD et le Tech Design par liens courts quand utile
- présente le découpage à l'humain avant publication : granularité, dépendances, merge/split, classification `AFK | HITL`
- si le support actif est un issue tracker, publie les tâches dans l'ordre des dépendances selon les conventions du projet

**Output :** une task spec par tâche dans `tasks/`, ou équivalent tracker.

**Contenu de l'output :**

Contenu obligatoire :

- id et titre
- contexte court
- objectif
- comportement end-to-end à construire
- acceptance criteria testables
- vérification attendue

Contenu conditionnel :

- parent si issu d'un PRD ou d'une issue parente
- edge cases utiles
- non-goals locaux si utile
- références au PRD
- références au Tech Design si utile
- commandes de feedback attendues si connues
- dépendances `blocked-by` si applicable
- type `AFK | HITL` si utile
- touchpoints probables, sans imposer un plan de code

À éviter :

- copie du PRD ou du Tech Design
- plan d'implémentation détaillé
- tâches horizontales par couche technique

**Tailles possibles :** task spec minimale pour tâche simple, task spec détaillée pour tâche critique ou ambiguë.

**Gate humain :** valider granularité, verticalité, ordre, dépendances, vérifiabilité et classification `AFK | HITL`.

**Important :** Une task spec n'est pas un plan d'implémentation détaillé. Fichiers précis, commandes et séquence de code restent dans le `Build Preflight`. Une tâche bloquée ne doit pas être prise en AFK.

Ne pas fermer, réécrire ou modifier implicitement l'issue parente lors de la création des slices.
