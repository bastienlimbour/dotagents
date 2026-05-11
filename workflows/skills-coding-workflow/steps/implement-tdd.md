# `/implement-tdd`

## Objectif

Implémenter en red-green-refactor strict.

## À utiliser quand

- L'utilisateur demande explicitement du TDD.
- Le comportement observable peut être défini avant l'implémentation.
- Le risque de régression justifie une boucle test-first.
- Une interface publique ou un comportement métier doit être stabilisé par des tests durables.

## Entrées

- Execution contract.
- Comportement observable attendu.
- Interface publique ou seam à tester.
- Critères d'acceptation.
- Tests existants et conventions de test du repo.

## Boucle centrale

```text
red -> green -> refactor
```

## Comportement

- Établir l'execution contract.
- Confirmer l'interface publique ou le comportement observable.
- Confirmer les comportements prioritaires à tester.
- Écrire un seul test qui échoue.
- Vérifier qu'il échoue pour la bonne raison.
- Écrire l'implémentation minimale.
- Vérifier que le test passe.
- Répéter comportement par comportement.
- Refactorer seulement lorsque les tests sont verts.
- Privilégier les tests de comportement via interfaces publiques.
- Écrire des tests qui survivent aux refactors : si un test casse alors que le comportement public n'a pas changé, le test est probablement trop lié aux détails d'implémentation.
- Mocker uniquement les frontières système : API externe, email, paiement, temps, filesystem, réseau ou équivalent.
- Éviter de mocker les modules internes.

## Vérification finale

- Chaque comportement ajouté est couvert par un test qui a d'abord échoué pour la bonne raison.
- La suite ciblée passe après implémentation.
- Les refactors éventuels ont été faits uniquement en phase verte.
- Les tests restent orientés comportement public plutôt que détails internes.

## Limites

- Ne pas écrire tous les tests d'abord puis toute l'implémentation ensuite.
- Ne pas tester les détails d'implémentation.
- Ne pas fermer d'issue automatiquement en v1.
