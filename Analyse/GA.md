# Intégration Google Analytics 4 (GA4) — Analyse des changements

> Ce document décrit les modifications nécessaires pour intégrer Google Analytics 4 sur la page `index.html`.

---

## Prérequis

### Création d'un compte Google Analytics 4
1. Se rendre sur [analytics.google.com](https://analytics.google.com)
2. Créer un **compte** (ex : "Léa Macioszczyk — CRO")
3. Créer une **propriété** (ex : "leamacio.com")
4. Configurer un **flux de données Web** avec l'URL `https://leamacio.com`
5. Récupérer l'**ID de mesure** au format `G-TG5JL24KRW`

> **Important :** L'ID de mesure est propre à chaque propriété. Le placeholder `G-TG5JL24KRW` utilisé dans ce document doit être remplacé par l'ID réel obtenu à l'étape 5.

---

## Modification 1 — Insertion du tag Google Analytics (gtag.js)

### Fichier impacté
`index.html` — section `<head>`, lignes 3–34

### Changement
Ajouter le snippet Google Analytics **immédiatement après** la balise `<meta charset="UTF-8">` (ligne 4), avant les autres balises meta. Ce positionnement en tête du `<head>` garantit que le script de tracking se charge le plus tôt possible.

### Code à insérer
```html
<!-- Google Analytics 4 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-TG5JL24KRW"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-TG5JL24KRW');
</script>
```

### Détails techniques
- Le script est chargé en mode `async` : il ne bloque pas le rendu de la page
- `dataLayer` est un tableau global utilisé par Google Tag Manager / gtag.js pour stocker les événements
- `gtag('config', 'G-TG5JL24KRW')` enregistre automatiquement un événement `page_view` à chaque chargement de page
- **Impact performance** : le script ajoute ~28 Ko (compressé) au chargement initial. L'attribut `async` limite l'impact sur le First Contentful Paint (FCP)

---

## Modification 2 — Bannière de consentement aux cookies (RGPD)

### Contexte réglementaire
Google Analytics dépose des cookies de mesure d'audience (`_ga`, `_ga_*`) sur le navigateur de l'utilisateur. Le **RGPD** (applicable en France et dans l'UE) et la **directive ePrivacy** imposent de :
- Informer l'utilisateur de l'utilisation de cookies
- Recueillir son **consentement explicite avant** le dépôt de cookies non essentiels
- Permettre le **refus** sans dégradation de l'expérience

La CNIL précise que les cookies de mesure d'audience peuvent être exemptés de consentement **uniquement** si la finalité est strictement limitée à la mesure d'audience anonyme. GA4 dans sa configuration par défaut ne remplit pas cette condition (données envoyées aux serveurs Google, possibilité de recoupement).

### Fichier impacté
`index.html` — section `<head>` (script) + fin du `<body>` (HTML bannière) + section `<style>` (CSS)

### Approche recommandée : Google Consent Mode v2

#### a) Modifier le snippet gtag.js pour intégrer le Consent Mode

Remplacer le snippet de la Modification 1 par :

```html
<!-- Google Analytics 4 avec Consent Mode v2 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-TG5JL24KRW"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}

  // Consent Mode v2 : refus par défaut (RGPD)
  gtag('consent', 'default', {
    'analytics_storage': 'denied',
    'ad_storage': 'denied',
    'ad_user_data': 'denied',
    'ad_personalization': 'denied',
    'wait_for_update': 500
  });

  gtag('js', new Date());
  gtag('config', 'G-TG5JL24KRW');
</script>
```

**Explication :** Avec `analytics_storage: 'denied'` par défaut, GA4 n'envoie que des pings anonymes (sans cookies) tant que l'utilisateur n'a pas donné son consentement. Les données collectées sans consentement ne contiennent pas d'identifiant utilisateur, mais GA4 utilise la modélisation pour estimer les métriques manquantes.

#### b) Ajouter une bannière de consentement (HTML)

Insérer avant la balise `</body>` :

```html
<!-- Bannière de consentement cookies -->
<div id="cookie-banner" class="cookie-banner" role="dialog" aria-label="Gestion des cookies">
  <div class="cookie-banner__content">
    <p class="cookie-banner__text">
      Ce site utilise des cookies de mesure d'audience (Google Analytics) pour
      améliorer votre expérience. Aucun cookie publicitaire n'est utilisé.
    </p>
    <div class="cookie-banner__actions">
      <button id="cookie-accept" class="btn btn-primary cookie-banner__btn" type="button">Accepter</button>
      <button id="cookie-refuse" class="btn btn-secondary cookie-banner__btn" type="button">Refuser</button>
    </div>
  </div>
</div>
```

#### c) Ajouter le CSS de la bannière

Ajouter dans la section `<style>` :

```css
/* ============================================
   COOKIE BANNER (RGPD)
   ============================================ */
.cookie-banner {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 10000;
  background: var(--noir-bg);
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding: 1rem 1.5rem;
  display: flex;
  justify-content: center;
}

.cookie-banner.hidden {
  display: none;
}

.cookie-banner__content {
  max-width: 900px;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.cookie-banner__text {
  color: var(--gris-texte);
  font-family: var(--font-body);
  font-size: 0.875rem;
  margin: 0;
  flex: 1;
  min-width: 280px;
}

.cookie-banner__actions {
  display: flex;
  gap: 0.75rem;
}

.cookie-banner__btn {
  font-size: 0.875rem;
  padding: 0.5rem 1.25rem;
}
```

#### d) Ajouter le script de gestion du consentement

Insérer avant `</body>`, après la bannière :

```html
<script>
  (function() {
    var COOKIE_KEY = 'ga_consent';

    function hideBanner() {
      document.getElementById('cookie-banner').classList.add('hidden');
    }

    function getConsent() {
      return localStorage.getItem(COOKIE_KEY);
    }

    function setConsent(value) {
      localStorage.setItem(COOKIE_KEY, value);
    }

    // Si le choix a déjà été fait, masquer la bannière et appliquer
    var saved = getConsent();
    if (saved === 'granted') {
      gtag('consent', 'update', { 'analytics_storage': 'granted' });
      hideBanner();
    } else if (saved === 'denied') {
      hideBanner();
    }

    // Bouton Accepter
    document.getElementById('cookie-accept').addEventListener('click', function() {
      setConsent('granted');
      gtag('consent', 'update', { 'analytics_storage': 'granted' });
      hideBanner();
    });

    // Bouton Refuser
    document.getElementById('cookie-refuse').addEventListener('click', function() {
      setConsent('denied');
      hideBanner();
    });
  })();
</script>
```

**Explication :** Le choix de l'utilisateur est stocké dans `localStorage` (pas un cookie supplémentaire). Lors des visites suivantes, la bannière ne s'affiche plus et le consentement est automatiquement réappliqué.

---

## Modification 3 (optionnelle) — Suivi des événements clés

### Contexte
GA4 enregistre automatiquement les pages vues, mais pour une landing page CRO, il est pertinent de suivre les **interactions de conversion** afin de mesurer l'efficacité de la page.

### Fichier impacté
`index.html` — ajout d'attributs `data-*` sur les éléments interactifs existants + script de tracking

### Événements recommandés

| Événement | Déclencheur | Éléments concernés |
|-----------|-------------|-------------------|
| `cta_click` | Clic sur un bouton CTA | Boutons "Réserver un appel", "Voir les offres", "Me contacter" (7 boutons CTA sur la page) |
| `form_submit` | Soumission du formulaire de contact | `<form class="contact__form">` (section Contact) |
| `section_view` | Scroll vers une section | Sections : hero, probleme, a-propos, methode, offres, contact, faq |
| `faq_toggle` | Ouverture d'une question FAQ | Éléments `<details>` dans la section FAQ |

### Code à insérer (avant `</body>`)

```html
<script>
  // Tracking des clics CTA
  document.querySelectorAll('.btn-primary, .btn-secondary, .btn-secondary-cyan').forEach(function(btn) {
    btn.addEventListener('click', function() {
      gtag('event', 'cta_click', {
        'event_category': 'engagement',
        'event_label': this.textContent.trim()
      });
    });
  });

  // Tracking soumission formulaire
  var form = document.querySelector('.contact__form');
  if (form) {
    form.addEventListener('submit', function() {
      gtag('event', 'form_submit', {
        'event_category': 'conversion',
        'event_label': 'contact'
      });
    });
  }

  // Tracking scroll vers les sections (Intersection Observer)
  if ('IntersectionObserver' in window) {
    var sections = document.querySelectorAll('section[id]');
    var observer = new IntersectionObserver(function(entries) {
      entries.forEach(function(entry) {
        if (entry.isIntersecting) {
          gtag('event', 'section_view', {
            'event_category': 'scroll',
            'event_label': entry.target.id
          });
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.3 });

    sections.forEach(function(section) { observer.observe(section); });
  }
</script>
```

### Note
Ce tracking ne nécessite pas de consentement supplémentaire : les événements sont envoyés via gtag.js, qui respecte déjà l'état du Consent Mode configuré en Modification 2. Si l'utilisateur a refusé les cookies, les événements sont quand même envoyés mais sans identifiant utilisateur (mode anonyme GA4).

---

## Résumé des modifications

| # | Modification | Fichier | Type de changement | Complexité |
|---|-------------|---------|-------------------|------------|
| 1 | Snippet gtag.js | `index.html` `<head>` | Ajout de 2 balises `<script>` | Faible |
| 2 | Bannière RGPD + Consent Mode | `index.html` `<head>` + `<body>` + `<style>` | Modification snippet + ajout HTML/CSS/JS | Moyenne |
| 3 | Tracking événements (optionnel) | `index.html` avant `</body>` | Ajout d'1 balise `<script>` | Faible |

### Impact global
- **Performance :** +28 Ko (gtag.js, chargé en async) — impact marginal
- **JavaScript :** La page actuelle est quasi sans JS. Ces ajouts introduisent du JavaScript mais restent légers et n'interfèrent pas avec le fonctionnement existant (checkbox hack du menu mobile, etc.)
- **Responsive / Epic 12 :** La bannière cookie utilise flexbox avec `flex-wrap` et `min-width`, compatible tous navigateurs modernes. Aucun impact sur le layout existant
- **RGPD :** Le Consent Mode v2 assure la conformité. Le consentement est refusé par défaut

### Action requise avant implémentation
- **Créer le compte GA4** et récupérer l'ID de mesure `G-TG5JL24KRW`
- **Décider** si la Modification 3 (tracking événements) doit être implémentée
