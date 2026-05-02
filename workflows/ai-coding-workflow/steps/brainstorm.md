# Brainstorm

**Skill :** `brainstorm`

**Statut :** On-demand step.

**Rôle :** Ouvrir largement l'espace d'idées, générer des options, structurer les pistes sans converger.

**Quand l'utiliser :** Idée floue, nouveau produit, nouvelle direction, feature majeure, exploration produit/technique, manque d'options.

**Inputs possibles :** Objectif du brainstorming, contexte, intuition, notes, transcript vocal, idées existantes, directions à explorer, données, code ou doc projet.

**Actions :**

- créé un fichier `brainstorming.md` local dans le dossier `.initiatives/<NNN-initiative-name>/`
- définit l'objectif du brainstorming et le contexte
- pose des questions ouvertes sans relâche pour stimuler la réflexion et générer des pistes
- explore problèmes, opportunités, personas, solutions, proposition de valeur, cas d'usage, fonctionnalités, hypothèses, contraintes, risques
- clusterise les idées au fil du brainstorming pour éviter le vrac
- continue jusqu'à demande d'arrêt explicite ou fin de timebox

**Output :** synthèse de brainstorming en session, `brainstorming.md` local optionnel, ou commentaire tracker seulement si un support actif existe déjà.

**Publication de l'artefact :** Par défaut, garder le brainstorming en session/chat ou dans `.initiatives/<initiative>/brainstorming.md` gitignored. Ne pas créer d'issue parente GitHub pour du brainstorming divergent sauf demande explicite ; si une issue parente existe déjà, proposer un commentaire de synthèse sans transcript brut.

**Contenu de l'output :**

Contenu obligatoire :

- contexte / objectif du brainstorming
- synthèse par thèmes
- pistes prometteuses à filtrer ensuite
- questions ouvertes

Contenu conditionnel :

- problèmes et opportunités
- utilisateurs/personas possibles
- propositions de valeur
- solutions et variantes
- cas d'usage
- fonctionnalités candidates
- hypothèses
- contraintes et risques

À éviter :

- transcript complet de la session
- décision produit prématurée
- liste brute de toutes les idées sans regroupement

**Tailles possibles :** micro-brainstorm ciblé, ou brainstorm complet 30 à 120 minutes.

**Gate humain :** choisir les pistes à filtrer dans `Brief`, `PRD`, `Tech Design` ou une décision explicite.

**Important :** `Brainstorm` diverge volontairement. Il ne tranche pas.
