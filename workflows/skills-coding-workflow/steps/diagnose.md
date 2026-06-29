# `/diagnose`

## Objectif

Diagnostiquer et corriger bugs, régressions difficiles et problèmes de performance avec une boucle disciplinée.

## À utiliser quand

- L'utilisateur fournit une erreur, une régression, un symptôme de performance ou un comportement inattendu.
- La cause racine n'est pas évidente.
- Il faut construire une reproduction fiable avant de modifier le code.
- Un fix risquerait de masquer le symptôme sans comprendre le problème.

## Entrées

- Description du bug ou symptôme.
- Étapes de reproduction existantes.
- Logs, traces, screenshots ou erreurs.
- Tests existants.
- Codebase et documentation pertinente.
- Issue ou spec liée, si disponible.

## Boucle centrale

```
reproduce -> minimise -> hypothesise -> instrument -> fix -> regression-test
```

## Comportement

- Construire ou identifier une boucle de reproduction fiable.
- Minimiser la reproduction lorsque utile.
- Formuler 3 à 5 hypothèses falsifiables, classées par probabilité ou impact.
- Instrumenter minimalement si nécessaire.
- Préférer debugger ou logs ciblés aux logs massifs.
- Utiliser des marqueurs temporaires uniques au format `[DEBUG-xxxx]` si des logs sont nécessaires.
- Corriger seulement lorsqu'une cause est suffisamment comprise.
- Ajouter ou recommander des tests de régression lorsque pertinent.
- Supprimer le code debug et les prototypes temporaires.
- Confirmer que la reproduction originale ne reproduit plus.
- Expliquer la cause racine et le fix.

## Feedback loops possibles

- Test automatisé qui échoue.
- Script `curl`.
- Commande CLI avec fixture.
- Playwright, Puppeteer ou navigateur headless.
- Trace replay.
- Harness jetable.
- Fuzz loop.
- `git bisect run`.
- Differential test.
- Script manuel guidé par l'humain.

## Vérification finale

- La reproduction originale ne reproduit plus.
- Le test de régression passe ou la vérification équivalente est documentée.
- Les logs debug sont supprimés.
- Les prototypes ou harness temporaires sont supprimés ou explicitement conservés.
- La cause racine est expliquée.

## Limites

- Ne pas patcher au hasard.
- Ne pas masquer le symptôme sans comprendre la cause.
- Ne pas laisser de logs debug.
