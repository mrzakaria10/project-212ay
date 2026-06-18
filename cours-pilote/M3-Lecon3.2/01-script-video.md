# Leçon 3.2 — Refactorer un composant existant
## Script Vidéo — ~15 min

### [0:00-0:30] HOOK
> Tu as un composant de 300 lignes qui fait tout — état, affichage, API calls, validation. Tu sais qu'il faut le refactorer mais par où commencer ? L'IA peut t'aider à restructurer sans casser le comportement.

### [0:30-3:00] CONCEPT — Refacto en 3 étapes

**(Slide)**
```
1. ANALYSER   → Comprendre ce que fait le composant
2. SÉPARER    → Diviser en sous-composants logiques
3. TYPER      → Ajouter les interfaces manquantes
```

> L'IA est excellente pour le refactoring parce qu'elle voit le pattern global que toi tu ne vois plus à force de regarder le même code.

### [3:00-9:00] DÉMO — Refacto d'un UserDashboard

**Avant — Composant monolithique de 200 lignes :**
```tsx
function UserDashboard() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [search, setSearch] = useState('');
  const [selected, setSelected] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch('/api/users').then(...).catch(...);
  }, []);

  // ... 150 lignes de JSX mélangé
}
```

**Prompt de refacto :**
```
Refactore ce composant React en 3 sous-composants :
- UserList (affiche la liste)
- UserSearchBar (input de recherche)
- UserDetailCard (carte détail utilisateur)

Le composant parent UserDashboard orchestre les appels API
et la state. TypeScript. Garde la même logique.
```

**Après — Structure propre :**
```
UserDashboard (state + API calls)
├── UserSearchBar (props: onSearch)
├── UserList (props: users, loading)
│   └── UserDetailCard (props: user)
└── (gestion d'erreur + loading)
```

### [9:00-10:00] ACTION
> Prends un composant > 150 lignes dans ton projet. Copie-le dans ChatGPT/Claude et demande un plan de refactoring. Applique-le.

### [10:00-10:30] OUTRO
> Dernière leçon du module : optimiser les performances.
