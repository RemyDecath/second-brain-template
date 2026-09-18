<!-- Version générique du pattern d'extensibilité — inspiré d'un système réel, sans donnée réelle. -->
---
description: Comment créer une nouvelle branche (dossier de premier niveau) dans ce second brain.
created_date: <AAAA-MM-JJ>
---

# Pattern d'extensibilité

Applique ce pattern chaque fois que tu ajoutes un nouveau type de dossier au même niveau que
`1_Projets/`, `2_Casquettes/` ou `3_Ressources/`, ou une nouvelle sous-branche à l'intérieur d'un
dossier existant.

## Structure de dossier

```
NouvelleBranche/
├── NouvelleBranche.md          ← hub, avec Registry Rapide
└── Sous-element/
    └── Sous-element.md         ← note de contexte homonyme (R1)
```

## Contenu obligatoire du hub

- Frontmatter (`description`, `created_date`).
- Un en-tête de 2 lignes : ce que contient la branche, ce qui y entre.
- Un **Registry Rapide** : table `| Élément | Description | Chemin |`.
- Une règle de sortie (quand un élément quitte la branche, et vers où).

## Format d'une note de contexte

Voir `3_Ressources/_Templates/template_note_contexte.md` : résumé court, état actuel, faits datés et
sourcés, points d'attention, liens, registry des notes atomiques si débordement (R4).

## Mise à jour du routage

Si la branche est destinée à un usage fréquent, ajoute une ligne de renvoi dans
`.github/copilot-instructions.md` (section routage) — jamais le détail de la branche elle-même,
seulement le chemin vers son hub.

## Checklist de création

- [ ] Créer le dossier de la nouvelle branche.
- [ ] Créer le hub avec Registry Rapide (même vide au départ).
- [ ] Créer une première note de contexte homonyme d'un sous-élément.
- [ ] Vérifier que l'agent y accède via le registry, sans commande shell ni exploration à l'aveugle.
- [ ] Consigner la décision dans `_systeme/journal.md`.
