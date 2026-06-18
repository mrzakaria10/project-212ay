# Leçon 1.3 : Limites et bonnes pratiques

**Module :** M1 — Comprendre l'IA pour les développeurs
**Durée :** 10 min

---

## H — Hook

L'IA peut générer du code, corriger des bugs, écrire de la doc. Mais elle peut aussi inventer des fonctions qui n'existent pas, suggérer des failles de sécurité, et vous faire perdre des heures si vous lui faites trop confiance.

C'est la leçon la plus importante du module.

---

## C — Concept : Les 3 grandes limites

### 1. Hallucinations

L'IA invente des choses. Elle peut proposer :
- Une méthode `prisma.user.searchVector()` qui n'existe pas
- Une API imaginaire `fetchWithRetry()` qui n'est dans aucune spec
- Des chiffres, des versions de packages, des noms de fonctions faux

L'IA ne sait pas dire **"je ne sais pas"**. Elle va toujours produire quelque chose, même si c'est faux.

### 2. Pas de compréhension réelle

L'IA ne **comprend pas** votre code. Elle prédit statistiquement la suite d'une séquence de tokens. Elle peut générer du code qui :
- Compile mais fait n'importe quoi
- Semble correct mais est logiquement faux
- Oublie des cas d'usage spécifiques à votre domaine

### 3. Contexte limité

Au-delà de ~100 000 tokens (quelques fichiers), l'IA perd le fil. Elle peut :
- Oublier des imports ou dépendances
- Ignorer des contraintes posées plus tôt
- Produire du code incohérent avec le reste du projet

---

## D — Démo : 3 pièges en action

### Piège 1 — L'API imaginaire

```typescript
// Prompt : "Génère une fonction de recherche utilisateur avec Prisma"
async function searchUsers(query: string) {
  const results = await prisma.user.searchVector(query);
  // ⚠️ searchVector() n'existe pas dans Prisma
  return results;
}
```

**Le problème :** La méthode `searchVector()` semble plausible mais n'existe pas. Si tu ne vérifies pas la doc Prisma, tu passes 30 minutes à debuguer.

**La solution :** Vérifier la documentation officielle. Utiliser `findMany` avec `where` + `contains` à la place.

### Piège 2 — La faille de sécurité

```typescript
// Prompt : "Endpoint de téléchargement de fichier"
app.get('/download/:file', (req, res) => {
  const filePath = path.join('/uploads', req.params.file);
  res.download(filePath);
  // ⚠️ Path traversal : /download/../../etc/passwd
});
```

**Le problème :** Un attaquant peut faire `/download/../../etc/passwd` pour lire n'importe quel fichier du système.

**La solution :** Valider le paramètre, interdire les `..`, limiter à un dossier précis.

### Piège 3 — Edge case oublié

```typescript
function getAverage(numbers: number[]) {
  const sum = numbers.reduce((a, b) => a + b, 0);
  return sum / numbers.length;
  // ⚠️ Division par zéro si le tableau est vide
}
```

**Le problème :** `numbers.length === 0` → division par zéro → `Infinity`.

**La solution :**
```typescript
function getAverage(numbers: number[]): number {
  if (numbers.length === 0) return 0;
  return numbers.reduce((a, b) => a + b, 0) / numbers.length;
}
```

---

## B — Bonnes pratiques : Les 5 règles d'or

```
┌─────────────────────────────────────────────────────────┐
│  5 RÈGLES POUR CODER AVEC L'IA SANS RISQUE              │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  1. TOUJOURS lire le code généré avant de l'exécuter     │
│                                                          │
│  2. TOUJOURS tester les cas limites (vide, null, extrême)│
│                                                          │
│  3. Ne JAMAIS copier du code que tu ne comprends pas     │
│                                                          │
│  4. Vérifier la sécurité (injections, path traversal)    │
│                                                          │
│  5. L'IA est un accélérateur, PAS un substitut           │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

### Règle d'or
> **L'IA écrit le code. TOI, tu décides ce qui est bon.**

### Checklist avant d'accepter du code IA
- [ ] J'ai lu chaque ligne
- [ ] Je comprends ce que fait le code
- [ ] Les cas limites sont gérés
- [ ] Pas de faille de sécurité évidente
- [ ] Les noms de fonctions/méthodes existent vraiment

---

## A — Action (5 min)

1. Récupère un code généré par IA depuis un de tes projets, ou génère-en un nouveau avec ChatGPT sur un sujet que tu maîtrises

2. Relis-le **ligne par ligne** en cherchant :
   - Une fonction ou méthode qui n'existe pas dans la doc officielle
   - Un edge case non géré (tableau vide, objet null, valeur négative)
   - Une faille de sécurité potentielle

3. Si tu trouves **au moins un problème**, tu valides la leçon. Si tu n'en trouves pas, creuse plus loin — il y en a toujours un.

---

## 🎯 Bilan du Module 1

| Leçon | Compétence acquise |
|-------|-------------------|
| 1.1 — Panorama | Classer les outils en 3 familles |
| 1.2 — Cas d'usage | Utiliser le bon outil au bon moment |
| 1.3 — Limites | Garder un esprit critique et appliquer les bonnes pratiques |

**Prochaine étape :** ✅ Quiz du Module 1 → Module 2 : Prompter efficacement pour générer du code.
