---
description: Configuration personnelle du second brain — à remplir après clonage.
created_date: <AAAA-MM-JJ>
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

- **Casse des noms de fichiers** : `<ex. Snake_Case, kebab-case>`.
- **Format de date** : `<ex. AAAA-MM-JJ>`.

## 5. Plafonds

Valeurs par défaut, modifiables ici :

- `.github/copilot-instructions.md` : < 120 lignes.
- Hub et note de contexte : < 80 lignes.
- Note atomique : < 150 lignes.

## 6. Périmètre sensible

Ce qui ne doit **jamais** être écrit dans le vault, quelle que soit la source (alimente la règle
de gouvernance d'écriture R9) :

- `<ex. santé d'autrui>`
- `<ex. rémunération, la sienne ou celle d'un tiers>`
- `<ex. données confidentielles d'un employeur ou d'un client>`

## 7. Outils externes branchés

| Outil | Ce qu'il peut lire | Action directe, sans demander | Accord obligatoire |
|---|---|---|---|
| `google-workspace` | Docs, Slides, Sheets, Gmail, Calendar | Export local d'un fichier vers un dossier temporaire | Toute écriture chez Google : création, modification, envoi, partage |
| `<autre outil>` | `<ce qu'il peut lire>` | `<ce qu'il peut faire seul>` | `<ce qui nécessite ton accord>` |
