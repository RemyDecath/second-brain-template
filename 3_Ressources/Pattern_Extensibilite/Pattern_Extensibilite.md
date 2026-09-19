---
description: Comment créer une nouvelle branche ou une nouvelle note dans ce second brain.
created_date: 2026-09-18
---

# Pattern d'extensibilité

Ce pattern décrit la **forme attendue** d'un dossier et d'une note. Ce n'est pas un gabarit à
recopier : aucune structure n'est imposée au-delà du frontmatter. Pour des exemples remplis, ouvre
`docs/exemples/` — ils sont hors du contexte de l'agent, c'est ce fichier-ci qui fait foi pour lui.

## Structure de dossier

À appliquer pour tout dossier de premier niveau ou sous-branche.

```
NouvelleBranche/
├── NouvelleBranche.md          ← hub, avec Registry Rapide
└── Sous-element/
    └── Sous-element.md         ← note de contexte homonyme
```

## La seule règle non négociable

Tout fichier de contenu commence par un frontmatter — bloc `---` en **première ligne**, sans rien
au-dessus — contenant une `description:` d'une phrase :

```markdown
---
description: <une phrase — l'essentiel de ce fichier>
created_date: 2026-09-18
---
```

La revue hebdomadaire régénère les Registry Rapide à partir de ces `description:`. Sans elles, la
routine ne trouve rien et les registries se périment.

## Ce qu'on attend d'un hub

Le hub porte le nom de son dossier et sert de point d'entrée : l'agent le lit pour savoir où aller,
sans explorer le disque. Au minimum :

- **Périmètre** : ce qu'on y range, ce qu'on n'y range pas (avec le renvoi vers le bon dossier).
- **Registry Rapide** : une table `| Élément | Description | Chemin |`, une ligne par sous-élément.
- **Règle de sortie** : quand un élément quitte la branche, et vers où.

## Ce qu'on attend d'une note de contexte

Elle porte le nom de son dossier et répond à « où ça en est » sous le plafond de `config.md §5` :

- un `status:` dans le frontmatter — `actif`, `en pause` ou `clos` ;
- un résumé de quelques lignes ;
- l'état actuel ;
- les faits **datés et sourcés** — `fait [AAAA-MM-JJ, source]` ;
- les points d'attention, les liens `[[NoteLiée]]` ;
- un **Registry des notes atomiques** (même table que celle d'un hub), dès qu'une note atomique
  existe dans le dossier. C'est le 3e niveau de routage : hub → note de contexte → note atomique.

Au-delà du plafond, on n'étend pas : on extrait un sujet en note atomique dans le même dossier et on
l'ajoute à ce registry. Si c'est une **table** qui déborde et non de la prose, on ne l'extrait pas :
on la partitionne selon son axe naturel (par initiale, par année), le parent devenant un hub.

## Mise à jour du routage

Si la branche est destinée à un usage fréquent, ajoute une ligne de renvoi dans
`.github/copilot-instructions.md` (section 2, routage) — jamais le détail de la branche elle-même,
seulement le chemin vers son hub. Si le plafond du socle est atteint, c'est qu'une règle doit en
être retirée — pas que le plafond doit monter.

## Checklist de création

- [ ] Créer le dossier de la nouvelle branche.
- [ ] Créer le hub avec son Registry Rapide (même vide au départ).
- [ ] Créer une première note de contexte homonyme d'un sous-élément.
- [ ] Vérifier que l'agent y accède via le registry, sans commande shell ni exploration à l'aveugle.
- [ ] Ajouter la branche au registry de son hub parent.
- [ ] Consigner la décision dans `_systeme/journal.md`.
