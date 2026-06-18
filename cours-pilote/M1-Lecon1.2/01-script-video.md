# Leçon 1.2 — Cas d'usage concrets
## Script Vidéo — Durée : ~12 min

---

### [0:00 — 0:30] INTRO HOOK

**(Face caméra)**

> Tu sais maintenant qu'il existe trois familles d'outils IA. Mais dans ton quotidien de développeur, à quel moment précis s'en servir ? Est-ce que tu utilises Claude pour tout, ou Copilot pour tout ?
>
> Dans cette leçon, on va suivre un mini-projet réel du début à la fin — et je vais te montrer quel outil utiliser à chaque étape.

---

### [0:30 — 3:30] CONCEPT — Les 4 moments clés

**(Slide : frise chronologique d'un projet)**

**Orateur :**
> Dans la vie d'un projet web, il y a **4 moments** où l'IA est la plus utile :

**[SLIDE]**
```
┌──────────────┬──────────────┬──────────────┬──────────────┐
│ 1. INIT      │ 2. CODE      │ 3. CORRIGER  │ 4. FINALISER │
│ Boilerplate  │ Routes       │ Bugs         │ Doc          │
│ Structure    │ Composants   │ Refactoring  │ Tests        │
│ DB Schema    │ Logique      │ Performances │ Déploiement  │
├──────────────┼──────────────┼──────────────┼──────────────┤
│ → Chat (C)   │ → IDE (Cop)  │ → IDE + Chat │ → Chat (C)   │
└──────────────┴──────────────┴──────────────┴──────────────┘
```

**Orateur :**
> * **Initialisation** — poser la structure, le plan. Meilleur outil : **Claude/ChatGPT** (chat). On a besoin de réflexion, pas de vitesse.
> * **Développement** — écrire le code. Meilleur outil : **Copilot/Cursor** (IDE). On a besoin de vitesse, pas de réflexion.
> * **Correction** — bugs, refactoring. Outil : **IDE + Chat** selon la complexité.
> * **Finalisation** — documentation, tests. Meilleur outil : **Chat** pour générer, **IDE** pour valider.

---

### [3:30 — 9:00] DÉMO — Mini-projet : API de gestion de tâches

**(Écran : terminal + VS Code + Claude)**

**Orateur :**
> On va construire une API de gestion de tâches. Je vais utiliser l'IA à chaque étape, mais pas le même outil.

---

#### Étape 1 — Initialisation avec Claude (2 min)

> J'ouvre Claude et je tape :

```
Je veux créer une API REST avec Express + TypeScript + Prisma (SQLite)
pour une todolist. L'API doit avoir :
- CRUD complet sur les tâches (title, completed, createdAt)
- Validation des entrées avec Zod
- Un système d'erreurs cohérent

Donne-moi la commande d'initialisation et la structure de dossiers.
```

**[Montrer la réponse]**
```
npm init -y
npm install express prisma @prisma/client zod
npm install -D typescript ts-node @types/express

mkdir src/routes src/middleware src/lib

// schema.prisma
model Task {
  id        Int      @id @default(autoincrement())
  title     String
  completed Boolean  @default(false)
  createdAt DateTime @default(now())
}
```

> Claude me fournit aussi le code du router, du middleware d'erreurs, et les schémas Zod. En un seul prompt, j'ai l'architecture complète.

---

#### Étape 2 — Développement avec Copilot (2 min)

> Maintenant que la structure est posée, j'ouvre VS Code et je commence à coder l'endpoint GET /tasks.

**[VS Code screen]**

```
// Je tape :
app.get('/tasks', async (req, res) => {
  // Copilot me propose directement :
  const tasks = await prisma.task.findMany({
    orderBy: { createdAt: 'desc' }
  });
  res.json(tasks);
});
```

> Copilot a compris que j'utilise Prisma, que ma table s'appelle `task`, et que je veux un tri chronologique. Je n'ai même pas fini ma phrase.

---

#### Étape 3 — Bug avec Cursor (1 min 30)

> Je me rends compte que le POST /tasks ne valide pas correctement les doublons. Je sélectionne le handler dans Cursor, Cmd+K :

```
Ce endpoint devrait rejeter les titres en double (case-insensitive).
Ajoute la vérification avant l'insertion en base.
```

**[Cursor propose la correction]**
```typescript
app.post('/tasks', async (req, res) => {
  const { title } = req.body;

  const existing = await prisma.task.findFirst({
    where: { title: { equals: title, mode: 'insensitive' } }
  });
  if (existing) {
    return res.status(409).json({ error: 'Une tâche avec ce titre existe déjà' });
  }

  const task = await prisma.task.create({ data: { title } });
  res.status(201).json(task);
});
```

---

#### Étape 4 — Documentation avec ChatGPT (1 min)

> Je finis le projet, j'ouvre ChatGPT :

```
Génère un README.md pour mon API Express/TypeScript/Prisma.
Inclus : installation, endpoints, exemples de requêtes, variables d'env.
Sois concis. Le projet s'appelle "task-api".
```

**[Slide : README généré]**
> En 10 secondes, j'ai un README complet, bien formaté, prêt à commit.

---

**[SLIDE — Récap]**
```
┌──────────┬──────────────────────┬────────────┬──────────┐
│ Étape    │ Action               │ Outil      │ Temps    │
├──────────┼──────────────────────┼────────────┼──────────┤
│ Init     │ Structure + Prisma   │ Claude     │ 2 min    │
│ Code     │ Route GET /tasks     │ Copilot    │ 30 sec   │
│ Bug      │ Doublon titre        │ Cursor     │ 1 min    │
│ Doc      │ README               │ ChatGPT    │ 10 sec   │
└──────────┴──────────────────────┴────────────┴──────────┘
```

**Orateur :**
> Ce que tu dois retenir : **chaque outil a son moment**. Claude pour réfléchir, Copilot pour coder, Cursor pour corriger, ChatGPT pour finaliser.

---

### [9:00 — 10:00] ACTION

> Maintenant c'est à toi. Voici ta mission :
>
> **1.** Va sur Claude/ChatGPT et fais générer la structure d'une API (n'importe quel sujet — recettes, utilisateurs, produits).
>
> **2.** Copie la structure, ouvre VS Code, et utilise Copilot pour écrire **au moins un endpoint** — laisse-le te proposer la suite.
>
> **3.** Note le temps que tu as gagné par rapport à une écriture manuelle.
>
> Partage ton temps gagné dans les commentaires !

---

### [10:00 — 10:30] OUTRO

> Dans la prochaine leçon, on parle des **limites** — ce que l'IA ne peut PAS faire, et les erreurs à éviter. C'est la leçon la plus importante du module, ne la saute pas.
>
> Je te laisse, va coder.
