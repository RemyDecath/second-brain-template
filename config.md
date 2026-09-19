---
description: Configuration personnelle du second brain — à remplir après clonage.
created_date: 2026-09-18
---

# Configuration

> Ce fichier isole tout ce qui est propre à toi, pour que le reste du dépôt reste générique.
> Lu par l'agent en début de session, avant toute autre chose.

## 1. Identité & usage

- **Prénom** : `<Prénom>` — comment l'agent te désigne.
- **Rôle** : `<ex. Développeuse, Consultant indépendant, Étudiant>`.
- **Contexte** : `<pro | perso | mixte>` — influence le ton et les exemples que l'agent choisit.

## 2. Casquettes principales

Rôles permanents (sans date de fin), 2 à 4 maximum. Chacun devient un dossier dans
`2_Casquettes/`.

- `<Casquette 1, ex. « Référent Sécurité »>`
- `<Casquette 2, ex. « Bénévole association X »>`

## 3. Ton et langue

- **Langue** : `<français | anglais | ...>`.
- **Ton** : `<ex. direct et concis, pédagogique, informel>`.

## 4. Conventions

Ces deux choix ne portent que sur les **noms de notes libres** (notes atomiques, ressources). Trois
règles sont structurelles et ne se configurent pas : un dossier et sa note de contexte portent le
même nom (`Projet_X/Projet_X.md`), un hub porte le nom de son dossier, une capture d'Inbox est
datée (`AAAA-MM-JJ-nom-court.md`).

- **Casse des noms de fichiers** : `<ex. Snake_Case, kebab-case>`.
- **Format de date** : `<ex. AAAA-MM-JJ>`.

## 5. Plafonds

**Source de vérité unique** : le socle lit ces valeurs ici et ne les répète pas. Le socle dit *quand*
un plafond s'applique ; cette table dit *combien*. Modifiables, à condition de rester des nombres.

| Fichier | Plafond |
|---|---|
| `.github/copilot-instructions.md` | < 150 lignes |
| `config.md` (ce fichier), `README.md` | < 80 lignes |
| Hub, note de contexte, procédure | < 80 lignes |
| Note atomique, capture d'`0_Inbox/` | < 150 lignes |
| Journaux, tables, files d'attente | aucun plafond — leur croissance est bornée autrement |

## 6. Périmètre sensible

Ce qui ne doit **jamais** être écrit dans le vault, quelle que soit la source — y compris si tu le
dictes toi-même à l'agent :

- `<ex. santé d'autrui>`
- `<ex. rémunération, la sienne ou celle d'un tiers>`
- `<ex. données confidentielles d'un employeur ou d'un client>`

## 7. Outils externes branchés

| Outil | Ce qu'il peut lire | Action directe, sans demander | Accord obligatoire |
|---|---|---|---|
| `google-workspace` | Docs, Slides, Sheets, Gmail, Calendar | Export local d'un fichier vers un dossier temporaire | Toute écriture chez Google : création, modification, envoi, partage |
| `<autre outil>` | `<ce qu'il peut lire>` | `<ce qu'il peut faire seul>` | `<ce qui nécessite ton accord>` |
