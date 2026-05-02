# Ship Readiness

**Skill :** `ship-readiness`

**Statut :** On-demand step, gate optionnel de livraison.

**Rôle :** Vérifier qu'un changement est prêt à être livré dans de bonnes conditions.

**Quand l'utiliser :** Release sensible, flow critique, changement utilisateur ou infra, migration, risque sécurité/performance.

**Inputs possibles :** diff, commits, PRD, task specs, QA, review, CI, logs, contexte release.

**Actions :**

- vérifie CI, checks automatisés et preuves disponibles
- vérifie qualité, sécurité, performance et accessibilité si pertinent
- vérifie migrations, variables d'env, monitoring, owner de rollback et rollback plan
- distingue blockers, risques acceptés et recommandations avant livraison

**Output :** verdict `Go / No-Go`, checklist de pré-livraison, ou équivalent tracker.

**Publication de l'artefact :** Si une PR, release issue, issue parente ou tracker actif existe, proposer d'y publier le verdict `Go / No-Go`, blockers, risques acceptés et preuves. Sans support actif, garder le verdict en session ou proposer un fichier local seulement pour une livraison qui doit être auditée.

**Contenu de l'output :**

Contenu obligatoire :

- verdict `Go / No-Go`
- blockers
- risques acceptés
- preuves ou checks disponibles
- rollback plan
- recommandations avant livraison

Contenu conditionnel :

- checks qualité
- checks sécurité
- performance
- accessibilité si pertinent
- migrations et variables d'env
- monitoring / alerting

À éviter :

- checklist générique sans verdict
- risques implicites ou non assumés
- duplication complète de la QA ou de la review

**Tailles possibles :** checklist courte, ou gate complet de release.

**Gate humain :** accepter les risques ou bloquer la livraison.

**Important :** Ce n'est pas une étape normale de toutes les initiatives.
