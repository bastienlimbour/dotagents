# 006 - Build

**Skills :** `implement`, `implement-tdd`

**Statut :** Core requis.

**Rôle :** Implémenter une tâche en restant dans le scope et en planifiant l'exécution avant le code.

**Quand l'utiliser :** Pour chaque task spec, ou directement depuis un PRD minimal single-task ou tout input avec un Execution Contract suffisant.

**Inputs possibles :** PRD minimal, task spec, `tech-design.md`, ADRs, contexte repo, instructions projet.

**Actions :**

- démarre depuis un contexte propre et les artefacts strictement utiles
- vérifie le scope, l'Execution Contract et l'état du worktree sans modifier les changements non liés
- prépare un plan d'implémentation proportionné (Plan mode / Read only)
- confirme les changements d'interface publique et les comportements prioritaires à tester si la tâche est non triviale
- identifie le seam de test avant de coder quand `implement-tdd` est utilisé
- implémente le plan en restant dans le scope
- utilise red-green-refactor si `implement-tdd` est choisi
- debug si nécessaire
- exécute les vérifications nécessaires : tests, typecheck, lint, build ou commandes spécifiques
- vérifie la conformité à l'Execution Contract

**Output :** code implémenté + compte rendu en session.

**Contenu de l'output :**

Build Preflight :

- approche retenue
- zones ou fichiers probables si utile
- tests et checks prévus
- risques ou clarifications nécessaires pour une tâche `HITL`

Compte rendu final :

- changements effectués
- tests et checks exécutés
- résultat des vérifications
- statut final
- ambiguïtés ou blocages restants

À éviter :

- journal détaillé de toutes les micro-actions
- inventaire exhaustif de fichiers sans valeur de review
- élargissement du scope pour corriger des problèmes voisins

**Tailles possibles :** plan très court pour tâche évidente, plan détaillé pour tâche sensible ou HITL.

**Plan d'implémentation :** toujours présent mais adapté au scope et à la tâche. Il peut nécessiter une validation humaine (HITL) ou être auto-approuvé (AFK).

**Choix du skill :** `implement` pour intégration, UI, glue code, configuration. `implement-tdd` pour bug fix, logique métier, comportement sensible ou fort risque de régression.

**Gate humain :** validation du plan d'implémentation pour tâche `HITL`. Auto-approbation possible pour tâche `AFK` claire.

**Important :** Si l'Execution Contract est insuffisant, revenir vers `PRD`, `Tech Design`, `Slice`, `Grill Me` ou `Grill With Docs`.

#### TDD red-green-refactor

`implement-tdd` applique une boucle comportement par comportement :

1. écrire un test échouant qui exprime le comportement attendu
2. confirmer que le test échoue pour la bonne raison
3. implémenter le minimum pour passer au vert
4. refactorer seulement après un état vert
5. relancer les feedback loops utiles

Ne pas écrire tous les tests puis toute l'implémentation. Ce serait une slice horizontale. La bonne boucle est verticale : un test, un comportement, une implémentation minimale, puis le comportement suivant.

Les tests doivent vérifier le comportement via des interfaces publiques, idéalement en style intégration avec de vrais chemins de code. Éviter les tests couplés aux détails internes, les mocks excessifs, les tests de méthodes privées et les tests écrits après coup pour confirmer l'implémentation.

Mocks : uniquement aux frontières système quand c'est utile : API externes, temps, hasard, filesystem ou base de données si aucun substitut local pratique n'existe. Ne pas mocker les modules internes que l'on contrôle. Préférer un test DB, un adapter in-memory ou un local substitute quand cela donne un signal plus réaliste.
