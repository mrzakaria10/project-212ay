# Leçon 2.1 — Anatomie d'un bon prompt
## Script Vidéo — ~14 min

### [0:00-0:30] HOOK
> Tu tapes "crée un formulaire React" et l'IA te renvoie du code générique que tu dois retoucher pendant 20 minutes. Pourtant, ton collègue obtient exactement ce qu'il veut en un seul prompt. La différence ? Ce n'est pas l'outil, c'est la façon dont tu formules ta demande.

### [0:30-3:30] CONCEPT — Les 5 piliers d'un bon prompt

**(Slide)**
```
┌────────────────────────────────────────────┐
│ 1. RÔLE     → "Tu es expert React"         │
│ 2. CONTEXTE → "J'ai Next.js + Tailwind"    │
│ 3. TÂCHE    → "Crée un composant Card"     │
│ 4. FORMAT   → "Avec TypeScript, export default" │
│ 5. CONTRAINTE → "Pas de lib externe"       │
└────────────────────────────────────────────┘
```

> **1. Rôle** : "Tu es expert React / senior backend / architecte cloud" — ça change totalement la qualité.
> **2. Contexte** : Donne ton stack, versions, ce qui existe déjà.
> **3. Tâche** : Sois précis sur ce que tu veux.
> **4. Format** : TypeScript ? Props ? Export ? Dis-le.
> **5. Contrainte** : Limites, exclusions, edge cases.

### [3:30-9:00] DÉMO — Prompt faible vs fort

**Prompt faible :**
```
"Crée un formulaire React"
```
→ Résultat : formulaire générique, pas de style, pas de validation.

**Prompt fort :**
```
Tu es expert React + TypeScript. Je dois créer un formulaire
d'inscription avec :
- Champs : name, email, password, confirmPassword
- Validation Zod côté client
- Style Tailwind (design sombre)
- Gestion d'erreur par champ
- Submit avec appel API POST /api/register
- Loading state sur le bouton

Donne le code du composant complet avec TypeScript et export default.
```
→ Résultat : composant prêt à l'emploi, typé, stylé, avec validation.

**Comparaison :**
```
Prompt faible : "login form"          → 30 lignes génériques
Prompt fort  : (10 lignes précises)   → 80 lignes exploitables
```

### [9:00-10:00] ACTION
> Prends un projet perso. Choisis un composant que tu dois coder. Écris un prompt fort avec les 5 piliers. Compare le résultat avec ce que tu aurais écrit sans structure.

### [10:00-10:30] OUTRO
> Prochaine leçon : générer du boilerplate utile — des bases de projet complètes avec un seul prompt.
