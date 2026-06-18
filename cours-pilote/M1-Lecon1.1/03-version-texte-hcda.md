# Leçon 1.1 : Panorama des outils IA pour les développeurs

**Module :** M1 — Comprendre l'IA pour les développeurs
**Format :** 📖 Texte
**Durée estimée :** 10 min
**Niveau :** Intermédiaire

---

## H — Hook

Tu passes des heures à écrire du code répétitif — boilerplate, interfaces, routes CRUD — alors que la vraie valeur de ton travail est ailleurs. En parallèle, tu entends parler de GitHub Copilot, Cursor, Claude, ChatGPT, Gemini... mais tu ne sais pas lequel installer ni si ça vaut vraiment le coup.

Cette leçon va classer ces outils une bonne fois pour toutes.

---

## C — Concept

Il existe **trois grandes familles d'outils IA** pour les développeurs. Chacune a un usage, un contexte et une force différente.

### 1. Assistants dans l'IDE

| Outils | GitHub Copilot · Cursor · Codeium · Tabnine |
|--------|---------------------------------------------|
| **Contexte** | Intégrés dans VS Code, JetBrains, etc. |
| **Fonctionnement** | Analysent le fichier ouvert, le langage, les imports, et proposent des complétions en temps réel |
| **Force** | Vitesse pure — pas besoin de prompt, le code arrive pendant que tu tapes |
| **Usage** | Boilerplate, interfaces, tests unitaires, répétitions |

### 2. Chats généralistes

| Outils | Claude · ChatGPT · Gemini |
|--------|---------------------------|
| **Contexte** | Interfaces web ou API, indépendantes de l'IDE |
| **Fonctionnement** | Tu formules un prompt, l'IA réfléchit et répond avec explications + code |
| **Force** | Profondeur — explique, compare, conçoit, enseigne |
| **Usage** | Architecture, apprentissage, debug conceptuel, documentation |

### 3. Outils spécialisés

| Outils | Amazon Q Dev · Replit AI · Cody Sourcegraph |
|--------|----------------------------------------------|
| **Contexte** | Écosystèmes spécifiques (AWS, Replit, codebase legacy) |
| **Force** | Optimisés pour leur environnement |
| **Limite** | Moins polyvalents que les deux premières catégories |

### Stratégie conseillée

```
Maîtrise DEUX outils :
┌────────────────────┐   ┌────────────────────┐
│  Assistant IDE     │ + │  Chat généraliste  │
│  (Copilot/Cursor)  │   │  (Claude/ChatGPT)  │
│  → Vitesse         │   │  → Réflexion       │
│  → Code direct     │   │  → Conception      │
└────────────────────┘   └────────────────────┘
```

### Tableau comparatif complet

| Outil | Type | IDE ? | Gratuit ? | Idéal pour |
|-------|------|-------|-----------|------------|
| **GitHub Copilot** | Assistant IDE | Oui | Freemium (étudiants ✅) | Boilerplate, complétion |
| **Cursor** | Assistant IDE | Oui (IDE complet) | Freemium | Projets longs, refactoring |
| **Claude** | Chat généraliste | Non | Version gratuite | Architecture, explication |
| **ChatGPT** | Chat généraliste | Non | Version gratuite | Debug, apprentissage |
| **Gemini** | Chat généraliste | Non | Gratuit | Recherche, Google ecosystem |
| **Codeium** | Assistant IDE | Oui | Gratuit | Alternative à Copilot |

---

## D — Démo

### Scénario 1 : GitHub Copilot — Complétion boilerplate

**Contexte :** Tu crées un composant React TypeScript.

```typescript
// Fichier : UserProfile.tsx

// Tu tapes ça :
interface UserProfile {
  id: string;

// Copilot te propose automatiquement la suite :
  name: string;
  email: string;
  avatarUrl?: string;
  createdAt: Date;
  isActive: boolean;
}
```

**Ce qui s'est passé :** Copilot a reconnu le pattern d'interface TypeScript standard, a déduit les champs pertinents pour un "UserProfile", a correctement typé `createdAt` en `Date` (pas en `string`), et a marqué `avatarUrl` comme optionnel — tout ça sans que tu écrives le moindre prompt.

```typescript
// Puis tu tapes le composant :
const UserCard: React.FC<{ user: UserProfile }> = ({ user }) => (
  // Copilot propose directement la structure JSX :
  <div className="user-card">
    <img src={user.avatarUrl} alt={user.name} />
    <h3>{user.name}</h3>
    <p>{user.email}</p>
    <span className={`status ${user.isActive ? 'active' : 'inactive'}`}>
      {user.isActive ? 'Actif' : 'Inactif'}
    </span>
  </div>
);
```

---

### Scénario 2 : Claude — Conception d'architecture

**Contexte :** Tu veux réfléchir à la structure d'une API avant de coder.

**Prompt utilisateur :**
```
Je dois concevoir une API Express avec :
- Authentification JWT
- Connexion PostgreSQL
- Routes REST pour un blog (articles, catégories, utilisateurs)
- Validation des entrées

Donne-moi une structure de dossiers complète et le code
du middleware d'authentification.
```

**Réponse de Claude (résumé structuré) :**
```
/backend
├── src/
│   ├── middleware/
│   │   └── auth.js          ← Vérification JWT
│   ├── routes/
│   │   ├── articles.js
│   │   ├── categories.js
│   │   └── users.js
│   ├── models/
│   │   └── index.js         ← Connexion PostgreSQL
│   ├── controllers/
│   │   └── ...              ← Logique métier
│   └── app.js               ← Entry point
├── .env
└── package.json
```

**Middleware auth généré :**
```javascript
// middleware/auth.js
const jwt = require('jsonwebtoken');

const authenticate = (req, res, next) => {
  const header = req.headers.authorization;
  if (!header || !header.startsWith('Bearer ')) {
    return res.status(401).json({ error: 'Token manquant' });
  }

  try {
    const token = header.split(' ')[1];
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (err) {
    return res.status(403).json({ error: 'Token invalide ou expiré' });
  }
};
```

**Ce que Claude t'apporte en plus :** Il explique pourquoi le middleware doit être placé avant les routes protégées, pourquoi on sépare routes/controllers/models, et pourquoi le `try/catch` est important ici. Il t'enseigne la logique, pas juste le code.

---

### Scénario 3 : Cursor — Debug rapide

**Contexte :** Ton système de filtre ne marche pas quand la recherche contient des espaces.

**Code buggé :**
```typescript
const filtered = items.filter(item =>
  item.name.includes(searchTerm)
);
// Bug : si searchTerm = "hello world", la recherche échoue à cause
// des espaces et de la casse
```

**Dans Cursor :** Sélectionne le code → Cmd+K → Tape le prompt suivant :
```
Ce filtre ne fonctionne pas quand la recherche contient des espaces.
Corrige le problème en gardant la même structure.
```

**Résultat proposé par Cursor :**
```typescript
const filtered = items.filter(item =>
  item.name.toLowerCase().includes(searchTerm.toLowerCase().trim())
);
```

**Corrections apportées :**
1. `.toLowerCase()` — insensibilité à la casse
2. `.trim()` — suppression des espaces superflus dans la recherche

---

### Synthèse des apprentissages de la démo

| Scénario | Outil | Temps gagné | Compétence démontrée |
|----------|-------|-------------|---------------------|
| Boilerplate interface TS | Copilot | ~2 min | Complétion contextuelle |
| Architecture API REST | Claude | ~10 min | Conception + explication |
| Debug filtre | Cursor | ~5 min | Correction intelligente |

**Règle d'or :** L'IDE pour la **vitesse d'exécution**. Le chat pour la **qualité de réflexion**. Utilise les deux.

---

## A — Action

**⏱️ 5 minutes — à faire maintenant.**

### Tâche 1 : Assistant IDE

1. Ouvre VS Code (ou ton IDE préféré)
2. Crée un fichier `api.ts`
3. Commence à taper :

```typescript
async function fetchUserData(id: string) {
  const response = await fetch(
    // ← Laisse ton assistant IDE te proposer la suite
  );
}
```

4. Observe ce qu'il propose. Accepte, ajuste ou ignore — mais note son comportement.

### Tâche 2 : Chat généraliste

1. Va sur [claude.ai](https://claude.ai) ou [chatgpt.com](https://chatgpt.com)
2. Tape ce prompt exact :

```
Explique-moi la différence entre une Promise et async/await
en JavaScript avec un exemple simple.
```

3. Lis la réponse. Compare avec ce que tu aurais écrit toi-même.

### Objectif de l'action

Le but n'est pas de *tout comprendre* de la réponse. Le but est de **ressentir la différence** fondamentale :

- **Copilot** → Complète ton code en contexte → Productivité immédiate
- **Claude/ChatGPT** → T'explique un concept → Compréhension profonde

> 💬 **Partage ton expérience** dans les commentaires du cours. Quel outil t'a le plus surpris ? Lequel comptes-tu utiliser en priorité ?

---

**✅ Leçon 1.1 terminée.**

**Prochaine étape :** Leçon 1.2 — Cas d'usage concrets : comment ces outils s'intègrent dans un vrai projet web, de l'initialisation au déploiement.
