---
created_date: 2026-09-18 16:32:01
---
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
contexte homonyme (`Projet_X/Projet_X.md`) — c'est elle qu'on lit, jamais le dossier. Ce routage est
interne et obligatoire : l'utilisateur n'a pas à le demander dans son prompt.

Après toute création, qualification, transformation, déplacement, renommage, archivage ou
suppression, mets à jour tous les Registry Rapide concernés, retire les chemins devenus obsolètes,
préserve ou répare les wikilinks et vérifie les chemins. Ces mises à jour font partie de l'opération
par défaut ; ne demande pas à l'utilisateur de les rappeler.

Après toute écriture, fournis un résumé concis des fichiers et des changements effectués. Pour une
réponse fondée sur le vault, cite le chemin de la note source. Ces informations sont fournies par
défaut, sans demande particulière de l'utilisateur.

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

Toute décision, arbitrage ou évolution sur le fonctionnement du second brain va dans
`_systeme/journal.md` : organisation, règles, workflows, conventions, outils, intégrations et
gouvernance. Les frictions d'usage y sont conservées, mais ne limitent pas son périmètre. Quand une
conversation aboutit à une décision système explicite, consigne-la dans ce journal avant de
terminer, même si aucune friction n'est à l'origine de la décision. Les décisions métier vont dans
`3_Ressources/Decisions_Log/`.

Les procédures d'entretien (revue hebdo, rétro mensuelle) sont dans `_systeme/routines.md` — ne les
recopie pas ici, renvoie-y. Quand l'utilisateur demande une revue hebdomadaire ou une rétro
mensuelle, lis cette note et applique sa checklist complète sans attendre qu'il la recopie. Commence
par un diagnostic sans écriture, présente les décisions, puis attends un accord explicite avant
d'appliquer les changements.

## 7. Amélioration continue

Même question ou même correction posée 2 fois → propose une ligne dans
`_systeme/ameliorations.md`, sans jamais l'ajouter seul au socle. Règle ou skill : seulement après
la 3e répétition réelle.

## 8. Gouvernance d'écriture

Un *constat* (énoncé en direct par l'utilisateur, terme relevé, registry régénéré) s'écrit
directement. Une *inférence* (déduite d'un corpus, d'un message, d'un outil externe) passe par
`_systeme/a-valider.md`. Ce que `config.md` déclare sensible ne s'écrit jamais dans le vault, quelle
que soit la source. Lors d'une reformulation, conserve par défaut le frontmatter, les dates, les
faits, les sources et les wikilinks ; ne change que ce qui est demandé.

## 9. Inbox et TEMP

Toute capture brute entre par `0_Inbox/`. `0_Inbox/TEMP/` est réservé au travail jetable, vidé après
traitement. Lorsqu'une capture est qualifiée, déplace-la ou transforme-la vers la branche cible,
retire-la de l'Inbox et mets à jour les registries source et cible dans la même opération.

## 10. Création de note

Aucun gabarit n'est imposé : structure la note comme le sujet l'exige. Une seule contrainte, tout
fichier de contenu commence par un frontmatter — bloc `---` en **première ligne**, rien au-dessus —
avec une `description:` d'une phrase ; la revue hebdo régénère les registries à partir d'elle.

Avant toute création d'un dossier, d'un hub, d'une note de contexte ou d'une note atomique, lis
systématiquement le hub parent et `3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md`.
Cette lecture et l'application du pattern sont obligatoires par défaut : l'utilisateur n'a pas à
les demander dans son prompt. Pour une modification structurelle d'un contenu existant, applique
la même règle avant d'agir. Respecte ensuite la forme attendue et mets à jour le Registry Rapide
concerné.

Lorsqu'un contrôle de démarrage est demandé, vérifie au minimum les placeholders de `config.md`, les
Registry Rapide, les frontmatter, les captures de `0_Inbox/`, le contenu temporaire et les exemples
fictifs. Le contrôle est d'abord un diagnostic ; n'écris qu'après accord explicite.

## 11. Conventions Obsidian

Frontmatter YAML minimal (`description`, `created_date`), wikilinks `[[Nom]]`, lisibilité conservée
en Markdown brut même sans plugin.

## 12. Skills

Avant d'improviser une procédure récurrente, regarde `.agents/skills/`. La skill
`google-workspace` (optionnelle) donne accès à Docs, Sheets, Slides, Gmail et Calendar via le CLI
`gws` — voir `.agents/skills/google-workspace/SKILL.md`.
