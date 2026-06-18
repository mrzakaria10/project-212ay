# Leçon 3.2 : Refactorer un composant existant
## Version Texte HCDA

## H — Hook
Un composant de 300 lignes qui fait tout : état, API, affichage, validation. Tu sais qu'il faut le refactorer mais par où commencer ?

## C — Concept : Refacto en 3 étapes
1. **Analyser** — Comprendre les responsabilités du composant
2. **Séparer** — Diviser en sous-composants logiques
3. **Typer** — Ajouter les interfaces TypeScript manquantes

L'IA voit le pattern global que tu ne vois plus.

## D — Démo

**Avant** : Composant `UserDashboard` de 200 lignes avec state + JSX mélangé.

**Prompt de refactoring :**
```
Refactore ce composant React en 3 sous-composants :
UserList, UserSearchBar, UserDetailCard.
Le parent orchestre API + state. TypeScript.
```

**Après** :
```
UserDashboard (state + API calls)
├── UserSearchBar (props: onSearch)
├── UserList (props: users, loading)
│   └── UserDetailCard (props: user)
└── Loading / Error states
```

**Résultat :** 200 lignes → 60 lignes par fichier, chaque fichier a une responsabilité unique.

## A — Action
Prends un composant > 150 lignes. Demande un plan de refacto à Claude. Applique-le.
