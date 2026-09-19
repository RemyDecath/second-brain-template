---
description: Journal système — décisions et évolutions du fonctionnement du second brain, datées.
created_date: 2026-09-18 15:49:43
---

# Journal système

Consigne toute décision, arbitrage ou évolution concernant le fonctionnement du second brain :
organisation, règles, workflows, conventions, outils, intégrations et gouvernance. Les frictions
d'usage y sont conservées comme signaux d'amélioration, mais elles ne sont pas le seul contenu du
journal. Jamais de contenu métier — pour ça, voir `3_Ressources/Decisions_Log/`.

## Règles

- **Aucun plafond de lignes.** Ce fichier croît par ajout ; sa taille est bornée par la remise à
  zéro mensuelle, jamais par un nombre de lignes. Ne le signale pas en revue hebdo.
- Une entrée par décision ou sujet, ajoutée en fin de fichier, jamais de réécriture rétroactive.
- Une entrée récente peut en amender une ancienne en la référençant explicitement.
- Écriture directe, sans validation préalable : c'est un constat, pas une inférence.
- Au changement de mois, archivage du contenu dans `_systeme/journal/journal-AAAA-MM.md`, ajout de
  la ligne correspondante au registry de `_systeme/_systeme.md`, et remise à zéro de ce fichier.

## Format d'une entrée

`### AAAA-MM-JJ — <type> — <sujet>`, où `<type>` vaut :

- **`décision`** — un arbitrage sur le fonctionnement : la décision, son motif, son effet.
- **`friction`** — un accroc d'usage, écrit **même sans décision à la clé** : ce qui a coincé, dans
  quel contexte. C'est la matière première du comptage des répétitions — une friction non écrite ne
  sera jamais comptée, et la répétition passera inaperçue.
- **`revue`** — trace d'une revue hebdo ou d'une rétro : ce qui a été traité, ce qui reste. Elle
  sert de borne à la revue suivante, qui ne remonte pas au-delà.
- **`incident`** — perte, corruption, synchronisation ratée : ce qui s'est passé, ce qui l'a réparé.

Le type est ce qui rend le journal filtrable : la rétro mensuelle lit les `friction` pour repérer
les répétitions, et la revue hebdo cherche la dernière `revue` pour savoir où s'arrêter.

## Entrées

### 2026-09-19 — décision — Audit du modèle : correctifs P0 et P1

**Sujet** — Audit complet du template avant diffusion. Six défauts bloquants et six pistes
d'optimisation identifiés ; lots P0 (socle exécutable) et P1 (durabilité, tokens) appliqués.

**Décisions**

- **Renvois `R1`–`R12` supprimés.** 18 renvois pointaient vers un référentiel inexistant ; une
  insertion de section les avait décalés. Remplacés par des renvois en clair. *Motif : un
  identifiant que rien ne définit est une instruction que l'agent ne peut pas suivre.*
- **Exceptions de sobriété explicitées.** Régénérer un registry et réparer un chemin introuvable
  supposent de parcourir : autorisé, borné à une seule branche et au seul frontmatter. *Motif : la
  revue hebdo était impossible à exécuter sans violer la règle de sobriété.*
- **Le registry est déclaré index régénérable, jamais source de vérité.** En cas de désaccord avec
  le système de fichiers, c'est lui qui a tort.
- **Plafonds : source de vérité unique dans `config.md §5`**, et ils ne comptent que la prose. Une
  table qui déborde se **partitionne** (par initiale, par année) au lieu de s'extraire. *Motif :
  glossaire et journal de décisions étaient plafonnés à ~55 entrées, soit environ un an d'usage.*
- **Archives : règle doublée.** L'exclusion `.copilotignore` n'est plus l'unique protection ; le
  socle interdit la lecture (section 10). Tout archivé va dans un sous-dossier, seul périmètre que
  le motif d'exclusion couvre. *Motif : le support de `.copilotignore` dépend de l'application.*
- **Tutoriel et exemples déplacés dans `docs/`, exclu du contexte.** Le README passe de 371 à 36
  lignes. *Motif : ~4 000 tokens par session pour un contenu sans valeur pour l'agent, et 20 blocs
  de prompts qu'il pouvait confondre avec des instructions. Effet de bord : plus aucun exemple
  fictif à supprimer au setup.*
- **`_systeme/` devient une branche conforme** : hub `_systeme/_systeme.md` avec registry, journaux
  mensuels clos dans `_systeme/journal/`, exclu du contexte.
- **Revue hebdomadaire rendue incrémentale**, bornée par `git log --since` à partir de la dernière
  entrée de revue. *Motif : son coût croissait linéairement avec le vault ; il est désormais
  constant. L'étape « Commit » est reformulée en « Sauvegarder » pour un lecteur non technique.*
- **Règle ajoutée : un fait a un seul domicile**, ailleurs un wikilink.

**Effet** — Socle à 119 lignes sur 120, plafonds respectés partout, aucun renvoi mort, aucun
placeholder de date. Restent ouverts (lot P2) : sections README « récupérer le modèle » et
« sauvegarde », procédure de rattrapage après édition manuelle hors Inbox, conventions de nommage
`config.md §4` à réconcilier avec l'homonymie structurelle, champs de frontmatter `status`/
`updated`, budget de contexte chiffré, `LICENSE`, chemin de mise à jour d'un fork.

### 2026-09-19 — décision — Audit du modèle : correctifs P2

**Sujet** — Dernier lot de l'audit : confort d'usage, adoption, et réponse au risque de perte de
données identifié en séance (le vault n'existait qu'en local).

**Décisions**

- **Sauvegarde par Google Drive pour ordinateur**, ajoutée au tutoriel comme étape obligatoire
  (sections 1.2 et 1.3) : le dossier vit dans *Mon Drive*, marqué **Disponible hors connexion**.
  *Motif : un second brain qui n'existe qu'à un endroit se perd avec son disque. Le mode hors
  connexion n'est pas un détail — sans lui, Google Drive ne télécharge pas les fichiers et les deux
  applications lisent des notes vides.* Mise en garde ajoutée sur l'usage simultané depuis deux
  ordinateurs, qui produit des doublons de synchronisation.
- **Frontmatter : `status:` ajouté aux notes de contexte** (`actif`, `en pause`, `clos`).
  *Revirement par rapport à l'audit, qui recommandait aussi un champ `updated:` : git connaît déjà
  la date de dernière modification (`git log -1 --format=%ad`), la stocker créerait un doublon qui
  dérive. Un seul champ ajouté, pas deux.*
- **Budget de contexte chiffré** dans la règle de sobriété : 5 fichiers ouverts au maximum par
  réponse, `grep` avant d'ouvrir, lecture par plage au-delà de 200 lignes. *Motif : la sobriété
  n'était qu'une consigne qualitative, alors que la skill google-workspace, elle, était chiffrée.*
- **Conventions de nommage réconciliées** (`config.md §4`) : les choix configurables ne portent que
  sur les noms de notes libres ; l'homonymie dossier/note, le nom des hubs et le préfixe daté des
  captures sont structurels et ne se configurent pas. *Motif : trois conventions incompatibles
  coexistaient, dont deux codées en dur dans les hubs.*
- **Tutoriel complété** : récupération du modèle (ZIP ou fork), rattrapage après édition manuelle
  hors Inbox, diagnostic des notes vides et des doublons de synchronisation, et réception des
  améliorations du modèle pour les forks (section 11).
- **Pas de fichier `LICENSE`.** Écarté volontairement : ce second brain est destiné à un usage en
  entreprise, et le choix d'une licence relève de l'employeur, pas du modèle. En l'absence de
  licence, le dépôt reste en « tous droits réservés » par défaut, ce qui est le comportement
  attendu ici. *À reconsidérer uniquement si le modèle est un jour diffusé publiquement.*
- Artefacts de synchronisation Google Drive exclus de git et du contexte.

**Effet** — Socle à 119 lignes sur 120. L'ajout du budget de contexte et de `status:` a imposé de
retirer l'énumération des hubs de la règle de routage, remplacée par la règle d'homonymie qui
l'engendre : le plafond a joué son rôle d'arbitre, comme le pattern le prévoit.

### 2026-09-19 — décision — Traçabilité : fermer la boucle entre écriture et routines

**Sujet** — Vérification que les règles d'écriture produisent assez de matière pour alimenter la
revue hebdo et la rétro mensuelle. La revue hebdo était bien alimentée ; la rétro tournait à vide
sur 4 de ses 7 étapes.

**Constat** — Le système enregistrait les *décisions* mais pas les *usages*. Quatre étapes de la
rétro (glossaire jamais reservi, règles jamais déclenchées, outils sans usage, relecture des
frictions) supposaient un journal d'usage qui n'a jamais existé. Et le compteur de répétitions ne
pouvait pas démarrer : rien n'enregistrait la 1re occurrence, et les sessions étant cloisonnées
par conception, l'agent n'en gardait aucun souvenir au moment de la 2e.

**Décisions**

- **Plafond du socle porté de 120 à 150 lignes**, sur arbitrage de l'utilisateur. Ce qui avait été
  coupé pour tenir sous 120 — notamment la capture des frictions — est rétabli.
- **La friction devient une écriture obligatoire**, au moment où elle se produit et même sans
  décision à la clé. *Motif : une friction non écrite ne sera jamais comptée, et la répétition
  passera inaperçue.* Correction d'une régression introduite au lot P1, où la mention des
  frictions avait disparu du socle en le condensant, alors que `journal.md` continuait de
  l'affirmer et que la rétro continuait de la lire.
- **Les entrées du journal sont typées** : `### AAAA-MM-JJ — décision | friction | revue | incident
  — Sujet`. Le journal devient filtrable, et la revue hebdo trouve sa borne par `grep` au lieu de
  se fier à une convention implicite.
- **Le comptage des répétitions est explicité en deux temps** : le journal compte de 1 à 2 (entrée
  `friction`), `ameliorations.md` compte de 2 à 3. Le seuil de la 3e répétition devient atteignable.
- **Les trois étapes non instrumentables de la rétro sont réécrites** en indices vérifiables ou en
  questions posées à l'utilisateur. Un terme de glossaire inutile se repère par `grep -rl` ; l'usage
  d'une règle ou d'un outil se demande, il ne se déduit pas. Règle ajoutée : ne jamais déduire un
  usage que rien n'a consigné.
- **Étape ajoutée à la rétro** : relire `Decisions_Log` pour repérer les décisions caduques.
  `3_Ressources/3_Ressources.md` promettait ce contrôle depuis le début sans qu'aucune routine ne
  le réalise — le fichier était en écriture seule.
- **Les journaux chronologiques sont exemptés de plafond** (`config.md §5`). Sans cette exemption,
  la revue hebdo aurait signalé `journal.md` tous les mois et proposé d'en « extraire le thème
  dominant », ce qui n'a pas de sens pour un journal remis à zéro chaque mois.

**Effet** — Socle à 135 lignes sur 150. Chaque étape des deux routines a désormais un producteur
identifié, ou pose explicitement sa question plutôt que d'inventer la réponse.

### 2026-09-19 — décision — Les plafonds ne s'appliquent qu'à ce qui se lit en entier

**Sujet** — Le journal système était plafonné par défaut. Signalé comme une mauvaise idée : un
journal borné par un nombre de lignes perd de l'historique, ce qui est l'inverse de sa fonction.

**Constat** — L'exemption ajoutée à l'entrée précédente ne vivait que dans `config.md §5`. Le socle,
seul texte lu à chaque session, n'excluait que les lignes de table et ne disait rien des journaux :
un agent appliquant cette règle à la lettre aurait signalé `journal.md` à chaque revue. Cause
racine plus large : la typologie des plafonds (socle, hub, note de contexte, note atomique) ne
couvrait pas tous les types de fichiers du dépôt. `journal.md` et `routines.md` tombaient dans un
trou où un plafond s'appliquait par défaut, sans que personne l'ait décidé.

**Décision** — Remplacer la liste d'exemptions par le principe qui l'engendre : **un plafond
s'applique à ce qui doit être lu en entier pour être compris** (socle, hub, note de contexte, note
atomique, procédure) ; **il ne s'applique pas à ce qui se consulte par extrait** (journaux, files
d'attente, tables), dont la croissance est bornée autrement — remise à zéro mensuelle, partition,
vidage en routine. Énoncé dans le socle, détaillé dans `config.md §5`, rappelé dans `journal.md`.

*Motif : une exemption se périme dès qu'un type de fichier apparaît, un principe non. Le test est
qu'il donne la bonne réponse sans qu'on l'ait prévue — `routines.md` se lit en entier pour être
appliquée, donc elle reste plafonnée, alors même qu'elle vit dans `_systeme/`.*

**Effet** — Socle à 141 lignes sur 150. `routines.md` (75/80) et `Pattern_Extensibilite.md` (77/80)
approchent de leur plafond : à surveiller, ce sont bien des fichiers lus en entier.

### 2026-09-19 — décision — Vérification de la couverture des plafonds

**Sujet** — Contrôle que le plafond ne s'applique qu'aux fichiers où il est pertinent, en
classifiant chaque fichier d'après les règles telles qu'écrites.

**Constat** — Deux fichiers n'étaient couverts par aucune règle : `config.md` et `README.md`. Le
premier est sérieux — il est lu **en entier à chaque session** et grossit avec les casquettes, les
outils et le périmètre sensible, soit exactement les conditions qui justifient un plafond. Rien ne
le bornait. Par ailleurs, la formulation « ce qui se consulte par extrait » était inexacte pour les
files d'attente : `a-valider.md` et `ameliorations.md` sont bien lus en entier, mais vidés en
routine.

**Décisions**

- **Critère à deux conditions** : un plafond s'impose quand un fichier est *lu en entier* **et**
  *croît sans borne propre*. Si l'une des deux manque, pas de plafond. Cela couvre les trois cas
  d'exemption pour la bonne raison : le journal n'est pas lu en entier, une table non plus, une
  file d'attente l'est mais ne croît pas.
- **`config.md` et `README.md` plafonnés à 80 lignes**, et les captures d'`0_Inbox/` rattachées au
  plafond des notes atomiques.
- **Le critère quitte `config.md` pour le socle.** Écrire le raisonnement dans `config.md` l'avait
  porté à 75/80 : un fichier de préférences utilisateur n'a pas à héberger les règles de l'agent.
  `config.md` ne garde que les valeurs, sous forme de table — dont les lignes ne comptent pas, par
  sa propre règle. Il retombe à 56/80.

**Effet** — 16 fichiers, tous classés, tous sous leur plafond. Points de pression :
`Pattern_Extensibilite.md` (77/80) et `_systeme/routines.md` (75/80).
