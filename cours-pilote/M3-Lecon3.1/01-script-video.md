# Leçon 3.1 — Expliquer une erreur avec contexte
## Script Vidéo — ~14 min

### [0:00-0:30] HOOK
> Tu colles une erreur dans ChatGPT, il te donne une réponse vague, tu passes 30 minutes à chercher. Le problème ? Tu lui as donné le symptôme sans le contexte. Cette leçon va changer ta façon de déboguer.

### [0:30-3:00] CONCEPT — La méthode CESE

**(Slide)** Les 4 ingrédients d'un bon debug prompt :

```
C — Code     : colle le bloc incriminé
E — Erreur   : message d'erreur exact (pas "ça marche pas")
S — Stack    : technos, versions, dépendances
E — Essai    : ce que tu as déjà testé
```

> Sans ces 4 éléments, l'IA répond au hasard. Avec, elle peut identifier la cause précise.

### [3:00-8:00] DÉMO — 3 bugs du quotidien

**Bug 1 — Erreur Prisma :**
```
MOYEN :
"J'ai une erreur Prisma"

FORT (CESE) :
"Code : const user = await prisma.user.findUnique({where:{email}})
 Erreur : 'TypeError: Cannot read properties of undefined'
 Stack : Express + Prisma + PostgreSQL, Node 18
 Essai : J'ai vérifié que l'email est bien une string"
```

**Bug 2 — React state non mis à jour :**
```
FORT :
"Code : [count, setCount] = useState(0); handleClick()
 Erreur : setCount(count+1) ne met pas à jour l'affichage dans le setTimeout
 Stack : React 18, Next.js 14
 Essai : J'ai essayé avec useRef, même problème"
```

**Bug 3 — 404 sur API Next.js :**
```
FORT :
"Code : route.ts dans app/api/test
 Erreur : GET /api/test renvoie 404
 Stack : Next.js 14 App Router
 Essai : Le fichier est bien nommé route.ts"
```

### [8:00-9:00] ACTION
> Prends une erreur récente que tu as eue. Rédige un prompt CESE. Teste-le dans ChatGPT/Claude. Compare avec ta méthode précédente.

### [9:00-9:30] OUTRO
> Prochaine leçon : refactorer un composant existant avec l'IA.
