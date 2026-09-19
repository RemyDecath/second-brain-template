---
description: Boîte de réception — capture brute, non qualifiée, à traiter.
created_date: 2026-09-18
---

# 0_Inbox

Contient toute capture rapide non encore triée : idée, lien, note vocale transcrite, tâche volante.
Y entre : tout ce qui n'a pas encore de dossier de destination évident.

## Périmètre

- **On y range** : captures du quotidien, en attente de qualification.
- **On n'y range pas** : ce qui a déjà une destination claire (projet, casquette, ressource) — le
  déposer directement à la bonne place.
- `TEMP/` est réservé au travail jetable : son contenu est supprimé après traitement, jamais versionné
  durablement.

## Convention de nommage

`AAAA-MM-JJ-<nom-court>.md`. Une capture reste brute : un frontmatter avec `description:`, un titre,
le contenu tel quel. La mise en forme, c'est le travail de la qualification qui suivra.

## Registry Rapide

<!-- Une ligne par capture en attente de tri. Exemple : -->
<!-- | 2025-01-15-idee-atelier | Idée d'atelier à creuser | 0_Inbox/2025-01-15-idee-atelier.md | -->

| Élément | Description | Chemin |
|---|---|---|

## Règle de sortie

Une capture quitte l'inbox dès qu'elle est qualifiée : elle est déplacée ou transformée en note dans
`1_Projets/`, `2_Casquettes/` ou `3_Ressources/`, puis retirée d'ici. Rien ne doit dormir plus de 7
jours (signalé en revue hebdo).
