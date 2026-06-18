# Leçon 1.3 — Limites et bonnes pratiques
## Script Vidéo — Durée : ~10 min

---

### [0:00 — 0:30] INTRO HOOK

> L'IA peut générer du code, corriger des bugs, écrire de la doc. Mais elle peut aussi inventer des fonctions qui n'existent pas, suggérer des failles de sécurité, et vous faire perdre des heures si vous lui faites trop confiance.
>
> Cette leçon est la plus importante du module. On va parler de ce que l'IA ne peut PAS faire.

---

### [0:30 — 3:00] CONCEPT — Les 3 grandes limites

**(Slide : 3 avertissements)**

**Orateur :**
> L'IA a trois limites fondamentales que tout développeur doit connaître :

> **1. Hallucinations** — L'IA invente des choses. Elle va vous sortir une fonction `prisma.task.findDuplicate()` qui n'existe pas, une méthode `Array.prototype.groupBy()` qui n'est pas standard, ou une API imaginaire. Elle ne sait pas dire "je ne sais pas".

> **2. Pas de compréhension réelle** — L'IA ne comprend PAS votre code. Elle prédit la suite statistiquement. Elle peut générer du code qui compile mais qui fait n'importe quoi.

> **3. Contexte limité** — Au-delà d'une certaine taille de code, l'IA oublie le début du fichier ou les dépendances.

**(Slide : Le piège du "ça a l'air correct")**

> Le piège numéro 1 : le code généré *a l'air* correct. Il est bien formaté, les noms de variables sont cohérents, les commentaires sont propres. Mais la logique peut être complètement erronée.

---

### [3:00 — 6:30] DÉMO — 3 pièges en action

#### Piège 1 — L'API imaginaire (2 min)

**(Écran : VS Code + Copilot)**

> Je demande à Copilot de générer une fonction qui fait une recherche avancée :

```typescript
// Je tape :
async function searchUsers(query: string) {
  const results = await prisma.user.searchVector(query); // ← Cette méthode N'EXISTE PAS
```

> Copilot propose `searchVector` comme si c'était une méthode Prisma standard. Elle n'existe pas. Si tu ne vérifies pas la doc, tu passes 30 minutes à chercher pourquoi ça ne marche pas.

#### Piège 2 — La faille de sécurité (2 min)

> Je demande à ChatGPT une fonction de téléchargement de fichier :

```
// ChatGPT me propose ça — apparemment correct :
app.get('/download/:file', (req, res) => {
  const filePath = path.join('/uploads', req.params.file);
  res.download(filePath);
});
```

> Problème : path traversal attack. Un utilisateur peut faire `/download/../../etc/passwd`. L'IA n'a pas pensé à la sécurité. C'est à TOI de valider.

#### Piège 3 — Le code qui a l'air correct (1 min)

```
// Ce code "marche" mais est faux logiquement :
function getAverage(numbers: number[]) {
  const sum = numbers.reduce((a, b) => a + b, 0);
  return sum / numbers.length; // Si le tableau est vide, division par zéro
}
```

> L'IA ne gère pas toujours les edge cases. C'est à toi d'ajouter la vérification.

---

### [6:30 — 8:30] BONNES PRATIQUES

**(Slide : Checklist de confiance)**

**Orateur :**
> Voici les 5 règles à suivre pour utiliser l'IA SANS danger :

> **1. TOUJOURS lire le code généré** avant de l'exécuter. Toujours. Sans exception.

> **2. TOUJOURS tester** ce que l'IA produit. Surtout les cas limites (vide, null, valeurs extrêmes).

> **3. Ne JAMAIS copier-coller** du code que tu ne comprends pas. Si tu ne peux pas l'expliquer, tu ne peux pas le maintenir.

> **4. Vérifier la sécurité** — l'IA ne pense pas aux injections, path traversal, ou auth bypass.

> **5. Utiliser l'IA comme accélérateur**, pas comme substitut. Tu es le pilote, elle est le copilote.

**(Slide : Règle d'or)**
```
┌────────────────────────────────────────────┐
│  RÈGLE D'OR :                              │
│                                            │
│  "L'IA écrit le code.                      │
│   TOI, tu décides ce qui est bon."         │
└────────────────────────────────────────────┘
```

---

### [8:30 — 9:30] ACTION

> Ta mission pour cette leçon :
>
> **1.** Récupère un code généré par IA que tu as dans un de tes projets (ou génères-en un avec ChatGPT).
>
> **2.** Relis-le ligne par ligne. Cherche :
>    - Une fonction ou méthode qui n'existe pas
>    - Un edge case non géré (tableau vide, null, etc.)
>    - Une faille de sécurité potentielle
>
> **3.** Si tu trouves au moins un problème, tu valides la leçon. Si tu n'en trouves pas, c'est que tu n'as pas assez cherché 😉

---

### [9:30 — 10:00] OUTRO — Bilan du module

> Ce module est terminé. Tu sais maintenant :
> - Classer les outils IA en 3 familles (Leçon 1.1)
> - Utiliser le bon outil au bon moment dans un projet (Leçon 1.2)
> - Reconnaître les limites et appliquer les bonnes pratiques (Leçon 1.3)
>
> Prochaine étape : **le quiz du module 1**. 4 questions, 70% pour valider.
>
> Rendez-vous au Module 2 : "Prompter efficacement pour générer du code".
