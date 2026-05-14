# `/capture`

## Objectif

Extraire une longue conversation, une session de recherche, une session de grilling ou une exploration dans une note markdown durable.

## À utiliser quand

- Une session a produit des conclusions utiles.
- Une recherche doit être conservée.
- Une longue discussion doit être condensée.
- Une session contient des décisions, conclusions, hypothèses ou questions ouvertes importantes à ne pas perdre.
- L'utilisateur veut éviter de garder uniquement le contexte conversationnel brut.

## Entrées

- Conversation courante.
- Notes ou résultats de recherche.
- Session de grilling.
- Exploration du codebase ou de documentation.
- Artefacts existants à référencer : brief, spec, issue, ADR, documentation, diff ou commit.
- Chemin cible fourni explicitement par l'utilisateur, s'il existe.

## Comportement

- Lire la conversation courante et les artefacts pertinents avant de condenser.
- Capturer la synthèse exploitable, pas le transcript brut.
- Ne pas dupliquer le contenu déjà capturé dans un artefact existant ; résumer brièvement et pointer vers le chemin, l'URL ou la référence.
- Si l'utilisateur donne un chemin, l'utiliser après avoir vérifié qu'il correspond au workflow.
- Si le fichier cible existe déjà, demander confirmation avant écrasement ou proposer un nouveau slug.
- Si aucun chemin n'est donné, recommander `.initiatives/<id>/research/` ou `docs/research/` selon le scope.
- Demander à l'utilisateur de confirmer le chemin cible.
- Vérifier avant écriture que la capture ne contient pas de secret, token, credential, donnée personnelle brute, prompt brut ou sortie LLM complète inutile.
- Après confirmation du chemin, écrire directement sans draft complet en conversation.
- Résumer ce qui a été créé.

## Sorties

```text
.initiatives/<id>/research/<slug>.md
docs/research/<slug>.md
```

## Format

Pas de template canonique.

La structure doit être choisie par l'agent selon ce qui est capturé : session de grilling, recherche, exploration codebase, longue discussion, comparaison d'options ou autre contexte durable.

Sections possibles, à utiliser seulement si pertinentes :

- `Context`
- `Key Findings`
- `Facts`
- `Assumptions`
- `Interpretation`
- `Decisions Or Conclusions`
- `Options Considered`
- `Open Questions`
- `Sources And References`

Règles :

- Garder un titre clair.
- Structurer le document selon le sujet, pas selon un template rigide.
- Lorsque c'est utile (après une session de grilling par exemple), extraire et séparer faits, hypothèses, interprétations, décisions, options, raisons des choix et questions ouvertes.
- Citer les sources ou références importantes lorsqu'elles existent.
- Référencer les artefacts canoniques existants au lieu de les recopier.
- Ne pas créer automatiquement d'ADR, de spec ou de brief depuis une capture.

## Règles de confirmation

```text
confirmation du chemin -> écriture du fichier -> résumé du résultat
```

L'agent n'a pas besoin de montrer tout le document en draft, sauf demande explicite de l'utilisateur.

Si le fichier cible existe déjà, l'agent doit obtenir une confirmation explicite avant de l'écraser ou proposer un autre nom.

## Vérification finale

- La capture est utile à relire hors conversation.
- Les faits, hypothèses, interprétations et décisions ou conclusions sont séparés lorsque cela compte.
- Les sources, chemins ou références importantes sont cités.
- Les artefacts existants ne sont pas dupliqués inutilement.
- Aucun secret, token, credential, donnée personnelle brute, prompt brut ou transcript LLM complet inutile n'est inclus.
- Aucun brief, spec, ADR ou issue n'a été créé ou mis à jour implicitement.

## Limites

- Ne pas mettre à jour `brief.md` automatiquement.
- Ne pas créer d'ADR automatiquement.
- Ne pas créer de spec ou d'issue automatiquement.
- Ne pas publier dans l'issue tracker distant par défaut.
- Ne pas servir de skill de handoff ou de reprise de session.
- Ne pas créer de continuation prompt, handoff chain, mode resume, scaffold script ou validation script.
- Ne pas conserver un log exhaustif des commandes ou des fichiers modifiés, sauf si ces éléments sont des sources pertinentes pour la capture.
