# Leçon 4.2 — Créer des tests unitaires de base
## Script Vidéo — ~12 min

### [0:00-0:30] HOOK
> Tu sais que tu devrais écrire des tests. Mais entre le code à livrer et les bugs à corriger, tu remets toujours ça au lendemain. L'IA peut générer une base de tests complète en quelques secondes.

### [0:30-3:00] CONCEPT — Tests assistés par IA
> L'IA est parfaite pour les tests unitaires parce qu'ils sont structurés et répétitifs.
> - Tests de fonctions pures
> - Tests d'API endpoints
> - Tests de composants (edge cases)
>
> Règle : générer les tests avec l'IA, exécuter, et ajuster les cas limites.

### [3:00-8:30] DÉMO — 3 scénarios

**Test unitaire (Vitest) :**
```
Génère des tests unitaires Vitest pour cette fonction :
[coller fonction]. Teste : cas normal, chaîne vide, null,
grand nombre, caractères spéciaux.
```

**Test d'API (Supertest) :**
```
Génère des tests d'intégration pour cette route Express :
GET /api/users. Teste : 200 OK, 404 si pas trouvé,
401 sans token. Utilise Vitest + Supertest.
```

**Test React Testing Library :**
```
Génère des tests RTL pour ce composant [coller].
Teste : rendu normal, loading state, empty state, erreur.
```

### [8:30-9:00] ACTION
> Prends une fonction de ton projet. Fais générer des tests unitaires par l'IA. Exécute-les. Corrige ce qui ne passe pas.

### [9:00-9:30] OUTRO
> Dernière leçon du module : le workflow complet.
