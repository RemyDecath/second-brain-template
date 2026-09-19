---
description: File d'attente des propositions d'évolution du système — arbitrée à la rétro mensuelle.
created_date: 2026-09-18
---

# Améliorations

Remplace le cycle de vie des issues GitHub : toute proposition d'évolution du système passe par
cette file avant d'atteindre le socle.

## Règle

Le comptage se fait en deux temps, avec deux fichiers :

- La **1re occurrence** ne vient pas ici : elle s'écrit comme entrée `friction` dans
  `_systeme/journal.md`. C'est le journal qui compte de 1 à 2.
- La **2e occurrence** ouvre une ligne dans la table ci-dessous. C'est ce fichier qui compte de 2
  à 3.
- La **3e répétition réelle** autorise enfin une règle ou une skill, jamais par anticipation et
  jamais ajoutée seule au socle.

Sans entrée `friction` au journal, la 2e occurrence ne sera pas reconnue comme telle et le compteur
ne démarrera jamais. Cette file est vidée à la rétro mensuelle (`_systeme/routines.md`).

## Table

<!-- Exemple de forme :
| 2026-01-20 | Question posée 2 fois sur le format de date des captures | Inscrire la convention dans `0_Inbox/0_Inbox.md` | proposé | -->

| Date | Constat (nb d'occurrences) | Proposition | Statut |
|---|---|---|---|
