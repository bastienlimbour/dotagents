# 007 - Review

**Skill :** `review`

**Statut :** Core recommandé.

**Rôle :** Revue de code à froid, distincte de l'implémentation.

**Quand l'utiliser :** Toute tâche non triviale, logique complexe, changement sensible, architecture, sécurité, performance, ou besoin de regard frais.

**Inputs possibles :** diff, commits, PRD, task spec, Tech Design, tests, résultats de vérification.

**Actions :**

- démarre idéalement dans un contexte frais, et possiblement avec un LLM différent de celui qui a implémenté le code
- pousse explicitement les standards projet utiles au reviewer
- compare code, PRD/task spec, Tech Design et acceptance criteria
- relit tests et vérifications
- cherche divergences, oublis, bugs, régressions
- vérifie les changements hors scope, secrets, config accidentelle et migrations oubliées
- évalue correctness, readability, architecture, security, performance
- vérifie que les tests couvrent le comportement réel et les edge cases importants
- signale dead code et simplifications évidentes
- signale explicitement les zones non revues ou le niveau de confiance si nécessaire

**Output :** feedback en session, ou commentaire de review dans le tracker/PR.

**Contenu de l'output :**

Contenu obligatoire :

- verdict
- findings par sévérité, ou `No findings` explicite
- références fichiers/lignes si possible
- couverture de tests et vérification

Contenu conditionnel :

- écarts au PRD, task spec ou Tech Design
- risques de régression
- suggestions de correction
- zones non revues ou niveau de confiance

À éviter :

- résumé optimiste avant les findings
- corrections de code avant d'avoir formulé les problèmes
- remarques de style non actionnables

**Tailles possibles :** review courte pour changement simple, review complète pour changement sensible.

**Gate humain :** accepter la tâche ou la renvoyer en correction.

**Important :** `Review` évalue le code. Ce n'est pas une checklist de validation fonctionnelle manuelle. Le reviewer liste d'abord les findings ; il ne modifie pas le code avant d'avoir formulé les problèmes.
