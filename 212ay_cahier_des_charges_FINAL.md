# 212ay.com

## Cahier des Charges Stratégie de Structuration des Cours

Vers une plateforme d'apprentissage africaine moderne, multilingue et certifiante

📅 Juin 2026 | 🌍 Maroc & Afrique | 🌐 AR · FR · EN | 🎬 Vidéo · Audio · Texte | 🏆 Certification incluse | 📋 Version Finale 3.0

## Table des matières
- 1 Contexte
- 2 Problématique
- 3 Solution proposée
- 4 Objectifs
- 5 Public cible
- 6 Structure des cours
- 7 Formats de contenu
- 8 Multilingue AR/FR/EN
- 9 User Flow complet
- 10 Architecture fonctionnelle
- 11 Cours exemple VIP Coding
- 12 Certification
- 13 KPI & Indicateurs
- 14 Exigences fonctionnelles
- 15 Roadmap

## Contexte

> 212ay.com est une plateforme de formation en ligne marocaine qui ambitionne de devenir la référence de l'apprentissage professionnel en Afrique francophone. Dans un marché de la formation numérique en pleine croissance, la plateforme doit se différencier par une structure pédagogique solide, une expérience utilisateur pensée pour le contexte africain, et une offre multilingue accessible.

Le marché de la formation en ligne en Afrique connaît une expansion rapide, portée par la pénétration du mobile, une population jeune et une demande croissante de compétences numériques. Des plateformes comme VC4A Academy ont montré qu'un modèle axé sur la progression, les modules concrets et la certification finale répond efficacement aux attentes des apprenants africains.

212ay.com doit donc passer d'une simple bibliothèque de contenus à une plateforme de parcours guidés , avec une architecture pédagogique standardisée, des formats flexibles et un système de validation reconnu.

## Problématique

> 🚨 Problème central : Sans architecture pédagogique structurée, 212ay risque d'être perçu comme un catalogue de vidéos plutôt qu'une vraie plateforme de formation — entraînant un faible engagement et un taux de complétion bas.

### Problèmes identifiés
- Difficulté pour l'utilisateur à identifier le bon cours selon son niveau et son objectif.
- Absence de progression pédagogique visible et motivante.
- Pas d'adaptation du format au mode d'apprentissage de chaque utilisateur.
- Aucun mécanisme de validation et de certification reconnaissable.
- Contenu disponible dans une seule langue, excluant une partie du public cible.
- Faible différenciation entre 212ay et une simple bibliothèque de vidéos YouTube.

## Solution Proposée

> ✅ Architecture pédagogique standardisée : Construire 212ay autour d'un parcours guidé Parcours → Module → Leçon → Quiz → Projet → Certificat , avec trois formats (vidéo, audio, texte) et contenu en trois langues (AR, FR, EN).

### Architecture en couches

```text
🎯 PARCOURS → 📦 MODULE → 📖 LEÇON → ✅ QUIZ → 🛠️ PROJET → 🏆 CERTIFICAT
```

Chaque cours doit offrir trois niveaux d'expérience : un choix guidé selon l'objectif et la langue, une consommation flexible (vidéo, audio, texte), et une validation finale avec certificat valorisable professionnellement.

## Objectifs du Projet

## Public Cible

| Segment | Besoin principal | Format préféré | Langues |
| --- | --- | --- | --- |
| 🎓 Étudiants | Monter en compétence pour l'emploi | Vidéo + Quiz | FR / AR |
| 💻 Développeurs juniors | Apprentissage pratique et portfolio | Vidéo + Texte + Projet | FR / EN |
| 🚀 Entrepreneurs | Formation orientée action | Vidéo + Audio | FR / EN |
| 🔄 En reconversion | Parcours guidés et certification | Audio + Texte + Quiz | AR / FR |

## Structure Standard des Cours

### Template d'une fiche cours

| Bloc | Contenu requis |
| --- | --- |
| 🎯 Hero | Titre, bénéfice principal, CTA d'inscription, langues et formats disponibles |
| 📋 Programme | Liste des modules et leçons avec durée estimée |
| 👥 Pour qui ? | Profil cible décrit en 3–5 points |
| 🎯 Résultats | 3 à 5 compétences mesurables en fin de parcours |
| 📺 Formats | Vidéo, audio, texte avec sélecteur de langue |
| ✅ Validation | Quiz par module, projet final, conditions du certificat |
| ❓ FAQ | Questions fréquentes contextualisées |

### Template d'une leçon — Format HCDA

### Schéma HCDA
- H Hook Accroche 2 phrases qui pose le problème concret
- C Concept Explication claire avec analogie ou exemple réel
- D Démo Exemple pratique, code ou cas d'usage terrain
- A Action Tâche immédiate à réaliser par l'apprenant

## Formats de Contenu

La même leçon doit exister sous trois formes synchronisées . L'apprenant choisit son format préféré sans changer le fond du contenu.

| Format | Usage principal | Avantage utilisateur | Exigence produit |
| --- | --- | --- | --- |
| 🎬 Vidéo | Apprentissage visuel | Plus engageant, démonstration directe | Hébergement CDN, player, sous-titres |
| 🎧 Audio | Apprentissage mobile | Consommation en déplacement | Lecteur audio, téléchargement offline |
| 📖 Texte | Révision rapide | Skimming, accessibilité, traduction facile | Article structuré, transcription complète |

## Gestion Multilingue AR / FR / EN

### Règles de contenu multilingue
- Titre du cours en AR, FR et EN.
- Description courte en AR, FR et EN.
- Objectifs pédagogiques en AR, FR et EN.
- Sous-titres vidéo en AR, FR et EN.
- Quiz localisés dans les trois langues.
- Certificat généré dans la langue choisie par l'utilisateur.

### Exemple de fiche cours multilingue

| Champ | Français | English | العربية |
| --- | --- | --- | --- |
| Titre | Comment l'IA peut booster votre code | How AI Can Boost Your Code | كيف يساعدك الذكاء الاصطناعي على تحسين كودك |
| Description | Mini-parcours pratique pour coder plus vite avec l'IA. | A practical mini-course to code faster using AI. | مسار عملي قصير للبرمجة الأسرع باستخدام الذكاء الاصطناعي |
| Résultat | Savoir utiliser GitHub Copilot et écrire des prompts efficaces. | Use GitHub Copilot and write powerful prompts. | استخدام GitHub Copilot وكتابة Prompts فعّالة |

## User Flow Complet

### Diagramme de flux — De la découverte au certificat

```text
🏠 Arrivée 212ay → 🔍 Filtrer les cours → Connecté ? OUI → 📋 Fiche du cours → Choisir format → Choisir langue → 📖 Suivre leçon ✅ Quiz module → Score ≥ 70% ? NON → Revoir leçon OUI → Module suivant → 🛠️ Projet final → 🏆 CERTIFICAT → 📤 Partager
```

### Étapes UX détaillées

### Étapes UX détaillées
- **1 — Arrivée sur 212ay.com** : L'utilisateur découvre la plateforme via la page d'accueil. Il voit les parcours mis en avant par catégorie et objectif.
- **2 — Filtrage des cours** : Filtrage par domaine, niveau (débutant/intermédiaire/avancé), langue (AR/FR/EN) et format (vidéo/audio/texte).
- **3 — Création de compte / Connexion** : Inscription rapide avec email ou compte social. Profil utilisateur avec niveau, langue préférée et objectifs.
- **4 — Consultation de la fiche cours** : L'utilisateur lit le programme, les objectifs, la durée et les conditions de certification avant de s'inscrire.
- **5 — Choix du format et de la langue** : L'apprenant choisit son format: 🎬 Vidéo 🎧 Audio 📖 Texte et sa langue: AR FR EN
- **6 — Suivi des modules et leçons** : Progression visible avec barre d'avancement. Chaque leçon contient le contenu + une micro-action ou question.
- **7 — Quiz de validation par module** : Quiz de 3 à 5 questions à la fin de chaque module. Score minimum 70% requis pour passer au module suivant.
- **8 — Projet final** : Évaluation pratique finale. L'apprenant soumet un livrable concret (code, document, présentation) lié aux compétences du parcours.
- **9 — Certificat 212ay** : Le certificat est généré automatiquement avec identifiant unique, QR code et lien de vérification public.
- **10 — Partage du certificat** : Partage sur LinkedIn, WhatsApp ou téléchargement PDF. Le certificat renforce le profil professionnel de l'apprenant.

## Architecture Fonctionnelle

L'architecture produit supporte la gestion du contenu, le suivi d'apprentissage, les certificats et le multilingue sur l'ensemble des couches techniques.

### Architecture visuelle
- **🖥️ Client**
  - Web Browser (Chrome, Firefox, Safari)
  - Mobile Web (PWA responsive)
  - Application Progressive Web App
- **⚙️ Plateforme 212ay**
  - Frontend Next.js (React)
  - API Node.js / REST
  - Authentification JWT / OAuth
  - Moteur LMS (suivi progression)
  - Service génération certificats PDF
- **📚 Contenu**
  - Vidéos (CDN / AWS S3)
  - Fichiers Audio (MP3)
  - Textes & PDFs
  - Banque de quiz (JSON)
  - Ressources téléchargeables
- **🗄️ Données**
  - PostgreSQL (Supabase)
  - Redis (cache sessions)
  - Analytics (Plausible)
  - Stockage médias (S3)

### Flux de données complet

```text
👤 Utilisateur ⟶ Next.js ⟶ API Node.js ⟶ Auth + LMS ⟶ Contenu CDN ⟶ DB + Cache
```

### Stack technique recommandée

| Couche | Technologie | Justification |
| --- | --- | --- |
| Frontend | Next.js 14 + TypeScript + Tailwind CSS | SSR, performance, SEO multilingue |
| Backend API | Node.js + Express ou Fastify | Familier à l'équipe, ecosystème riche |
| Base de données | PostgreSQL via Supabase | Déjà utilisé, RLS pour sécurité |
| Authentification | Supabase Auth + JWT | Social login, gestion rôles intégrée |
| Médias vidéo | Cloudflare Stream ou Mux | Streaming adaptatif, sous-titres |
| Certificats PDF | Puppeteer ou PDFKit | Génération dynamique côté serveur |
| Déploiement | Vercel (frontend) + Railway/Render (API) | CI/CD simplifié, scaling automatique |
| Cache | Redis (Upstash) | Sessions, rate limiting, cours populaires |

## Cours Exemple : IA + VIP Coding

### 🤖 Comment l'IA peut vous aider à faire du VIP Coding
Codez plus vite, mieux et de façon plus intelligente grâce à l'IA comme copilote de développement.
- ⏱️ 3h00
- 💻 Intermédiaire
- 🎬 Vidéo + Audio + Texte
- 🌐 AR / FR / EN
- 🏆 Certificat inclus
- 4 modules

> Objectif : À la fin de ce cours, l'apprenant sait utiliser l'IA comme copilote de développement pour générer du code, corriger des bugs, produire de la documentation et livrer des projets plus rapidement et avec une meilleure qualité.

### Structure du parcours

```text
M1 : Comprendre l'IA → M2 : Prompter → M3 : Debug & Refactor → M4 : Automatiser → Projet Final → 🏆 Certificat
```

### Détail des modules

### Modules
- **Comprendre l'IA pour les développeurs** : Panorama des outils IA (GitHub Copilot, Cursor, Gemini, Claude). Cas d'usage concrets. Limites et bonnes pratiques. Choisir le bon outil selon le contexte.
- **Prompter efficacement pour générer du code** : Anatomie d'un bon prompt technique. Générer du boilerplate. Demander des explications claires. Comparaison de prompts faibles vs prompts forts.
- **Déboguer et refactorer avec l'IA** : Expliquer une erreur à l'IA. Corriger un bug complexe. Améliorer un composant existant. Optimiser les performances avec des suggestions IA.
- **Automatiser documentation et tests** : Générer automatiquement la documentation. Créer des tests unitaires avec l'IA. Revue de code assistée. Construire un workflow de productivité complet.
- **Projet Final — Mini-app assistée par IA** : Construire un mini-projet complet (API REST + Frontend) en utilisant l'IA à chaque étape : génération, debug, documentation, tests. Livrable : dépôt GitHub documenté.

### Exemple de leçon — 3 langues

| Élément | Français | English | العربية |
| --- | --- | --- | --- |
| Titre | Générer un composant React avec un bon prompt | Generate a React component with a strong prompt | إنشاء مكوّن React باستخدام Prompt فعّال |
| Objectif | Savoir demander un composant réutilisable à l'IA. | Learn how to request a reusable component from AI. | تعلم كيفية طلب مكوّن قابل لإعادة الاستخدام |
| Démo | Tu es expert React. Génère un Card TypeScript avec props title, description, imageUrl et styling Tailwind. | You are a React expert. Generate a TypeScript Card component with title, description, imageUrl props and Tailwind styling. | أنت خبير React. أنشئ مكوّن Card بلغة TypeScript مع Tailwind |

## Système de Certification

### Conditions d'obtention
- Compléter 100 % des modules obligatoires.
- Obtenir un score minimum de 70 % au quiz final.
- Soumettre le projet final si le parcours l'exige.
- Accepter le règlement d'émission du certificat.

### Aperçu du certificat 212ay

### Aperçu du certificat
212 212ay.com Certificat de Réussite Ce certificat est décerné à Zakaria Derkaoui pour avoir complété avec succès le parcours "Comment l'IA peut vous aider à faire du VIP Coding" 📅 Date 16 Juin 2026 🌐 Langue Français ⏱️ Durée 3 heures 🔑 ID 212AY-2026-0042 📱 QR Code Vérification publique

### Usages du certificat

## KPI & Indicateurs

### KPI clés
- **Taux d'inscription cible** : 60%
- **Taux de démarrage** : 50%
- **Taux de complétion** : 35%
- **Taux de certification** : 25%

### Entonnoir de conversion

### Entonnoir de conversion
- **Visiteurs** : 1 000 visiteurs (100%)
- **Inscrits** : 600 inscrits (60%)
- **Démarrages** : 500 apprenants (50%)
- **Modules complétés** : 350 complétions (35%)
- **Certificats obtenus** : 250 certificats (25%)

### KPI produit recommandés

| Indicateur | Description | Cible |
| --- | --- | --- |
| Taux d'inscription | Visiteurs qui créent un compte | > 60% |
| Taux de démarrage | Inscrits qui commencent un cours | > 50% |
| Taux de complétion | Apprenants qui finissent le parcours | > 35% |
| Format préféré | Vidéo vs Audio vs Texte | Mesurer & adapter |
| Langue préférée | AR vs FR vs EN | Mesurer & adapter |
| Taux de certification | Apprenants qui obtiennent le certificat | > 25% |

## Exigences Fonctionnelles

### Exigences non fonctionnelles
- Interface responsive mobile et desktop.
- Temps de chargement optimisé pour réseaux faibles (Afrique).
- Sous-titres et transcription pour accessibilité maximale.
- Architecture compatible avec la montée en charge.
- Sécurité renforcée sur comptes, certificats et données.
- Support RTL complet pour l'arabe.

## Roadmap de Mise en Œuvre

### Roadmap
- **📐 Phase 1 — Fondation**
  - Définir le template standard d'un cours
  - Définir le template HCDA d'une leçon
  - Concevoir le modèle certificat
  - Définir le modèle multilingue AR/FR/EN
  - Choisir et configurer la stack technique
  - Configurer Supabase + Next.js + Auth
- **🚀 Phase 2 — MVP Contenu**
  - Produire 3 à 5 parcours pilotes
  - Intégrer vidéo + audio + texte sur LMS
  - Ajouter quiz et suivi de progression
  - Générer les premiers certificats PDF
  - Tests utilisateurs et itérations UX
  - Lancer le cours IA + VIP Coding en pilote
- **📈 Phase 3 — Optimisation**
  - Ajouter les recommandations de cours
  - Dashboard analytics complet
  - Mesurer préférence format et langue
  - Optimiser le taux de complétion
  - Lancer la PWA mobile
  - Monétisation et parcours premium

> ✅ Recommandation finale : La meilleure stratégie pour 212ay est d'industrialiser une structure unique de cours tout en laissant la spécialisation se faire au niveau du contenu. Le cours "IA pour VIP Coding" est le pilote idéal — il parle directement à un public tech marocain, répond à un besoin concret de productivité, et peut être décliné facilement en vidéo, audio et texte dans les trois langues visées.
