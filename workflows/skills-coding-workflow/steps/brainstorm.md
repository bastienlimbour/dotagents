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
- Poser une question ouverte à la fois.
- Avant une question, fournir si utile du contexte, des idées stimulantes ou des angles alternatifs.
- Mettre à jour `brainstorming.md` tout au long de la session sans redemander confirmation.
- Marquer les idées comme évoquées, prometteuses, rejetées ou encore à explorer lorsque utile.
- À la fin, proposer une synthèse finale.

## Sorties

```text
.initiatives/<id>/brainstorming.md
```

## Format

Contenu possible :

- Contexte de départ.
- Idées générées.
- Axes explorés.
- Personas.
- Cas d'usage.
- Angles de différenciation.
- Idées de fonctionnalités.
- Risques attendus ou inattendus.
- Options absurdes mais stimulantes.
- Pistes prometteuses.
- Pistes rejetées.
- Questions ouvertes.
- Synthèse finale.

## Règles de confirmation

- Confirmer l'initiative cible et le chemin `brainstorming.md` au début.
- Une fois confirmé, mettre à jour `brainstorming.md` sans redemander à chaque fois.
- Ajouter la synthèse finale si l'utilisateur confirme ou termine explicitement la session.

## Limites

- Ne pas converger trop tôt.
- Ne pas produire de spec.
- Ne pas produire d'issues de tâches.
- Ne pas faire de validation approfondie par défaut.
