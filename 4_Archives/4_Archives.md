---
description: Archives — terminé ou inactif, hors contexte IA par défaut.
created_date: <AAAA-MM-JJ>
---

# 4_Archives

Contient tout ce qui est terminé (projets clos) ou inactif (casquettes abandonnées, ressources
obsolètes). Y entre : uniquement du contenu déplacé depuis un autre dossier, jamais créé ici.

## Périmètre

- **On y range** : ce qui ne sert plus au quotidien mais mérite d'être conservé.
- **On n'y range pas** : quoi que ce soit encore actif — dans le doute, laisser à sa place d'origine.

## Convention de nommage

On conserve le nom et la structure d'origine du dossier déplacé, sans renommage.

## Registry Rapide

<!-- Une ligne par élément archivé. Exemple : -->
<!-- | Ancien_Projet | Clos le AAAA-MM-JJ | 4_Archives/Ancien_Projet/ | -->

| Élément | Description | Chemin |
|---|---|---|

## Règle de sortie

Le contenu de `4_Archives/` sort du contexte IA via `.copilotignore` (R12) : l'agent lit ce hub — il
lui dit ce qui a été archivé et où — mais pas les dossiers archivés eux-mêmes. Un élément n'en
ressort que sur demande explicite (réactivation d'un projet, par exemple), en le déplaçant hors de
`4_Archives/`.
