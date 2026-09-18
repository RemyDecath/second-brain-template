---
description: Comment créer une nouvelle branche ou une nouvelle note dans ce second brain.
created_date: <AAAA-MM-JJ>
---

# Pattern d'extensibilité

<!-- Version générique, inspirée d'un système réel, sans donnée réelle. -->

Ce pattern décrit la **forme attendue** d'un dossier et d'une note. Ce n'est pas un gabarit à
recopier : aucune structure n'est imposée au-delà du frontmatter. Pour un exemple rempli, ouvre
`1_Projets/EXEMPLE_Projet/` ou `2_Casquettes/EXEMPLE_Casquette/`.

## Structure de dossier

Applique-la chaque fois que tu ajoutes un dossier de premier niveau ou une sous-branche.

```
NouvelleBranche/
├── NouvelleBranche.md          ← hub, avec Registry Rapide
└── Sous-element/
    └── Sous-element.md         ← note de contexte homonyme (R1)
```

## La seule règle non négociable

Tout fichier de contenu commence par un frontmatter — bloc `---` en **première ligne**, sans rien
au-dessus — contenant une `description:` d'une phrase :

```markdown
---
description: <une phrase — l'essentiel de ce fichier>
created_date: <AAAA-MM-JJ>
---
```

La revue hebdomadaire régénère les Registry Rapide à partir de ces `description:`. Sans elles, la
routine ne trouve rien et les registries se périment.

## Ce qu'on attend d'un hub

Le hub porte le nom de son dossier. Il sert de point d'entrée : l'agent le lit pour savoir où aller,
sans explorer le disque (R3). Il contient au minimum :

- **Périmètre** : ce qu'on y range, ce qu'on n'y range pas (avec le renvoi vers le bon dossier).
- **Registry Rapide** : une table `| Élément | Description | Chemin |`, une ligne par sous-élément.
- **Règle de sortie** : quand un élément quitte la branche, et vers où.

## Ce qu'on attend d'une note de contexte

Elle porte le nom de son dossier (R1) et répond à « où ça en est » en moins de 80 lignes :

- un résumé de quelques lignes ;
- l'état actuel ;
- les faits **datés et sourcés** — `fait [AAAA-MM-JJ, source]` ;
- les points d'attention, les liens `[[NoteLiée]]`.

Au-delà du plafond, on n'étend pas : on extrait un sujet en note atomique dans le même dossier, et
on l'ajoute au registry de la note parente (R4).

## Mise à jour du routage

Si la branche est destinée à un usage fréquent, ajoute une ligne de renvoi dans
`.github/copilot-instructions.md` (section routage) — jamais le détail de la branche elle-même,
seulement le chemin vers son hub.

## Checklist de création

- [ ] Créer le dossier de la nouvelle branche.
- [ ] Créer le hub avec son Registry Rapide (même vide au départ).
- [ ] Créer une première note de contexte homonyme d'un sous-élément.
- [ ] Vérifier que l'agent y accède via le registry, sans commande shell ni exploration à l'aveugle.
- [ ] Consigner la décision dans `_systeme/journal.md`.
