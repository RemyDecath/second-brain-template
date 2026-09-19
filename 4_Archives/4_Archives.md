---
description: Archives — terminé ou inactif, hors contexte IA par défaut.
created_date: 2026-09-18
---

# 4_Archives

Contient tout ce qui est terminé (projets clos) ou inactif (casquettes abandonnées, ressources
obsolètes). Y entre : uniquement du contenu déplacé depuis un autre dossier, jamais créé ici.

## Périmètre

- **On y range** : ce qui ne sert plus au quotidien mais mérite d'être conservé.
- **On n'y range pas** : quoi que ce soit encore actif — dans le doute, laisser à sa place d'origine.

## Convention de nommage

On conserve le nom et la structure d'origine du dossier déplacé, sans renommage.

**Toujours dans un sous-dossier**, jamais en fichier isolé à la racine de `4_Archives/`. Une note
seule à archiver reçoit son propre dossier (`Ancienne_Note/Ancienne_Note.md`). C'est ce qui rend
l'exclusion de contexte effective : le motif `.copilotignore` ne couvre que les sous-dossiers.

## Registry Rapide

<!-- Une ligne par élément archivé. Exemple : -->
<!-- | Ancien_Projet | Clos le AAAA-MM-JJ | 4_Archives/Ancien_Projet/ | -->

| Élément | Description | Chemin |
|---|---|---|

## Règle de sortie

Le contenu de `4_Archives/` sort du contexte IA de deux façons : `.copilotignore` l'exclut, et le
socle interdit sa lecture (section 10) — la règle compte plus que l'exclusion, dont le support
dépend de l'application. L'agent lit ce hub, qui lui dit ce qui a été archivé et où ; cela suffit à
répondre sans ouvrir les dossiers archivés.

Un élément n'en ressort que sur demande explicite (réactivation d'un projet, par exemple), en le
déplaçant hors de `4_Archives/`. L'agent effectue ce déplacement **sans avoir pu lire le fichier au
préalable** : c'est normal, il le lit une fois sorti.
