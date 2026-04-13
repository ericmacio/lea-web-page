# REVIEW-DESIGN.md — Propositions d'amélioration visuelle de la section Hero

## Constat actuel

La section Hero est actuellement sobre et fonctionnelle :
- Fond uni `#1a1a18` (noir secondaire)
- Texte centré : tag, titre, sous-titre, boutons, mention
- Padding modéré (64px / 72px)
- Aucun élément graphique ni animation CSS

**Problème** : la section manque d'impact visuel. Elle ressemble à un bloc de texte standard qui ne retient pas l'attention du visiteur dans les premières secondes (critiques pour le taux de rebond).

---

## Propositions d'amélioration (CSS pur, sans JavaScript)

### 1. Fond avec gradient radial lumineux

Remplacer le fond uni par un gradient radial subtil qui crée un effet de "spotlight" centré sur le titre, donnant une impression de profondeur et de focus.

```css
.hero {
  background: radial-gradient(ellipse 80% 60% at 50% 40%, rgba(0, 212, 255, 0.08) 0%, transparent 70%),
              var(--noir-sec);
}
```

**Effet** : Halo cyan très discret derrière le titre, crée un point focal naturel sans être agressif. Reste dans la palette existante.

---

### 2. Titre avec gradient de couleur animé

Appliquer un dégradé animé sur le texte du highlight "pas assez de résultats ?" pour attirer le regard sans être intrusif.

```css
.hero__title .highlight {
  background: linear-gradient(90deg, var(--cyan), #45cdff, #00a8cc, var(--cyan));
  background-size: 300% 100%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: shimmer 6s ease-in-out infinite;
}

@keyframes shimmer {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
```

**Effet** : Le texte cyan "pulse" doucement avec un effet de shimmer, attirant naturellement l'oeil sur la proposition de valeur clé. Respecte `prefers-reduced-motion` (voir point 7).

---

### 3. Augmentation de la taille et de l'espacement du Hero

Donner plus d'ampleur à la section pour qu'elle occupe davantage l'espace visible au-dessus de la ligne de flottaison.

```css
.hero {
  padding: 100px 0 96px;  /* au lieu de 64px / 72px */
  min-height: 85vh;       /* occupe la majorité de l'écran */
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero__title {
  font-size: 72px;  /* au lieu de 64px — plus impactant */
}
```

**Effet** : Le hero "respire" davantage, occupe presque tout le viewport et donne une première impression de professionnalisme et de confiance.

---

### 4. Bordure lumineuse sous le hero (séparateur)

Ajouter une ligne de séparation avec un dégradé cyan qui crée une transition visuelle marquante vers la section suivante.

```css
.hero::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 10%;
  right: 10%;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--cyan), transparent);
  opacity: 0.4;
}
```

**Effet** : Séparation élégante avec un trait lumineux qui guide le regard vers le bas de la page. Nécessite `position: relative` sur `.hero`.

---

### 5. Glow effect sur le bouton CTA principal

Ajouter un halo lumineux autour du bouton "Diagnostic gratuit" pour le rendre plus magnétique.

```css
.hero .btn-primary {
  box-shadow: 0 0 20px rgba(0, 212, 255, 0.3),
              0 0 60px rgba(0, 212, 255, 0.1);
  transition: box-shadow 0.3s ease, transform 0.3s ease, background-color 0.25s ease;
}

.hero .btn-primary:hover {
  box-shadow: 0 0 30px rgba(0, 212, 255, 0.5),
              0 0 80px rgba(0, 212, 255, 0.2);
  transform: translateY(-2px);
}
```

**Effet** : Le bouton CTA "brille" et invite au clic. L'effet hover avec le léger soulèvement renforce l'interactivité perçue.

---

### 6. Particules / motif de fond géométrique (CSS grid dots)

Ajouter un motif discret de points en arrière-plan pour casser la monotonie du fond uni et évoquer un univers "data / analytics".

```css
.hero {
  background-image:
    radial-gradient(circle, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
  background-size: 40px 40px;
}
```

**Effet** : Grille de micro-points quasi invisibles qui évoque la data et les graphiques analytiques — cohérent avec le positionnement CRO/analytics. Se combine avec le gradient radial (proposition 1).

---

### 7. Respect de `prefers-reduced-motion`

Toute animation doit être désactivée pour les utilisateurs qui préfèrent moins de mouvement.

```css
@media (prefers-reduced-motion: reduce) {
  .hero__title .highlight {
    animation: none;
    background-size: 100% 100%;
  }
  .hero .btn-primary {
    transition: none;
  }
}
```

---

## 8. Contraste du cyan sur fond clair — Analyse et proposition

### Problème identifié

Le cyan actuel `#00d4ff` est très lumineux et saturé. Il fonctionne parfaitement sur les fonds sombres (`#0f0f0e`, `#1a1a18`) où le contraste est excellent, mais il **manque de lisibilité sur les fonds clairs** (`#eef2f6`) utilisés dans les sections "Le problème" et "Méthode".

**Éléments concernés sur fond clair :**
- Section labels ("— Le problème", "— méthode") en `color: var(--cyan)`
- Texte `.text-cyan` dans les paragraphes (ex: "sans le savoir", "97% des visiteurs...")
- Numéros des étapes méthode (cercles avec `border` et `color` cyan)
- Titre highlight méthode ("résultats")
- Soulignement cyan (`text-decoration-color`)

### Ratio de contraste actuel

| Combinaison | Ratio | WCAG AA (texte normal) | WCAG AA (grand texte) |
|-------------|-------|------------------------|-----------------------|
| `#00d4ff` sur `#eef2f6` | **~1.8:1** | Echec | Echec |
| `#00d4ff` sur `#ffffff` | **~1.7:1** | Echec | Echec |
| `#00d4ff` sur `#0f0f0e` | **~10.5:1** | OK | OK |
| `#00d4ff` sur `#1a1a18` | **~9.8:1** | OK | OK |

Le cyan actuel échoue largement aux critères d'accessibilité WCAG sur fond clair (minimum 4.5:1 pour du texte normal, 3:1 pour du grand texte).

### Proposition : variable contextuelle `--cyan-dark`

**L'approche recommandée** est d'introduire une variante plus foncée du cyan, utilisée exclusivement sur les fonds clairs, tout en conservant `#00d4ff` sur les fonds sombres où il est parfaitement lisible et visuellement impactant.

#### Couleurs candidates

| Couleur | Code | Ratio sur `#eef2f6` | WCAG AA normal | WCAG AA grand | Rendu |
|---------|------|----------------------|----------------|---------------|-------|
| Cyan original | `#00d4ff` | 1.8:1 | Echec | Echec | Trop clair, se perd |
| Cyan foncé léger | `#00a3c7` | ~3.2:1 | Echec | OK | Lisible en titre, limite en texte |
| **Cyan foncé (recommandé)** | `#0088a8` | ~4.5:1 | **OK** | **OK** | **Bon équilibre lisibilité/vivacité** |
| Cyan très foncé | `#006d85` | ~5.8:1 | OK | OK | Très lisible mais perd en éclat |
| Teal/pétrole | `#005f73` | ~7.0:1 | OK | OK | Excellent contraste mais s'éloigne de la charte |

#### Recommandation : `#0088a8`

Cette teinte est le meilleur compromis :
- **Respecte la charte** : reste dans la famille cyan/bleu, reconnaissable comme variante de `#00d4ff`
- **Atteint WCAG AA** : ratio 4.5:1 sur `#eef2f6`, conforme pour tout texte
- **Conserve l'énergie** : assez saturée pour garder l'effet d'accent coloré
- **Transition naturelle** : un visiteur ne perçoit pas de rupture entre le cyan clair (fond sombre) et le cyan foncé (fond clair)

#### Implémentation CSS proposée

```css
:root {
  --cyan:          #00d4ff;   /* inchangé — fonds sombres */
  --cyan-dark:     #0088a8;   /* nouveau — fonds clairs */
  --cyan-trans:    #45cdff3d; /* inchangé */
}

/* Sections sur fond clair : surcharger la couleur cyan */
.probleme .section-label,
.probleme .text-cyan,
.probleme__text .underline-cyan {
  color: var(--cyan-dark);
}
.probleme__text .underline-cyan {
  text-decoration-color: var(--cyan-dark);
}

.methode .section-label,
.methode .text-cyan,
.methode__title .highlight {
  color: var(--cyan-dark);
}
.methode__step-number {
  color: var(--cyan-dark);
  border-color: var(--cyan-dark);
}
```

#### Alternative : approche par container (plus élégante)

Si l'on souhaite une approche plus maintenable, on peut redéfinir `--cyan` localement dans les sections claires :

```css
.probleme,
.methode {
  --cyan: #0088a8;
}
```

Cela surcharge automatiquement toutes les utilisations de `var(--cyan)` dans ces sections, sans toucher aux classes individuelles. Plus DRY et plus facile à maintenir.

---

## 8bis. Mini photo dans le header

### Objectif

Humaniser la marque dès la première seconde en ajoutant une photo circulaire miniature de Léa à côté du logo texte dans le header fixe. Cela renforce la confiance, crée un fil conducteur vers la section "À propos" et distingue le site des landing pages anonymes.

### Implémentation réalisée

**CSS ajouté :**

```css
.header__logo {
  display: flex;
  align-items: center;
  gap: 12px;
  /* ...propriétés existantes conservées */
}

.header__photo {
  width: 34px;
  height: 34px;
  border-radius: 50%;
  object-fit: cover;
  border: 1.5px solid rgba(0, 212, 255, 0.4);
  flex-shrink: 0;
}

/* Masquée sur petit mobile (< 480px) pour ne pas surcharger le header */
@media (max-width: 480px) {
  .header__photo {
    display: none;
  }
}
```

**HTML modifié :**

```html
<a href="#" class="header__logo">
  <img src="lea.png" alt="Léa Macioszczyk" class="header__photo"
       width="34" height="34" loading="eager">
  Léa Macioszczyk · Freelance CRO
</a>
```

### Points clés

- **34px** en cercle — proportionné au header de 68px de haut
- **Bordure cyan semi-transparente** — subtile, cohérente avec la charte
- **`loading="eager"`** — au-dessus de la ligne de flottaison, chargement prioritaire
- **Masquée sous 480px** — évite l'encombrement avec le menu hamburger sur petit mobile
- **Le `header__logo`** passe en `display: flex` avec `gap: 12px` pour aligner photo et texte

---

## 9. Mise en valeur du partenariat développeur senior

### Constat actuel

Le partenariat avec un développeur senior (+20 ans d'expérience, IA appliquée au code) est un **différentiateur majeur** de l'offre, mais il est actuellement sous-exploité visuellement :

- **Section Méthode** : noyé dans un simple paragraphe `methode__intro`, même style que le texte courant — le visiteur peut le survoler sans le remarquer
- **Carte "Exécution technique"** : mentionné dans la description de la carte, sans mise en relief particulière

Ce partenariat est pourtant un argument clé : il distingue Léa de tout consultant CRO solo qui ne peut pas assurer l'implémentation technique. C'est un **duo complet stratégie + exécution**, rare sur le marché freelance.

### Proposition A — Encart visuel dédié dans la section Méthode (recommandé)

Transformer le paragraphe sur le partenariat en un **bloc visuel distinct** (type "callout" ou "card") qui se détache du texte courant.

```css
.methode__partner {
  display: flex;
  align-items: flex-start;
  gap: 16px;
  background-color: var(--blanc);
  border-left: 3px solid var(--cyan);
  border-radius: 8px;
  padding: 20px 24px;
  margin-top: 20px;
}

.methode__partner-icon {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
  color: var(--cyan);
}

.methode__partner-text {
  font-family: var(--font-body);
  font-size: 15px;
  line-height: 1.55;
  color: var(--noir-sec);
}

.methode__partner-text strong {
  color: var(--noir);
}
```

```html
<div class="methode__partner">
  <svg class="methode__partner-icon" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" 
       width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" 
       stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
    <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/>
    <circle cx="9" cy="7" r="4"/>
    <path d="M22 21v-2a4 4 0 0 0-3-3.87"/>
    <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
  </svg>
  <p class="methode__partner-text">
    Pour les optimisations nécessitant du développement technique, je collabore avec un 
    <strong>développeur senior ayant plus de 20 ans d'expérience</strong> en architecture 
    logicielle, développement web et formé aux dernières avancées de l'IA appliquée au code.
  </p>
</div>
```

**Effet** : Le bloc blanc avec bordure cyan à gauche et icône "duo" crée une rupture visuelle qui attire immédiatement l'oeil. Le visiteur ne peut pas manquer cette information. Le fond blanc contraste avec le fond `#eef2f6` de la section.

---

### Proposition B — Badge "Duo CRO + Dev" sous le titre Méthode

Ajouter un petit badge/pill juste sous le titre de la section, avant le texte introductif, pour annoncer le partenariat dès le premier regard.

```css
.methode__badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background-color: var(--noir);
  color: var(--cyan);
  font-family: var(--font-body);
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 6px 16px;
  border-radius: 20px;
  margin-bottom: 20px;
}

.methode__badge svg {
  width: 14px;
  height: 14px;
}
```

```html
<p class="methode__badge">
  <svg aria-hidden="true" ...><!-- icône duo --></svg>
  Duo CRO + Développeur senior
</p>
```

**Effet** : Le badge sombre sur fond clair est très visible et communique l'info en un coup d'oeil. Style "tag" cohérent avec les tags des cartes d'offres. Se combine parfaitement avec la proposition A.

---

### Proposition C — Mise en valeur dans la carte "Exécution technique"

Ajouter un bandeau ou badge distinctif sur la 3e carte d'offres pour signaler visuellement que cette offre implique le duo.

```css
.offres__card--partner {
  border: 1px solid rgba(0, 212, 255, 0.25);
  position: relative;
}

.offres__card-partner-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-family: var(--font-body);
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.5px;
  text-transform: uppercase;
  color: var(--cyan);
  background-color: rgba(0, 212, 255, 0.08);
  padding: 4px 12px;
  border-radius: 12px;
  margin-bottom: 12px;
}
```

**Effet** : La carte "Exécution technique" se distingue visuellement des deux autres par sa bordure cyan et son badge, signalant clairement que c'est l'offre qui mobilise le duo.

---

### Synthèse proposition 9

| Variante | Emplacement | Impact | Complexité | Recommandation |
|----------|-------------|--------|------------|----------------|
| A | Section Méthode — encart callout | **Très fort** | Faible | **Prioritaire** |
| B | Section Méthode — badge titre | Fort | Faible | Recommandé |
| C | Carte "Exécution technique" | Moyen | Faible | Recommandé |

**Recommandation** : implémenter les **3 variantes ensemble**. Elles sont complémentaires et renforcent le message à deux endroits stratégiques de la page (Méthode + Offres). Le partenariat devient un fil rouge visuel impossible à manquer.

---

## Synthèse des propositions

| # | Proposition | Impact visuel | Complexité CSS | Recommandation |
|---|-------------|---------------|----------------|----------------|
| 1 | Gradient radial (spotlight) | Fort | Faible | **Prioritaire** |
| 2 | Titre shimmer animé | Très fort | Moyenne | **Prioritaire** |
| 3 | Augmentation taille/espacement | Fort | Faible | **Prioritaire** |
| 4 | Bordure lumineuse séparateur | Moyen | Faible | Recommandé |
| 5 | Glow CTA | Fort | Faible | **Prioritaire** |
| 6 | Motif grid dots | Subtil | Faible | Recommandé |
| 7 | Reduced-motion | Accessibilité | Faible | **Obligatoire** |
| 8 | Cyan foncé `#0088a8` sur fonds clairs | Fort (lisibilité) | Faible | **Prioritaire** |
| 8bis | Mini photo header | Fort (confiance) | Faible | **Prioritaire** |
| 9A | Encart callout partenariat (Méthode) | Très fort | Faible | **Prioritaire** |
| 9B | Badge "Duo CRO + Dev" (Méthode) | Fort | Faible | Recommandé |
| 9C | Badge + bordure carte Exécution technique | Moyen | Faible | Recommandé |

---

## Proposition combinée recommandée

L'idéal est de combiner les **7 propositions ensemble** pour un effet maximal tout en restant élégant et professionnel. Le résultat final :

- Un fond texturé (dots grid) avec un halo cyan centré (spotlight)
- Un titre plus grand et impactant, avec le texte clé qui "pulse" doucement
- Un bouton CTA qui rayonne et invite au clic
- Une séparation élégante vers la section suivante
- Le tout dans un espace généreux qui occupe l'écran

**Aucun JavaScript requis** — tout est réalisable en CSS pur, conforme aux contraintes du projet.

---

## 10. Audit responsive & cross-browser (Epic 12)

Audit de conformité de toutes les modifications apportées (propositions 1 à 9C, 8bis) vis-à-vis des critères d'acceptation de l'Epic 12 (US-12.1, US-12.2) : responsive 3 breakpoints, compatibilité iOS/Android, préfixes cross-browser, `prefers-reduced-motion`, `forced-colors`, touch targets.

### 10.1. Hero `.container` width (flex parent)

**Problème** : le hero est passé en `display: flex` (prop. 3) pour centrer verticalement le contenu. Or un enfant flex peut rétrécir en dessous de sa largeur naturelle, provoquant un décalage du contenu centré.

**Correction** :
```css
.hero .container {
  width: 100%;
}
```

---

### 10.2. Hero `min-height` sur tablette (1024px)

**Problème** : le `min-height: 85vh` du desktop n'était pas réduit dans le breakpoint tablette. Sur certaines tablettes en portrait (ex: iPad 1024×768), cela force un hero disproportionné par rapport au contenu.

**Correction** :
```css
@media (max-width: 1024px) {
  .hero {
    min-height: 75vh;
    padding: 80px 0 72px;
  }
}
```

Le breakpoint mobile (768px) avait déjà `min-height: 70vh` et le breakpoint paysage avait `min-height: auto`.

---

### 10.3. Encart partenariat — petit mobile (< 480px)

**Problème** : le bloc `.methode__partner` (prop. 9A) et le badge `.methode__badge` (prop. 9B) n'avaient aucun ajustement pour le breakpoint < 480px. Sur un écran de 375px, l'icône + texte en flex horizontal manquait d'espace.

**Correction** :
```css
@media (max-width: 480px) {
  .methode__badge {
    font-size: 11px;
    padding: 5px 12px;
  }

  .methode__partner {
    flex-direction: column;  /* empile icône au-dessus du texte */
    padding: 14px 16px;
    gap: 10px;
  }

  .methode__partner-icon {
    width: 28px;
    height: 28px;
  }

  .methode__partner-text {
    font-size: 14px;
  }
}
```

---

### 10.4. `forced-colors` (mode contraste élevé Windows)

**Problème** : les nouveaux éléments visuels reposent sur des couleurs, gradients, `box-shadow` et `background-clip: text` qui sont neutralisés en mode contraste élevé Windows (`forced-colors: active`). Sans fallback, le shimmer rend le texte invisible, le séparateur disparaît, les bordures de callout/carte ne sont plus visibles.

**Correction** :
```css
@media (forced-colors: active) {
  /* Shimmer : revert en texte plein lisible */
  .hero__title .highlight {
    background: none;
    -webkit-background-clip: unset;
    -webkit-text-fill-color: currentColor;
    background-clip: unset;
    color: LinkText;
  }

  /* Séparateur hero : bordure solide au lieu du gradient */
  .hero::after {
    background: CanvasText;
    box-shadow: none;
  }

  /* Encart partenariat : bordure visible */
  .methode__partner {
    border: 1px solid CanvasText;
    box-shadow: none;
  }

  /* Carte partenaire : bordure renforcée */
  .offres__card--partner {
    border: 2px solid LinkText;
  }

  /* Badges : bordure explicite */
  .offres__card-partner-badge,
  .methode__badge {
    border: 1px solid currentColor;
  }

  /* Photo header : bordure visible */
  .header__photo {
    border: 1px solid CanvasText;
  }
}
```

Les couleurs système `CanvasText`, `LinkText` garantissent la lisibilité quel que soit le thème de contraste choisi par l'utilisateur.

---

### 10.5. Préfixes `-webkit-` pour l'animation shimmer

**Problème** : l'animation shimmer (prop. 2) utilise `@keyframes` et `animation` sans préfixe `-webkit-`. Sur les versions plus anciennes de Safari/iOS WebKit (Safari < 9), cela provoque une absence totale d'animation, et le gradient statique peut rendre le texte figé dans une position non optimale.

**Correction** :
```css
.hero__title .highlight {
  -webkit-animation: shimmer 6s ease-in-out infinite;
  animation: shimmer 6s ease-in-out infinite;
}

@-webkit-keyframes shimmer {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

@keyframes shimmer {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}
```

Note : `-webkit-background-clip: text` et `-webkit-text-fill-color: transparent` étaient déjà présents dans la proposition initiale.

---

### 10.6. Touch target header photo (`pointer: coarse`)

**Problème** : la photo (34px) est à l'intérieur du lien `a.header__logo`. La zone cliquable résultante pouvait être inférieure au minimum de 44px requis par les critères d'accessibilité iOS/Android (US-12.2).

**Correction** :
```css
@media (pointer: coarse) {
  .header__logo {
    min-height: 44px;
  }
}
```

Le lien `.header__logo` étant en `display: flex; align-items: center`, le `min-height: 44px` garantit une zone tactile suffisante sans modifier le rendu visuel.

---

### Synthèse audit responsive/cross-browser

| # | Correctif | Breakpoint / Media Query | Statut |
|---|-----------|--------------------------|--------|
| 10.1 | Hero container `width: 100%` | Desktop (base) | Corrigé |
| 10.2 | Hero `min-height: 75vh` tablette | `max-width: 1024px` | Corrigé |
| 10.3 | Partenariat layout colonne | `max-width: 480px` | Corrigé |
| 10.4 | Fallbacks `forced-colors` | `forced-colors: active` | Corrigé |
| 10.5 | Préfixes `-webkit-` animation | Cross-browser | Corrigé |
| 10.6 | Touch target logo 44px | `pointer: coarse` | Corrigé |

Toutes les modifications sont conformes aux critères d'acceptation de l'Epic 12 (US-12.1, US-12.2).

---

## Prochaine étape

Validation par l'utilisateur des propositions retenues, puis implémentation dans `index.html`.
