# Skills

Une skill est un mode d'emploi outillé, écrit pour l'agent, quand une tâche redevient récurrente.

## Règle d'écriture

Une skill ne s'écrit qu'à la **3e répétition réelle** d'une tâche — jamais par anticipation « au
cas où ». Avant la 3e répétition, la proposition passe par `_systeme/ameliorations.md`.

## Format attendu

Un dossier `nom-de-la-skill/` contenant :

- `SKILL.md` — frontmatter `name` + `description` (quand l'utiliser), puis la procédure et les
  règles à suivre.
- `scripts/` (optionnel) — outils exécutables appelés par la procédure.
- `references/` (optionnel) — documentation de détail chargée seulement si `SKILL.md` ne suffit
  pas.
