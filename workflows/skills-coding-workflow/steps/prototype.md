# `/prototype`

## Objectif

Créer du code jetable pour répondre rapidement à une question de design, produit, UI, logique ou technique.

Le résultat utile n'est pas le prototype lui-même. Le résultat utile est la décision ou l'apprentissage qu'il rend possible.

## À utiliser quand

- Une question doit être tranchée par une expérimentation rapide.
- Une direction UI, produit, logique métier ou technique est incertaine.
- Il est moins coûteux de tester une hypothèse avec du code jetable que de spéculer.
- L'utilisateur veut comparer plusieurs variantes avant de choisir.

## Entrées

- Question précise à résoudre.
- Code ou zone concernée.
- Contraintes de production à ne pas impacter.
- Critère permettant de décider quoi faire après le prototype.

## Comportement

- Définir la question à laquelle le prototype doit répondre.
- Dire clairement que le prototype est jetable.
- Placer le prototype près du code concerné lorsque utile.
- Éviter la persistance par défaut.
- Éviter le polish.
- Isoler le prototype du comportement de production.
- Fournir une commande, URL, route ou instruction d'usage pour le tester.
- À la fin, proposer de supprimer, absorber ou conserver temporairement le prototype.
- Capturer ou recommander de capturer la décision apprise dans l'artefact approprié : spec, issue, ADR ou note locale.

## Prototypes UI

- Produire 3 variantes par défaut lorsque l'objectif est de comparer des directions UI.
- Ne pas dépasser 5 variantes sans demande explicite.
- Rendre les variantes réellement différentes, pas de simples variations cosmétiques.
- Utiliser des variantes switchables lorsque utile, par exemple via `?variant=`.
- Prévoir un switcher visible pendant le prototype lorsque cela aide à comparer.
- Garder les variantes cachées en production.
- Préférer un accès stable comme une route ou un flag temporaire.

## Prototypes logique

- Utiliser un harness, TUI, script ou petite app isolée.
- Rendre l'état visible.
- Prévoir des actions simples, par exemple clavier ou commandes, lorsque c'est utile pour explorer une state machine ou une logique métier.
- Privilégier les fonctions pures ou state machines isolées lorsque pertinent.

## Sorties

- Prototype jetable isolé.
- Instruction pour le tester.
- Décision ou apprentissage produit par le prototype.
- Recommandation : supprimer, absorber ou conserver temporairement.

## Vérification finale

- La question initiale a reçu une réponse ou l'incertitude restante est explicite.
- Le prototype est isolé du comportement de production.
- Une commande, route, URL ou instruction de test est fournie.
- Une décision de suite est proposée.

## Limites

- Ne pas traiter le prototype comme implémentation production par défaut.
- Ne pas persister de données sauf besoin explicite.
- Ne pas laisser le prototype sans décision.
