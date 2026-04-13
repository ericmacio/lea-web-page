# Document de Design — Landing Page CRO Freelance

## 1. Informations Générales

| Propriété | Valeur |
|-----------|--------|
| **Projet** | Landing page pour offre de conseil CRO (Conversion Rate Optimization) |
| **Cible** | PME, TPE, startups ayant un site e-commerce ou vitrine avec du trafic mais peu de conversions |
| **Objectif** | Présenter l'UVP de Léa Macioszczyk, générer des prises de contact et des demandes de diagnostic gratuit |
| **Format** | Page HTML unique, statique, sans JavaScript |
| **Langue** | Français |
| **Référence visuelle** | https://talented-answers-795492.framer.app/ |

---

## 2. Palette de Couleurs

| Nom d'usage | Code | Utilisation |
|-------------|------|-------------|
| Noir principal | `#0f0f0e` | Fond des sections sombres (header, hero, à propos, offres, FAQ, footer) |
| Noir secondaire | `#1a1a18` | Fond des cartes d'offres, variantes de fond sombre |
| Gris foncé | `#7a7870` | Textes secondaires, sous-titres sur fond sombre |
| Gris clair | `#a3a198` | Textes tertiaires, labels de section (ex: "— Le problème") |
| Blanc | `#ffffff` | Textes principaux sur fond sombre, fond des sections claires |
| Cyan / Bleu vif | `#00d4ff` | CTA principaux, accents, boutons, labels de section (tiret coloré) |
| Cyan transparent | `#45cdff3d` | Effets de survol, backgrounds subtils, bordures légères |

---

## 3. Typographies

| Usage | Police | Style |
|-------|--------|-------|
| **Titres principaux** (h1, h2 de section) | `Instrument Serif` | Italique pour les mots-clés mis en valeur |
| **Textes courants** (paragraphes, navigation, boutons, labels) | `DM Sans` | Regular (400), Medium (500), Semi-bold (600) |

**Import Google Fonts :**
```
Instrument Serif : 400, 400 italic
DM Sans : 400, 500, 600, 700
```

---

## 4. Structure de la Page (Sections)

La page se compose de **10 zones** distinctes, dans l'ordre suivant :

### 4.1. Header (Navigation fixe)

- **Fond** : `#0f0f0e` avec légère bordure basse ou séparation subtile
- **Layout** : Flexbox, alignement horizontal, `justify-content: space-between`
- **Gauche** : Logo texte "Léa Macioszczyk · Freelance CRO" en `Instrument Serif` italique, couleur blanche
- **Centre** : Navigation — liens en `DM Sans` majuscules, couleur blanche, espacement régulier
  - À PROPOS | MÉTHODE | OFFRES | CONTACT
- **Droite** : Bouton CTA "Diagnostic gratuit" avec icône graphique (petit pictogramme), fond `#00d4ff`, texte noir, coins arrondis (border-radius ~25px)
- **Position** : `position: sticky` ou `fixed` en haut de page, z-index élevé
- **Hauteur** : ~60-70px
- **Padding horizontal** : ~40-80px

---

### 4.2. Section Hero

- **Fond** : `#0f0f0e` (sombre)
- **Layout** : Centré, text-align center, largeur max ~900px
- **Contenu** :
  1. **Tag/Label** : "CRO FREELANCE · E-COMMERCE & SITE VITRINE" — texte petit, lettres majuscules, `DM Sans`, espacement large (`letter-spacing`), couleur `#7a7870`
  2. **Titre principal** (h1) : "Votre site a du **trafic** mais **pas assez de résultats** ?" — `Instrument Serif`, grande taille (~48-56px), blanc, mots "trafic" et "mais" en italique, "pas assez de résultats" en couleur `#00d4ff` ou souligné
  3. **Sous-titre** : Paragraphe descriptif en `DM Sans`, couleur `#a3a198`, taille ~16-18px, largeur max ~700px
  4. **Boutons CTA** : Deux boutons côte à côte
     - "Diagnostic gratuit" — fond `#00d4ff`, texte noir
     - "Voir les offres" — fond transparent, bordure blanche ou grise, texte blanc
  5. **Mention** : "Livré par email, sans appel obligatoire." — petit texte, couleur `#7a7870`
- **Espacement vertical** : Padding ~100-120px top/bottom

---

### 4.3. Section "Le Problème"

- **Fond** : `#ffffff` (clair)
- **Layout** : Deux colonnes (60% / 40%) ou disposition à vérifier
- **Contenu colonne gauche** :
  1. **Label** : "— Le problème" — texte cyan `#00d4ff`, petites majuscules, `DM Sans`
  2. **Titre** (h2) : "La plupart des sites perdent des conversions **sans le savoir**." — `Instrument Serif`, grande taille (~40-48px), noir `#0f0f0e`, "sans le savoir" en italique
  3. **Paragraphe** : Statistique Baymard Institute (97% des visiteurs), texte `#7a7870`, `DM Sans`
  4. **Paragraphe** : "Ce sont des frictions invisibles..." — complément explicatif
  5. **Phrase clé** : "Le problème, c'est qu'on ne les voit pas à l'oeil nu. Ils se détectent dans les données." — mise en évidence, "se détectent dans les données" souligné ou en couleur cyan
- **Contenu colonne droite** : 3 cartes problèmes empilées verticalement
  - Chaque carte :
    - **Titre** en gras `DM Sans` semi-bold, noir
    - **Description** en `DM Sans` regular, gris `#7a7870`
    - Fond blanc ou gris très clair, léger padding, pas de bordure marquée
  - Les 3 cartes :
    1. "Une page qui manque de réassurance"
    2. "Un parcours utilisateur trop complexe"
    3. "Un décalage entre l'offre et le message"
- **Espacement** : Padding ~80-100px top/bottom

---

### 4.4. Section "À Propos"

- **Fond** : `#0f0f0e` (sombre)
- **Layout** : Deux colonnes — image à gauche, texte à droite
- **Contenu gauche** :
  - Photo circulaire de Léa (`docs/lea.png`), `border-radius: 50%`, taille ~250-300px
- **Contenu droite** :
  1. **Label** : "— À propos" — texte cyan `#00d4ff`, petites majuscules
  2. **Titre** (h2) : "**Consultante** conversion & performance digitale" — `Instrument Serif` italique, blanc, grande taille (~36-44px), "Consultante" en style distinct (italique accentué)
  3. **Paragraphes** : Texte de présentation en `DM Sans`, couleur `#a3a198`, taille ~16px
     - Paragraphe 1 : Spécialisation CRO, aide aux entreprises
     - Paragraphe 2 : Parcours marketing digital, approche basée sur la donnée
     - Paragraphe 3 : Logique d'amélioration continue
- **Espacement** : Padding ~80-100px top/bottom

---

### 4.5. Section "Méthode"

- **Fond** : `#ffffff` (clair)
- **Layout** : Texte introductif centré en haut, puis 4 étapes numérotées en liste verticale
- **Contenu intro** :
  1. **Label** : "— méthode" — texte cyan `#00d4ff`, petites majuscules
  2. **Titre** (h2) : "Analyse, hypothèses, tests, **résultats**." — `Instrument Serif` italique, noir, grande taille
  3. **Paragraphe** : Description de la méthodologie + mention du collaborateur développeur senior
- **Les 4 étapes** : Affichées en liste verticale, chaque étape avec :
  - **Numéro** : Grand chiffre (1, 2, 3, 4) en gris clair ou cyan, `DM Sans` bold
  - **Titre d'étape** : `DM Sans` semi-bold, noir
  - **Description** : `DM Sans` regular, gris `#7a7870`
  - Séparation visuelle entre chaque étape (ligne fine horizontale ou espacement)
  - Les 4 étapes :
    1. **Analyse des données** — GA4, heatmaps, session replays
    2. **Formulation d'hypothèses** — Méthode PXL
    3. **Tests A/B & mesure** — GoStellar, analyse statistique
    4. **Apprentissage & implémentation** — Déploiement des résultats
- **Espacement** : Padding ~80-100px top/bottom

---

### 4.6. Section "Offres"

- **Fond** : `#0f0f0e` (sombre)
- **Layout** : Texte introductif centré en haut, puis 3 cartes en ligne horizontale (grille 3 colonnes)
- **Contenu intro** :
  1. **Label** : "— offres" — texte cyan `#00d4ff`, petites majuscules
  2. **Titre** (h2) : "Un point d'entrée selon votre situation." — `Instrument Serif`, blanc
  3. **Sous-titre** : "Trois formules pensées pour s'adapter..." — `DM Sans`, gris
- **Les 3 cartes** :
  - Fond : `#1a1a18` (noir légèrement plus clair)
  - Border-radius : ~12-16px
  - Padding intérieur : ~30-40px
  - **Structure de chaque carte** :
    - Tag en haut : type d'offre en majuscules, petite taille, couleur `#7a7870`
    - Durée/période sous le tag
    - Titre de l'offre en `DM Sans` bold, blanc, ~20-24px
    - Description en `DM Sans` regular, gris `#a3a198`
    - **Prix** : Grande taille, blanc, `DM Sans` bold
    - Mention "Pour qui" : Texte en gris, expliquant la cible
    - **Liste de fonctionnalités** : Éléments avec check/puce cyan
    - **Bouton CTA** : "Me contacter" — bordure cyan, texte cyan, fond transparent, coins arrondis

  | Carte | Tag | Durée | Titre | Prix |
  |-------|-----|-------|-------|------|
  | 1 | ONE-SHOT | 2 SEMAINES | Audit opérationnel | 499€ |
  | 2 | ACCOMPAGNEMENT | MINIMUM 3 MOIS | Accompagnement CRO | 799€ /mois |
  | 3 | OFFRE COMPLÉMENTAIRE | — | Exécution technique | sur devis |

- **Espacement** : Padding ~80-100px top/bottom

---

### 4.7. Bannière CTA intermédiaire

- **Fond** : `#00d4ff` (cyan) — pleine largeur
- **Layout** : Centré, text-align center
- **Contenu** :
  1. "Vous ne savez pas par où commencer ?" — `DM Sans`, noir, taille moyenne
  2. "Je jette un oeil à votre site gratuitement." — `DM Sans`, noir, taille grande ou bold
  3. **Bouton** : "Diagnostic gratuit" — fond noir `#0f0f0e`, texte blanc, coins arrondis
- **Espacement** : Padding ~50-60px top/bottom

---

### 4.8. Section "Contact"

- **Fond** : Divisé en deux — gauche fond sombre `#0f0f0e`, droite fond clair `#ffffff`
- **Layout** : Deux colonnes (50/50)
- **Colonne gauche (sombre)** :
  1. **Label** : "— contact" — texte cyan `#00d4ff`
  2. **Titre** (h2) : "Si vous pensez que votre site peut générer **plus de résultats**." — `Instrument Serif`, blanc, "plus de résultats" en italique ou cyan
  3. **Sous-titre** : "Parlons-en." — `Instrument Serif` italique, blanc
  4. **3 points de réassurance** (icônes + texte) :
     - "Réponse sous 48h. C'est moi (Léa) qui vous réponds..."
     - "Honnêteté avant tout. Si le CRO n'est pas la bonne solution..."
     - "Diagnostic offert. Si vous partagez votre URL..."
- **Colonne droite (claire)** : Formulaire de contact
  - **Champs** :
    - Prénom / Nom* — input texte, placeholder "Marie Dupont"
    - Email* — input email, placeholder "marie@pro.com"
    - URL de votre site* — input url, placeholder "https://monsite.fr"
    - Vous êtes intéressé par* — select/dropdown ("Sélectionner")
    - Votre situation* — textarea, placeholder "Quelques mots sur votre site..."
  - **Bouton** : "Envoyer" — fond `#00d4ff`, texte noir, icône flèche, coins arrondis
  - **Style des champs** : Bordure légère grise, fond blanc, padding ~12px, border-radius ~8px
- **Espacement** : Padding ~80-100px top/bottom

---

### 4.9. Section "FAQ"

- **Fond** : `#0f0f0e` (sombre)
- **Layout** : Centré, largeur max ~800-900px
- **Contenu** :
  1. **Label** : "— QUESTIONS FRÉQUENTES" — texte cyan `#00d4ff`, petites majuscules
  2. **Titre** (h2) : "Vous hésitez encore ?" — `Instrument Serif`, blanc, grande taille
  3. **Accordéon** : 5 questions avec expand/collapse (réalisable en CSS pur via `<details>/<summary>`)
     - Fond de chaque item : blanc/gris très clair
     - Icône "+" à gauche de chaque question
     - Texte question en `DM Sans`, noir
     - Texte réponse en `DM Sans`, gris `#7a7870`
     - Border-radius léger, espacement entre items ~8-12px

  | # | Question |
  |---|----------|
  | 1 | Concrètement, c'est quoi le CRO ? |
  | 2 | Est-ce que le CRO fonctionne pour les petits sites avec peu de trafic ? |
  | 3 | Combien de temps avant de voir des résultats concrets ? |
  | 4 | Quelle différence entre le CRO, le SEO et le redesign ? |
  | 5 | Que se passe-t-il si l'audit ne révèle rien de significatif ? |

- **Espacement** : Padding ~80-100px top/bottom

---

### 4.10. Footer

- **Fond** : `#0f0f0e` (sombre), éventuellement légèrement distinct du fond FAQ avec bordure top subtile
- **Layout** : Flexbox, `justify-content: space-between`, alignement vertical center
- **Contenu** :
  - **Gauche** : "Léa Macioszczyk · Freelance CRO" — `Instrument Serif` italique, blanc
  - **Droite** : "© 2026 — Tous droits réservés" — `DM Sans`, gris `#7a7870`
- **Hauteur** : ~60-70px
- **Padding horizontal** : ~40-80px

---

## 5. Principes de Mise en Page

### 5.1. Conteneur principal
- **Largeur max** : 1200px centré (`max-width: 1200px; margin: 0 auto`)
- **Padding latéral** : 20-40px pour petits écrans

### 5.2. Alternance des fonds
La page alterne systématiquement entre sections sombres et claires :
```
Header      → sombre (#0f0f0e)
Hero        → sombre (#0f0f0e)
Problème    → clair  (#ffffff)
À propos    → sombre (#0f0f0e)
Méthode     → clair  (#ffffff)
Offres      → sombre (#0f0f0e)
Bannière CTA→ cyan   (#00d4ff)
Contact     → mixte  (sombre + clair)
FAQ         → sombre (#0f0f0e)
Footer      → sombre (#0f0f0e)
```

### 5.3. Boutons (styles récurrents)
- **Primaire** : `background: #00d4ff`, `color: #0f0f0e`, `border-radius: 25px`, `padding: 12px 28px`, `font-family: DM Sans`, `font-weight: 600`
- **Secondaire** : `background: transparent`, `border: 1px solid #ffffff`, `color: #ffffff`, `border-radius: 25px`, `padding: 12px 28px`
- **Secondaire cyan** : `background: transparent`, `border: 1px solid #00d4ff`, `color: #00d4ff`, `border-radius: 25px`

### 5.4. Labels de section
- Format : "— NOM" (tiret long + espace + nom en majuscules)
- Couleur : `#00d4ff`
- Police : `DM Sans`, taille ~12-14px, `letter-spacing: 2px`, `text-transform: uppercase`

### 5.5. Responsive
- La page doit être responsive avec des breakpoints standards :
  - **Desktop** : > 1024px — layout complet multi-colonnes
  - **Tablette** : 768px - 1024px — colonnes réduites, certaines sections passent en une colonne
  - **Mobile** : < 768px — tout en une colonne, navigation simplifiée (hamburger menu en CSS pur)

---

## 6. Assets Requis

| Fichier | Emplacement | Usage |
|---------|-------------|-------|
| `lea.png` | `docs/lea.png` | Photo section "À propos", affichée en cercle |

---

## 7. Contraintes Techniques

- **Pas de JavaScript** : Toutes les interactions (accordéon FAQ, navigation mobile) doivent être réalisées en CSS pur (`<details>/<summary>` pour l'accordéon, checkbox hack pour le menu hamburger)
- **HTML unique** : Un seul fichier `.html` avec CSS intégré ou fichier CSS séparé
- **Fonts externes** : Import via Google Fonts (Instrument Serif + DM Sans)
- **Pas de framework CSS** : CSS personnalisé uniquement
- **Formulaire** : Le formulaire de contact est un formulaire HTML statique (l'action de soumission n'est pas définie dans le cadre de ce projet)

---

## 8. Arborescence des Ancres de Navigation

```
#hero         → Section Hero (haut de page)
#probleme     → Section Le Problème
#a-propos     → Section À Propos
#methode      → Section Méthode
#offres       → Section Offres
#contact      → Section Contact
#faq          → Section FAQ
```

Les liens de navigation du header pointent vers ces ancres avec un scroll fluide (`scroll-behavior: smooth` en CSS).

---

## 9. Contenu Textuel

Le contenu exact est défini dans `docs/texte.txt` et doit être repris **strictement sans modification**. Aucune réécriture, reformulation ou ajout de contenu n'est autorisé. Seule la dernière ligne ("Create a free website with Framer...") doit être omise car c'est un élément Framer, non pertinent pour la page HTML.
