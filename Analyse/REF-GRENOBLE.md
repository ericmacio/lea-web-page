# REF-GRENOBLE.md -- Referencement local Grenoble / Isere

> **Date** : avril 2026
> **Objectif** : Permettre a la page d'apparaitre sur des recherches locales
> ("Freelance CRO Grenoble", "optimisation conversion Isere", etc.)
> tout en conservant un positionnement national / remote.

---

## 1. Etat actuel

La page est aujourd'hui **100% geo-agnostique** :

- Aucune mention de Grenoble, Isere, Rhone-Alpes ou Auvergne-Rhone-Alpes
- Le `areaServed` de tous les schemas est `{"@type": "Country", "name": "France"}`
- Pas d'adresse, de code postal ni de coordonnees geographiques
- Le llms.txt indique "France (principalement a distance)"
- Pas de page Google Business Profile associee

**Consequence** : la page est invisible pour toute recherche incluant un terme geographique local.

---

## 2. Strategie recommandee

### Principe : ancrage local + rayonnement national

L'idee n'est pas de se limiter a Grenoble mais d'**ancrer la credibilite locale** tout en gardant le message "j'interviens partout en France a distance". Cela permet de :

- Capter les recherches locales ("freelance CRO Grenoble", "CRO Isere")
- Rassurer les acteurs locaux (proximite, possibilite de rencontres en personne)
- Ne pas perdre le positionnement national existant

---

## 3. Recommandations

### 3.1 Enrichir les schemas avec des donnees geographiques -- IMPLEMENTE (2026-04-10)

**a) Ajouter `address` et `geo` au schema `ProfessionalService`**

Remplacer le `areaServed` actuel par un tableau incluant la France et Grenoble, et ajouter une adresse :

```json
{
  "@type": "ProfessionalService",
  "name": "Lea Macioszczyk -- Freelance CRO",
  ...
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "Grenoble",
    "addressRegion": "Auvergne-Rhone-Alpes",
    "postalCode": "38000",
    "addressCountry": "FR"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 45.1885,
    "longitude": 5.7245
  },
  "areaServed": [
    {"@type": "City", "name": "Grenoble"},
    {"@type": "AdministrativeArea", "name": "Isere"},
    {"@type": "AdministrativeArea", "name": "Auvergne-Rhone-Alpes"},
    {"@type": "Country", "name": "France"}
  ]
}
```

**b) Ajouter `areaServed` local aux schemas `Service`**

Meme logique sur les 3 schemas Service existants : ajouter Grenoble et Isere en plus de France.

**c) Enrichir le schema `Person`**

Ajouter une propriete `workLocation` :

```json
{
  "@type": "Person",
  "name": "Lea Macioszczyk",
  ...
  "workLocation": {
    "@type": "Place",
    "address": {
      "@type": "PostalAddress",
      "addressLocality": "Grenoble",
      "addressRegion": "Auvergne-Rhone-Alpes",
      "postalCode": "38000",
      "addressCountry": "FR"
    }
  }
}
```

---

### 3.2 Ajouter des signaux geographiques dans le contenu HTML -- IMPLEMENTE (2026-04-10)

L'objectif est d'integrer les mots-cles geographiques de maniere **naturelle** dans le contenu visible, sans forcer ni nuire a la lisibilite.

**a) Section "A propos"**

Ajouter une mention de la localisation dans la presentation :

> Actuel : "Specialisee en optimisation de la conversion (CRO), j'aide les entreprises..."
>
> Suggere : "Basee a Grenoble et intervenant dans toute la France, je suis specialisee en optimisation de la conversion (CRO). J'aide les entreprises..."

Cela place naturellement "Grenoble" et "France" dans un paragraphe cle.

**b) Section Hero (sous-titre)**

Ajouter un ancrage geographique discret :

> Actuel : "J'aide les e-commerces et les sites vitrines a transformer leur trafic en resultats mesurables..."
>
> Suggere : "J'aide les e-commerces et les sites vitrines a transformer leur trafic en resultats mesurables (ventes ou prises de contact) grace a une approche CRO [...]. Basee a Grenoble, j'interviens partout en France."

**c) Footer**

Ajouter la localisation dans le footer :

```html
<span class="footer__location">Grenoble, France</span>
```

Cela cree un signal geographique persistant sur toute la page.

---

### 3.3 Optimiser les meta tags -- IMPLEMENTE (2026-04-10)

**a) Meta description**

> Actuel : "Consultante CRO freelance : audit de conversion, tests A/B et optimisation du taux de conversion pour e-commerces et sites vitrines. Diagnostic gratuit de votre site."
>
> Suggere : "Consultante CRO freelance a Grenoble : audit de conversion, tests A/B et optimisation du taux de conversion pour e-commerces et sites vitrines. Intervention dans toute la France. Diagnostic gratuit."

Le mot "Grenoble" est place en debut de description pour maximiser son poids.

**b) Title tag**

> Actuel : "Optimisation du taux de conversion (CRO) -- Freelance e-commerce & site vitrine | Lea Macioszczyk"
>
> Suggere : "Consultante CRO freelance Grenoble -- Optimisation du taux de conversion | Lea Macioszczyk"

Plus court, plus cible. "CRO Grenoble" devient le keyword principal du title.

**c) Open Graph / Twitter Card**

Mettre a jour og:title et twitter:title avec la meme formulation que le title tag pour assurer la coherence.

---

### 3.4 Mettre a jour llms.txt -- IMPLEMENTE (2026-04-10)

Ajouter la localisation dans la description et la zone d'intervention :

```markdown
# Lea Macioszczyk -- Consultante CRO Freelance a Grenoble

> Consultante freelance basee a Grenoble, specialisee en optimisation
> du taux de conversion (CRO) pour e-commerces et sites vitrines.
> Intervention dans toute la France.

## Zone d'intervention
- Basee a Grenoble (38000), Isere, Auvergne-Rhone-Alpes
- Intervention a distance dans toute la France
```

---

### 3.5 Ajouter une question FAQ ciblee geographiquement

Ajouter une question dans la FAQ existante (HTML + schema FAQPage) :

**Question** : "Intervenez-vous uniquement a Grenoble et en Isere ?"

**Reponse** : "Je suis basee a Grenoble mais j'interviens dans toute la France. Mon accompagnement CRO se fait principalement a distance (visioconference, outils collaboratifs). Pour les entreprises de Grenoble, de l'Isere et de la region Auvergne-Rhone-Alpes, des rencontres en personne sont possibles si necessaire."

Cette question permet de :
- Placer naturellement "Grenoble", "Isere" et "Auvergne-Rhone-Alpes" dans le contenu
- Repondre a une question reelle que les prospects locaux se posent
- Etre indexee dans le schema FAQPage (visible dans les rich snippets et les reponses IA)

---

### 3.6 Creer une page Google Business Profile

**En dehors du site mais fortement recommande.**

Creer un profil Google Business avec :
- Categorie : "Consultant en marketing" ou "Service de marketing digital"
- Adresse : Grenoble, 38000
- Zone de service : Grenoble, Isere, Auvergne-Rhone-Alpes, France
- Lien vers leamacio.com
- Description reprenant les mots-cles CRO + Grenoble

**Pourquoi** : Google Business Profile est le signal local #1 pour Google Search et Google Maps. Les IA (Gemini, Google AI Overviews) s'appuient aussi sur ces donnees pour les requetes locales. Sans profil, les recherches "CRO Grenoble" sur Google ne feront jamais remonter la page dans le pack local.

---

### 3.7 Envisager une page dediee (optionnel, long terme)

Si le referencement local devient un axe strategique important, creer une page dediee `grenoble.html` ou `/cro-grenoble/` avec :
- Un contenu specifique au marche grenoblois (tissu economique local, startups, PME tech...)
- Des mots-cles longue traine : "audit CRO Grenoble", "optimisation site e-commerce Isere", "freelance conversion Rhone-Alpes"
- Un lien depuis la page principale

**Avantage** : Permet de cibler agressivement les mots-cles locaux sans diluer le positionnement national de la page principale.

**Inconvenient** : Maintenance d'une page supplementaire. A ne faire que si le marche local justifie l'effort.

---

## 4. Mots-cles geographiques a cibler

| Mot-cle | Volume estime | Difficulte |
|---|---|---|
| Freelance CRO Grenoble | Faible (niche) | Tres faible |
| Consultant CRO Grenoble | Faible (niche) | Tres faible |
| Optimisation conversion Grenoble | Faible | Tres faible |
| Freelance CRO Isere | Tres faible | Quasi nulle |
| Audit site web Grenoble | Moyen | Moyenne |
| Optimisation e-commerce Grenoble | Faible | Faible |
| Test A/B Grenoble | Tres faible | Quasi nulle |
| Consultant marketing digital Grenoble | Moyen | Moyenne |

**Note** : Les volumes sont faibles car la niche CRO est specifique, mais la concurrence locale l'est aussi. Quelques signaux bien places suffisent a dominer ces requetes.

---

## 5. Resume -- Plan d'implementation

| # | Action | Effort | Impact local | Fichiers concernes |
|---|---|---|---|---|
| 3.1 | Enrichir schemas avec geo (address, areaServed, workLocation) | Faible | Eleve | index.html |
| 3.2 | Ajouter mentions geographiques dans le contenu | Faible | Eleve | index.html |
| 3.3 | Mettre a jour meta tags (title, description, OG) | Faible | Eleve | index.html |
| 3.4 | Mettre a jour llms.txt | Tres faible | Moyen | llms.txt |
| 3.5 | Ajouter une FAQ locale | Faible | Moyen-Eleve | index.html |
| 3.6 | Creer Google Business Profile | Moyen | Tres eleve | externe |
| 3.7 | Page locale dediee (optionnel) | Eleve | Tres eleve | nouveau fichier |

**Priorite suggeree** : 3.1 + 3.2 + 3.3 + 3.4 d'abord (effort faible, impact immediat), puis 3.5 et 3.6.
