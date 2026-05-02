# 002 - Validate

**Skill :** `validate`

**Statut :** Core optionnel.

**Rôle :** Réduire l'incertitude externe avant d'investir dans un PRD complet, un Tech Design ou une implémentation coûteuse.

**Quand l'utiliser :** Doute sur marché, concurrence, utilisateurs, dépendances externes, business model, faisabilité ou risque produit. À sauter si l'idée est sûre ou l'enjeu faible.

**Inputs possibles :** `brief.md`, synthèse `grill-me` ou `grill-with-docs`, hypothèses à tester, questions ouvertes, contraintes business ou utilisateur.

**Actions :**

- transforme les incertitudes en hypothèses testables et seuils de décision
- timeboxe la recherche selon l'enjeu
- recherches web approfondies et collecte de signaux externes
- analyse concurrence, alternatives, marché, utilisateurs ou business model si pertinent
- challenge les hypothèses du brief
- identifie risques, dépendances externes et contraintes majeures
- produit un verdict motivé `Go / No-Go / Pivot` avec niveau de confiance

**Output :** synthèse de validation en session, `validation.md` local optionnel, ou commentaire tracker si une initiative active existe.

**Publication de l'artefact :** Par défaut, garder la validation en session/chat ou dans `.initiatives/<initiative>/validation.md` gitignored. Si une issue parente existe déjà et que la validation justifie `Go / No-Go / Pivot`, proposer un commentaire de synthèse et consolider la décision importante dans le PRD ou le body canonique.

**Contenu de l'output :**

Contenu obligatoire :

- hypothèses testées
- méthode et sources utiles
- signaux clés observés
- recommandations
- verdict `Go / No-Go / Pivot` et niveau de confiance

Contenu conditionnel :

- analyse marché / concurrence / alternatives
- signaux utilisateurs ou business
- faisabilité
- dépendances externes
- risques et contraintes

À éviter :

- synthèse encyclopédique du marché
- liste de sources non utilisées dans le raisonnement
- longs extraits copiés depuis le web

**Tailles possibles :** validation rapide sur quelques hypothèses, ou validation complète pour initiative stratégique.

**Gate humain :** continuer, pivoter ou abandonner.

**Important :** `Validate` teste une direction convergée. Il ne remplace ni `Brief` ni `PRD`.
