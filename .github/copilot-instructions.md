# Instructions Copilot — Second Brain

Ce dépôt est un second brain personnel organisé en 5 dossiers (méthode IPCRA) :
`0_Inbox` capture le brut · `1_Projets` a des dates de fin · `2_Casquettes` sont des rôles
permanents · `3_Ressources` est réutilisable et transverse · `4_Archives` est terminé ou inactif.

## 1. Lire `config.md` en premier

En début de session, lis `config.md` : identité, casquettes actives, ton attendu, périmètre
sensible (R9) et outils externes branchés. Il rend ce socle générique.

## 2. Routage : hub → registry → cible

Pour toute demande, identifie le dossier IPCRA concerné, lis son hub homonyme
(`0_Inbox/0_Inbox.md`, `1_Projets/1_Projets.md`, `2_Casquettes/2_Casquettes.md`,
`3_Ressources/3_Ressources.md`, `4_Archives/4_Archives.md`), utilise son **Registry Rapide** pour
trouver le chemin exact, puis accède directement à la cible. Chaque dossier important a sa note de
contexte homonyme (`Projet_X/Projet_X.md`) — c'est elle qu'on lit, jamais le dossier.

## 3. Sobriété

Arrête-toi dès que la réponse est déterminable au niveau courant. N'ouvre une source secondaire
qu'en cas de donnée manquante, contradiction, ambiguïté réelle ou demande explicite de recoupement.
Aucune exploration à l'aveugle (`find`/`ls` global) quand un registry existe.

## 4. Plafonds

`copilot-instructions.md` < 120 lignes · hub et note de contexte < 80 · note atomique < 150. Au
dépassement, propose d'extraire le thème qui domine dans une note atomique — jamais d'extension,
jamais d'extraction sans accord.

## 5. Glossaire

Avant d'interpréter un acronyme ou un terme spécifique, consulte
`3_Ressources/Glossaire/Glossaire.md`. Terme absent ou ambigu → demande, ne devine pas. Après
clarification, mets à jour l'entrée.

## 6. Journal système et routines

Toute friction d'usage ou décision sur la forme du système va dans `_systeme/journal.md`. Les
procédures d'entretien (revue hebdo, rétro mensuelle) sont dans `_systeme/routines.md` — ne les
recopie pas ici, renvoie-y.

## 7. Amélioration continue

Même question ou même correction posée 2 fois → propose une ligne dans
`_systeme/ameliorations.md`, sans jamais l'ajouter seul au socle. Règle ou skill : seulement après
la 3e répétition réelle.

## 8. Gouvernance d'écriture

Un *constat* (énoncé en direct par l'utilisateur, terme relevé, registry régénéré) s'écrit
directement. Une *inférence* (déduite d'un corpus, d'un message, d'un outil externe) passe par
`_systeme/a-valider.md`. Ce que `config.md` déclare sensible ne s'écrit jamais dans le vault, quelle
que soit la source.

## 9. Inbox et TEMP

Toute capture brute entre par `0_Inbox/`. `0_Inbox/TEMP/` est réservé au travail jetable, vidé après
traitement.

## 10. Création de note

Aucun gabarit n'est imposé : structure la note comme le sujet l'exige. Une seule contrainte, tout
fichier de contenu commence par un frontmatter — bloc `---` en **première ligne**, rien au-dessus —
avec une `description:` d'une phrase ; la revue hebdo régénère les registries à partir d'elle. Pour
la forme attendue d'un hub, d'une note de contexte ou d'un nouveau dossier, renvoie à
`3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md`.

## 11. Conventions Obsidian

Frontmatter YAML minimal (`description`, `created_date`), wikilinks `[[Nom]]`, lisibilité conservée
en Markdown brut même sans plugin.

## 12. Skills

Avant d'improviser une procédure récurrente, regarde `.agents/skills/`. La skill
`google-workspace` (optionnelle) donne accès à Docs, Sheets, Slides, Gmail et Calendar via le CLI
`gws` — voir `.agents/skills/google-workspace/SKILL.md`.
