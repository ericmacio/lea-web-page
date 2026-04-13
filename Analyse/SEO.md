# Optimisation SEO — Landing Page CRO

> Ce document recense les optimisations de référencement naturel (SEO) pour améliorer le positionnement de la page `index.html` sur les requêtes liées à l'activité CRO.

---

## Univers de mots-clés cibles

### Mots-clés principaux (intention commerciale forte)
| Mot-clé | Volume estimé (FR/mois) | Concurrence | Pertinence |
|---------|------------------------|-------------|------------|
| consultant CRO freelance | Faible | Faible | Directe |
| freelance optimisation conversion | Faible | Faible | Directe |
| audit CRO site web | Faible–Moyen | Moyenne | Directe |
| optimisation taux de conversion | Moyen | Moyenne | Directe |
| CRO e-commerce | Moyen | Moyenne | Directe |

### Mots-clés secondaires (intention informationnelle → acquisition)
| Mot-clé | Volume estimé (FR/mois) | Concurrence | Pertinence |
|---------|------------------------|-------------|------------|
| optimisation de site web | Élevé | Élevée | Forte |
| améliorer conversion site web | Moyen | Moyenne | Forte |
| augmenter ventes site e-commerce | Moyen | Moyenne | Forte |
| pourquoi mon site ne convertit pas | Faible | Faible | Forte |
| taux de conversion e-commerce | Moyen | Moyenne | Forte |
| test A/B site web | Moyen | Moyenne | Moyenne |
| UX et conversion | Faible | Faible | Moyenne |
| optimisation parcours utilisateur | Faible | Faible | Forte |
| frictions site web | Faible | Faible | Forte |
| améliorer expérience utilisateur site | Moyen | Moyenne | Forte |

### Mots-clés longue traîne (faible concurrence, haute intention)
- "comment améliorer le taux de conversion de mon site"
- "freelance CRO France"
- "audit conversion site e-commerce"
- "consultant optimisation site vitrine"
- "pourquoi mes visiteurs n'achètent pas"

---

## État actuel du SEO on-page

### Ce qui est déjà en place
- `<title>` contenant "CRO" et "Optimisation du taux de conversion"
- `<meta name="description">` descriptive et ciblée
- Balises Open Graph et Twitter Card
- `<link rel="canonical">`
- `sitemap.xml` et `robots.txt`
- Structure HTML sémantique (`<header>`, `<section>`, `<footer>`, `<nav>`)
- Attribut `lang="fr"` sur `<html>`
- Un seul `<h1>`, hiérarchie `<h2>` correcte

### Ce qui manque ou peut être amélioré
Les points ci-dessous sont classés par impact SEO décroissant.

---

## Modification 1 — Enrichir le `<title>` avec les mots-clés cibles

**Priorité : Haute**
**Fichier :** `index.html`, ligne 27

### Actuel
```html
<title>Léa Macioszczyk — Freelance CRO | Optimisation du taux de conversion</title>
```

### Problème
Le titre est bien structuré mais n'inclut pas les termes "e-commerce", "site web" ou "audit" que les prospects sont susceptibles de rechercher. Le nom propre en début de titre consomme des caractères précieux sans valeur SEO pour un site encore peu connu.

### Recommandation
```html
<title>Optimisation du taux de conversion (CRO) — Freelance e-commerce & site vitrine | Léa Macioszczyk</title>
```

**Pourquoi :** Placer les mots-clés à fort potentiel en début de titre maximise leur poids SEO. Le nom propre reste en fin de titre pour le branding. Le titre fait 95 caractères — Google affiche environ 55–60 caractères, mais indexe l'intégralité.

---

## Modification 2 — Enrichir la `<meta description>` avec un appel à l'action

**Priorité : Haute**
**Fichier :** `index.html`, ligne 28

### Actuel
```html
<meta name="description" content="J'aide les e-commerces et les sites vitrines à transformer leur trafic en résultats mesurables grâce à une approche CRO simple, concrète et orientée résultats.">
```

### Problème
La description est bien rédigée mais n'inclut pas certains mots-clés secondaires ("audit", "taux de conversion", "test A/B") et ne contient pas d'appel à l'action explicite qui inciterait au clic dans les résultats de recherche.

### Recommandation
```html
<meta name="description" content="Consultante CRO freelance : audit de conversion, tests A/B et optimisation du taux de conversion pour e-commerces et sites vitrines. Diagnostic gratuit de votre site.">
```

**Pourquoi :** Cette version inclut les mots-clés "audit de conversion", "tests A/B", "taux de conversion", "e-commerces", "sites vitrines" tout en terminant par un appel à l'action ("Diagnostic gratuit"). Elle fait 163 caractères (Google affiche ~155–160).

---

## Modification 3 — Ajouter des données structurées Schema.org (JSON-LD)

**Priorité : Haute**
**Fichier :** `index.html`, section `<head>`

### Problème
Aucune donnée structurée n'est présente. Google ne peut pas identifier qu'il s'agit d'un professionnel proposant des services. Sans Schema.org, la page ne peut pas bénéficier de résultats enrichis (rich snippets) dans les SERP.

### Recommandation
Ajouter un bloc JSON-LD avant `</head>` avec deux schémas complémentaires :

#### a) Schema `ProfessionalService` — Identifie l'activité
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "ProfessionalService",
  "name": "Léa Macioszczyk — Freelance CRO",
  "description": "Consultante freelance spécialisée en optimisation du taux de conversion (CRO) pour e-commerces et sites vitrines. Audit de conversion, tests A/B, accompagnement CRO.",
  "url": "https://leamacio.com/",
  "image": "https://leamacio.com/lea.png",
  "priceRange": "€€",
  "areaServed": {
    "@type": "Country",
    "name": "France"
  },
  "serviceType": [
    "Optimisation du taux de conversion",
    "Audit CRO",
    "Tests A/B",
    "Accompagnement CRO e-commerce"
  ],
  "founder": {
    "@type": "Person",
    "name": "Léa Macioszczyk",
    "jobTitle": "Consultante CRO",
    "image": "https://leamacio.com/lea.png"
  }
}
</script>
```

#### b) Schema `FAQPage` — Permet l'affichage des FAQ dans les SERP
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Concrètement, c'est quoi le CRO ?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Le CRO (Conversion Rate Optimization) consiste à améliorer le pourcentage de visiteurs qui réalisent une action clé sur votre site : un achat, une demande de devis, une prise de contact, une inscription. Plutôt que de dépenser plus en publicité pour attirer du trafic, le CRO maximise la valeur du trafic que vous avez déjà en identifiant ce qui freine vos visiteurs et en optimisant leur expérience. C'est l'un des leviers les plus rentables du marketing digital."
      }
    },
    {
      "@type": "Question",
      "name": "Est-ce que le CRO fonctionne pour les petits sites avec peu de trafic ?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Oui, mais l'approche diffère. Avec un trafic modeste, les tests A/B classiques prennent plus de temps à produire des résultats statistiquement fiables. Dans ce cas, je me concentre sur l'audit et l'analyse qualitative (heatmaps, replays, tests utilisateurs) pour identifier les frictions les plus évidentes."
      }
    },
    {
      "@type": "Question",
      "name": "Combien de temps avant de voir des résultats concrets ?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "L'audit livré en 2 semaines vous donne des actions immédiates. Pour l'accompagnement continu, les premiers résultats mesurables arrivent généralement entre 4 et 8 semaines après la mise en place des premiers tests."
      }
    },
    {
      "@type": "Question",
      "name": "Quelle différence entre le CRO, le SEO et le redesign ?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Le SEO vous amène du trafic. Le redesign change l'apparence de votre site. Le CRO optimise ce qui se passe entre l'arrivée du visiteur et la conversion. Ce sont des leviers complémentaires, mais si vous avez déjà du trafic et que vos résultats ne suivent pas, le CRO est le levier le plus rentable à court terme."
      }
    },
    {
      "@type": "Question",
      "name": "Que se passe-t-il si l'audit ne révèle rien de significatif ?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "C'est extrêmement rare, il y a toujours des frictions à corriger. Mais si votre site est déjà très bien optimisé, je vous le dis honnêtement et je vous oriente vers d'autres leviers plus pertinents."
      }
    }
  ]
}
</script>
```

**Pourquoi :** Le schema `FAQPage` est particulièrement puissant : Google peut afficher les questions/réponses directement dans les résultats de recherche, occupant davantage d'espace visuel et augmentant significativement le taux de clic (CTR). Le schema `ProfessionalService` aide Google à comprendre la nature de l'activité et la zone géographique.

---

## Modification 4 — Optimiser les balises `<h2>` avec les mots-clés

**Priorité : Moyenne**
**Fichier :** `index.html`, lignes des `<h2>`

### Problème
Les `<h2>` actuels sont orientés copywriting (accroche émotionnelle), ce qui est excellent pour la conversion, mais ils ne contiennent quasiment aucun mot-clé recherché par les prospects. Google accorde un poids important aux mots contenus dans les headings.

### Actuel vs. Recommandé

| Section | Actuel | Recommandé |
|---------|--------|------------|
| Problème (ligne 1704) | "La plupart des sites perdent des conversions sans le savoir." | "La plupart des sites web perdent des conversions sans le savoir." |
| À propos (ligne 1743) | "Consultante conversion & performance digitale" | "Consultante CRO : optimisation de la conversion & performance digitale" |
| Méthode (ligne 1758) | "Analyse, hypothèses, tests, résultats." | "Optimisation du taux de conversion : analyse, hypothèses, tests, résultats." |
| Offres (ligne 1801) | "Un point d'entrée selon votre situation." | "Nos offres d'optimisation CRO selon votre situation." |
| Contact (ligne 1879) | "Si vous pensez que votre site peut générer plus de résultats." | Pas de changement (CTA, pas un heading informatif) |
| FAQ (ligne 1937) | "Vous hésitez encore ?" | "Questions fréquentes sur le CRO et l'optimisation de conversion" |

**Pourquoi :** L'objectif est d'injecter les mots-clés cibles dans les headings sans dénaturer le ton commercial de la page. Les modifications proposées restent naturelles et lisibles tout en intégrant "sites web", "CRO", "optimisation de la conversion", "taux de conversion".

**Attention :** Le document `docs/texte.txt` fait référence pour le contenu textuel. Les modifications ci-dessus doivent être validées pour s'assurer qu'elles ne contreviennent pas à l'argumentaire d'origine. Si un heading ne peut pas être modifié, le mot-clé peut être intégré dans le paragraphe qui suit immédiatement.

---

## Modification 5 — Ajouter des balises `<meta>` keywords complémentaires et `<meta>` author

**Priorité : Faible**
**Fichier :** `index.html`, section `<head>`

### Recommandation
```html
<meta name="author" content="Léa Macioszczyk">
<meta name="subject" content="Optimisation du taux de conversion (CRO) — Freelance e-commerce">
```

**Note :** La balise `<meta name="keywords">` n'est plus prise en compte par Google depuis 2009. Elle n'est donc pas recommandée. En revanche, `author` et `subject` apportent du contexte sémantique sans risque.

---

## Modification 6 — Optimiser les balises Open Graph et Twitter Card

**Priorité : Moyenne**
**Fichier :** `index.html`, lignes 34–44

### Problème
Les balises OG/Twitter doivent être alignées avec le nouveau `<title>` et la nouvelle `<meta description>` pour cohérence. Les mots-clés doivent aussi apparaître dans le contenu partagé sur les réseaux sociaux.

### Recommandation
```html
<!-- Open Graph -->
<meta property="og:title" content="Optimisation du taux de conversion (CRO) — Freelance e-commerce & site vitrine">
<meta property="og:description" content="Consultante CRO freelance : audit de conversion, tests A/B et optimisation du taux de conversion pour e-commerces et sites vitrines. Diagnostic gratuit.">
<meta property="og:image" content="https://leamacio.com/lea.png">
<meta property="og:type" content="website">
<meta property="og:url" content="https://leamacio.com/">
<meta property="og:locale" content="fr_FR">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Optimisation du taux de conversion (CRO) — Freelance e-commerce & site vitrine">
<meta name="twitter:description" content="Consultante CRO freelance : audit de conversion, tests A/B et optimisation. Diagnostic gratuit de votre site.">
<meta name="twitter:image" content="https://leamacio.com/lea.png">
```

**Ajouts :** `og:locale` pour indiquer la langue aux plateformes sociales.

---

## Modification 7 — Améliorer la sémantique HTML pour le SEO

**Priorité : Moyenne**
**Fichier :** `index.html`

### a) Ajouter `<main>` autour du contenu principal
Le contenu entre le header et le footer devrait être englobé dans une balise `<main>`. Cela aide Google à distinguer le contenu principal du contenu de navigation/footer.

```html
<main>
  <section id="hero" class="hero">...</section>
  <section id="probleme" class="probleme">...</section>
  <!-- ... toutes les sections ... -->
  <section id="faq" class="faq">...</section>
</main>
<footer class="footer">...</footer>
```

### b) Utiliser `<article>` pour les cartes d'offres
Chaque carte d'offre est un contenu autonome et pourrait bénéficier d'une balise `<article>` au lieu de `<div>` :

```html
<article class="offres__card">
  ...
</article>
```

### c) Ajouter des attributs `aria-label` sur les sections
Pour renforcer la sémantique :
```html
<section id="methode" class="methode" aria-label="Méthode d'optimisation CRO">
<section id="offres" class="offres" aria-label="Offres d'audit et accompagnement CRO">
```

---

## Modification 8 — Ajouter un texte `alt` enrichi sur l'image de profil

**Priorité : Faible**
**Fichier :** `index.html`, ligne 1740

### Actuel
```html
alt="Léa Macioszczyk — Consultante CRO"
```

### Recommandation
```html
alt="Léa Macioszczyk — Consultante freelance en optimisation du taux de conversion (CRO) pour e-commerce et sites vitrines"
```

**Pourquoi :** L'attribut `alt` est indexé par Google Images et contribue au référencement. Un texte plus descriptif intégrant les mots-clés cibles améliore la visibilité sur Google Images.

---

## Résumé

| # | Modification | Impact SEO | Complexité | Fichier |
|---|-------------|-----------|------------|---------|
| 1 | Enrichir `<title>` | Fort | Faible | `<head>` |
| 2 | Enrichir `<meta description>` | Fort | Faible | `<head>` |
| 3 | Données structurées JSON-LD | Fort | Moyenne | `<head>` |
| 4 | Mots-clés dans les `<h2>` | Moyen | Faible | HTML body |
| 5 | `<meta>` author/subject | Faible | Faible | `<head>` |
| 6 | Aligner OG/Twitter + `og:locale` | Moyen | Faible | `<head>` |
| 7 | Sémantique HTML (`<main>`, `<article>`) | Moyen | Faible | HTML body |
| 8 | Texte `alt` enrichi | Faible | Faible | HTML body |

### Prochaines étapes suggérées
1. **Priorité 1 :** Modifications 1, 2 et 3 (title, description, JSON-LD) — impact fort, effort faible à moyen
2. **Priorité 2 :** Modifications 4 et 6 (h2 et OG/Twitter) — impact moyen, effort faible
3. **Priorité 3 :** Modifications 5, 7 et 8 — impact faible à moyen, effort faible

### Note importante
La modification 4 (h2) altère le contenu textuel visible. Les formulations proposées doivent être validées par rapport au document `docs/texte.txt` qui fait référence pour l'argumentaire commercial.
