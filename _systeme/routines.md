---
description: Deux routines d'entretien du système — revue hebdomadaire et rétro mensuelle.
created_date: 2026-09-18
---

# Routines

## 1. Revue hebdomadaire

**Principe : la revue est incrémentale.** Elle ne relit jamais tout le vault — son coût doit rester
constant quand le nombre de notes grandit. Elle ne regarde que ce qui a bougé depuis la revue
précédente, dont la date est celle de la dernière entrée de type `revue` du journal :
`grep -n '^### .* — revue — ' _systeme/journal.md | tail -1`. En l'absence d'entrée précédente
(première revue), faire une passe complète, une seule fois.

Établir le périmètre :

```bash
git log --since="<date de la dernière revue>" --name-only --pretty=format: -- '*.md' | sort -u
```

Puis, dans cet ordre :

1. **Régénérer les Registry Rapide** des seules branches touchées, à partir des `description:` —
   sans ouvrir le corps des notes :
   `grep -r -m1 -H '^description:' <branche>/ --include='*.md'`
2. **Arbitrer `_systeme/a-valider.md`** : présenter les entrées une par une, accepter, corriger ou
   jeter.
3. **Signaler**, sur le périmètre établi uniquement :
   - fichiers sans `description:` → `grep -L '^description:' <fichiers modifiés>`
   - notes dépassant leur plafond (`config.md §5`) → `wc -l <fichiers modifiés>`, en ne retenant
     que les fichiers plafonnés ; journaux, files et lignes de table ne comptent pas. Une table
     trop longue se partitionne, elle ne s'extrait pas
   - captures d'`0_Inbox/` vieilles de plus de 7 jours (la date est dans le nom du fichier)
   - éléments déposés en fichier isolé à la racine de `4_Archives/` → à replacer dans un
     sous-dossier, sans quoi l'exclusion de contexte ne les couvre pas
4. **Vider `0_Inbox/TEMP/`.**
5. **Sauvegarder** : enregistrer l'état du vault dans l'historique (un *commit* git). C'est ce qui
   rend les versions précédentes récupérables — l'agent s'en charge, il suffit de le lui demander.
6. **Consigner** l'entrée de trace dans `_systeme/journal.md`, au format
   `### AAAA-MM-JJ — revue — Revue hebdomadaire` : ce qui a été traité, ce qui reste ouvert. Sans
   elle, la revue suivante ne sait pas où s'arrêter et repart sur une passe complète.

## 2. Rétro mensuelle

À exécuter en début de mois, après l'archivage du journal (voir `_systeme/journal.md`). Distincte de
la revue hebdomadaire.

Trois de ces points portent sur l'**usage** du système. Rien n'enregistre les consultations du
glossaire, les déclenchements de règles ou les appels d'outils : ces points se traitent soit par un
indice vérifiable, soit en posant la question. **Ne déduis jamais un usage que rien n'a consigné.**

1. **Répétitions arrivées à 3 occurrences** — croiser `_systeme/ameliorations.md` avec les entrées
   `friction` du mois : `grep -n '^### .* — friction — ' _systeme/journal.md`. Ce sont les seules
   candidates légitimes à une règle ou une skill.
2. **Glossaire** — proposer à la suppression les termes qui n'apparaissent **nulle part ailleurs**
   dans le vault : `grep -rl "<terme>" --include='*.md' .` ne renvoie que le glossaire lui-même. Un
   terme défini que rien n'emploie ne sert à rien. C'est un indice, pas une preuve : la suppression
   reste soumise à accord.
3. **Règles du socle** — poser la question, ne pas la deviner : « une règle t'a-t-elle gêné ce
   mois-ci, ou t'a-t-elle semblé inutile ? » Recouper avec les entrées `friction` qui citent une
   règle.
4. **Outils externes** (`config.md §7`) — même approche : demander lesquels ont réellement servi, et
   recouper avec les mentions d'outils dans le journal du mois.
5. **Relire le journal du mois** (`décision`, `friction`, `incident`) : une répétition révèle-t-elle
   une règle mal formulée, une convention à clarifier, une amélioration à proposer ?
6. **Tables proches de l'illisible** (glossaire, journal de décisions, registries d'archives) —
   proposer leur partition.
7. **Décisions métier** — relire `3_Ressources/Decisions_Log/` : une décision est-elle devenue
   caduque ? La signaler, jamais la supprimer d'initiative (`3_Ressources/3_Ressources.md`).
8. **Arbitrer chaque ligne** de `_systeme/ameliorations.md`.

Sortie : pour chaque point, une décision **Garder / Supprimer / Reformuler**, soumise à ton accord.
La rétro ne modifie jamais seule le socle (`.github/copilot-instructions.md`). Elle se termine par
une entrée `### AAAA-MM-JJ — revue — Rétro mensuelle` dans le journal.
