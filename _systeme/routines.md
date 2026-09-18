---
description: Deux routines d'entretien du système — revue hebdomadaire et rétro mensuelle.
created_date: <AAAA-MM-JJ>
---

# Routines

## 1. Revue hebdomadaire

À exécuter chaque semaine, dans cet ordre :

1. Régénérer les Registry Rapide des hubs à partir des champs `description:` des notes qu'ils
   référencent.
2. Présenter les entrées de `_systeme/a-valider.md` une par une : accepter, corriger ou jeter.
3. Signaler : fichiers sans `description:`, notes dépassant leur plafond (R4), captures
   d'`0_Inbox/` vieilles de plus de 7 jours.
4. Vider `0_Inbox/TEMP/`.
5. Commit.

## 2. Rétro mensuelle

À exécuter en début de mois, après l'archivage du journal (voir `_systeme/journal.md`). Distincte de
la revue hebdomadaire.

1. Repérer les répétitions ayant atteint 3 occurrences (candidates à une règle ou une skill, R8).
2. Purger le glossaire : proposer à la suppression les entrées jamais reservies depuis un mois
   (`3_Ressources/Glossaire/Glossaire.md`).
3. Repérer les règles du socle jamais déclenchées.
4. Repérer les outils externes sans usage réel sur le mois (voir `config.md` §7).
5. Relire toutes les décisions, évolutions et frictions du journal du mois écoulé : une répétition
   révèle-t-elle une règle mal formulée, une convention à clarifier ou une amélioration à proposer ?
6. Arbitrer chaque ligne de `_systeme/ameliorations.md`.

Sortie : pour chaque point, une décision **Garder / Supprimer / Reformuler**, soumise à ton accord.
La rétro ne modifie jamais seule le socle (`.github/copilot-instructions.md`).
