# 004 - Tech Design

**Skill :** `tech-design`

**Statut :** Core si impact technique non trivial.

**Rôle :** Source de vérité technique. Le Tech Design définit comment construire le produit et formalise les décisions structurantes.

**Quand l'utiliser :** Impact technique non trivial : architecture, data model, intégration, migration, sécurité, performance, scalabilité, observabilité, refactor structurel, choix de stack ou librairie durable.

**Inputs possibles :** `prd.md`, synthèse `grill-me` ou `grill-with-docs`, contexte repo, architecture existante, docs techniques existantes, ADRs, conventions, services externes, contraintes stack, exigences non fonctionnelles.

**Actions :**

- choisit le niveau de Tech Design utile : lite ou complet
- explore le repo et les patterns existants
- lit `CONTEXT.md`, `CONTEXT-MAP.md` et décisions pertinentes si disponibles
- vérifie la doc officielle quand une décision dépend d'un framework ou d'une lib
- documente l'état existant pertinent, les contraintes et les exigences techniques
- propose architecture, modules et patterns
- identifie les deep modules possibles : interface simple, comportement encapsulé, frontière de test claire
- applique le deletion test aux modules suspects : si supprimer le module fait disparaître la complexité, il était probablement shallow ; si la complexité réapparaît chez les callers, il apporte de la locality
- explicite les seams et adapters seulement quand ils correspondent à une vraie variation
- sépare décisions techniques et plan d'implémentation immédiat
- arbitre stack, librairies, services, data model, interfaces/API, migrations et stratégie de tests
- identifie impacts sur l'existant, risques, rollback et dette éventuelle
- compare alternatives et formalise compromis
- crée ou référence des ADR si nécessaire

**Output :** résumé Tech Design dans l'issue parente par défaut, commentaire détaillé si nécessaire, ou `tech-design.md` local si le mode Markdown local est choisi, avec ADRs si nécessaire.

**Publication de l'artefact :** Si une issue parente existe, proposer de consolider un Tech Design Lite dans son body. Pour un Tech Design non trivial, proposer un commentaire détaillé lié depuis le body canonique. En mode Markdown local, proposer `.initiatives/<initiative>/tech-design.md`. Les décisions durables doivent être proposées en ADR ou doc projet, pas seulement dans un commentaire.

**Contenu de l'output :**

Contenu obligatoire :

- contexte technique et état existant pertinent
- contraintes et exigences non fonctionnelles
- approche ou architecture cible
- décisions techniques clés
- modules touchés ou créés
- stratégie de testing technique
- risques techniques
- questions ouvertes

Contenu conditionnel :

- interfaces stables, seams et adapters si pertinents
- frontières de test et test surface
- opportunités de deepening, leverage et locality
- intégrations et services externes
- data model
- interfaces/API
- migrations et compatibilité
- sécurité
- performance et scalabilité
- accessibilité si impact technique
- observabilité, monitoring, logs
- plan de rollback si pertinent
- alternatives étudiées
- compromis retenus
- ADRs à créer ou mettre à jour

À éviter :

- réécriture du PRD
- plan de code fichier par fichier
- inventaire exhaustif du repo
- sections sécurité, performance ou observabilité sans impact réel

**Tailles possibles :** Tech Design Lite pour changement limité, Tech Design complet pour architecture, migration ou initiative structurante.

**Gate humain :** valider les arbitrages techniques, frontières de modules et interfaces structurantes avant `Slice` ou `Build`.

**Important :** Par défaut, Tech Design vient après PRD. Si la faisabilité technique est l'incertitude principale, faire un spike léger avant PRD, puis le Tech Design complet après PRD.

Un ADR n'est utile que si la décision est difficile à renverser, surprenante sans contexte, et issue d'un vrai compromis.

Vocabulaire recommandé : `module`, `interface`, `implementation`, `seam`, `adapter`, `depth`, `leverage`, `locality`. Ici, une interface n'est pas seulement une signature de type : c'est tout ce qu'un caller doit savoir pour utiliser correctement le module.

La depth est une propriété de l'interface : beaucoup de comportement utile pour peu de surface à apprendre. L'interface est aussi la surface de test ; si un test doit passer derrière l'interface, la forme du module est probablement mauvaise.

La locality concentre changements, bugs et connaissances à un endroit au lieu de les disperser chez les callers. Un seam ou adapter unique indique souvent une abstraction hypothétique ; deux variantes réelles justifient mieux le seam.
