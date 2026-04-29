# 001 - Brief

**Skill :** `brief`

**Statut :** Core optionnel.

**Rôle :** Transformer une ou plusieurs idées en direction produit claire. Le brief est une note d'opportunité légère avant d'investir dans un PRD.

**Quand l'utiliser :** Après brainstorming, nouveau produit, grosse feature, idée encore floue, besoin de cadrer l'opportunité. À sauter pour une feature claire et limitée.

**Inputs possibles :** Idée brute, notes, transcript, `brainstorming.md`, signaux utilisateurs, contexte business ou produit.

**Actions :**

- choisit le niveau de brief utile : léger ou complet
- sélectionne et fait converger les idées/pistes prometteuses
- clarifie problème, cible, proposition de valeur
- décrit la solution envisagée dans les grandes lignes, sans détails techniques
- cadre le scope pressenti : MVP, V1, Later, Excluded
- explicite hypothèses, risques, contraintes, non-goals et questions ouvertes
- recommande le prochain gate : `Grill Me`, `Grill With Docs`, `Validate` ou `PRD`

**Output :** `brief.md` ou équivalent tracker.

**Contenu de l'output :**

Contenu obligatoire :

- problème
- cible / utilisateurs
- proposition de valeur
- direction de solution
- scope pressenti
- non-goals
- hypothèses, risques ou questions ouvertes qui changent la suite

Contenu conditionnel :

- cas d'usage principaux
- fonctionnalités importantes
- scope framing `MVP / V1 / Later / Excluded`
- contraintes
- prochain gate recommandé

À éviter :

- détails techniques
- liste exhaustive d'idées non retenues
- duplication brute du brainstorming

**Tailles possibles :** brief léger, ou brief complet pour nouveau produit / grosse initiative.

**Gate humain :** confirmer la direction et le scope initial avant `Grill Me`, `Grill With Docs`, `Validate` ou `PRD`.

**Important :** Le brief converge vers une direction produit claire, mais ne remplace pas le PRD, la validation externe ou le Tech Design.
