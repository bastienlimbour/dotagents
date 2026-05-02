# Diagnose

**Skill :** `diagnose`

**Statut :** On-demand step.

**Rôle :** Diagnostiquer un bug complexe ou une régression avec une boucle disciplinée avant de corriger.

**Quand l'utiliser :** Bug non trivial, régression difficile, performance dégradée, erreur intermittente, cause racine inconnue, échec de test incompris.

**Inputs possibles :** rapport de bug, logs, stack traces, diff récent, tests échouants, contexte utilisateur, environnement, étapes de reproduction.

**Actions :**

- note environnement, commande de reproduction et fiabilité du repro
- construit d'abord un feedback loop fiable : failing test, script HTTP, commande CLI, script navigateur, trace rejouée, harness jetable, fuzz/property loop, bisect ou boucle HITL structurée
- améliore la boucle : plus rapide, plus déterministe, signal plus précis
- reproduit le problème utilisateur ou documente pourquoi il ne peut pas être reproduit
- minimise le cas d'échec sans perdre le symptôme réel
- formule 3 à 5 hypothèses classées, falsifiables, avec prédiction observable
- instrumente si nécessaire en changeant une seule variable à la fois
- limite les logs aux extraits utiles pour falsifier une hypothèse
- tague toute instrumentation temporaire avec un préfixe unique pour nettoyage
- identifie la cause racine avant de corriger
- applique le fix minimal
- ajoute ou adapte un test de régression au bon seam si ce seam existe
- relance les feedback loops utiles
- nettoie logs temporaires, harness jetables et prototypes de debug avant de déclarer terminé

**Output :** cause racine, correction, test de régression, commandes de vérification, risques restants.

**Publication de l'artefact :** Si un bug issue, sub-issue ou tracker actif existe, proposer d'y publier cause racine, fix, test de régression et vérifications. Sans support actif, garder la synthèse en session ; ne proposer une nouvelle issue que si le diagnostic révèle un suivi nécessaire. Les logs, harness et instrumentations temporaires restent locaux et doivent être nettoyés.

**Contenu de l'output :**

Contenu obligatoire :

- symptôme observé
- environnement et reproduction minimale, ou raison de non-reproduction
- feedback loop construit, commande ou limitation de reproduction
- hypothèses testées
- cause racine
- fix appliqué
- test de régression, ou absence de seam correct documentée
- vérifications exécutées
- risques ou follow-ups

À éviter :

- logs longs non annotés
- correction sans cause racine isolée
- empilement de plusieurs fixes non falsifiés

**Tailles possibles :** diagnostic court pour bug isolé, ou investigation complète pour régression complexe.

**Gate humain :** valider l'impact du bug, le niveau de risque du fix et les éventuels follow-ups.

**Important :** `Diagnose` évite les corrections au hasard. Ne pas empiler plusieurs fixes sans avoir isolé la cause.

Si aucun feedback loop crédible ne peut être construit, s'arrêter explicitement, lister ce qui a été tenté et demander l'accès à l'environnement, un artefact capturé ou l'autorisation d'ajouter une instrumentation temporaire. Ne pas passer à l'hypothèse pure sans boucle.

Pour une régression de performance, mesurer d'abord : baseline, profiler, query plan ou harness de timing. Corriger seulement après mesure.
