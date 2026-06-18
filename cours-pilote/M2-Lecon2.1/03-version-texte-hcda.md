# Leçon 2.1 : Anatomie d'un bon prompt
## Version Texte HCDA

## H — Hook
Tu tapes "crée un formulaire React" et l'IA te renvoie du code générique que tu passes 20 min à retoucher. Ton collègue obtient exactement ce qu'il veut en un seul prompt. La différence ? La structure de sa demande.

## C — Concept : Les 5 piliers

| Pilier | Exemple |
|--------|---------|
| **1. Rôle** | "Tu es expert React senior" |
| **2. Contexte** | "Projet Next.js 14 + Tailwind + Prisma" |
| **3. Tâche** | "Crée un formulaire d'inscription avec 4 champs" |
| **4. Format** | "TypeScript, export default, props typées" |
| **5. Contrainte** | "Pas de lib externe, gère les états vide/erreur/loading" |

## D — Démo

**Prompt faible :** `"Crée un formulaire React"`
→ Code générique sans validation, sans style, sans gestion d'état.

**Prompt fort :**
```
Tu es expert React + TypeScript. Je dois créer un formulaire
d'inscription avec : champs name/email/password/confirmPassword,
validation Zod, style Tailwind sombre, gestion d'erreur par champ,
submit POST /api/register, loading state. Donne le composant complet.
```
→ Code prêt à l'emploi, typé, stylé, avec validation.

## A — Action
Prends un composant de ton projet. Écris un prompt structuré (5 piliers). Compare avec un prompt sans structure.
