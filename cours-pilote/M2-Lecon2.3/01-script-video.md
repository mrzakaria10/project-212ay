# Leçon 2.3 — Prompts faibles vs prompts forts
## Script Vidéo — ~15 min

### [0:00-0:30] HOOK
> Si tu devais retenir une seule compétence de tout le module, c'est celle-ci : la différence entre un prompt faible et un prompt fort peut multiplier ta productivité par 10.

### [0:30-3:00] CONCEPT — La matrice prompt

**(Slide)**
```
                PRÉCIS
                  │
      GÉNÉRIQUE ──┼── SPÉCIFIQUE
                  │
                CONTEXTUEL
```

> **Prompt faible** = vague, pas de contexte, pas de format → résultat générique à retoucher
> **Prompt fort** = rôle + contexte + tâche + format + contrainte → résultat quasi exploitable

### [3:00-8:00] DÉMO — 5 matchs faible vs fort

**Match 1 — API :**
```
FAIBLE : "Crée une API"
FORT :   "Tu es senior backend. Crée une API Express avec TypeScript,
         Prisma, validation Zod, CRUD users, pagination, middleware auth JWT."
```

**Match 2 — Composant :**
```
FAIBLE : "Fais un bouton"
FORT :   "Composant Button React + Tailwind avec variants primary/secondary/ghost,
         taille sm/md/lg, loading state, désactivé, onClick typé."
```

**Match 3 — Explication :**
```
FAIBLE : "Explique les closures"
FORT :   "Explique les closures JavaScript à un junior. Utilise une analogie
         concrète (le vestiaire). Donne 2 exemples de code commentés."
```

**Match 4 — Debug :**
```
FAIBLE : "Mon code ne marche pas"
FORT :   "J'ai ce bug [coller l'erreur]. Contexte : Express + Prisma.
         Le endpoint POST /tasks plante avec 500. Voici le handler. Quelle est la cause ?"
```

**Match 5 — Refacto :**
```
FAIBLE : "Améliore mon code"
FORT :   "Refactore ce composant React (ci-dessous). Il fait 200 lignes.
         Sépare-le en sous-composants. Ajoute les types manquants. Contexte : Next.js 14."
```

### [8:00-9:00] ACTION
> Prends un dernier prompt faible que tu as écrit récemment. Réécris-le en prompt fort avec les 5 piliers. Teste les deux versions et compare.

### [9:00-9:30] OUTRO + Quiz
> Module terminé ! Passe au quiz pour valider. Puis Module 3 : Déboguer et refactorer.
