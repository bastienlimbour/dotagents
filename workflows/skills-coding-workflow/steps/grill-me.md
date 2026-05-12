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
- Ne pas s'arrêter parce que le plan semble "assez clair" ; continuer tant qu'il reste des branches critiques, ambiguïtés ou hypothèses faibles.
- Creuser la réponse reçue avant de passer à une nouvelle branche.
- Traiter les réponses vagues ou provisoires comme des signaux à clarifier.
- Challenger les contradictions, compromis cachés, alternatives non considérées et décisions difficiles à inverser.
- Utiliser des angles de questionnement adaptés au contexte : intention, contraintes, non-objectifs, alternatives, hypothèses, modes d'échec, dépendances, réversibilité et impacts downstream.
- Continuer jusqu'à obtenir une compréhension partagée.
- Résumer une branche lorsqu'elle est résolue, sans remplacer le grilling par de la synthèse prématurée.

## Sorties

La sortie par défaut est une compréhension partagée en conversation.

Un artefact peut être créé seulement si l'utilisateur le demande explicitement, ou si l'agent propose une capture et obtient confirmation.

## Vérification finale

- Les questions critiques ont reçu une réponse ou sont explicitement restées ouvertes.
- Les décisions dépendantes ont été traitées dans un ordre cohérent.
- Les recommandations de l'agent sont séparées des décisions utilisateur.
- Les hypothèses importantes ont été rendues explicites.
- Les alternatives sérieuses ont été considérées ou volontairement écartées.
- Les risques, modes d'échec et décisions difficiles à inverser ont été examinés.
- L'utilisateur confirme que la compréhension partagée est suffisante pour passer à la suite, ou les questions ouvertes sont explicitement listées.

## Limites

- Pas de mise à jour automatique de documentation.
- Pas de création d'artefact sauf demande explicite.
- Pas d'implémentation pendant la session.
- Pas de log ou capture automatique ; utiliser `/capture` seulement après demande ou confirmation.
- Si la session révèle un besoin de documentation durable, proposer `/grill-with-docs` au lieu de mettre à jour les docs depuis `/grill-me`.
