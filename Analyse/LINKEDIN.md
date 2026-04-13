# LINKEDIN.md — Ajout du lien LinkedIn dans la section "À propos"

## Objectif

Ajouter un lien vers le profil LinkedIn de Léa Macioszczyk dans la section "À propos" de la page `index.html`, afin de renforcer la crédibilité professionnelle et permettre aux visiteurs de consulter son profil.

## Profil LinkedIn

**URL** : https://fr.linkedin.com/in/léa-macioszczyk

## Emplacement prévu

Section "À propos" (`<section id="a-propos">`), sous le texte de présentation de Léa, à proximité du bouton CTA existant.

## Implémentation (Option 1 retenue — Icône LinkedIn cliquable)

L'icône LinkedIn SVG bicolore a été ajoutée après le dernier paragraphe de la section "À propos".

### Couleurs du logo LinkedIn

Le logo utilise deux couleurs pour respecter la charte officielle LinkedIn :

| Élément | Couleur | Code |
|---|---|---|
| **Fond du carré** | Bleu officiel LinkedIn | `#0A66C2` |
| **Lettres "in"** | Blanc | `#ffffff` |

Le SVG est structuré en deux parties distinctes :
- Un `<rect>` pour le carré de fond, utilisant `fill="currentColor"` (coloré via CSS `color: #0A66C2`)
- Un `<path>` pour les lettres "in", avec `fill="#ffffff"` en dur

### Code HTML implémenté

```html
<a href="https://fr.linkedin.com/in/l%C3%A9a-macioszczyk" target="_blank" rel="noopener noreferrer" class="a-propos__linkedin" aria-label="Profil LinkedIn de Léa Macioszczyk">
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" aria-hidden="true">
    <rect width="24" height="24" rx="3" fill="currentColor"/>
    <path d="M5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286z" fill="#ffffff"/>
  </svg>
</a>
```

### Style CSS implémenté

```css
.a-propos__linkedin {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 44px;
  color: #0A66C2;              /* Bleu officiel LinkedIn — fond du carré */
  -webkit-transition: opacity 0.2s;
  transition: opacity 0.2s;
  margin-top: 16px;
}

.a-propos__linkedin:hover,
.a-propos__linkedin:focus-visible {
  opacity: 0.8;
}

.a-propos__linkedin:focus {
  outline: 2px solid var(--cyan);
  outline-offset: 2px;
  border-radius: 4px;
}

.a-propos__linkedin svg {
  width: 28px;
  height: 28px;
}
```

## Conformité Epic 12

- **Touch target** : 44×44px (conforme iOS/Android)
- **URL encodée** (`%C3%A9` pour `é`) pour compatibilité cross-browser
- **Préfixe `-webkit-transition`** pour Safari ancien
- **Focus visible** avec `outline` cyan + fallback `:focus` pour Safari < 15.4
- **`aria-label`** + `aria-hidden="true"` sur le SVG pour l'accessibilité
- **`rel="noopener noreferrer"`** pour la sécurité (reverse tabnapping)
- **SVG inline** : aucune dépendance externe
- **Pas de JavaScript**
