---
description: Ressources — contenu réutilisable et transverse (glossaire, décisions, templates).
created_date: <AAAA-MM-JJ>
---

# 3_Ressources

Contient ce qui sert à plusieurs projets ou casquettes à la fois : glossaire, journal des décisions
métier, templates de création de note. Y entre : tout contenu de référence, pas d'action en cours.

## Périmètre

- **On y range** : définitions, décisions transverses, gabarits de fichiers.
- **On n'y range pas** : un projet ou une casquette en cours (→ dossiers dédiés), du contenu
  archivé et inactif (→ `4_Archives/`).

## Convention de nommage

Un sous-dossier par type de ressource, avec sa note de contexte homonyme :
`Glossaire/Glossaire.md`, `Decisions_Log/Decisions_Log.md`, `_Templates/` (préfixe `_` = hors
routage IA, listé dans `.copilotignore`).

## Registry Rapide

| Élément | Description | Chemin |
|---|---|---|
| Glossaire | Termes et acronymes du domaine | 3_Ressources/Glossaire/Glossaire.md |
| Decisions_Log | Décisions métier, table chronologique | 3_Ressources/Decisions_Log/Decisions_Log.md |
| _Templates | Gabarits de création de note | 3_Ressources/_Templates/ |

## Règle de sortie

Une ressource devenue obsolète (terme jamais reservi, décision caduque) est signalée en rétro
mensuelle, jamais supprimée d'initiative par l'agent.
