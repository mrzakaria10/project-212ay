# Leçon 3.3 — Optimiser structure et performance
## Script Vidéo — ~15 min

### [0:00-0:30] HOOK
> Ton app marche, mais elle rame. Re-rendus infinis, appels API en cascade, bundle trop lourd. L'IA peut t'aider à diagnostiquer et corriger ces problèmes — si tu sais quoi lui demander.

### [0:30-3:30] CONCEPT — Les 3 profondeurs de l'optimisation

**(Slide)**
```
┌──────────────────────────────────────┐
│  NIVEAU 1 — Structure               │
│  Séparer les composants, props       │
├──────────────────────────────────────┤
│  NIVEAU 2 — Rendu                   │
│  useMemo, useCallback, React.memo   │
├──────────────────────────────────────┤
│  NIVEAU 3 — Réseau                  │
│  Debounce, pagination, cache        │
└──────────────────────────────────────┘
```

> On commence toujours par le niveau 1 avant le 3. 80% des perfs sont dans la structure.

### [3:00-8:30] DÉMO — 3 optimisations

**Opti 1 — Structure : Re-rendus inutiles**
```
AVANT : <Parent> → <List> → <Item> (tout le monde re-render)
APRÈS : Props bien découpées + React.memo sur Item
```

Prompt :
```
Ce composant List re-rend tout quand un seul item change.
Ajoute React.memo, keys uniques, et découpe les props
pour éviter les re-rendus inutiles. TypeScript.
```

**Opti 2 — useMemo / useCallback**
```
AVANT : const filtered = items.filter(...) // recalculé à chaque render
APRÈS : const filtered = useMemo(() => ..., [items])
```

**Opti 3 — Performance réseau**
```
AVANT : fetch('/api/search?q=' + input) // appel à chaque frappe
APRÈS : debounce 300ms + cache des résultats récents
```

### [8:30-9:00] ACTION
> Prends une page lente de ton projet. Copie le composant dans Claude. Demande : "Trouve les problèmes de performance". Applique une des suggestions.

### [9:00-9:30] OUTRO + Bilan
> Module 3 terminé ! Passe au quiz. Puis Module 4 : Documentation, tests et workflow final.
