# `/brainstorm`

## Objectif

Mener une session d'exploration divergente pour élargir le champ des idées.

## À utiliser quand

- L'utilisateur veut explorer une idée largement.
- Un projet ou une feature est encore ouvert.
- Il faut davantage d'options, angles, personas, cas d'usage ou différenciation.

## Comportement

- Confirmer l'initiative et le chemin `brainstorming.md` au début.
- Créer `brainstorming.md` après confirmation avec le contexte de départ.
- Avant de diverger, cadrer légèrement l'idée : problème, utilisateur cible, succès attendu, contraintes et non-objectifs connus.
- Si une réponse se trouve dans le codebase ou la documentation, explorer ces sources avant de demander à l'utilisateur.
- Reformuler l'idée en problème ou question d'opportunité lorsque cela aide, par exemple sous forme `How might we...`.
- Poser une question à la fois.
- Préférer une question à choix multiples quand cela réduit la charge cognitive.
- Avant une question, fournir si utile du contexte, des idées stimulantes ou des angles alternatifs.
- Agir comme partenaire de réflexion : proposer des angles inattendus, challenger les hypothèses faibles et éviter d'être une simple machine à idées.
- Utiliser les angles d'idéation de manière sélective, sans dérouler une checklist mécanique.
- Ne pas évaluer trop tôt pendant la divergence, mais noter les risques, hypothèses et questions ouvertes utiles pour la suite.
- Mettre à jour `brainstorming.md` tout au long de la session sans redemander confirmation.
- Marquer les idées comme évoquées, prometteuses, rejetées ou encore à explorer lorsque utile.
- Si la session arrive naturellement à maturité, regrouper les idées en quelques directions prometteuses sans forcer une décision.
- À la fin, proposer une synthèse finale.

## Angles possibles

À utiliser seulement lorsqu'ils aident la conversation :

- Inversion : explorer l'opposé de l'idée initiale.
- Suppression ou simplification : chercher ce qu'on peut enlever ou rendre 10x plus simple.
- Retrait temporaire d'une contrainte : imaginer l'option sans contrainte de temps, budget ou technique, puis revenir au réel.
- Changement de persona ou segment utilisateur : voir comment l'idée change selon l'audience.
- Analogie : emprunter un modèle à un autre domaine, produit ou industrie.
- Version 10x plus ambitieuse : pousser l'idée au-delà de l'incrémental.
- Décomposition : séparer le problème en sous-problèmes et recombiner les pistes.

## Sorties

```text
.initiatives/<id>/brainstorming.md
```

## Format

Template :

Les lignes de guidance dans le template sont des placeholders à remplacer dans l'artefact généré.

```markdown
# Brainstorming: <title>

## Starting Context
Describe the initial idea, prompt, initiative context, and any known constraints or assumptions.

## Ideas
Group generated ideas by context-specific categories. Add or rename categories as the brainstorming evolves.

### <Context-Specific Category>
List raw ideas for this category without status tags.

## Promising Directions
Capture the directions that currently seem most valuable or worth exploring further.

## Assumptions To Test
Capture important assumptions, bets, or kill risks surfaced during the session. Do not validate them here.

## Deferred Ideas
Capture useful ideas intentionally postponed for later.

## Rejected Ideas
Capture ideas explicitly rejected and briefly why they were rejected.

## Open Questions
List unresolved questions that matter for future exploration, validation, brief, or spec work.

## Final Synthesis
Summarize the main outcomes only when the brainstorming session explicitly ends.
```

Règles de sections :

- `Starting Context` : required.
- `Ideas` : required.
- Catégories sous `Ideas` : adaptable. Exemples possibles : `Problems`, `Personas`, `Use Cases`, `Feature Ideas`, `Differentiation Angles`, `Risks And Constraints`, `Wild Ideas`, `Pricing`, `Distribution`, `Technical Bets`.
- `Promising Directions` : required.
- `Assumptions To Test` : optional, mais recommandé dès qu'une direction prometteuse émerge.
- `Deferred Ideas` : optional.
- `Rejected Ideas` : optional.
- `Open Questions` : required.
- `Final Synthesis` : optional, ajoutée seulement quand la session se termine explicitement.

Ne pas imposer de tags de statut dans `Ideas`. Les idées restent classées par catégories contextuelles ; la convergence se fait dans `Promising Directions`, `Deferred Ideas` et `Rejected Ideas`.

## Règles de confirmation

- Confirmer l'initiative cible et le chemin `brainstorming.md` au début.
- Une fois confirmé, mettre à jour `brainstorming.md` sans redemander à chaque fois.
- Ajouter la synthèse finale si l'utilisateur confirme ou termine explicitement la session.

## Limites

- Ne pas converger trop tôt.
- Ne pas imposer de convergence si l'utilisateur veut encore explorer.
- Ne pas transformer la session en design doc.
- Ne pas produire de spec.
- Ne pas produire d'issues de tâches.
- Ne pas faire de validation marché, concurrentielle, technique ou business approfondie par défaut.
- Ne pas créer de decision log obligatoire.
