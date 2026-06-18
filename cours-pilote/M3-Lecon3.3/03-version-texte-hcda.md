# Leçon 3.3 : Optimiser structure et performance
## Version Texte HCDA

## H — Hook
Ton app marche mais elle rame. Re-rendus, appels API en cascade, bundle lourd. L'IA peut diagnostiquer — si tu sais quoi demander.

## C — Concept : 3 niveaux d'optimisation

| Niveau | Problème | Solution |
|--------|----------|----------|
| **1 — Structure** | Composant monolithique | Découper, props claires |
| **2 — Rendu** | Re-rendus inutiles | useMemo, useCallback, memo |
| **3 — Réseau** | Appels redondants | Debounce, cache, pagination |

> Règle : 80% des perfs sont réglées au niveau 1. Ne saute pas d'étape.

## D — Démo

**Niveau 1 — React.memo :**
```
AVANT : <List> re-rend tout à chaque changement d'un item
APRÈS : React.memo(Item) + keys uniques + props découpées
```

**Niveau 2 — useMemo :**
```
AVANT : const filtered = items.filter(...) // recalculé à chaque render
APRÈS : const filtered = useMemo(() => items.filter(...), [items])
```

**Niveau 3 — Debounce :**
```
AVANT : fetch('/api/search?q=' + input) // 100 appels en 2 sec
APRÈS : debounce(fetchSearch, 300) // 1 appel après la frappe
```

## A — Action
Prends une page lente. Demande à Claude de trouver les problèmes de perfs. Applique une suggestion.
