# Stratégie de référencement Google — Landing Page CRO

> Ce document définit la stratégie globale d'optimisation du référencement naturel (SEO) de la page `index.html` sur Google, en ciblant les mots-clés : **CRO**, **optimisation site web**, **amélioration taux de conversion**, **test A/B** et tout l'univers sémantique lié à l'activité.

---

## 1. État des lieux — Ce qui est déjà en place

### SEO on-page (réalisé)
| Élément | Statut | Détail |
|---------|--------|--------|
| `<title>` optimisé | ✅ | Contient "CRO", "optimisation taux de conversion", "e-commerce", "site vitrine" |
| `<meta description>` | ✅ | Inclut "audit de conversion", "tests A/B", "taux de conversion" + CTA |
| `<meta author>` et `<meta subject>` | ✅ | Présents |
| Open Graph / Twitter Card | ✅ | Alignés avec le titre et la description optimisés |
| `<link rel="canonical">` | ✅ | `https://leamacio.com/` |
| `<html lang="fr">` | ✅ | |
| `<h1>` unique | ✅ | Contient "trafic" et "résultats" |
| `<h2>` enrichis en mots-clés | ✅ | "CRO", "optimisation du taux de conversion", "sites web", "optimisation CRO" intégrés |
| Balise `<main>` | ✅ | Englobe le contenu principal |
| `aria-label` sur sections | ✅ | Présents sur les sections clés |
| Alt text enrichi sur image profil | ✅ | Descriptif avec mots-clés CRO |
| `sitemap.xml` | ✅ | Présent et référencé dans robots.txt |
| `robots.txt` | ✅ | `Allow: /` + lien sitemap |
| Google Analytics 4 | ✅ | Avec Consent Mode v2 (RGPD) |
| Favicon SVG | ✅ | |

### Ce qui manque
| Élément | Statut | Impact estimé |
|---------|--------|---------------|
| Données structurées JSON-LD | ✅ | ProfessionalService + FAQPage en place |
| Inscription Google Search Console | ✅ | Réalisée le 06/04/2026 |
| Stratégie de contenu (blog/pages) | ❌ | **Fort** — limité à une seule URL |
| Backlinks / netlinking | ❌ | **Fort** — autorité de domaine faible |
| Google Business Profile | ❓ | **Moyen** — pertinent si activité localisable |
| Performance / Core Web Vitals | ❓ À auditer | **Moyen** — impact ranking |
| Pages secondaires (mentions légales, etc.) | ❌ | **Faible** — signal de confiance |

---

## 2. Stratégie proposée — Vue d'ensemble

La stratégie se décompose en **4 axes** complémentaires, classés par priorité :

```
Axe 1 — SEO technique (on-page)          → Impact immédiat
Axe 2 — Inscription & outils Google      → Indispensable
Axe 3 — Stratégie de contenu             → Moyen terme
Axe 4 — Netlinking & autorité            → Long terme
```

---

## 3. Axe 1 — SEO technique (on-page)

### 3.1 Données structurées JSON-LD ✅ FAIT

**Statut : Implémenté** | **Date : déjà en place au 06/04/2026**

Les deux blocs JSON-LD sont présents dans le `<head>` de `index.html` (lignes ~1931-2005) :

#### a) Schema `ProfessionalService` ✅
Identifie l'activité comme un service professionnel avec :
- name, description riche en mots-clés, url, image
- areaServed : France
- serviceType : Optimisation du taux de conversion, Audit CRO, Tests A/B, Accompagnement CRO e-commerce
- founder : Person (Léa Macioszczyk, Consultante CRO)

#### b) Schema `FAQPage` ✅
Reprend les 5 questions/réponses de la section FAQ, permettant :
- L'affichage des FAQ directement dans les SERP (rich snippets)
- Une augmentation significative du CTR
- L'intégration naturelle des mots-clés cibles dans les réponses

> **Validation** : tester les données structurées avec l'outil Google Rich Results Test (`search.google.com/test/rich-results`) pour confirmer leur bonne prise en compte.

---

### 3.2 Optimiser les performances (Core Web Vitals)

**Priorité : Haute** | **Impact : Moyen-Fort** | **Effort : Moyen**

Google utilise les Core Web Vitals comme facteur de classement. Les points à auditer et optimiser :

#### a) Images
- **Convertir `lea.png` en format WebP** avec fallback PNG via `<picture>`. Le format WebP est 25-35% plus léger, ce qui améliore le LCP (Largest Contentful Paint).
- **Vérifier les dimensions** : l'image est chargée en 280x280 (section à propos) et 34x34 (header). Si le fichier source est beaucoup plus grand, fournir des versions redimensionnées.
- L'attribut `loading="lazy"` est déjà en place sur l'image principale — c'est correct.
- L'attribut `loading="eager"` est sur l'image du header — c'est correct (above the fold).

#### b) CSS
- Le CSS est actuellement inline dans `<style>`, ce qui est bon pour le premier rendu (pas de requête bloquante supplémentaire).
- **Envisager le CSS critique** : s'assurer que le CSS au-dessus de la ligne de flottaison est chargé en premier. Avec un CSS inline unique, c'est déjà le cas.

#### c) Google Fonts
- Deux polices sont chargées (Instrument Serif + DM Sans). Le `<link rel="preconnect">` est déjà en place.
- **Ajouter `font-display: swap`** si ce n'est pas déjà fait (via le paramètre `&display=swap` dans l'URL Google Fonts — c'est déjà le cas).
- **Envisager le self-hosting** des polices pour éliminer les requêtes externes vers Google Fonts et améliorer le temps de chargement.

#### d) Scripts
- Le script Google Analytics est chargé en `async` — correct.
- **Aucun autre JS bloquant** — la page est principalement HTML/CSS pur, ce qui est un atout majeur pour la performance.

#### e) Audit recommandé
Passer la page dans les outils suivants et corriger les éventuels problèmes :
- **Google PageSpeed Insights** (`pagespeed.web.dev`) — score performance, accessibilité, SEO
- **Google Lighthouse** (DevTools Chrome > onglet Lighthouse)
- **GTmetrix** — analyse détaillée du temps de chargement

---

### 3.3 Ajouter des pages complémentaires

**Priorité : Moyenne** | **Impact : Faible-Moyen** | **Effort : Faible**

Des pages secondaires renforcent la crédibilité du site aux yeux de Google :

- **Page Mentions légales** (`/mentions-legales.html`) — obligatoire légalement en France, signal de confiance pour Google
- **Page Politique de confidentialité** (`/politique-confidentialite.html`) — obligatoire avec GA4/cookies, renforce le signal E-E-A-T (Experience, Expertise, Authoritativeness, Trustworthiness)

Ces pages doivent être liées depuis le footer et incluses dans le `sitemap.xml`.

---

### 3.4 Enrichir le contenu textuel existant

**Priorité : Moyenne** | **Impact : Moyen** | **Effort : Faible**

Sans dénaturer le design ni le ton de la page, quelques enrichissements textuels ciblés sont possibles :

- **Ajouter un paragraphe de contexte** dans la section "Le problème" intégrant naturellement les expressions "optimisation site web" et "amélioration taux de conversion"
- **Enrichir les descriptions des offres** avec les termes "test A/B", "audit de conversion", "analyse de données"
- **Ajouter des termes de longue traîne** dans les réponses FAQ : "comment améliorer le taux de conversion de mon site", "pourquoi mes visiteurs n'achètent pas"

> **Règle importante** : le contenu doit rester naturel et orienté utilisateur. Le bourrage de mots-clés (keyword stuffing) est pénalisé par Google. Viser une densité de 1-2% par mot-clé principal.

---

## 4. Axe 2 — Inscription & outils Google

### 4.1 Google Search Console ✅ FAIT

**Statut : Réalisé** | **Date : 06/04/2026**

L'inscription sur Google Search Console a été effectuée pour le domaine `leamacio.com`.

**Actions réalisées :**
1. ✅ Vérification de la propriété du domaine
2. ✅ Soumission du sitemap `https://leamacio.com/sitemap.xml`
3. ✅ Demande d'indexation de la page principale

**Suivi à effectuer régulièrement :**
- Les requêtes de recherche qui génèrent des impressions
- Le taux de clic (CTR) par requête
- Les éventuelles erreurs d'exploration
- La couverture de l'index
- Les problèmes de Core Web Vitals

### 4.2 Google Business Profile

**Priorité : Moyenne** | **Impact : Moyen** | **Effort : Faible**

Si l'activité peut être rattachée à une localisation (même en freelance à domicile), créer un profil **Google Business Profile** (`business.google.com`) :
- Catégorie : "Consultant en marketing" ou "Agence de marketing digital"
- Lien vers le site web
- Description riche en mots-clés
- Photos professionnelles

Cela permet d'apparaître dans les résultats locaux ("consultant CRO + ville") et sur Google Maps.

### 4.3 Google Analytics — Suivi des conversions

**Priorité : Moyenne** | **Impact : Indirect** | **Effort : Moyen**

GA4 est déjà installé. Configurer des **événements de conversion** pour mesurer l'efficacité du SEO :
- **Soumission du formulaire de contact** → événement `generate_lead`
- **Clic sur "Diagnostic gratuit"** → événement `click_cta`
- **Scroll jusqu'à la section offres** → événement `view_offers`

Ces données permettront d'optimiser les pages et le contenu en fonction des requêtes qui convertissent le mieux.

---

## 5. Axe 3 — Stratégie de contenu

### 5.1 Créer un blog / section articles

**Priorité : Haute** | **Impact : Fort** | **Effort : Élevé (continu)**

C'est le levier SEO le plus puissant à moyen/long terme. Un blog permet de :
- **Cibler les mots-clés informationnels** à volume élevé (que la landing page seule ne peut pas capter)
- **Démontrer l'expertise** (signal E-E-A-T)
- **Générer du trafic organique** qui sera redirigé vers les offres
- **Obtenir des backlinks naturels** (les articles utiles sont partagés et cités)

#### Articles prioritaires à créer

| # | Titre proposé | Mot-clé cible | Volume estimé | Intention |
|---|---------------|---------------|---------------|-----------|
| 1 | "Qu'est-ce que le CRO ? Guide complet pour comprendre l'optimisation du taux de conversion" | CRO, optimisation taux de conversion | Moyen | Informationnelle |
| 2 | "Comment améliorer le taux de conversion de votre site e-commerce : 10 actions concrètes" | améliorer taux de conversion, optimisation site web | Moyen-Élevé | Informationnelle |
| 3 | "Test A/B : comment tester et optimiser votre site web étape par étape" | test A/B site web | Moyen | Informationnelle |
| 4 | "Pourquoi votre site ne convertit pas : les 7 frictions les plus courantes" | pourquoi mon site ne convertit pas | Faible | Informationnelle |
| 5 | "Audit CRO : que contient un audit de conversion et pourquoi en faire un ?" | audit CRO, audit de conversion | Faible | Commerciale |
| 6 | "CRO vs SEO vs Redesign : quel levier choisir pour votre site ?" | CRO vs SEO | Faible | Informationnelle |
| 7 | "Taux de conversion e-commerce : benchmarks 2026 et comment se situer" | taux de conversion e-commerce | Moyen | Informationnelle |
| 8 | "Optimisation du parcours utilisateur : comment réduire les frictions sur votre site" | optimisation parcours utilisateur, frictions site web | Faible | Informationnelle |

#### Recommandations pour chaque article
- **Longueur** : 1500-2500 mots minimum (les articles longs et complets se positionnent mieux)
- **Structure** : utiliser des `<h2>` et `<h3>` contenant les mots-clés secondaires
- **Maillage interne** : chaque article doit contenir au moins 1-2 liens vers la landing page (sections offres ou contact)
- **CTA** : intégrer un appel à l'action vers le diagnostic gratuit dans chaque article
- **Fréquence** : publier 2-4 articles par mois dans les premiers mois, puis 1-2 par mois en régime de croisière

### 5.2 Optimiser le maillage interne

**Priorité : Moyenne** | **Impact : Moyen** | **Effort : Faible**

Une fois le blog en place :
- Chaque article renvoie vers la landing page et vers 1-2 autres articles connexes
- La landing page peut intégrer un lien vers les articles les plus pertinents (ex : dans la section FAQ, lier "En savoir plus" vers l'article correspondant)
- Utiliser des **ancres de texte descriptives** contenant les mots-clés (éviter les "cliquez ici")

---

## 6. Axe 4 — Netlinking & autorité de domaine

### 6.1 Stratégie de backlinks

**Priorité : Haute** | **Impact : Fort** | **Effort : Élevé (continu)**

Les backlinks (liens entrants depuis d'autres sites) restent l'un des facteurs de classement les plus importants de Google. Pour un site récent, c'est souvent le facteur limitant.

#### Sources de backlinks à exploiter

| Source | Action | Difficulté | Qualité du lien |
|--------|--------|------------|-----------------|
| **Profil LinkedIn** | Ajouter le lien du site dans le profil et les publications | Facile | Moyenne (nofollow mais trafic direct) |
| **Annuaires freelance** (Malt, Crème de la Crème, Codeur.com, etc.) | Créer un profil complet avec lien vers le site | Facile | Moyenne |
| **Articles invités** (guest blogging) | Proposer des articles sur des blogs marketing/e-commerce | Moyen | Forte |
| **Témoignages clients** | Offrir un témoignage à un outil/service utilisé en échange d'un lien | Moyen | Forte |
| **Répertoires professionnels** | Inscription sur des annuaires de consultants (France Num, etc.) | Facile | Moyenne |
| **Forums et communautés** | Participer activement sur des forums e-commerce/marketing (avec lien en signature) | Moyen | Faible-Moyenne |
| **Relations presse / médias** | Être cité comme experte CRO dans des articles de presse en ligne | Difficile | Très forte |
| **Études de cas / données originales** | Publier des résultats anonymisés de missions CRO → contenu naturellement partagé | Moyen | Forte |

#### Bonnes pratiques
- **Qualité > quantité** : un seul lien depuis un site à forte autorité vaut plus que 50 liens depuis des annuaires obscurs
- **Diversité** : varier les sources (blogs, annuaires, réseaux sociaux, presse)
- **Ancres variées** : ne pas utiliser toujours la même ancre de texte (risque de pénalité)
- **Éviter** : achat de liens, PBN (Private Blog Networks), échanges de liens massifs — pratiques pénalisées par Google

### 6.2 Présence sur les réseaux sociaux

**Priorité : Moyenne** | **Impact : Indirect** | **Effort : Moyen (continu)**

Les signaux sociaux ne sont pas un facteur de classement direct, mais ils contribuent indirectement :
- **LinkedIn** (déjà en place — lien dans la section À propos) : publier régulièrement du contenu CRO, partager les articles du blog
- **Twitter/X** : créer un profil professionnel, partager des insights CRO
- **Publication régulière** : les contenus partagés génèrent du trafic et potentiellement des backlinks naturels

---

## 7. Plan d'action priorisé

### Phase 1 — Actions immédiates (semaines 1-2)

| # | Action | Axe | Impact | Effort |
|---|--------|-----|--------|--------|
| ~~1~~ | ~~**Données structurées JSON-LD**~~ (ProfessionalService + FAQPage) | ~~SEO technique~~ | ✅ Déjà en place | — |
| ~~2~~ | ~~**Google Search Console**~~ + sitemap soumis | ~~Outils Google~~ | ✅ Réalisé le 06/04/2026 | — |
| 3 | **Auditer les Core Web Vitals** avec PageSpeed Insights et corriger les problèmes | SEO technique | Moyen | Moyen |
| 4 | **Convertir `lea.png` en WebP** avec fallback | Performance | Moyen | Faible |

### Phase 2 — Actions à court terme (semaines 3-6)

| # | Action | Axe | Impact | Effort |
|---|--------|-----|--------|--------|
| 5 | **Créer les pages mentions légales et politique de confidentialité** | SEO technique | Faible-Moyen | Faible |
| 6 | **Créer un Google Business Profile** | Outils Google | Moyen | Faible |
| 7 | **Configurer les événements de conversion GA4** | Mesure | Indirect | Moyen |
| 8 | **S'inscrire sur les plateformes freelance** (Malt, etc.) avec lien vers le site | Netlinking | Moyen | Faible |

### Phase 3 — Actions à moyen terme (mois 2-4)

| # | Action | Axe | Impact | Effort |
|---|--------|-----|--------|--------|
| 9 | **Mettre en place le blog** (structure, premier article pilier) | Contenu | Fort | Élevé |
| 10 | **Publier les 3 premiers articles** (priorité : articles 1, 2 et 3 du tableau §5.1) | Contenu | Fort | Élevé |
| 11 | **Démarrer le guest blogging** sur 2-3 blogs marketing/e-commerce | Netlinking | Fort | Moyen |

### Phase 4 — Actions continues (mois 4+)

| # | Action | Axe | Impact | Effort |
|---|--------|-----|--------|--------|
| 12 | **Publier 1-2 articles/mois** sur le blog | Contenu | Fort | Moyen |
| 13 | **Développer le netlinking** progressivement | Netlinking | Fort | Moyen |
| 14 | **Analyser les données Search Console** et ajuster la stratégie | Mesure | Moyen | Faible |
| 15 | **Enrichir le contenu de la landing page** en fonction des requêtes identifiées | SEO technique | Moyen | Faible |

---

## 8. Modifications techniques de la page `index.html`

Récapitulatif des modifications concrètes à apporter au fichier `index.html` :

### ~~Modification A — Données structurées JSON-LD~~ ✅ DÉJÀ EN PLACE
- Les deux blocs JSON-LD (ProfessionalService + FAQPage) sont déjà intégrés dans le `<head>` (lignes ~1931-2005)
- À valider avec Google Rich Results Test

### Modification B — Conversion image WebP (Priorité 2)
- **Où** : les deux balises `<img src="lea.png">` (header ligne ~2018 et section à propos ligne ~2126)
- **Quoi** : remplacer par `<picture>` avec source WebP et fallback PNG
- **Pré-requis** : générer le fichier `lea.webp` à partir de `lea.png`
- **Impact** : amélioration du LCP (Core Web Vitals)

### Modification C — Self-hosting des polices (Priorité 3)
- **Où** : les `<link>` Google Fonts dans le `<head>` (lignes 54-56)
- **Quoi** : télécharger les fichiers de polices, les héberger localement, remplacer les `<link>` par des `@font-face` dans le CSS
- **Impact** : suppression de 2-3 requêtes HTTP externes, amélioration du temps de chargement

### Modification D — Pages complémentaires (Priorité 3)
- **Où** : footer de `index.html` + nouveaux fichiers
- **Quoi** : créer `mentions-legales.html` et `politique-confidentialite.html`, ajouter des liens dans le footer
- **Impact** : signal de confiance, conformité légale

### Modification E — Mise à jour du sitemap (Priorité 3)
- **Où** : `sitemap.xml`
- **Quoi** : ajouter les nouvelles pages (mentions légales, politique de confidentialité, et plus tard les articles de blog)
- **Impact** : aide Google à découvrir toutes les pages du site

---

## 9. KPIs et suivi

### Indicateurs à suivre mensuellement

| KPI | Outil | Objectif à 3 mois | Objectif à 6 mois |
|-----|-------|-------------------|-------------------|
| Position moyenne sur "consultant CRO freelance" | Search Console | Top 30 | Top 10 |
| Position moyenne sur "optimisation taux de conversion" | Search Console | Top 50 | Top 20 |
| Impressions organiques / mois | Search Console | 500+ | 2000+ |
| Clics organiques / mois | Search Console | 50+ | 200+ |
| CTR moyen | Search Console | > 3% | > 5% |
| Score PageSpeed (mobile) | PageSpeed Insights | > 90 | > 95 |
| Nombre de backlinks | Search Console / Ahrefs | 10+ | 30+ |
| Nombre de pages indexées | Search Console | 5+ | 15+ |

### Revue stratégique
- **Mensuelle** : analyser les requêtes Search Console, identifier les opportunités de contenu
- **Trimestrielle** : évaluer la progression des KPIs, ajuster la stratégie de contenu et de netlinking
- **Semestrielle** : audit SEO complet (technique + contenu + backlinks)

---

## 10. Résumé de la stratégie

```
┌─────────────────────────────────────────────────────────────────┐
│                    STRATÉGIE SEO GLOBALE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  IMMÉDIAT (sem. 1-2)                                           │
│  ├── ✅ JSON-LD (ProfessionalService + FAQPage) — FAIT         │
│  ├── ✅ Google Search Console — FAIT                           │
│  └── Audit Core Web Vitals + optimisation images               │
│                                                                 │
│  COURT TERME (sem. 3-6)                                        │
│  ├── Pages légales                                             │
│  ├── Google Business Profile                                   │
│  ├── Conversion tracking GA4                                   │
│  └── Profils plateformes freelance                             │
│                                                                 │
│  MOYEN TERME (mois 2-4)                                        │
│  ├── Mise en place du blog                                     │
│  ├── 3 premiers articles piliers                               │
│  └── Guest blogging (2-3 sites)                                │
│                                                                 │
│  CONTINU (mois 4+)                                             │
│  ├── Publication régulière (1-2 articles/mois)                 │
│  ├── Développement netlinking                                  │
│  └── Analyse et ajustements basés sur Search Console           │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

> **Note** : Le document `analyse/SEO.md` reste la référence technique pour les modifications on-page déjà identifiées. Le présent document couvre la stratégie globale de référencement, incluant les actions on-page restantes, les actions off-page et la stratégie de contenu à long terme.
