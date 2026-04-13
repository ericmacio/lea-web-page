# Revue de Code — index.html Landing Page CRO

> Ce document recense les optimisations et améliorations potentielles de la page `index.html`.
> Les points sont classés par sévérité : Critique, Important, Modéré.
> **Aucune modification n'a été appliquée.**
>
> **Note Epic 12 :** Chaque recommandation a été vérifiée pour garantir la compatibilité avec l'Epic 12 (responsive, cross-browser, cross-device). Les points nécessitant des précautions particulières sont signalés par un encadré "Attention Epic 12".

---

## Points Critiques

### 1. Formulaire sans `action` — les données ne sont jamais envoyées
**Ligne ~1891**

Le `<form>` n'a ni attribut `action` ni `method`. À la soumission, le navigateur effectue un GET vers la page courante, ce qui rafraîchit la page sans envoyer les données.

**Recommandation :** Ajouter un service tiers (Formspree, Netlify Forms, etc.) :
```html
<form class="contact__form" action="https://formspree.io/f/VOTRE_CLE" method="POST">
```

---

### 2. Menu mobile accessible au clavier sur desktop — piège d'accessibilité
**Lignes 281–346 (CSS) / 1661–1675 (HTML)**

L'overlay mobile utilise `visibility: hidden` / `opacity: 0` mais n'est pas retiré de l'arbre d'accessibilité. Sur desktop, les utilisateurs au clavier peuvent naviguer (Tab) dans les liens cachés du menu mobile.

**Recommandation :** Ajouter `aria-hidden="true"` sur `.mobile-nav-overlay`. Étant donné que la page utilise déjà du JS inline (`onclick`) pour fermer le menu, on peut aussi toggler `aria-hidden` via le même mécanisme.

**Attention Epic 12 :** Ne **pas** utiliser `tabindex="-1"` sur les liens car cela peut interférer avec les événements tactiles sur certains navigateurs mobiles Android (Chrome < 90). Privilégier la solution `aria-hidden` + CSS `pointer-events: none` quand le menu est fermé.

---

## Points Importants

### 3. Labels de formulaire non associés aux champs — accessibilité WCAG
**Lignes 1893–1916**

Aucun `<label>` n'a d'attribut `for` et aucun `<input>` n'a d'attribut `id`. Les lecteurs d'écran ne peuvent pas associer les labels à leurs champs. Cliquer sur un label ne focus pas le champ. Non-conformité WCAG 2.1 Niveau A (critères 1.3.1 et 4.1.2).

**Recommandation :** Ajouter des paires `for`/`id` :
```html
<label class="contact__field-label" for="nom">Prénom / Nom<span>*</span></label>
<input id="nom" type="text" class="contact__input" placeholder="Marie Dupont" required>
```

---

### 4. `outline: none` sur les champs sans remplacement suffisant
**Ligne 1378**

Le `outline` est supprimé sur les champs de formulaire au focus. Le changement de `border-color` (1px, passage de `#d0d0ca` à cyan) est trop subtil pour satisfaire WCAG 2.1 SC 2.4.7 (Focus Visible).

**Recommandation :** Utiliser `outline` sur `:focus-visible` avec fallback `:focus` pour les navigateurs plus anciens :
```css
/* Fallback pour Safari < 15.4, anciens navigateurs */
.contact__input:focus,
.contact__select:focus,
.contact__textarea:focus {
  outline: 2px solid var(--cyan);
  outline-offset: 2px;
}

/* Navigateurs modernes : outline uniquement au clavier */
.contact__input:focus:not(:focus-visible),
.contact__select:focus:not(:focus-visible),
.contact__textarea:focus:not(:focus-visible) {
  outline: none;
}
```

**Attention Epic 12 :** `:focus-visible` seul n'est pas supporté par Safari < 15.4 (iOS 15.3 et antérieur). Le pattern ci-dessus avec double déclaration assure une compatibilité maximale tout en améliorant l'expérience sur les navigateurs modernes.

---

### 5. Pas de balises Open Graph / Twitter Card — mauvais rendu au partage
**Section `<head>`**

Aucune balise Open Graph (`og:title`, `og:description`, `og:image`) ni Twitter Card. Le partage sur LinkedIn, WhatsApp, Slack ou X affichera un aperçu sans image et avec un titre générique. Pour une page d'acquisition client, c'est pénalisant.

**Recommandation :**
```html
<meta property="og:title" content="Léa Macioszczyk — Freelance CRO">
<meta property="og:description" content="J'aide les e-commerces et les sites vitrines à transformer leur trafic en résultats mesurables.">
<meta property="og:image" content="https://leamacio.com/lea.png">
<meta property="og:type" content="website">
<meta property="og:url" content="https://leamacio.com/">
<meta name="twitter:card" content="summary_large_image">
```

---

### 6. Pas de balise `<link rel="canonical">`
**Section `<head>`**

Sans URL canonique, les moteurs de recherche peuvent indexer plusieurs versions de la page (avec/sans slash final, www/non-www, http/https), diluant le référencement.

**Recommandation :**
```html
<link rel="canonical" href="https://leamacio.com/">
```

---

### 7. Pas de favicon
**Section `<head>`**

Aucun `<link rel="icon">`. Le navigateur tente de charger `/favicon.ico` et génère une erreur 404. Impact sur l'onglet navigateur et les favoris.

**Recommandation :**
```html
<link rel="icon" href="/favicon.ico" sizes="any">
<link rel="icon" href="/favicon.svg" type="image/svg+xml">
```

---

### 8. Image de profil sans dimensions ni optimisation — impact LCP et CLS
**Ligne 1738**

```html
<img src="docs/lea.png" alt="..." class="a-propos__photo">
```

- Pas d'attributs `width`/`height` → décalage de mise en page (CLS) pendant le chargement
- Format PNG probablement non optimal → un WebP serait plus léger
- Pas de `loading="lazy"` (l'image est sous le pli)

**Recommandation :**
```html
<img src="docs/lea.png" alt="Léa Macioszczyk — Consultante CRO"
     class="a-propos__photo" width="280" height="280" loading="lazy">
```

**Attention Epic 12 :** Les attributs `width`/`height` sur l'image n'interfèrent pas avec le CSS responsive car `.a-propos__photo` a déjà un `width`/`height` CSS qui prend le dessus. L'attribut `loading="lazy"` est supporté par tous les navigateurs modernes (Chrome 77+, Firefox 75+, Safari 15.4+, Edge 79+). Pour Safari < 15.4, l'image se charge normalement (pas de régression).

---

### 9. Styles inline (`style="..."`) multiples — maintenabilité réduite
**Lignes 1684, 1702, 1703, 1705, 1741, 1744, 1758, 1799, 1800**

8+ occurrences de `style="color: var(--cyan)"`, `style="color: #fff"`, `style="font-style: normal"`. Ces styles :
- Contournent le système de variables CSS
- Ne peuvent pas être mis à jour centralement
- Certains utilisent des valeurs brutes (`#fff`) au lieu des variables (`var(--blanc)`)

**Recommandation :** Créer des classes utilitaires :
```css
.text-cyan { color: var(--cyan); }
.text-white { color: var(--blanc); }
.font-normal { font-style: normal; }
```

---

### 10. Icônes SVG décoratives sans `aria-hidden="true"`
**Lignes 1646, 1670, 1687, 1709, 1716, 1723, 1817, 1834, etc.**

Toutes les icônes SVG inline (boutons, cartes) n'ont pas `aria-hidden="true"`. Les lecteurs d'écran tentent de lire le contenu SVG (paths), ce qui crée une expérience confuse.

**Recommandation :** Ajouter `aria-hidden="true"` sur chaque SVG décoratif :
```html
<svg aria-hidden="true" xmlns="...">...</svg>
```

---

## Points Modérés

### 11. Règles CSS responsive dupliquées
**Lignes 893–1067 vs. 1255–1264, 1413–1448, 1569–1597**

Les media queries pour `.cta-banner`, `.contact`, `.faq` et `.footer` sont déclarées deux fois : une première fois dans le bloc responsive principal (qui précède les définitions CSS et ne s'applique pas correctement), et une seconde fois après les définitions (qui fonctionne). Les premières déclarations sont donc du code mort.

**Recommandation :** Supprimer les règles responsive du bloc principal (lignes 893–1067) pour les sections dont les media queries sont déjà dupliquées après leurs définitions. Réorganiser le CSS pour que chaque section ait ses media queries immédiatement après ses styles de base.

---

### 12. Caractère Unicode `➜` — risque de rendu inconsistant
**Ligne 1331**

```css
content: '➜';
```

Le caractère U+279C peut s'afficher différemment ou pas du tout sur certains appareils Android ou Windows anciens. Un SVG ou une flèche simple (`→`) serait plus fiable.

**Recommandation :** Utiliser `→` (U+2192) ou un SVG inline en pseudo-élément.

**Attention Epic 12 :** Ce point est directement lié à la compatibilité cross-device. Le caractère `➜` (Dingbats) dépend des polices système installées. Sur Android stock (sans Google Noto Color Emoji), Windows 7/8, et certains Linux légers, il peut apparaître comme un rectangle vide. Le remplacement par `→` garantit un rendu universel.

---

### 13. Section Contact contourne le pattern `.container`
**Lignes 1279–1286**

Toutes les sections utilisent `<div class="container">` sauf Contact qui applique `max-width`, `margin`, `padding` directement sur le `<section>`. Cela crée un pattern inconsistant nécessitant un wrapper supplémentaire (`div.contact-wrapper`) et des overrides responsive dupliqués.

**Recommandation :** Refactorer pour utiliser le pattern `.container` standard.

---

### 14. Transition hover `opacity: 1 → 1` sur la navigation desktop — code inutile
**Lignes 221–244**

```css
.header__nav a { opacity: 1; }
.header__nav a:hover { opacity: 1; }
```

Les deux états ont la même opacité. La transition ne produit aucun effet visible. Seul le soulignement cyan fonctionne.

**Recommandation :** Supprimer les déclarations d'opacité inutiles ou implémenter un vrai effet (ex: `opacity: 0.7` par défaut, `1` au hover).

---

## Résumé

| # | Sévérité | Issue | Impact |
|---|----------|-------|--------|
| 1 | Critique | Formulaire sans `action` | Fonctionnel |
| 2 | Critique | Menu mobile accessible au clavier sur desktop | Accessibilité |
| 3 | Important | Labels formulaire non associés | Accessibilité |
| 4 | Important | `outline: none` sans remplacement | Accessibilité |
| 5 | Important | Pas de balises Open Graph | SEO / Marketing |
| 6 | Important | Pas de `canonical` | SEO |
| 7 | Important | Pas de favicon | UX |
| 8 | Important | Image sans dimensions | Performance (CLS) |
| 9 | Important | Styles inline multiples | Maintenabilité |
| 10 | Important | SVG sans `aria-hidden` | Accessibilité |
| 11 | Modéré | CSS responsive dupliqué | Maintenabilité |
| 12 | Modéré | Caractère Unicode `➜` | Compatibilité |
| 13 | Modéré | Contact hors pattern `.container` | Cohérence |
| 14 | Modéré | Hover opacity no-op | Code mort |

---

## Compatibilité Epic 12 — Résumé des précautions

| # | Recommandation | Risque Epic 12 | Précaution |
|---|---------------|----------------|------------|
| 2 | aria-hidden sur menu mobile | Moyen | Ne pas utiliser `tabindex="-1"` (problèmes tactiles Android) |
| 4 | `:focus-visible` | Moyen | Fallback `:focus` obligatoire pour Safari < 15.4 |
| 8 | `loading="lazy"` sur image | Faible | Dégradation gracieuse sur Safari < 15.4 |
| 12 | Remplacement `➜` | **Directement lié** | `→` a un support Unicode universel |
| Autres | — | Aucun | Compatible tous navigateurs/devices |

---

## Prochaines étapes suggérées

1. **Priorité 1 :** Corriger les points critiques (formulaire, accessibilité menu) — attention aux précautions Epic 12
2. **Priorité 2 :** Corriger les points importants d'accessibilité (labels, outline avec fallback, aria-hidden SVG)
3. **Priorité 3 :** Ajouter les balises SEO/OG et le favicon
4. **Priorité 4 :** Refactorer les styles inline et le CSS dupliqué
5. **Priorité 5 :** Remplacer le caractère `➜` par `→` (compatibilité cross-device)
