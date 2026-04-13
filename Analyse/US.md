# User Stories — Landing Page CRO Freelance

> Ce document décrit les user stories nécessaires à l'implémentation de la landing page.
> Chaque US est rattachée à une **Epic** et suit le format : *"En tant que [persona], je veux [action], afin de [bénéfice]"*.
> Les critères d'acceptation (CA) définissent les conditions de validation.

---

## Epic 1 — Structure de base & configuration

### US-1.1 : Squelette HTML et imports de ressources

**En tant que** développeur,
**je veux** créer le fichier HTML de base avec les métadonnées, les imports Google Fonts (Instrument Serif, DM Sans) et la structure sémantique globale,
**afin de** disposer d'une fondation technique prête pour l'intégration de toutes les sections.

**Critères d'acceptation :**
- [x] Un fichier `index.html` est créé à la racine du projet
- [x] Le `<head>` contient les balises `meta charset`, `viewport`, `title` et `description` en français
- [x] Les polices Instrument Serif (400, 400 italic) et DM Sans (400, 500, 600, 700) sont importées via Google Fonts
- [x] Le CSS est intégré dans une balise `<style>` ou dans un fichier `style.css` lié
- [x] Un reset CSS minimal est appliqué (box-sizing, margin, padding)
- [x] La propriété `scroll-behavior: smooth` est définie sur `html`
- [x] Les variables CSS sont définies pour la palette de couleurs : `#0f0f0e`, `#1a1a18`, `#7a7870`, `#a3a198`, `#ffffff`, `#00d4ff`, `#45cdff3d`
- [x] La page s'affiche sans erreur dans un navigateur moderne

**Priorité :** Haute
**Dépendances :** Aucune

---

### US-1.2 : Conteneur principal et classes utilitaires

**En tant que** développeur,
**je veux** définir le conteneur principal (max-width 1200px, centré) et les classes CSS réutilisables (labels de section, boutons primaire/secondaire/secondaire-cyan),
**afin de** garantir une cohérence visuelle sur l'ensemble de la page et éviter la duplication de code.

**Critères d'acceptation :**
- [x] Un conteneur `.container` est défini avec `max-width: 1200px`, `margin: 0 auto`, padding latéral 20-40px
- [x] La classe `.section-label` applique : couleur `#00d4ff`, DM Sans, 12-14px, letter-spacing 2px, text-transform uppercase
- [x] La classe `.btn-primary` applique : fond `#00d4ff`, texte `#0f0f0e`, border-radius 25px, padding 12px 28px, DM Sans semi-bold
- [x] La classe `.btn-secondary` applique : fond transparent, bordure blanche, texte blanc, border-radius 25px
- [x] La classe `.btn-secondary-cyan` applique : fond transparent, bordure `#00d4ff`, texte `#00d4ff`, border-radius 25px
- [x] Les boutons ont un effet de survol visible (changement d'opacité ou de couleur via `#45cdff3d`)

**Priorité :** Haute
**Dépendances :** US-1.1

---

## Epic 2 — Header & Navigation

### US-2.1 : Header fixe avec navigation

**En tant que** visiteur,
**je veux** voir une barre de navigation fixe en haut de la page avec le nom de la consultante, les liens de navigation et un bouton d'appel à l'action,
**afin de** pouvoir naviguer facilement vers chaque section de la page à tout moment.

**Critères d'acceptation :**
- [x] Le header est positionné en `sticky` (ou `fixed`) en haut de page avec un z-index élevé
- [x] Le fond est `#0f0f0e`, hauteur ~60-70px, padding horizontal 40-80px
- [x] À gauche : "Léa Macioszczyk · Freelance CRO" en Instrument Serif, blanc (font-size 21px, non italique)
- [x] Au centre : 4 liens de navigation (À PROPOS, MÉTHODE, OFFRES, CONTACT) en DM Sans, majuscules, couleur `#a3a198`
- [x] Chaque lien pointe vers l'ancre correspondante (#a-propos, #methode, #offres, #contact)
- [x] À droite : bouton "Diagnostic gratuit" en style `.btn-primary` avec une petite icône
- [x] Le bouton "Diagnostic gratuit" pointe vers la section #contact
- [x] Le layout utilise flexbox avec `justify-content: space-between` et `align-items: center`

**Priorité :** Haute
**Dépendances :** US-1.1, US-1.2

---

### US-2.2 : Menu hamburger responsive (mobile)

**En tant que** visiteur sur mobile,
**je veux** accéder à la navigation via un menu hamburger,
**afin de** pouvoir naviguer sur la page sans que le header soit surchargé sur petit écran.

**Critères d'acceptation :**
- [x] En dessous de 768px, les liens de navigation et le bouton CTA sont masqués
- [x] Une icône hamburger (3 barres) apparaît, réalisée en CSS pur
- [x] Le mécanisme d'ouverture/fermeture utilise un checkbox hack CSS (pas de JavaScript)
- [x] Le menu ouvert affiche les liens en colonne sur fond `#0f0f0e`
- [x] Un clic sur un lien ferme le menu (via ancre + label/checkbox)

**Priorité :** Moyenne
**Dépendances :** US-2.1

---

## Epic 3 — Section Hero

### US-3.1 : Bloc Hero avec titre, sous-titre et CTA

**En tant que** visiteur,
**je veux** voir dès l'arrivée sur la page un titre accrocheur, une description de l'offre et des boutons d'action,
**afin de** comprendre immédiatement la proposition de valeur et pouvoir agir.

**Critères d'acceptation :**
- [x] La section a un fond `#0f0f0e`, padding vertical ~100-120px
- [x] Le tag "CRO FREELANCE · E-COMMERCE & SITE VITRINE" est affiché en DM Sans, majuscules, espacement large, couleur `#7a7870`
- [x] Le titre h1 affiche le texte exact de `docs/texte.txt` : "Votre site a du trafic mais pas assez de résultats ?"
- [x] Les mots "trafic" et "mais" sont en Instrument Serif italique
- [x] "pas assez de résultats" est mis en évidence (couleur `#00d4ff`)
- [x] Le sous-titre reprend le paragraphe descriptif exact de `docs/texte.txt`, en DM Sans, couleur `#a3a198`, largeur max ~700px
- [x] Deux boutons côte à côte : "Diagnostic gratuit" (`.btn-primary`) et "Voir les offres" (`.btn-secondary`)
- [x] "Voir les offres" pointe vers #offres, "Diagnostic gratuit" pointe vers #contact
- [x] Sous les boutons : "Livré par email, sans appel obligatoire." en petit, couleur `#7a7870`
- [x] Le contenu est centré horizontalement

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 4 — Section "Le Problème"

### US-4.1 : Bloc problème en deux colonnes

**En tant que** visiteur,
**je veux** comprendre pourquoi mon site ne convertit pas à travers des explications claires et des exemples de frictions,
**afin de** prendre conscience du problème et de la nécessité d'une expertise CRO.

**Critères d'acceptation :**
- [x] La section a un fond blanc `#ffffff`, padding vertical ~80-100px
- [x] Le label "— Le problème" est affiché en style `.section-label`
- [x] Le titre h2 reprend le texte exact : "La plupart des sites perdent des conversions sans le savoir." avec "sans le savoir" en Instrument Serif italique
- [x] Le paragraphe explicatif (statistique 97%, frictions invisibles) reprend le texte exact de `docs/texte.txt`
- [x] La phrase "se détectent dans les données" est mise en évidence (soulignement cyan)
- [x] Layout en 2 colonnes : texte à gauche (~50%), cartes à droite (~50%)
- [x] 3 cartes empilées verticalement à droite, chacune avec titre (DM Sans semi-bold, noir) et description (DM Sans, gris `#7a7870`)
- [x] Les cartes reprennent exactement les 3 frictions de `docs/texte.txt`
- [x] En responsive mobile (< 768px), les colonnes passent en une seule colonne

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 5 — Section "À Propos"

### US-5.1 : Présentation de la consultante

**En tant que** visiteur,
**je veux** voir la photo et le parcours de la consultante,
**afin de** savoir à qui je m'adresse et évaluer sa crédibilité.

**Critères d'acceptation :**
- [x] La section a un fond `#0f0f0e`, padding vertical ~80-100px
- [x] Le label "— À propos" est affiché en style `.section-label`
- [x] Layout en 2 colonnes : photo à gauche, texte à droite
- [x] La photo `docs/lea.png` est affichée en cercle (`border-radius: 50%`), taille ~250-300px
- [x] Le titre h2 reprend : "Consultante conversion & performance digitale" en Instrument Serif italique, blanc
- [x] Les 3 paragraphes descriptifs reprennent exactement le texte de `docs/texte.txt`, en DM Sans, couleur `#a3a198`
- [x] En responsive mobile, la photo passe au-dessus du texte (colonne unique, photo centrée)
- [x] L'ancre `id="a-propos"` est définie sur la section

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 6 — Section "Méthode"

### US-6.1 : Présentation de la méthodologie en 4 étapes

**En tant que** visiteur,
**je veux** comprendre la méthode de travail de la consultante étape par étape,
**afin de** savoir comment se déroule une mission CRO et être rassuré sur le processus.

**Critères d'acceptation :**
- [x] La section a un fond `#eef2f6`, padding vertical ~80-100px
- [x] Le label "— méthode" est affiché en style `.section-label`
- [x] Le titre h2 reprend : "Analyse, hypothèses, tests, résultats." en Instrument Serif italique, "résultats" mis en évidence (cyan)
- [x] Le paragraphe introductif reprend exactement le texte de `docs/texte.txt`, incluant la mention du développeur senior
- [x] 4 étapes numérotées (1 à 4) sont affichées verticalement
- [x] Chaque étape affiche : numéro (grand, gris), titre (DM Sans semi-bold, noir), description (DM Sans, gris `#7a7870`)
- [x] Une séparation visuelle (ligne fine horizontale) sépare chaque étape
- [x] Les textes de chaque étape correspondent exactement à `docs/texte.txt`
- [x] L'ancre `id="methode"` est définie sur la section

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 7 — Section "Offres"

### US-7.1 : Affichage des 3 cartes d'offres

**En tant que** visiteur,
**je veux** voir les différentes formules proposées avec leurs prix, descriptions et caractéristiques,
**afin de** choisir l'offre adaptée à ma situation et passer à l'action.

**Critères d'acceptation :**
- [x] La section a un fond `#1a1a18`, padding vertical ~80-100px
- [x] Le label "— offres" est affiché en style `.section-label`
- [x] Le titre h2 reprend : "Un point d'entrée selon votre situation." en Instrument Serif, blanc
- [x] Le sous-titre reprend le texte exact de `docs/texte.txt`
- [x] 3 cartes sont affichées côte à côte en grille (3 colonnes)
- [x] Chaque carte a un fond `#0f0f0e`, border-radius ~14px, padding ~32px
- [x] **Carte 1 — ONE-SHOT** : tag "ONE-SHOT", durée "2 SEMAINES", titre "Audit opérationnel", prix "499€", cible "Pour qui", 3 fonctionnalités listées, bouton "Me contacter"
- [x] **Carte 2 — ACCOMPAGNEMENT** : tag "ACCOMPAGNEMENT", durée "MINIMUM 3 MOIS", titre "Accompagnement CRO", prix "799€ /mois", cible "Pour qui", 4 fonctionnalités listées, bouton "Me contacter"
- [x] **Carte 3 — OFFRE COMPLÉMENTAIRE** : tag "OFFRE COMPLÉMENTAIRE", titre "Exécution technique", prix "sur devis", cible "Pour qui", 2 fonctionnalités listées
- [x] Tous les textes proviennent strictement de `docs/texte.txt`
- [x] Les boutons "Me contacter" sont en style `.btn-secondary-cyan` et pointent vers #contact
- [x] Les fonctionnalités sont listées avec une puce cyan
- [x] En responsive mobile, les cartes passent en colonne unique
- [x] L'ancre `id="offres"` est définie sur la section

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 8 — Bannière CTA intermédiaire

### US-8.1 : Bannière d'appel à l'action diagnostic gratuit

**En tant que** visiteur,
**je veux** voir une bannière visible m'invitant à demander un diagnostic gratuit,
**afin de** pouvoir passer à l'action facilement même si je ne suis pas encore décidé sur une offre.

**Critères d'acceptation :**
- [x] La bannière a un fond `#00d4ff`, pleine largeur, padding vertical ~50-60px
- [x] Le texte "Vous ne savez pas par où commencer ?" est affiché en DM Sans, noir
- [x] Le texte "Je jette un oeil à votre site gratuitement." est affiché en DM Sans bold, noir, taille plus grande
- [x] Un bouton "Diagnostic gratuit" est affiché : fond `#0f0f0e`, texte blanc, coins arrondis
- [x] Le bouton pointe vers la section #contact
- [x] Le contenu est centré horizontalement

**Priorité :** Moyenne
**Dépendances :** US-1.2

---

## Epic 9 — Section "Contact"

### US-9.1 : Bloc contact split (texte + formulaire)

**En tant que** visiteur intéressé,
**je veux** pouvoir remplir un formulaire de contact avec mes informations et ma demande,
**afin de** prendre contact avec la consultante et obtenir un diagnostic ou un devis.

**Critères d'acceptation :**
- [x] La section est divisée en 2 colonnes : gauche fond `#1a1a18`, droite fond `#eef2f6`
- [x] **Colonne gauche :**
  - [x] Le label "— contact" est affiché en style `.section-label`
  - [x] Le titre h2 reprend : "Si vous pensez que votre site peut générer plus de résultats." avec "plus de résultats" en italique/cyan
  - [x] "Parlons-en." est affiché en Instrument Serif italique, blanc
  - [x] 3 points de réassurance sont listés avec le texte exact de `docs/texte.txt` :
    - "Réponse sous 48h..."
    - "Honnêteté avant tout..."
    - "Diagnostic offert..."
  - [x] Chaque point est précédé d'un texte en gras (titre du point) suivi du détail
- [x] **Colonne droite (formulaire) :**
  - [x] Champ "Prénom / Nom" — input text, required, placeholder "Marie Dupont"
  - [x] Champ "Email" — input email, required, placeholder "marie@pro.com"
  - [x] Champ "URL de votre site" — input url, required, placeholder "https://monsite.fr"
  - [x] Champ "Vous êtes intéressé par" — select avec option par défaut "Sélectionner", required
  - [x] Champ "Votre situation" — textarea, required, placeholder "Quelques mots sur votre site, votre trafic, ce qui bloque...."
  - [x] Bouton "Envoyer" en style `.btn-primary` avec icône flèche
  - [x] Les champs ont une bordure grise légère, fond blanc, padding ~12px, border-radius ~8px
  - [x] Tous les champs sont marqués comme obligatoires (attribut `required`)
- [x] En responsive mobile, les colonnes passent en une seule (texte au-dessus, formulaire en dessous)
- [x] L'ancre `id="contact"` est définie sur la section

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 10 — Section "FAQ"

### US-10.1 : Accordéon FAQ en CSS pur

**En tant que** visiteur hésitant,
**je veux** consulter les réponses aux questions fréquentes en cliquant sur chaque question,
**afin de** lever mes dernières objections avant de prendre contact.

**Critères d'acceptation :**
- [x] La section a un fond `#1a1a18`, padding vertical ~80-100px
- [x] Le label "— QUESTIONS FRÉQUENTES" est affiché en style `.section-label`
- [x] Le titre h2 reprend : "Vous hésitez encore ?" en Instrument Serif italique, blanc
- [x] 5 éléments accordéon sont affichés, utilisant `<details>` / `<summary>` (CSS pur, pas de JS)
- [x] Chaque élément a un fond `#eef2f6`, border-radius 8px, espacement 8px entre items
- [x] L'icône "+" est visible à gauche de chaque question (se transforme en "−" cyan à l'ouverture via CSS)
- [x] Le texte de chaque question est en DM Sans, noir
- [x] Le texte de chaque réponse est en DM Sans, gris `#7a7870`
- [x] Les 5 questions et réponses correspondent exactement au contenu de `docs/texte.txt`
- [x] Largeur max de l'accordéon : 900px
- [x] L'ancre `id="faq"` est définie sur la section

**Priorité :** Haute
**Dépendances :** US-1.2

---

## Epic 11 — Footer

### US-11.1 : Pied de page

**En tant que** visiteur,
**je veux** voir le nom de la consultante et les mentions légales en bas de page,
**afin de** savoir que je suis sur un site professionnel et identifié.

**Critères d'acceptation :**
- [x] Le footer a un fond `#0f0f0e`, une bordure top subtile le séparant de la FAQ
- [x] Layout flexbox, `justify-content: space-between`, hauteur 68px, padding horizontal 48px
- [x] À gauche : "Léa Macioszczyk · Freelance CRO" en Instrument Serif, blanc
- [x] À droite : "© 2026 — Tous droits réservés" en DM Sans, couleur `#7a7870`
- [x] Le footer est aligné verticalement au centre

**Priorité :** Moyenne
**Dépendances :** US-1.1

---

## Epic 12 — Responsive Design

### US-12.1 : Adaptation tablette (768px - 1024px)

**En tant que** visiteur sur tablette,
**je veux** que la page s'adapte correctement à mon écran,
**afin de** lire le contenu et interagir sans difficulté.

**Critères d'acceptation :**
- [x] Les sections à 2 colonnes (Problème, À propos, Contact) réduisent les gaps et proportions
- [x] Les 3 cartes d'offres restent en 3 colonnes avec taille réduite (textes compactés)
- [x] Les tailles de titre sont réduites proportionnellement (h1: 44px, h2: 34-36px)
- [x] Le padding horizontal et vertical est ajusté (container: 32px)
- [x] Aucun débordement horizontal n'est visible (overflow-x: hidden)

**Priorité :** Moyenne
**Dépendances :** US-3.1 à US-11.1

---

### US-12.2 : Adaptation mobile (< 768px)

**En tant que** visiteur sur smartphone,
**je veux** que la page soit entièrement lisible et navigable en une seule colonne,
**afin de** vivre une expérience fluide sur petit écran.

**Critères d'acceptation :**
- [x] Toutes les sections multi-colonnes passent en colonne unique
- [x] Le menu hamburger remplace la navigation classique (cf. US-2.2)
- [x] Les cartes d'offres s'empilent verticalement (max-width 480px)
- [x] La photo de Léa passe au-dessus du texte dans la section À propos (centrée)
- [x] La section Contact affiche d'abord le texte, puis le formulaire en dessous
- [x] Les titres h1 passent à 34px (28px sur petit mobile), les h2 à 28-30px (24-26px sur petit mobile)
- [x] Les boutons s'affichent en pleine largeur
- [x] Le formulaire de contact est utilisable (font-size 16px sur touch pour éviter le zoom iOS, padding augmenté)
- [x] Aucun débordement horizontal n'est visible (overflow-x: hidden)
- [x] Compatibilité cross-browser : préfixes -webkit-/-moz- pour appearance, text-size-adjust, font-smoothing
- [x] Compatibilité iOS : safe-area-inset, viewport-fit=cover, tap-highlight désactivé
- [x] Compatibilité Android : touch targets minimum 44px (pointer: coarse)
- [x] Support prefers-reduced-motion pour accessibilité
- [x] Support forced-colors (mode contraste élevé Windows)
- [x] Breakpoint petit mobile (< 480px) avec tailles encore réduites
- [x] Paysage mobile (landscape < 500px hauteur) avec padding compact

**Priorité :** Moyenne
**Dépendances :** US-2.2, US-3.1 à US-11.1

---

## Récapitulatif & Ordre d'implémentation

| Ordre | US | Titre | Priorité |
|-------|----|-------|----------|
| 1 | US-1.1 | Squelette HTML et imports | Haute |
| 2 | US-1.2 | Conteneur et classes utilitaires | Haute |
| 3 | US-2.1 | Header fixe avec navigation | Haute |
| 4 | US-3.1 | Section Hero | Haute |
| 5 | US-4.1 | Section Problème | Haute |
| 6 | US-5.1 | Section À Propos | Haute |
| 7 | US-6.1 | Section Méthode | Haute |
| 8 | US-7.1 | Section Offres | Haute |
| 9 | US-8.1 | Bannière CTA | Moyenne |
| 10 | US-9.1 | Section Contact | Haute |
| 11 | US-10.1 | Section FAQ | Haute |
| 12 | US-11.1 | Footer | Moyenne |
| 13 | US-2.2 | Menu hamburger mobile | Moyenne |
| 14 | US-12.1 | Responsive tablette | Moyenne |
| 15 | US-12.2 | Responsive mobile | Moyenne |
