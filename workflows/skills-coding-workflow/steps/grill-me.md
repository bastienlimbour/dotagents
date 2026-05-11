# `/grill-me`

## Objectif

Interviewer l'utilisateur de manière insistante pour clarifier un plan, une idée, un design ou une décision.

## À utiliser quand

- L'utilisateur demande explicitement à être challengé ou grillé.
- Un plan, design ou choix contient encore des hypothèses floues.
- Une décision importante mérite d'être testée avant d'être transformée en spec, brief ou implémentation.
- La conversation doit résoudre les dépendances entre décisions une par une.

## Entrées

- Conversation courante.
- Plan, idée, design ou décision proposée.
- Codebase ou documentation projet si la réponse peut s'y trouver.
- Artefacts existants : brief, spec, notes de recherche, ADRs ou issue.

## Comportement

- Poser une question à la fois.
- Fournir une recommandation pour chaque question.
- Explorer le codebase si la réponse se trouve dans le repo.
- Parcourir les dépendances entre décisions une par une.
- Continuer jusqu'à obtenir une compréhension partagée.
- Résumer les décisions clarifiées lorsque cela aide à stabiliser la suite.

## Sorties

La sortie par défaut est une compréhension partagée en conversation.

Un artefact peut être créé seulement si l'utilisateur le demande explicitement, ou si l'agent propose une capture et obtient confirmation.

## Vérification finale

- Les questions critiques ont reçu une réponse ou sont explicitement restées ouvertes.
- Les décisions dépendantes ont été traitées dans un ordre cohérent.
- Les recommandations de l'agent sont séparées des décisions utilisateur.

## Limites

- Pas de mise à jour automatique de documentation.
- Pas de création d'artefact sauf demande explicite.
