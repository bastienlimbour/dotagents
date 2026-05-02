# 009 - Capitalize

**Skill :** `capitalize`

**Statut :** Core si décision durable ou doc à maintenir.

**Rôle :** Aligner la doc projet et la doc IA/agents avec ce qui a vraiment été construit.

**Quand l'utiliser :** Après changement durable de convention, architecture, API, comportement documenté, ADR, artefact futur ou règle agent.

**Inputs possibles :** code livré, diff, commits, PRD, task specs, Tech Design, ADRs, docs existantes.

**Actions :**

- met à jour docs obsolètes
- vérifie que la doc durable ne duplique pas un artefact temporaire
- crée ou ajuste ADRs
- crée ou met à jour `CONTEXT.md` ou `CONTEXT-MAP.md` si le vocabulaire domaine durable change
- met à jour `.agents/` si la configuration consommée par les agents change
- met à jour doc IA/agents si une règle doit persister
- réaligne PRD, Tech Design ou artefacts futurs invalidés
- supprime, archive, ferme ou consolide les artefacts temporaires qui ne doivent plus guider les agents
- ouvre follow-up de dette ou refactoring si nécessaire

**Output :** docs mises à jour, ADRs, règles agent, follow-ups, ou note indiquant qu'aucune capitalisation n'est utile.

**Publication de l'artefact :** Consolider les informations durables dans le code, les tests, les docs projet, `CONTEXT.md`, `CONTEXT-MAP.md`, `.agents/` ou `docs/decisions/`. Si une issue parente, sub-issue ou tracker existe, proposer de mettre à jour le body/commentaire final, fermer les items terminés ou ouvrir les follow-ups. En mode Markdown local, proposer de supprimer ou archiver `.initiatives/<initiative>/` après consolidation ; demander confirmation avant toute suppression.

**Contenu de l'output :**

Si rien n'est à capitaliser :

- une phrase indiquant qu'aucune mise à jour durable n'est utile

Si une capitalisation est faite :

- fichiers docs modifiés
- ADRs créées ou ajustées
- vocabulaire domaine créé ou mis à jour si applicable
- règles agent modifiées
- configuration `.agents/` modifiée si applicable
- artefacts futurs réalignés
- artefacts temporaires supprimés, archivés ou fermés
- follow-ups ouverts
- décisions devenues durables

À éviter :

- résumé complet de l'initiative
- documentation de décisions temporaires
- duplication du PRD, du Tech Design ou des task specs

**Tailles possibles :** note courte si rien à capitaliser, mise à jour complète si décision durable.

**Gate humain :** valider ce qui devient source de vérité durable.

**Important :** Capitalize ne documente pas pour le plaisir ; il maintient ce qui doit rester utile et vrai. Les artefacts temporaires ne doivent pas survivre par défaut et créer du doc rot.
