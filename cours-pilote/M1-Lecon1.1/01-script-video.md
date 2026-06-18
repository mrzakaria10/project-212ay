# Leçon 1.1 — Panorama des outils IA pour les développeurs
## Script Vidéo — Durée : ~10 min

**Ton : professionnel, direct, orienté pratique**
**Format : face caméra + écran partagé (slides / démos code)**

---

### [0:00 — 0:30] INTRO HOOK — 30 secondes

**(Plan : face caméra, fond sobre, éclairage neutre. Calme, direct.)**

> Tu passes des heures à écrire du boilerplate alors que ton vrai problème, c'est la logique métier ? Tu sais que des outils IA existent, mais tu ne sais pas par lequel commencer ni lequel est vraiment utile au quotidien ?
>
> Bienvenue dans la Leçon 1.1. On va faire un tour d'horizon des outils IA pour développeurs — pas pour te vendre du rêve, mais pour que tu saches exactement quoi utiliser, quand et pourquoi.

---

### [0:30 — 3:30] CONCEPT — 3 minutes

**(Plan : orateur + slide partagé)**

**Orateur :**
> Il y a deux ans, coder sans IA était normal. Aujourd'hui, coder sans IA, c'est comme refuser d'utiliser l'autocomplétion dans VS Code. Les outils ont explosé, mais ils se classent en trois grandes familles.

**[SLIDE — 3 familles]**
```
┌─────────────────────────────────────────────────────────────┐
│  1. Assistants IDE    │  2. Chats généralistes  │  3. Spécialisés │
│  GitHub Copilot      │  Claude                │  Amazon Q Dev   │
│  Cursor              │  ChatGPT               │  Tabnine        │
│  Codeium             │  Gemini                │  Replit AI      │
│  Complétion temps    │  Explication,          │  Écosystème     │
│  réel dans l'éditeur │  architecture, doc     │  spécifique     │
└─────────────────────────────────────────────────────────────┘
```

**Orateur :**
> Les **assistants dans l'IDE** — Copilot, Cursor — sont tes compagnons du quotidien. Ils analysent ton contexte en temps réel : le fichier ouvert, le langage, les imports. C'est comme avoir un pair programmer silencieux qui propose la suite du code sans que tu aies à ouvrir un chat.
>
> Les **chats généralistes** — Claude, ChatGPT — sont parfaits pour les tâches qui sortent de ton éditeur : réfléchir à une architecture, générer un plan de projet, traduire un algorithme, ou poser une question conceptuelle.
>
> Les **outils spécialisés** — Amazon Q, Replit AI — sont optimisés pour des écosystèmes précis. Utiles dans leur domaine, moins polyvalents.

**[SLIDE — Tableau comparatif]**
```
┌──────────────────┬────────────────────────────┬─────────────────┐
│ Outil            │ Usage principal            │ Gratuit ?       │
├──────────────────┼────────────────────────────┼─────────────────┤
│ GitHub Copilot   │ Complétion dans VS Code    │ Freemium        │
│                  │                            │ (étudiants ✅)   │
├──────────────────┼────────────────────────────┼─────────────────┤
│ Cursor           │ IDE complet avec IA        │ Freemium        │
├──────────────────┼────────────────────────────┼─────────────────┤
│ Claude           │ Réflexion, explication,    │ Version gratuite│
│                  │ documentation              │                 │
├──────────────────┼────────────────────────────┼─────────────────┤
│ ChatGPT          │ Debug, code, apprentissage │ Version gratuite│
├──────────────────┼────────────────────────────┼─────────────────┤
│ Gemini           │ Recherche, écosystème      │ Gratuit         │
│                  │ Google                     │                 │
└──────────────────┴────────────────────────────┴─────────────────┘
```

**Orateur :**
> Le piège, c'est de vouloir tout utiliser. La bonne stratégie ? En maîtriser **deux** : un assistant IDE pour la vitesse au quotidien, et un chat généraliste pour la réflexion.

---

### [3:30 — 8:30] DÉMO — 5 minutes

**(Plan : écran plein, voix off. Démo enregistrée ou rejouée en direct.)**

**Orateur :**
> Assez de théorie. On passe à trois scénarios concrets.

---

#### SCÉNARIO 1 — GitHub Copilot dans VS Code (2 min)

**[Écran : VS Code, fichier UserProfile.tsx]**

> J'ouvre un fichier React TypeScript vierge. Je commence à taper une interface.

```
// Je tape :
interface UserProfile {
  id: string;
```

> Sans que je fasse rien d'autre, Copilot me propose automatiquement la suite :

```
  name: string;
  email: string;
  avatarUrl?: string;
  createdAt: Date;
  isActive: boolean;
}
```

> Regarde ce qui s'est passé : Copilot a détecté que j'écrivais une interface TypeScript. Il m'a proposé `avatarUrl` optionnel avec le `?`, il a mis `createdAt` en `Date` plutôt qu'en `string`, et il a complété avec des champs réalistes — `isActive`, `email`. Tout ça sans un seul prompt, sans ouvrir un chat, sans quitter mon clavier.

> Je tape maintenant `function UserCard({ user }: { user: UserProfile })` et le squelette du composant s'écrit sous mes doigts.

---

#### SCÉNARIO 2 — Claude pour l'architecture (1 min 30)

**[Écran : interface Claude.ai ou ChatGPT]**

> Deuxième scénario. Je ne suis pas dans mon IDE — je veux réfléchir à une architecture. J'ouvre Claude et je tape ce prompt :

```
Je dois concevoir une API Express avec :
- Authentification JWT
- Connexion PostgreSQL
- Routes REST pour un blog (articles, catégories, utilisateurs)
- Validation des entrées

Donne-moi une structure de dossiers complète et le code
du middleware d'authentification.
```

**[Faire défiler la réponse de Claude — arborescence + code]**

> Ce qui est intéressant ici, ce n'est pas juste le code. Claude m'explique **pourquoi** le middleware doit être placé avant les routes protégées, **pourquoi** il faut séparer les dossiers `routes/`, `middleware/`, `controllers/`. Il m'enseigne une structure, pas juste une syntaxe.

---

#### SCÉNARIO 3 — Cursor pour le debug rapide (1 min 30)

**[Écran : Cursor IDE, code sélectionné]**

> Troisième cas : je reçois un bug en production. Mon système de filtre ne marche pas quand la recherche contient des espaces.

```
// Code buggé :
const filtered = items.filter(item =>
  item.name.includes(searchTerm)
);
```

> Je sélectionne le code, je fais **Cmd+K** dans Cursor, et je tape :

```
Ce filtre ne fonctionne pas quand la recherche contient des espaces.
Corrige le problème en gardant la même structure.
```

**[Cursor propose la correction]**

> En 5 secondes, Cursor me renvoie la version corrigée avec `trim()` et `toLowerCase()` :

```
const filtered = items.filter(item =>
  item.name.toLowerCase().includes(searchTerm.toLowerCase().trim())
);
```

---

**[SLIDE — Récapitulatif démo]**

```
┌──────────────────────────┬────────────────────┬──────────────┐
│ Scénario                 │ Outil              │ Temps gagné  │
├──────────────────────────┼────────────────────┼──────────────┤
│ Boilerplate interface TS │ Copilot (IDE)      │ ~2 min       │
│ Architecture API REST    │ Claude (Chat)      │ ~10 min      │
│ Debug filtre avec espaces │ Cursor (IDE)      │ ~5 min       │
└──────────────────────────┴────────────────────┴──────────────┘
```

**Orateur :**
> Ce que tu dois retenir : l'IDE pour la **vitesse**, le chat pour la **réflexion**. Les deux se complètent. Un développeur efficace utilise les deux, pas un seul.

---

### [8:30 — 9:30] ACTION — 1 minute

**(Plan : retour face caméra.)**

**Orateur :**
> Maintenant, c'est à toi. Voici ta tâche concrète pour cette leçon. Ça te prendra **5 minutes max** :

> **1.** Ouvre VS Code, crée un fichier `api.ts`, et commence à taper une fonction `fetchUserData(id: string)`. Regarde ce que ton assistant IDE te propose. Accepte ou refuse, mais **observe**.

> **2.** Va sur Claude.ai ou ChatGPT, et tape ce prompt :
>
> *"Explique-moi la différence entre une Promise et async/await en JavaScript avec un exemple simple."*

> Le but n'est pas de tout comprendre du premier coup. Le but, c'est de **ressentir la différence** entre un outil qui *complète* (Copilot) et un outil qui *explique* (Claude).

> Partage ton ressenti dans les commentaires du cours.

---

### [9:30 — 10:00] OUTRO — 30 secondes

**(Plan : face caméra, sourire professionnel.)**

> Voilà pour cette Leçon 1.1. Tu sais maintenant classer les outils IA en trois familles et tu as une stratégie pour choisir les tiens.
>
> Dans la prochaine leçon, on passe aux cas d'usage concrets — tu vas voir comment ces outils s'intègrent dans un vrai projet web, étape par étape.
>
> Je te laisse. Va faire l'action.

**[Fondu au noir — Écran : 212ay.com / logo + "Continuez votre progression → Leçon 1.2"]**
