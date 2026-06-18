# Leçon 3.1 : Expliquer une erreur avec contexte
## Version Texte HCDA

## H — Hook
Tu colles une erreur dans ChatGPT, réponse vague, 30 min perdues. Le problème ? Tu donnes le symptôme sans le contexte.

## C — Concept : Méthode CESE

| Élément | Pourquoi | Exemple |
|---------|----------|---------|
| **C** Code | Voir exactement ce qui plante | Le bloc incriminé |
| **E** Erreur | Message exact (copier-coller) | "Cannot read properties of undefined" |
| **S** Stack | Technos + versions | "Express 4.18, Prisma 5, Node 18" |
| **E** Essai | Ce que tu as déjà testé | "J'ai essayé avec findFirst()" |

## D — Démo

**Prompt faible :** "J'ai une erreur Prisma"
→ L'IA devine. Réponse générique.

**Prompt CESE :**
```
Code : const user = await prisma.user.findUnique({where:{email}})
Erreur : TypeError: Cannot read properties of undefined (reading 'id')
Stack : Express + Prisma 5 + PostgreSQL, Node 18
Essai : email est bien une string, l'utilisateur existe en BDD
```
→ L'IA identifie : le champ `email` n'est pas indexé ou la requête retourne null.

**Autres cas concrets :**
- **Bug React** : setCount dans setTimeout → l'IA voit le closure stale
- **API 404** : route.ts mal placé dans App Router → l'IA voit l'erreur de structure

## A — Action
Prends une erreur récente. Rédige un prompt CESE. Teste dans Claude/ChatGPT.
