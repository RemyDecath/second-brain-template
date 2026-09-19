---
description: Système — fonctionnement du second brain lui-même : journal, routines, file d'améliorations.
created_date: 2026-09-18
---

# _systeme

Contient ce qui fait tourner le second brain, par opposition à ce qu'il contient. Y entre : toute
décision sur la **forme** du système — règles, conventions, workflows, outils, gouvernance.

Ce dossier n'est pas une branche IPCRA : il n'accueille jamais de contenu métier. Une décision
métier va dans `3_Ressources/Decisions_Log/`, pas ici.

## Périmètre

- **On y range** : décisions système datées, procédures d'entretien, inférences en attente de
  validation, propositions d'évolution du socle.
- **On n'y range pas** : projets, casquettes, ressources métier, captures — tout cela a sa branche
  IPCRA.

## Convention de nommage

Un fichier par fonction, en kebab-case, à plat. Les journaux mensuels clos partent dans
`journal/journal-AAAA-MM.md` : ce sous-dossier est exclu du contexte de l'agent, qui ne relit pas
l'historique au quotidien.

## Registry Rapide

| Élément | Description | Chemin |
|---|---|---|
| journal | Décisions et évolutions du système, mois en cours | `_systeme/journal.md` |
| routines | Revue hebdomadaire et rétro mensuelle | `_systeme/routines.md` |
| a-valider | Inférences en attente d'arbitrage | `_systeme/a-valider.md` |
| ameliorations | Propositions d'évolution du socle | `_systeme/ameliorations.md` |
| journal/ | Journaux mensuels clos — hors contexte, consultables sur demande | `_systeme/journal/` |

## Règle de sortie

Rien ne sort de `_systeme/` vers une branche IPCRA. Un journal mensuel clos descend dans
`journal/` et y reste : il n'est ni archivé dans `4_Archives/`, ni supprimé. La rétro mensuelle
peut proposer de purger une entrée devenue fausse, jamais de réécrire l'historique.
