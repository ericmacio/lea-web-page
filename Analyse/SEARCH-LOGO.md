# SEARCH-LOGO.md — Logo dans les résultats de recherche Google

## Contexte

Lorsqu'un site apparaît dans les résultats de recherche Google, un petit logo (icône) s'affiche à gauche du nom du site et de l'URL. Cette icône est appelée **favicon** (abréviation de "favorite icon").

### Origine du favicon dans les résultats Google

Google récupère automatiquement le favicon d'un site web pour l'afficher dans ses résultats de recherche. Il le détecte selon cet ordre de priorité :

1. **Balise `<link rel="icon">` dans le `<head>` du HTML** — c'est la méthode principale
2. **Fichier `/favicon.ico` à la racine du site** — méthode historique par défaut
3. Si aucun favicon n'est trouvé, Google affiche une **icône générique** représentant un globe/site web

### Situation actuelle de la page

La page `index.html` déclare actuellement un favicon SVG :

```html
<link rel="icon" href="favicon.svg" type="image/svg+xml">
```

Le fichier `favicon.svg` contient une icône stylisée représentant un graphique avec une courbe ascendante (en lien avec le thème CRO). Ce n'est pas la photo de Léa.

**Pourquoi l'icône actuelle peut apparaître comme un logo web générique dans Google :** Google n'indexe pas toujours les favicons SVG correctement. Il privilégie les formats bitmap (PNG, ICO). Si Google ne parvient pas à lire le SVG, il affiche l'icône générique par défaut.

---

## Ce qu'il faut faire pour afficher la photo de Léa

### Étape 1 — Préparer l'image

La photo `lea.png` ne peut pas être utilisée directement comme favicon : elle est trop grande et rectangulaire. Il faut créer une version spécifique :

1. **Recadrer la photo** de Léa en format **carré** (focus sur le visage)
2. **Redimensionner** en plusieurs tailles :
   - `favicon-16x16.png` (16×16 pixels) — taille standard navigateur
   - `favicon-32x32.png` (32×32 pixels) — taille haute résolution navigateur
   - `apple-touch-icon.png` (180×180 pixels) — pour les appareils Apple
   - `favicon.ico` (48×48 pixels) — format legacy compatible tous navigateurs
3. **Optionnel mais recommandé** : arrondir légèrement les coins de l'image pour un rendu plus esthétique dans les résultats Google

> **Outils gratuits utilisables** : [RealFaviconGenerator.net](https://realfavicongenerator.net), [Favicon.io](https://favicon.io), ou tout éditeur d'image (GIMP, Photoshop, Canva).

### Étape 2 — Placer les fichiers à la racine du site

Déposer les fichiers suivants à la racine du projet (au même niveau que `index.html`) :

```
/favicon.ico
/favicon-16x16.png
/favicon-32x32.png
/apple-touch-icon.png
```

### Étape 3 — Modifier le `<head>` de `index.html`

Remplacer la ligne actuelle :

```html
<link rel="icon" href="favicon.svg" type="image/svg+xml">
```

Par les déclarations suivantes :

```html
<!-- Favicon -->
<link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">
<link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
<link rel="shortcut icon" href="favicon.ico">
```

### Étape 4 (optionnel) — Conserver le SVG comme alternative

Si on souhaite garder le favicon SVG pour les navigateurs modernes tout en ayant la photo pour Google :

```html
<link rel="icon" href="favicon.svg" type="image/svg+xml">
<link rel="icon" type="image/png" sizes="32x32" href="favicon-32x32.png">
<link rel="icon" type="image/png" sizes="16x16" href="favicon-16x16.png">
<link rel="apple-touch-icon" sizes="180x180" href="apple-touch-icon.png">
<link rel="shortcut icon" href="favicon.ico">
```

Les navigateurs utiliseront le SVG (plus net), mais Google utilisera le PNG.

---

## Exigences Google pour les favicons

Google impose des règles spécifiques pour afficher un favicon dans ses résultats :

| Critère | Exigence |
|---|---|
| **Taille minimale** | 48×48 pixels (multiple de 48 recommandé) |
| **Format** | ICO, PNG, SVG (PNG recommandé) |
| **Forme** | Carré (Google le recadre sinon) |
| **Emplacement** | Accessible au robot Googlebot (ne pas bloquer dans robots.txt) |
| **Contenu** | Représentatif du site, pas trompeur |
| **URL stable** | Ne pas changer fréquemment l'URL du favicon |

**Important** : après modification, Google peut mettre **plusieurs jours à plusieurs semaines** pour mettre à jour le favicon dans ses résultats de recherche. Ce n'est pas instantané.

---

## Recommandation

Pour un rendu professionnel et personnel, utiliser **une photo de Léa recadrée en carré** (visage centré) comme favicon est une bonne approche. Cela renforce l'image de marque personnelle et la reconnaissance visuelle dans les résultats de recherche.

**Alternative** : si la photo est difficile à lire en 16×16 pixels (trop de détails), envisager un **logo simplifié** (par exemple les initiales "LC" stylisées sur fond sombre `#1a1a18` avec accent `#00d4ff`) qui serait plus lisible à petite taille tout en restant identifiable.
