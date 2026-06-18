# Leçon 1.2 : Cas d'usage concrets

**Module :** M1 — Comprendre l'IA pour les développeurs
**Durée :** 12 min

---

## H — Hook

Tu connais les trois familles d'outils IA. Mais à quel moment précis utiliser chacun dans ton quotidien de développeur ? Dois-tu utiliser Claude pour tout ? Copilot pour tout ? La réponse est non — chaque outil a son moment.

Dans cette leçon, on suit un mini-projet réel du début à la fin, et on voit quel outil utiliser à chaque étape.

---

## C — Concept : Les 4 moments clés de l'IA

Dans la vie d'un projet web, l'IA est la plus utile à **4 moments précis** :

| Phase | Action | Outil recommandé | Pourquoi |
|-------|--------|------------------|----------|
| **1. Init** | Boilerplate, structure, DB schema | Claude / ChatGPT | Besoin de réflexion, pas de vitesse |
| **2. Code** | Routes, composants, logique | Copilot / Cursor | Besoin de vitesse, pas de réflexion |
| **3. Corriger** | Bugs, refactoring, perfs | IDE + Chat | Selon complexité |
| **4. Finaliser** | Doc, tests, déploiement | ChatGPT / Claude | Génération rapide, validation IDE |

### Le bon outil au bon moment

```
Phase 1 (Init)    → Chat généraliste   → "Je réfléchis"
Phase 2 (Code)    → Assistant IDE      → "Je produis"
Phase 3 (Corriger)→ IDE + Chat         → "Je répare"
Phase 4 (Final)   → Chat généraliste   → "Je finalise"
```

---

## D — Démo : Mini-projet "API de gestion de tâches"

### Étape 1 — Initialisation avec Claude

**Prompt :**
```
Je veux créer une API REST avec Express + TypeScript + Prisma (SQLite)
pour une todolist. L'API doit avoir :
- CRUD complet sur les tâches (title, completed, createdAt)
- Validation des entrées avec Zod
- Un système d'erreurs cohérent

Donne-moi la commande d'initialisation et la structure de dossiers.
```

**Résultat Claude :**
```bash
npm init -y
npm install express prisma @prisma/client zod
npm install -D typescript ts-node @types/express

mkdir src/routes src/middleware src/lib
```

**Schema Prisma généré :**
```prisma
model Task {
  id        Int      @id @default(autoincrement())
  title     String
  completed Boolean  @default(false)
  createdAt DateTime @default(now())
}
```

**Routeur Express :**
```typescript
import { Router } from 'express';
import { z } from 'zod';
import { PrismaClient } from '@prisma/client';

const router = Router();
const prisma = new PrismaClient();

const taskSchema = z.object({
  title: z.string().min(1, 'Le titre est requis'),
});

router.get('/', async (req, res) => {
  const tasks = await prisma.task.findMany({
    orderBy: { createdAt: 'desc' }
  });
  res.json(tasks);
});

router.post('/', async (req, res) => {
  const data = taskSchema.parse(req.body);
  const task = await prisma.task.create({ data });
  res.status(201).json(task);
});

export default router;
```

**Ce que Claude t'apporte :** Une architecture complète, prête à l'emploi. Tu gagnes ~15 minutes de recherche et de setup.

---

### Étape 2 — Développement avec Copilot

Une fois la structure posée, tu codes les endpoints dans VS Code. Copilot te propose automatiquement :

```typescript
// Tu tapes : app.get('/tasks', async (req, res) => {
// Copilot complète directement :
  const tasks = await prisma.task.findMany({
    orderBy: { createdAt: 'desc' }
  });
  res.json(tasks);
});
```

Copilot a compris : Prisma → `prisma.task`, ordre chronologique inverse, et format de réponse JSON.

---

### Étape 3 — Correction avec Cursor

**Problème :** Le POST /tasks n'empêche pas les titres en double.

**Dans Cursor :** Sélectionne le handler → Cmd+K → prompt :

```
Ce endpoint devrait rejeter les titres en double (case-insensitive).
Ajoute la vérification avant l'insertion en base.
```

**Résultat :**
```typescript
router.post('/', async (req, res) => {
  const data = taskSchema.parse(req.body);

  const existing = await prisma.task.findFirst({
    where: {
      title: { equals: data.title, mode: 'insensitive' }
    }
  });
  if (existing) {
    return res.status(409).json({ error: 'Cette tâche existe déjà' });
  }

  const task = await prisma.task.create({ data });
  res.status(201).json(task);
});
```

---

### Étape 4 — Documentation avec ChatGPT

**Prompt :**
```
Génère un README.md pour mon API Express/TypeScript/Prisma.
Inclus : installation, endpoints, exemples de requêtes, variables d'env.
Sois concis. Le projet s'appelle "task-api".
```

**Résultat :** Un README complet, bien formaté, prêt pour GitHub, généré en 10 secondes.

---

### Synthèse de la démo

| Étape | Action | Outil | Temps réel | Temps sans IA |
|-------|--------|-------|-----------|--------------|
| Init | Structure + Prisma | Claude | 2 min | ~20 min |
| Code | Route GET /tasks | Copilot | 30 sec | ~5 min |
| Bug | Doublon titre | Cursor | 1 min | ~10 min |
| Doc | README | ChatGPT | 10 sec | ~15 min |
| **Total** | | | **~4 min** | **~50 min** |

---

## A — Action (5 min)

1. **Va sur Claude.ai ou ChatGPT** et fais générer la structure d'une API Express sur un sujet de ton choix (recettes, utilisateurs, produits, etc.)

2. **Ouvre VS Code**, copie la structure, installe les dépendances, et utilise **Copilot/Cursor** pour écrire au moins un endpoint complet

3. **Note le temps** que tu as gagné vs une écriture manuelle :

   | Sans IA | Avec IA | Temps gagné |
   |---------|---------|-------------|
   | ~50 min | ~4 min  | **~46 min** |

> **Partage ton temps gagné** dans les commentaires du cours. Le plus rapide gagne... du temps pour la prochaine leçon.

---

**✅ Leçon 1.2 terminée.**

**Prochaine leçon :** Leçon 1.3 — Limites et bonnes pratiques : ce que l'IA ne peut PAS faire.
