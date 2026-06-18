# Leçon 4.1 — Générer une documentation claire
## Script Vidéo — ~12 min

### [0:00-0:30] HOOK
> Tu finis un projet, il te reste 15 minutes, et tu dois écrire la doc. Tu laisses tomber, tu te dis "je ferai ça plus tard". Résultat : dans 3 mois, personne ne comprend ton code. L'IA peut générer une doc complète en 30 secondes.

### [0:30-3:00] CONCEPT — La documentation assistée par IA
> L'IA excelle dans 3 types de documentation :
> - **README** : présentation, installation, endpoints
> - **JSDoc / TSDoc** : documentation inline des fonctions
> - **API docs** : description des routes et paramètres
>
> Stratégie : générer avec l'IA, relire et ajuster manuellement.

### [3:00-8:30] DÉMO

**README automatique :**
```
Prends le code de mon API Express et génère un README.md complet
avec : titre, description, stack, installation, variables d'env,
liste des endpoints avec exemples, structure du projet.
```

**JSDoc sur une fonction :**
```
Ajoute JSDoc à cette fonction TypeScript :
- Description de ce qu'elle fait
- Paramètres avec types
- Retour
- Exemple d'utilisation
```

**API doc style OpenAPI :**
```
À partir de ces routes Express, génère une spec OpenAPI 3.0
en YAML. Décris chaque route avec ses paramètres et réponses.
```

### [8:30-9:00] ACTION
> Prends un de tes projets. Colle le code principal dans ChatGPT et demande un README complet. Publie-le.

### [9:00-9:30] OUTRO
> Prochaine leçon : les tests unitaires avec l'IA.
