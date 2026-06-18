# Leçon 1.2 : Cas d'usage concrets

**Module :** M1 — Comprendre l'IA pour les développeurs
**Format :** 📖 Texte
**Durée estimée :** 12 min
**Niveau :** Intermédiaire

---

## H — Hook

Tu connais les outils IA, tu as vu des démos sur YouTube — mais concrètement, à quoi ça ressemble d'utiliser l'IA du début à la fin d'une vraie fonctionnalité ? Est-ce que ça change vraiment la façon de coder, ou est-ce juste un coup de com' ?

Dans cette leçon, on construit une **API Todo complète** avec Express et SQLite, en utilisant l'IA à chaque étape. Tu vas voir le workflow réel : conception, génération, correction.

---

## C — Concept

Le workflow d'une fonctionnalité avec l'IA suit **3 phases** :

### Phase 1 : Conception avec un chat généraliste

Avant d'écrire une ligne de code, utilise Claude/ChatGPT pour **réfléchir** :
- Schéma de base de données
- Structure des dossiers et fichiers
- Choix techniques (middleware, validation, etc.)
- Ordre des routes et dépendances

> **Pourquoi un chat ?** Parce que la conception est une discussion. Tu poses des contraintes, l'IA propose, tu ajustes. Copilot ne peut pas faire ça — il ne voit que le fichier ouvert.

### Phase 2 : Génération avec un assistant IDE

Une fois le plan validé, utilise Copilot/Cursor pour **écrire le code** :
- Routes CRUD boilerplate
- Middleware standard
- Connexion base de données
- Configuration serveur

> **Pourquoi un assistant IDE ?** Parce que la génération est séquentielle. Copilot voit chaque fichier dans son contexte et propose le code juste au moment où tu en as besoin.

### Phase 3 : Correction et raffinement

Enfin, utilise un outil comme Cursor pour **améliorer** :
- Ajouter de la validation
- Gérer les cas d'erreur
- Refactorer le code
- Ajouter des commentaires et de la documentation

> **Règle d'or :** La phase 1 guide les phases 2 et 3. Ne saute jamais la conception — un mauvais plan génère du mauvais code, même avec la meilleure IA.

---

## D — Démo

### Projet : API Todo avec Express + SQLite

#### Phase 1 — Conception avec Claude

**Prompt :**
```
Je construis une API REST Todo avec Express et SQLite.
Je veux :
- Un modèle Task avec : id, title, completed (boolean),
  createdAt, priority (low/medium/high)
- Routes CRUD complètes
- Validation des entrées
- Gestion d'erreurs centralisée

Donne-moi le schéma de la base et la structure des dossiers.
```

**Résultat Claude :**

```
📁 projet/
├── src/
│   ├── database/
│   │   └── schema.sql
│   ├── routes/
│   │   └── tasks.js
│   ├── middleware/
│   │   ├── validateTask.js
│   │   └── errorHandler.js
│   └── app.js
├── .env
└── package.json
```

**Schéma SQL généré :**
```sql
CREATE TABLE tasks (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  title TEXT NOT NULL,
  completed BOOLEAN DEFAULT 0,
  priority TEXT CHECK(priority IN ('low', 'medium', 'high')) DEFAULT 'medium',
  createdAt DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

Claude explique aussi pourquoi `AUTOINCREMENT`, pourquoi `CHECK` pour la priorité, et pourquoi séparer la validation dans un middleware dédié.

---

#### Phase 2 — Génération avec Copilot

Avec la structure en tête, on ouvre VS Code.

**app.js** — On tape le démarrage, Copilot complète :
```javascript
const express = require('express');
const app = express();
app.use(express.json());

// Copilot propose :
const tasksRouter = require('./routes/tasks');
app.use('/api/tasks', tasksRouter);

// Puis le serveur :
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Serveur démarré sur le port ${PORT}`);
});
```

**routes/tasks.js** — Copilot génère les routes CRUD :
```javascript
const express = require('express');
const router = express.Router();
const { getDb } = require('../database/db');

// GET /api/tasks — Liste toutes les tâches
router.get('/', (req, res) => {
  const db = getDb();
  const tasks = db
    .prepare('SELECT * FROM tasks ORDER BY createdAt DESC')
    .all();
  res.json(tasks);
});

// POST /api/tasks — Crée une tâche
router.post('/', validateTask, (req, res) => {
  const { title, priority } = req.body;
  const db = getDb();
  const result = db
    .prepare('INSERT INTO tasks (title, priority) VALUES (?, ?)')
    .run(title, priority || 'medium');
  res.status(201).json({ id: result.lastInsertRowid });
});

// PUT /api/tasks/:id — Met à jour une tâche
router.put('/:id', validateTask, (req, res) => {
  const { title, completed, priority } = req.body;
  const db = getDb();
  db.prepare(
    `UPDATE tasks SET title = ?, completed = ?, priority = ?
     WHERE id = ?`
  ).run(title, completed, priority, req.params.id);
  res.json({ success: true });
});

// DELETE /api/tasks/:id — Supprime une tâche
router.delete('/:id', (req, res) => {
  const db = getDb();
  db.prepare('DELETE FROM tasks WHERE id = ?').run(req.params.id);
  res.json({ success: true });
});

module.exports = router;
```

Ce qui est remarquable : Copilot a deviné l'import de `getDb`, l'usage de `prepare().run()`, le `|| 'medium'` pour la priorité par défaut, le `res.status(201)` pour la création, et même la présence du middleware `validateTask` — tout ça sans que tu aies à le lui demander explicitement.

---

#### Phase 3 — Correction avec Cursor

Le middleware `validateTask` existe mais il est vide ou basique. On utilise Cursor pour le compléter.

**Action :** Sélectionner le fichier `middleware/validateTask.js` → Cmd+K → prompt :

```
Ajoute une validation complète avec Joi :
- title : string requis, 3-100 caractères
- priority : enum low/medium/high, défaut medium
- completed : boolean optionnel
Retourne des messages d'erreur clairs en français.
```

**Résultat Cursor en 5 secondes :**
```javascript
const Joi = require('joi');

const taskSchema = Joi.object({
  title: Joi.string()
    .min(3)
    .max(100)
    .required()
    .messages({
      'string.empty': 'Le titre est requis',
      'string.min': 'Le titre doit contenir au moins 3 caractères',
      'string.max': 'Le titre ne peut pas dépasser 100 caractères'
    }),
  priority: Joi.string()
    .valid('low', 'medium', 'high')
    .default('medium'),
  completed: Joi.boolean().optional()
});

const validateTask = (req, res, next) => {
  const { error, value } = taskSchema.validate(req.body, {
    abortEarly: false
  });

  if (error) {
    const messages = error.details.map(d => d.message);
    return res.status(400).json({ errors: messages });
  }

  req.body = value;
  next();
};

module.exports = validateTask;
```

En 30 secondes, on a une validation production-ready avec Joi, messages en français, et gestion des erreurs multiples (`abortEarly: false`).

---

### Synthèse : le workflow complet

| Phase | Outil | Durée sans IA | Durée avec IA | Gain |
|-------|-------|---------------|---------------|------|
| 1. Conception | Claude | 15 min | 3 min | 80% |
| 2. Génération | Copilot | 20 min | 5 min | 75% |
| 3. Correction | Cursor | 10 min | 2 min | 80% |
| **Total** | | **45 min** | **~10 min** | **~75%** |

---

## A — Action

**⏱️ 5 minutes — à faire maintenant.**

### Tâche 1 : Conception avec IA

Va sur Claude.ai ou ChatGPT et tape ce prompt :

```
Conçois-moi le schéma et les routes d'une API de blog
avec Express et SQLite avec :
- titre, contenu, auteur, date de création
- catégorie, status (brouillon/publié)
```

Lis la réponse. Note la structure proposée.

### Tâche 2 : Génération avec IDE

Ouvre VS Code, crée `app.js`, et commence à taper une API Express :
```javascript
const express = require('express');
// ← Laisse Copilot te proposer la suite
```

Observe si ce que Copilot génère est cohérent avec le plan de Claude.

### Question réflexion

> Est-ce que la structure proposée par Claude correspond à ce que Copilot a généré ? Si non, quelle approche te semble la plus pertinente ?

Partage ta réponse dans les commentaires du cours.

---

**✅ Leçon 1.2 terminée.**

**Prochaine étape :** Leçon 1.3 — Limites et bonnes pratiques : comprendre où l'IA échoue et comment garder un esprit critique.
