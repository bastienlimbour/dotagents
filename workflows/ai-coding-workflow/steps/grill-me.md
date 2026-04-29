# Grill Me

**Skill :** `grill-me`

**Statut :** On-demand step.

**Rôle :** Interviewer l'utilisateur, une question à la fois, jusqu'à compréhension partagée et résolution des branches importantes de l'arbre de décision.

**Quand l'utiliser :** Idée claire mais décisions implicites, plan/design à challenger, dépendances entre décisions, Execution Contract ambigu, demande explicite de "grill me".

**Inputs possibles :** brief, PRD, Tech Design, task spec, plan, intention, contexte repo.

**Actions :**

- identifie les questions bloquantes ou à fort levier
- pose des questions une par une
- propose une recommandation à chaque question, idéalement sous forme de choix quand c'est possible
- explore le repo au lieu de demander si la réponse est trouvable
- résout les dépendances dans le bon ordre
- arrête quand les décisions importantes sont résolues, laissées ouvertes explicitement, ou quand le gain marginal devient faible

**Output :** synthèse en session, ou intégration dans `brief.md`, `prd.md`, `tech-design.md` ou task specs.

**Contenu de l'output :**

Decision log court :

- décisions clarifiées
- recommandations retenues
- questions résolues
- branches laissées ouvertes
- hypothèses à intégrer dans l'étape suivante
- ambiguïtés restantes

À éviter :

- transcript complet de l'interview
- questions non bloquantes qui ralentissent l'étape suivante
- demandes d'information trouvable dans le repo ou les docs

**Tailles possibles :** micro-interview sur une décision, ou interview complète sur une intention.

**Gate humain :** répondre aux questions et valider les décisions retenues.

**Important :** Utiliser `Grill Me` en général une seule fois par intention, au point d'ambiguïté le plus utile :

- après `Brief` : clarifier la direction avant validation ou PRD
- après `PRD` : challenger scope, comportements et acceptance criteria
- après `Tech Design` : challenger les arbitrages techniques
- avant `Build` : seulement si l'Execution Contract est ambigu
