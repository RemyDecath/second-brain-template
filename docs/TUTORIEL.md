---
description: Tutoriel complet du second brain — installation, réglage, usage quotidien, dépannage.
created_date: 2026-09-18 16:44:11
---
# Tutoriel — Second Brain avec Obsidian et Copilot App

Ce dossier est un **second brain personnel prêt à l'emploi** : un endroit pour capturer ce qui vous passe par la tête, retrouver vos informations et faire avancer vos projets.

Vous n'avez pas besoin de savoir coder, d'utiliser un terminal ou de connaître Markdown. Le système repose sur deux applications qui ont des rôles différents :
- **Obsidian** sert à lire, naviguer dans le vault et prendre des notes rapides.
- **GitHub Copilot App** sert à comprendre, organiser et modifier le contenu du dossier.

> **La seule règle à connaître avant de commencer**
>
> - Les prises de notes manuelles se font **uniquement dans `0_Inbox/`**.
> - Pour organiser ou modifier le reste du dépôt, utilisez **Copilot App**.

Vous découvrirez les autres règles, le vocabulaire de Copilot App et le fonctionnement des sessions après l'installation, au moment où ces notions deviennent utiles.

## 1. Installer et mettre à l'abri

Avant de commencer, prévoyez :

1. Un compte GitHub avec accès à **GitHub Copilot**.
2. **Obsidian**, à télécharger depuis [obsidian.md](https://obsidian.md/download).
3. **GitHub Copilot App**, à installer directement depuis notre application interne **Workspace One**. N'utilisez pas le site officiel GitHub pour cette installation.
4. **Google Drive pour ordinateur**, à installer également depuis **Workspace One**. C'est votre filet de sécurité : voir l'étape 1.2.

### 1.1 Récupérer une copie du modèle

Le modèle vit sur GitHub. Deux façons de le récupérer, aucune ne demande de savoir coder :

- **Le plus simple** : sur la page GitHub du modèle, bouton vert **Code**, puis **Download ZIP**. Décompressez l'archive, vous obtenez un dossier prêt à l'emploi.
- **Le plus durable** : cliquez sur **Fork** en haut à droite pour créer votre propre copie sur GitHub, installez [GitHub Desktop](https://desktop.github.com/), puis utilisez **Clone repository** pour la récupérer sur votre ordinateur. C'est cette voie qui permet de recevoir plus tard les améliorations du modèle (section 12) et de conserver un historique de vos notes.

Renommez le dossier comme vous le souhaitez, par exemple `Second-Brain`.

### 1.2 Le mettre à l'abri avec Google Drive

**Ce dossier va contenir votre mémoire de travail. S'il n'existe qu'à un seul endroit, une panne de disque vous le fait perdre en entier.** Google Drive pour ordinateur règle le problème sans rien changer à vos habitudes : le dossier reste un dossier normal sur votre ordinateur, et chaque modification part automatiquement dans le cloud.

1. Ouvrez **Workspace One**, recherchez **Google Drive pour ordinateur** et lancez son installation depuis l'application interne, puis connectez-vous avec votre compte Google.
2. L'installation ajoute un emplacement **Google Drive** à votre ordinateur : un lecteur (souvent `G:`) sous Windows, un dossier `Google Drive` dans le Finder sous macOS. Ouvrez-le, puis entrez dans **Mon Drive**.
3. **Déplacez-y le dossier du second brain** récupéré à l'étape 1.1.

Faites ce déplacement **maintenant**, avant d'ouvrir le dossier dans Obsidian et dans Copilot App. Si vous le déplacez plus tard, les deux applications continueront de pointer vers l'ancien emplacement et ne verront plus vos notes.

### 1.3 Le rendre disponible hors connexion — indispensable

Par défaut, Google Drive **ne télécharge pas** les fichiers sur votre disque : il se contente de les afficher et ne va les chercher qu'au moment où vous les ouvrez. Obsidian et Copilot App, eux, ont besoin des fichiers réellement présents. Sans ce réglage, vous verrez des notes vides ou des erreurs de lecture, et l'agent travaillera sur des fichiers qu'il ne peut pas ouvrir.

1. Dans l'emplacement Google Drive, faites un **clic droit sur le dossier du second brain**.
2. Choisissez **Accès hors connexion** (le libellé peut varier selon la version).
3. Sélectionnez **Disponible hors connexion**.
4. Attendez que l'icône de synchronisation indique que le dossier est entièrement téléchargé.

Le dossier vit alors à deux endroits à la fois : sur votre disque, donc rapide et utilisable sans internet, et sur Google Drive, donc récupérable si votre ordinateur tombe en panne.

> **Un seul ordinateur à la fois.** Ne travaillez pas sur le même second brain depuis deux ordinateurs simultanément : Google Drive synchroniserait les deux versions et créerait des doublons de fichiers. Fermez Obsidian et Copilot App sur le premier avant d'ouvrir sur le second.

### 1.4 Avant de continuer

Le dossier doit maintenant rester à cet emplacement. Obsidian et Copilot App devront ouvrir **la même copie**, pas deux copies différentes. Notez son chemin quelque part, les étapes suivantes en ont besoin.

## 2. Installer et ouvrir le vault dans Obsidian

1. Installez puis ouvrez Obsidian.
2. Choisissez **Ouvrir un dossier comme vault existant** (le libellé peut varier légèrement selon votre version).
3. Sélectionnez le dossier qui contient `README.md`, `config.md`, `0_Inbox/`, `1_Projets/` et les autres dossiers principaux.
4. Vérifiez que l'arborescence du vault apparaît bien à gauche.

Aucun plugin supplémentaire n'est nécessaire pour commencer : le modèle fonctionne avec Obsidian tel qu'il s'installe. Vos réglages Obsidian (thème, raccourcis, plugins) restent propres à votre ordinateur et ne sont pas partagés avec le modèle. Si Obsidian demande si vous faites confiance à ce vault, acceptez uniquement si le dossier provient bien de la source attendue.

### Ce que vous pouvez faire dans Obsidian

- lire vos notes ;
- suivre les liens entre les notes ;
- parcourir les dossiers ;
- écrire une **capture brute dans `0_Inbox/` uniquement**.

Pour toute autre écriture, fermez l'édition dans Obsidian et demandez la modification à Copilot App.

## 3. Installer et ouvrir le projet dans Copilot App

1. Ouvrez **Workspace One**, recherchez **GitHub Copilot App** et lancez son installation depuis l'application interne. N'utilisez pas le site officiel GitHub.
2. Ouvrez GitHub Copilot App et connectez-vous avec votre compte GitHub.
3. Ouvrez ou ajoutez un projet à partir du **même dossier local** que celui choisi dans Obsidian. Si le modèle est fourni depuis GitHub, utilisez l'option de l'application permettant d'ouvrir ou de récupérer le dépôt ; s'il est déjà sur votre ordinateur, choisissez ce dossier existant.
4. Ouvrez une conversation dans ce projet et vérifiez que Copilot App voit `README.md` et `config.md`.
5. Dans le sélecteur de modèle, choisissez **GPT-5.6 Luna** et réglez le raisonnement sur **Médium**. Faites de ce réglage votre valeur par défaut pour éviter une surconsommation de facturation ; ne sélectionnez un niveau supérieur que pour une demande exceptionnellement complexe.

Le fichier `.github/copilot-instructions.md` indique automatiquement à Copilot App comment travailler dans ce second brain. Vous n'avez normalement pas besoin de le lire ou de le modifier.

### Vérification rapide

Copiez ce prompt dans Copilot App :

```text
Je viens d'ouvrir le second brain. Ne modifie aucun fichier pour l'instant.
Explique-moi brièvement le rôle de chaque dossier et rappelle-moi la règle
concernant les modifications manuelles. Signale les éventuels placeholders
encore présents dans config.md.
```

Si la réponse concerne bien ce dossier et ses règles, l'installation est terminée.

## 4. Comprendre Copilot App

Vous pouvez commencer à utiliser le système sans mémoriser son vocabulaire. Ces quelques repères deviennent utiles maintenant que les applications sont installées.

### Vocabulaire essentiel

| Terme        | Explication simple                                                   | Dans ce projet                                                                                          |
| ------------ | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Agent**    | L'assistant qui lit les fichiers, raisonne et réalise votre demande. | Il applique les règles de `.github/copilot-instructions.md` et peut organiser le vault.                 |
| **Skill**    | Un mode d'emploi spécialisé, parfois accompagné d'outils.            | `.agents/skills/` peut contenir des compétences optionnelles pour Copilot App.                          |
| **Contexte** | Les informations disponibles pour l'agent au moment où il répond.    | La conversation en cours, les instructions du projet et les notes utiles ; pas forcément tout le vault. |
| **Session**  | Une conversation de travail avec un objectif donné.                  | Elle sert à avancer sur un sujet cohérent, comme le setup ou un projet précis.                          |
| **Vault**    | Le dossier de notes ouvert dans Obsidian.                            | Ici, c'est le dossier de ce modèle, également ouvert dans Copilot App.                                  |

### Agent, skill et contexte : l'analogie du bureau

- L'application est le **bureau** dans lequel vous travaillez.
- L'agent est le **collègue** qui vous aide.
- Une skill est une **fiche de procédure** que ce collègue sait utiliser pour une tâche particulière.
- Le contexte est constitué des **documents posés sur le bureau** et de la conversation en cours.
- La session est la **réunion de travail** consacrée à un sujet.

Une skill n'est pas une note personnelle et ne remplace pas le vault. Elle explique comment réaliser une tâche répétitive ou accéder à un outil ; n'activez ou n'installez que les skills dont vous avez besoin.

### Pourquoi ne pas tout mettre dans une seule session ?

Une session n'est pas la mémoire permanente du second brain : les notes et les fichiers du vault le sont. Une très longue conversation finit par contenir trop de sujets et de détails ; certains éléments anciens peuvent être moins disponibles pour l'agent. Cela augmente le risque de :

- mélanger deux projets ou deux casquettes ;
- appliquer une ancienne décision au mauvais sujet ;
- modifier le mauvais fichier ;
- rendre les réponses plus lentes, moins claires et plus coûteuses à relire.

La règle pratique est **une tâche par session** : évitez de tout faire au même endroit. Une session doit rester centrée sur un seul objectif cohérent.

Cela optimise le contexte fourni à Copilot App : avec moins de sujets concurrents à distinguer, l'agent limite les réponses ou modifications hors sujet, donc les hallucinations. Des sessions plus courtes consomment aussi moins de contexte et contribuent à maîtriser les coûts.

- une session pour le premier setup ;
- une session par projet important ;
- une session dédiée à une casquette si le sujet est volumineux ;
- une session pour une revue hebdomadaire ou un traitement groupé de l'Inbox.

Ne mélangez pas dans une même session une question sur un projet, le tri de l'Inbox, une revue hebdomadaire et une modification du fonctionnement du système. Ouvrez une nouvelle session dès que vous changez de tâche ou de sujet ; cela aide Copilot App à conserver le bon contexte et à éviter les modifications au mauvais endroit.

Gardez la même session pour les questions de suivi sur le même sujet. Vous ne perdez pas les règles du projet en changeant de session : Copilot App peut relire `config.md`, les instructions et les notes pertinentes.

## 5. Comprendre les cinq dossiers

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

En cas de doute, mettez la capture dans `0_Inbox/` et laissez Copilot App vous proposer le classement.

Deux autres dossiers existent, que vous n'avez pas à alimenter vous-même : `_systeme/` (le fonctionnement du système — journal des décisions, routines d'entretien) et `docs/` (ce tutoriel et des exemples remplis). `docs/` est volontairement invisible pour Copilot App, pour ne pas encombrer son contexte à chaque conversation.

## 6. Premier réglage du projet

Effectuez ces étapes dans Copilot App, dans l'ordre. Les prompts sont prêts à copier-coller. Ils décrivent uniquement votre intention. Le routage, la lecture de `config.md` et des hubs, le respect du pattern, le frontmatter, la mise à jour des Registry Rapide et la cohérence des liens sont des règles natives du système : vous n'avez pas à les répéter.

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

La lecture du hub concerné et de `3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md` est une règle automatique de Copilot App. Vous n'avez pas besoin de la demander dans le prompt.

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

### Étape 5 — Faire un contrôle de départ

```text
Fais un contrôle de démarrage du second brain sans modifier de fichier.
Présente les problèmes par ordre d'importance et propose une correction
pour chacun. Attends mon accord avant toute modification.
```

## 7. Utilisation au quotidien

### 7.1 Capturer une idée manuellement

Dans Obsidian, créez une nouvelle note **dans `0_Inbox/`**. Donnez-lui un nom simple, par exemple `AAAA-MM-JJ-idee-cadeau.md`, puis notez ce que vous avez en tête sans chercher à le classer.

Une capture peut ressembler à ceci :

```markdown
---
description: Idée brute à qualifier.
created_date: AAAA-MM-JJ
---

# Idée cadeau

Texte libre, lien ou prochaine question.
```

Si vous ne savez pas comment nommer ou formater la capture, écrivez simplement dans une note de `0_Inbox/` et demandez ensuite à Copilot App de la remettre en forme.

### 7.2 Faire qualifier une capture par Copilot App

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

### 7.3 Demander une modification

Pour corriger, compléter ou réorganiser une note qui n'est plus dans Inbox, passez toujours par Copilot App :

```text
Dans la note [CHEMIN OU NOM DE LA NOTE], reformule la section [NOM DE LA SECTION]
pour la rendre plus claire et plus courte. Montre-moi la modification
proposée avant d'écrire dans le fichier.
```

### 7.4 Retrouver une information

```text
Je cherche ce que nous avons décidé au sujet de [SUJET].
Donne-moi la réponse.
Ne modifie aucun fichier.
```

### 7.5 Préparer une prochaine action

```text
À partir de la note [CHEMIN DU PROJET], donne-moi :
- l'état actuel ;
- les points bloquants ;
- les trois prochaines actions utiles ;
- les questions auxquelles je dois répondre.
Ne transforme pas cette analyse en nouvelles notes et ne modifie rien.
```

### 7.6 Archiver un projet terminé

```text
Le projet [NOM DU PROJET] est terminé.
Propose son archivage et attends mon accord. Après validation, archive-le
```

## 8. Entretien du système

Une fois par semaine, lancez ce prompt dans Copilot App :

```text
Fais la revue hebdomadaire du second brain.
```

Une fois par mois, utilisez :

```text
Fais la rétro mensuelle du second brain.
```

## 9. Règles à retenir

- **Inbox = capture manuelle.** Si vous hésitez, capturez là.
- **Copilot App = organisation et écriture du dépôt.** Même une petite correction dans un projet ou une ressource doit passer par l'application.
- **Modèle et coût : GPT-5.6 Luna + raisonnement Médium par défaut.** Vérifiez ce réglage au début d'une nouvelle session et n'augmentez le raisonnement que lorsque la tâche le nécessite.
- **Obsidian = lecture, navigation et capture.** N'éditez pas directement les autres dossiers.
- **`4_Archives/` n'est pas relu automatiquement par Copilot App** : demandez explicitement la réactivation d'un élément archivé.
- Les informations sensibles déclarées dans `config.md` ne doivent jamais être écrites dans le vault.
- Relisez le résumé des fichiers modifiés par Copilot App avant de continuer votre travail.
- **Votre sauvegarde tient à deux conditions** (section 1.2) : le dossier est dans *Mon Drive*, et il est marqué *Disponible hors connexion*. Vérifiez-le de temps en temps — l'icône de Google Drive dans la barre des tâches doit indiquer que tout est synchronisé.

## 10. En cas de problème

### Copilot App ne voit pas mes notes

Vérifiez qu'Obsidian et Copilot App utilisent exactement le même dossier local. Si vous avez ouvert une seconde copie du modèle, fermez-la et rouvrez le dossier d'origine dans les deux applications.

### Une modification faite dans Copilot App n'apparaît pas dans Obsidian

Demandez à Obsidian de recharger le vault ou fermez puis rouvrez le vault. Vérifiez également que Copilot App a bien terminé son opération et que le résumé indique le bon chemin de fichier.

### Je veux modifier directement une note située ailleurs que dans Inbox

Ne le faites pas dans Obsidian. Copiez votre demande dans Copilot App, par exemple :

```text
Modifie la note [CHEMIN] pour [OBJECTIF]. Montre-moi d'abord les changements
prévus, puis applique-les uniquement après ma confirmation.
```

### J'ai déjà modifié une note à la main, en dehors de `0_Inbox/`

Cela arrive et ce n'est pas grave. Le risque n'est pas la modification elle-même, c'est qu'elle décale le reste : un registre qui ne pointe plus au bon endroit, un lien cassé, un frontmatter abîmé. Faites vérifier :

```text
J'ai modifié à la main la note [CHEMIN], en dehors de 0_Inbox.
Vérifie ce que cette modification a pu casser : frontmatter, Registry Rapide,
wikilinks, plafond de la note. Présente les problèmes et propose une correction
pour chacun. N'écris rien avant mon accord.
```

Si la note est vraiment abîmée, Google Drive conserve ses versions précédentes : clic droit sur le fichier dans l'emplacement Google Drive, puis **Gérer les versions**.

### Une note apparaît vide, ou Obsidian dit qu'il ne peut pas l'ouvrir

C'est presque toujours le réglage hors connexion qui manque (section 1.3). Vérifiez que le dossier du second brain est bien marqué **Disponible hors connexion** dans Google Drive, et attendez la fin du téléchargement.

### Je vois des fichiers en double, avec un nom du type « ... (1).md »

Deux ordinateurs ont travaillé sur le même second brain en même temps. Fermez Obsidian et Copilot App partout sauf sur une machine, puis demandez le ménage :

```text
Le vault contient des fichiers en double créés par la synchronisation
(noms du type « ... (1).md »). Compare chaque doublon à l'original,
dis-moi lequel garder, et attends mon accord avant de supprimer quoi que ce soit.
```

## 11. Repères pour aller plus loin

- `config.md` contient vos préférences personnelles et votre périmètre sensible.
- `.github/copilot-instructions.md` contient les règles de travail de Copilot App.
- `3_Ressources/Pattern_Extensibilite/Pattern_Extensibilite.md` explique comment créer une nouvelle branche ou une nouvelle note.
- `docs/exemples/` contient un projet et une casquette entièrement remplis, à lire comme modèles.
- `_systeme/routines.md` décrit l'entretien hebdomadaire et la rétro mensuelle.
- `_systeme/_systeme.md` est le point d'entrée du dossier système.
- Le dossier `.agents/skills/` peut contenir des compétences optionnelles pour Copilot App. Elles ne sont pas nécessaires pour commencer.

Le modèle utilise du Markdown lisible, mais vous n'avez pas besoin d'en connaître la syntaxe : demandez à Copilot App de créer ou de modifier les notes en respectant les règles du système.

## 12. Recevoir les améliorations du modèle

Cette section ne concerne que ceux qui ont **forké** le modèle (étape 1.1, seconde option). Si vous avez téléchargé un ZIP, votre copie est indépendante : il n'y a rien à synchroniser, et vous pouvez ignorer cette section.

Le modèle continue d'évoluer : règles affinées, routines améliorées, corrections. Ces changements ne touchent que les fichiers du socle — `.github/copilot-instructions.md`, `docs/`, `3_Ressources/Pattern_Extensibilite/`, `_systeme/routines.md` — **jamais vos notes**.

Pour les récupérer :

1. Ouvrez votre fork sur GitHub.
2. Si un bandeau indique que votre branche est en retard sur le modèle d'origine, cliquez sur **Sync fork**, puis **Update branch**.
3. Dans GitHub Desktop, cliquez sur **Pull origin** pour rapatrier la mise à jour sur votre ordinateur.

Si GitHub refuse la synchronisation en signalant un conflit, c'est que vous avez modifié l'un des fichiers du socle de votre côté. Ne tentez pas de trancher à la main :

```text
La synchronisation avec le modèle d'origine signale un conflit.
Explique-moi quels fichiers sont concernés, ce que le modèle propose de changer,
et ce que je perdrais dans chaque cas. Attends mon arbitrage avant toute écriture.
```

Avant toute mise à jour, vérifiez que Google Drive a fini de synchroniser : vous disposez ainsi d'une version antérieure récupérable si le résultat ne vous convient pas.
