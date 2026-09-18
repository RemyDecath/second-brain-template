---
description: Journal système — frictions d'usage et décisions sur la forme du système, datées.
created_date: <AAAA-MM-JJ>
---

# Journal système

Consigne toute friction d'usage et toute décision sur *la forme* du système (organisation, règles,
outils, conventions). Jamais de contenu métier — pour ça, voir `3_Ressources/Decisions_Log/`.

## Règles

- Une entrée par sujet, ajoutée en fin de fichier, jamais de réécriture rétroactive.
- Une entrée récente peut en amender une ancienne en la référençant explicitement.
- Écriture directe, sans validation préalable (c'est un constat, pas une inférence — R9).
- Au changement de mois, archivage du contenu dans `journal-AAAA-MM.md` et remise à zéro de
  l'en-tête de ce fichier.

## Format d'une entrée

<!-- ## AAAA-MM-JJ — <sujet court>
**Décision** : ...
**Motif** : ...
**Effet** : ... -->

## Entrées

<!-- EXEMPLE — supprimer après appropriation. -->

## 2025-01-08 — Extraction de « Suivi_Cotisations » hors de la casquette Trésorerie

**Décision** : Le suivi des cotisations des adhérents est extrait de la note de contexte
`EXEMPLE_Casquette.md` vers une note atomique dédiée.
**Motif** : La note de contexte approchait son plafond de 80 lignes, dominée par le détail des
cotisations (R4).
**Effet** : `EXEMPLE_Casquette.md` reste sous le plafond ; le détail vit dans
`EXEMPLE_Note_Atomique.md`, référencé dans son registry des notes atomiques.
