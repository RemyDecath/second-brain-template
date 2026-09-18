---
created_date: 2026-09-18 16:44:11
---
# Second Brain avec Obsidian et Copilot App

Ce dossier est un **second brain personnel prêt à l'emploi** : un endroit pour capturer ce qui
vous passe par la tête, retrouver vos informations et faire avancer vos projets.

Vous n'avez pas besoin de savoir coder, d'utiliser un terminal ou de connaître Markdown. Le système
repose sur deux applications qui ont des rôles différents :

- **Obsidian** sert à lire, naviguer dans le vault et prendre des notes rapides.
- **GitHub Copilot App** sert à comprendre, organiser et modifier le contenu du dossier.

> **Règle essentielle**
>
> - Les prises de notes manuelles se font **uniquement dans `0_Inbox/`**.
> - Toute organisation ou modification du dépôt se fait **dans Copilot App** : créer, déplacer,
>   renommer, corriger, transformer, archiver une note ou mettre à jour un registre.
> - Dans Obsidian, vous pouvez lire et naviguer partout, mais vous ne modifiez pas directement les
>   autres dossiers.

Cette règle évite que l'organisation du vault et les instructions de l'assistant se contredisent.

## Vocabulaire essentiel

Quelques mots reviennent souvent dans Copilot App. Les comprendre aide à obtenir de meilleures
réponses et à garder un second brain facile à entretenir.

| Terme | Explication simple | Dans ce projet |
|---|---|---|
| **Agent** | L'assistant qui lit les fichiers, raisonne et réalise votre demande. | Il applique les règles de `.github/copilot-instructions.md` et peut organiser le vault. |
| **Skill** | Un mode d'emploi spécialisé, parfois accompagné d'outils. | `.agents/skills/` contient par exemple une skill optionnelle pour Google Workspace. |
| **Contexte** | Les informations disponibles pour l'agent au moment où il répond. | La conversation en cours, les instructions du projet et les notes utiles ; pas forcément tout le vault. |
| **Session** | Une conversation de travail avec un objectif donné. | Elle sert à avancer sur un sujet cohérent, comme le setup ou un projet précis. |
| **Vault** | Le dossier de notes ouvert dans Obsidian. | Ici, c'est le dossier de ce modèle, également ouvert dans Copilot App. |

### Agent, skill et contexte : l'analogie du bureau

- L'application est le **bureau** dans lequel vous travaillez.
- L'agent est le **collègue** qui vous aide.
- Une skill est une **fiche de procédure** que ce collègue sait utiliser pour une tâche particulière.
- Le contexte est constitué des **documents posés sur le bureau** et de la conversation en cours.
- La session est la **réunion de travail** consacrée à un sujet.

Une skill n'est pas une note personnelle et ne remplace pas le vault. Elle explique comment réaliser
une tâche répétitive ou accéder à un outil ; n'activez ou n'installez que les skills dont vous avez
besoin.

### Pourquoi ne pas tout mettre dans une seule session ?

Une session n'est pas la mémoire permanente du second brain : les notes et les fichiers du vault le
sont. Une très longue conversation finit par contenir trop de sujets et de détails ; certains
éléments anciens peuvent être moins disponibles pour l'agent. Cela augmente le risque de :

- mélanger deux projets ou deux casquettes ;
- appliquer une ancienne décision au mauvais sujet ;
- modifier le mauvais fichier ;
- rendre les réponses plus lentes, moins claires et plus coûteuses à relire.

La bonne règle est **une session par objectif cohérent** :

- une session pour le premier setup ;
- une session par projet important ;
- une session dédiée à une casquette si le sujet est volumineux ;
- une session pour une revue hebdomadaire ou un traitement groupé de l'Inbox.

Gardez la même session pour les questions de suivi sur le même sujet. Démarrez-en une nouvelle
lorsque vous changez de projet, de casquette ou de type de tâche. Vous ne perdez pas les règles du
projet en changeant de session : Copilot App peut relire `config.md`, les instructions et les notes
pertinentes.

## 1. Ce qu'il faut installer

Avant de commencer, prévoyez :

1. Un compte GitHub avec accès à **GitHub Copilot**.
2. **Obsidian**, à télécharger depuis [obsidian.md](https://obsidian.md/download).
3. **GitHub Copilot App**, à installer depuis le site ou l'application officielle GitHub.
4. Une copie de ce dossier sur votre ordinateur.

Le dossier doit rester au même endroit après l'installation. Obsidian et Copilot App doivent ouvrir
**la même copie** du dossier, pas deux copies différentes.

## 2. Installer et ouvrir le vault dans Obsidian

1. Installez puis ouvrez Obsidian.
2. Choisissez **Ouvrir un dossier comme vault existant** (le libellé peut varier légèrement selon
   votre version).
3. Sélectionnez le dossier qui contient `README.md`, `config.md`, `0_Inbox/`, `1_Projets/` et les
   autres dossiers principaux.
4. Vérifiez que l'arborescence du vault apparaît bien à gauche.

Le modèle contient déjà ses réglages Obsidian. Aucun plugin supplémentaire n'est nécessaire pour
commencer. Si Obsidian demande si vous faites confiance à ce vault, acceptez uniquement si le
dossier provient bien de la source attendue.

### Ce que vous pouvez faire dans Obsidian

- lire vos notes ;
- suivre les liens entre les notes ;
- parcourir les dossiers ;
- écrire une **capture brute dans `0_Inbox/` uniquement**.

Pour toute autre écriture, fermez l'édition dans Obsidian et demandez la modification à Copilot App.

## 3. Installer et ouvrir le projet dans Copilot App

1. Installez puis ouvrez GitHub Copilot App.
2. Connectez-vous avec votre compte GitHub.
3. Ouvrez ou ajoutez un projet à partir du **même dossier local** que celui choisi dans Obsidian.
   Si le modèle est fourni depuis GitHub, utilisez l'option de l'application permettant d'ouvrir ou
   de récupérer le dépôt ; s'il est déjà sur votre ordinateur, choisissez ce dossier existant.
4. Ouvrez une conversation dans ce projet et vérifiez que Copilot App voit `README.md` et
   `config.md`.

Le fichier `.github/copilot-instructions.md` indique automatiquement à Copilot App comment travailler
dans ce second brain. Vous n'avez normalement pas besoin de le lire ou de le modifier.

### Vérification rapide

Copiez ce prompt dans Copilot App :

```text
Je viens d'ouvrir le second brain. Ne modifie aucun fichier pour l'instant.
Explique-moi brièvement le rôle de chaque dossier et rappelle-moi la règle
concernant les modifications manuelles. Signale les éventuels placeholders
encore présents dans config.md.
```

Si la réponse concerne bien ce dossier et ses règles, l'installation est terminée.

## 4. Comprendre les cinq dossiers

Le classement suit la méthode **IPCRA** :

| Dossier | À quoi sert-il ? | Exemple |
|---|---|---|
| `0_Inbox/` | Captures brutes, pas encore triées | idée, lien, tâche volante |
| `1_Projets/` | Engagements avec un objectif et une fin | déménagement, lancement d'un site |
| `2_Casquettes/` | Rôles permanents que vous occupez | parent, responsable d'association |
| `3_Ressources/` | Informations réutilisables et transverses | glossaire, décision, méthode |
| `4_Archives/` | Contenu terminé ou inactif | ancien projet clôturé |

### Comment décider où mettre quelque chose ?

- Vous ne savez pas encore quoi en faire ? **`0_Inbox/`**.
- Il y a un résultat à atteindre et une date de fin ? **`1_Projets/`**.
- Cela correspond à un rôle qui dure dans le temps ? **`2_Casquettes/`**.
- Cela peut servir dans plusieurs contextes ? **`3_Ressources/`**.
- C'est terminé ou inactif ? **`4_Archives/`**.

En cas de doute, mettez la capture dans `0_Inbox/` et laissez Copilot App vous proposer le
classement.

## 5. Premier réglage du projet

Effectuez ces étapes dans Copilot App, dans l'ordre. Les prompts sont prêts à copier-coller.
Ils décrivent uniquement votre intention. Le routage, la lecture de `config.md` et des hubs, le
respect du pattern, le frontmatter, la mise à jour des Registry Rapide et la cohérence des liens
sont des règles natives du système : vous n'avez pas à les répéter.

### Étape 1 — Faire expliquer le système

```text
Je débute avec ce second brain et je ne suis pas développeur.
Explique-moi le fonctionnement avec des mots simples :
1. ce que je fais dans Obsidian ;
2. ce que je fais dans Copilot App ;
3. comment une note passe de 0_Inbox à son emplacement définitif.
Ne modifie aucun fichier pour cette explication.
```

### Étape 2 — Personnaliser `config.md`

```text
Aide-moi à personnaliser config.md. Pose-moi les questions une par une
pour renseigner mon prénom, mon rôle, mon contexte, mes 2 à 4 casquettes,
ma langue, mon ton, mes conventions de nommage, mes plafonds, mon périmètre
sensible et les outils externes que j'utilise.

Ne devine aucune information et ne mets aucune donnée sensible dans le fichier.
Quand j'ai répondu, montre-moi un résumé complet et demande mon accord avant
d'écrire dans config.md.
```

### Étape 3 — Créer la première casquette

Remplacez les éléments entre crochets avant d'envoyer le prompt :

La lecture du hub concerné et de `3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md`
est une règle automatique de Copilot App. Vous n'avez pas besoin de la demander dans le prompt.

```text
À partir de config.md, crée ma première casquette « [NOM DE LA CASQUETTE] ».
Elle correspond à [DESCRIPTION DU RÔLE].

Propose les fichiers à créer et le contenu prévu, puis attends mon accord.
Après validation, crée ma casquette.
```

### Étape 4 — Créer le premier projet

```text
Crée un projet « [NOM DU PROJET] » dans 1_Projets/.
Objectif : [OBJECTIF].
Date ou période de fin prévue : [DATE OU PÉRIODE].

Propose d'abord la structure et les informations manquantes.
Après mon accord, crée ce projet.
```

### Étape 5 — Retirer les exemples fictifs

Les dossiers `EXEMPLE_Projet` et `EXEMPLE_Casquette` servent uniquement à comprendre le modèle.
Gardez-les tant que vous en avez besoin, puis demandez à Copilot App de les retirer :

```text
Le système est configuré. Supprime les exemples fictifs du modèle.
Présente les éléments que tu comptes retirer et attends ma confirmation.
Après confirmation, supprime uniquement ces exemples. Ne touche pas à mes notes.
```

### Étape 6 — Faire un contrôle de départ

```text
Fais un contrôle de démarrage du second brain sans modifier de fichier.
Présente les problèmes par ordre d'importance et propose une correction
pour chacun. Attends mon accord avant toute modification.
```

## 6. Utilisation au quotidien

### 6.1 Capturer une idée manuellement

Dans Obsidian, créez une nouvelle note **dans `0_Inbox/`**. Donnez-lui un nom simple, par exemple
`AAAA-MM-JJ-idee-cadeau.md`, puis notez ce que vous avez en tête sans chercher à le classer.

Une capture peut ressembler à ceci :

```markdown
---
description: Idée brute à qualifier.
created_date: AAAA-MM-JJ
---

# Idée cadeau

Texte libre, lien ou prochaine question.
```

Si vous ne savez pas comment nommer ou formater la capture, écrivez simplement dans une note de
`0_Inbox/` et demandez ensuite à Copilot App de la remettre en forme.

### 6.2 Faire qualifier une capture par Copilot App

```text
J'ai ajouté la capture 0_Inbox/AAAA-MM-JJ-idee-cadeau.md.
Lis-la et propose :
1. son classement entre Projet, Casquette, Ressource ou maintien temporaire
   dans Inbox ;
2. le nom et le chemin de la note cible ;
3. les éventuelles informations manquantes.

Ne déplace, ne renomme et ne modifie aucun fichier avant mon accord.
```

Après avoir validé la proposition :

```text
Applique le classement que nous venons de valider pour
0_Inbox/AAAA-MM-JJ-idee-cadeau.md.
Effectue la qualification.
```

### 6.3 Demander une modification

Pour corriger, compléter ou réorganiser une note qui n'est plus dans Inbox, passez toujours par
Copilot App :

```text
Dans la note [CHEMIN OU NOM DE LA NOTE], reformule la section [NOM DE LA SECTION]
pour la rendre plus claire et plus courte. Montre-moi la modification
proposée avant d'écrire dans le fichier.
```

### 6.4 Retrouver une information

```text
Je cherche ce que nous avons décidé au sujet de [SUJET].
Donne-moi la réponse.
Ne modifie aucun fichier.
```

### 6.5 Préparer une prochaine action

```text
À partir de la note [CHEMIN DU PROJET], donne-moi :
- l'état actuel ;
- les points bloquants ;
- les trois prochaines actions utiles ;
- les questions auxquelles je dois répondre.
Ne transforme pas cette analyse en nouvelles notes et ne modifie rien.
```

### 6.6 Archiver un projet terminé

```text
Le projet [NOM DU PROJET] est terminé.
Propose son archivage et attends mon accord. Après validation, archive-le
```

## 7. Entretien du système

Une fois par semaine, lancez ce prompt dans Copilot App :

```text
Fais la revue hebdomadaire du second brain.
```

Une fois par mois, utilisez :

```text
Fais la rétro mensuelle du second brain.
```

## 8. Règles à retenir

- **Inbox = capture manuelle.** Si vous hésitez, capturez là.
- **Copilot App = organisation et écriture du dépôt.** Même une petite correction dans un projet ou
  une ressource doit passer par l'application.
- **Obsidian = lecture, navigation et capture.** N'éditez pas directement les autres dossiers.
- **`4_Archives/` n'est pas relu automatiquement par Copilot App** : demandez explicitement la
  réactivation d'un élément archivé.
- Les informations sensibles déclarées dans `config.md` ne doivent jamais être écrites dans le
  vault.
- Relisez le résumé des fichiers modifiés par Copilot App avant de continuer votre travail.

## 9. En cas de problème

### Copilot App ne voit pas mes notes

Vérifiez qu'Obsidian et Copilot App utilisent exactement le même dossier local. Si vous avez ouvert
une seconde copie du modèle, fermez-la et rouvrez le dossier d'origine dans les deux applications.

### Une modification faite dans Copilot App n'apparaît pas dans Obsidian

Demandez à Obsidian de recharger le vault ou fermez puis rouvrez le vault. Vérifiez également que
Copilot App a bien terminé son opération et que le résumé indique le bon chemin de fichier.

### Je veux modifier directement une note située ailleurs que dans Inbox

Ne le faites pas dans Obsidian. Copiez votre demande dans Copilot App, par exemple :

```text
Modifie la note [CHEMIN] pour [OBJECTIF]. Montre-moi d'abord les changements
prévus, puis applique-les uniquement après ma confirmation.
```

## 10. Repères pour aller plus loin

- `config.md` contient vos préférences personnelles et votre périmètre sensible.
- `.github/copilot-instructions.md` contient les règles de travail de Copilot App.
- `3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md` explique comment créer une
  nouvelle branche ou une nouvelle note.
- `_systeme/routines.md` décrit l'entretien hebdomadaire et la rétro mensuelle.
- Le dossier `.agents/skills/` contient des compétences optionnelles pour Copilot App, notamment
  l'intégration Google Workspace. Elles ne sont pas nécessaires pour commencer.

Le modèle utilise du Markdown lisible, mais vous n'avez pas besoin d'en connaître la syntaxe :
demandez à Copilot App de créer ou de modifier les notes en respectant les règles du système.
