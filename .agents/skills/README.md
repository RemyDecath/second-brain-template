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

## Skill livrée : `google-workspace`

Portée telle quelle depuis un système existant, en anglais (voir son `SKILL.md` pour le pourquoi).
Elle est **optionnelle** : le socle n'y renvoie que par une ligne d'aiguillage, jamais comme
prérequis.

**Prérequis** :

```bash
npm install -g @googleworkspace/cli
```

puis un fichier `client_secret.json` (identifiants OAuth Google Cloud, à créer toi-même) placé dans
`~/.config/gws/`.

**Suppression** si tu n'utilises pas Google Workspace :

```bash
rm -rf .agents/skills/google-workspace
```

Puis retire la ligne d'aiguillage correspondante dans `.github/copilot-instructions.md`
(section 12).
