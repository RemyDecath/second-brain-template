# Second Brain — template

Template de « second brain » pour Obsidian, pensé pour être lu efficacement par un agent GitHub
Copilot (App / CLI) sans exploser le coût en tokens à chaque conversation.

## Le problème que ça résout

Un vault Obsidian classique force l'agent à explorer à l'aveugle (recherche plein texte, listing de
dossiers) pour retrouver une information. Ce template introduit un **routage à 2 niveaux** : un
socle d'instructions minimal renvoie vers des hubs, qui renvoient vers des cibles précises. L'agent
ne descend d'un niveau que si nécessaire.

## Stack

Obsidian (pour l'écriture et la navigation humaine) + GitHub Copilot App/CLI (pour l'assistance IA),
Markdown brut partout — aucun plugin Obsidian n'est requis pour que le système fonctionne.

## Schéma d'indexation

```
copilot-instructions.md  →  Hub de dossier (Registry)  →  Note de contexte  →  Note atomique
      (routage)                (table de chemins)          (l'essentiel)        (le détail)
```

Les 5 dossiers (méthode IPCRA) :

| Dossier | Rôle |
|---|---|
| `0_Inbox/` | Capture brute, non qualifiée |
| `1_Projets/` | Engagements avec une date de fin |
| `2_Casquettes/` | Rôles permanents, sans date de fin |
| `3_Ressources/` | Réutilisable et transverse (glossaire, décisions, templates) |
| `4_Archives/` | Terminé ou inactif, hors contexte IA |

## Démarrage

1. Cloner ce dépôt.
2. L'ouvrir comme vault dans Obsidian.
3. Remplir `config.md` (identité, casquettes, ton, périmètre sensible, outils branchés).
4. Créer ta première casquette en suivant `3_Ressources/_Templates/PATTERN_EXTENSIBILITE.md`.
5. Supprimer les fichiers d'exemple (voir ci-dessous).

## Fichiers d'exemple à supprimer

Une histoire fictive minimale (une association, un trésorier, un projet de refonte de site) illustre
le système : `1_Projets/EXEMPLE_Projet/`, `2_Casquettes/EXEMPLE_Casquette/`, et les lignes
`EXEMPLE` dans `Glossaire.md`, `Decisions_Log.md` et `_systeme/journal.md`. Chaque fichier porte
l'en-tête `<!-- EXEMPLE — supprimer après appropriation -->`.

Suppression des dossiers d'exemple, une fois le système approprié :

```bash
rm -rf 1_Projets/EXEMPLE_Projet 2_Casquettes/EXEMPLE_Casquette
```

Retire ensuite leurs lignes des registries de `1_Projets/1_Projets.md` et
`2_Casquettes/2_Casquettes.md`, et les lignes `EXEMPLE` dans `Glossaire.md`, `Decisions_Log.md` et
`_systeme/journal.md`.

## La skill `google-workspace`

Skill optionnelle donnant accès à Drive, Docs, Sheets, Slides, Gmail et Calendar via le CLI `gws`.
Prérequis, usage et commande de suppression : `.agents/skills/README.md` et
`.agents/skills/google-workspace/SKILL.md`.

## Étendre le système

Pour ajouter une nouvelle branche (dossier de premier niveau ou sous-dossier), suis
`3_Ressources/_Templates/PATTERN_EXTENSIBILITE.md`.

## Plafonds

`.github/copilot-instructions.md` < 120 lignes · hub et note de contexte < 80 lignes · note
atomique < 150 lignes. Au dépassement : consolider ou extraire, jamais étendre (voir `config.md`
§5 pour les modifier).
