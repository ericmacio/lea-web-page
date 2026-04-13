# REF-AUDIT-CRO.md -- Referencement sur "Audit CRO"

> **Date** : avril 2026
> **Objectif** : Ameliorer le positionnement de la page sur les recherches
> liees a "audit CRO", "audit de conversion", "audit site web CRO", etc.

---

## 1. Etat actuel

### Points forts

- Le mot "audit" apparait **18 fois** dans le fichier HTML (meta, schemas, contenu visible, FAQ)
- Le schema `Service` decrit l'offre avec prix (499 EUR) et livrables
- La meta description inclut "audit de conversion"
- 3 questions FAQ mentionnent l'audit (trafic faible, delais, resultats)
- Le prix et le delai (499 EUR, 2 semaines) sont transparents

### Points faibles

Le probleme principal : **"audit" est present dans les metadonnees mais sous-represente dans le contenu visible**. Sur les 18 occurrences, seules 4-5 sont dans le texte affiche a l'ecran.

| Probleme | Detail |
|---|---|
| **Mauvais intitule** | L'offre s'appelle "Audit operationnel" au lieu de "Audit de conversion" -- le terme francais que les gens recherchent |
| **Pas de section dediee** | Aucune explication visible de ce que contient l'audit (format, nombre de recommandations, exemples) |
| **Mots-cles longue traine absents** | "audit de conversion", "audit UX", "audit e-commerce", "audit site web CRO" n'apparaissent nulle part dans le contenu visible |
| **Pas de FAQ specifique** | Aucune question du type "A quoi ressemble l'audit ?" ou "Que contient l'audit CRO ?" |
| **Pas de preuve sociale** | Aucun temoignage ou etude de cas specifique a l'audit |
| **Pas de lien diagnostic -> audit** | Le "Diagnostic gratuit" est propose en CTA mais pas positionne comme porte d'entree vers l'audit payant |
| **Schema incomplet** | Pas de `duration` ni de `potentialAction` sur le schema Service de l'audit |

---

## 2. Mots-cles a cibler

| Mot-cle | Volume estime | Present sur la page ? |
|---|---|---|
| audit CRO | Moyen | Schema uniquement |
| audit de conversion | Moyen | Meta description uniquement |
| audit site web | Moyen-eleve | Absent |
| audit conversion site e-commerce | Faible | Absent |
| audit UX | Moyen | Absent |
| freelance audit CRO | Faible | Absent |
| audit CRO Grenoble | Tres faible | Absent |
| prix audit CRO | Faible | Prix visible, mais pas le mot-cle complet |
| audit e-commerce | Moyen | Absent |
| audit taux de conversion | Faible | Absent |

---

## 3. Recommandations

---

### PRIORITE 1 -- Actions a fort impact, faible effort

#### 3.1 Renommer "Audit operationnel" en "Audit de conversion"

**Ou** : Titre de la carte offre (actuellement "Audit operationnel"), tag one-shot, option du formulaire de contact, schema Service.

**Pourquoi** : "Audit de conversion" est le mot-cle francais recherche. "Operationnel" est un terme technique interne qui ne parle pas aux prospects. Ce renommage aligne le titre visible avec l'intention de recherche.

**Fichiers concernes** : index.html (carte offre, formulaire contact), schemas JSON-LD

---

#### 3.2 Etoffer la description de l'offre audit avec les livrables

**Ou** : Carte offre "Audit de conversion" -- ajouter un bloc detaillant le contenu concret.

**Texte suggere** (a inserer dans ou sous la description de la carte) :

> L'audit comprend :
> - Analyse complete de votre parcours utilisateur via GA4, heatmaps et session replays
> - Identification des frictions et points de fuite sur vos pages strategiques
> - 10 a 20 recommandations UX et copywriting priorisees par impact
> - Hypotheses de tests A/B actionnables, pretes a implementer
> - Livrable : rapport detaille au format PDF

**Pourquoi** : Les visiteurs (et les IA) ont besoin de savoir concretement ce qu'ils obtiennent. Actuellement, les livrables ne sont visibles que dans le schema JSON-LD (invisible). Cela place aussi les mots-cles "heatmaps", "session replays", "recommandations UX", "tests A/B" dans le contenu visible.

**Fichiers concernes** : index.html (section offres)

---

#### 3.3 Ajouter une question FAQ dediee a l'audit

**Question suggeree** : "Que contient l'audit de conversion et sous quel format est-il livre ?"

**Reponse suggeree** :
> "L'audit de conversion est un rapport detaille livre en PDF apres 2 semaines d'analyse. Il comprend : une cartographie complete du parcours utilisateur basee sur vos donnees GA4, des captures de heatmaps et session replays illustrant les frictions identifiees, 10 a 20 recommandations UX et copywriting classees par impact, et des hypotheses de tests A/B pretes a implementer. Chaque recommandation est accompagnee d'une explication concrete et actionnable, exploitable directement par votre equipe technique."

**Pourquoi** : Cette question cible directement les requetes "audit CRO contenu", "que contient un audit CRO", "format audit de conversion". Elle enrichit aussi le schema FAQPage existant.

**Fichiers concernes** : index.html (section FAQ + schema FAQPage)

---

#### 3.4 Integrer "audit de conversion" dans le contenu visible existant

Placements naturels suggeres :

**a) Section Hero -- sous-titre** :

> Actuel : "J'aide les e-commerces et les sites vitrines a transformer leur trafic en resultats mesurables [...] Basee a Grenoble, j'interviens partout en France."
>
> Suggere : "J'aide les e-commerces et les sites vitrines a transformer leur trafic en resultats mesurables [...] grace a une approche CRO [...]. De l'audit de conversion aux tests A/B, j'interviens partout en France depuis Grenoble."

**b) Section Methode -- texte d'introduction** :

> Actuel : "J'analyse vos donnees et les croise avec une analyse UX (experience utilisateur) pour identifier precisement ce qui freine vos visiteurs."
>
> Suggere : "Mon travail commence par un audit de conversion approfondi : j'analyse vos donnees et les croise avec une analyse UX pour identifier precisement ce qui freine vos visiteurs."

**c) Section Probleme -- dernier paragraphe** :

> Actuel : "Le probleme, c'est qu'on ne les voit pas a l'oeil nu. Ils se detectent dans les donnees."
>
> Suggere : "Le probleme, c'est qu'on ne les voit pas a l'oeil nu. C'est exactement ce que revele un audit de conversion : ils se detectent dans les donnees."

**Pourquoi** : Chaque mention supplementaire de "audit de conversion" dans le contenu visible renforce le signal de pertinence pour Google et les IA, sans forcer ni nuire a la lisibilite.

**Fichiers concernes** : index.html (sections hero, methode, probleme)

---

### PRIORITE 2 -- Actions a impact moyen, effort modere

#### 3.5 Enrichir le schema Service de l'audit

Ajouter `duration` et `potentialAction` au schema existant :

```json
{
  "@type": "Service",
  "name": "Audit de conversion CRO",
  "description": "...",
  ...
  "duration": "P14D",
  "serviceOutput": {
    "@type": "Report",
    "name": "Rapport d'audit de conversion",
    "description": "Rapport PDF detaille avec analyse des parcours utilisateurs, heatmaps, recommandations UX priorisees et hypotheses de tests A/B."
  },
  "potentialAction": {
    "@type": "OrderAction",
    "target": "https://leamacio.com/#contact"
  }
}
```

**Pourquoi** : `duration` et `serviceOutput` permettent aux IA de repondre precisement a "combien de temps dure un audit CRO ?" et "que recoit-on apres un audit ?".

**Fichiers concernes** : index.html (schema JSON-LD Service)

---

#### 3.6 Creer un lien explicite "Diagnostic gratuit -> Audit payant"

**Ou** : Sous la carte audit, ajouter une mention du type :

> "Pas encore sur ? Commencez par un diagnostic gratuit de votre site. Si des optimisations sont identifiees, l'audit de conversion vous donnera une feuille de route complete."

**Pourquoi** : Cree un parcours de conversion clair (gratuit -> payant) et place une occurrence supplementaire de "audit de conversion" + "diagnostic gratuit" proches l'un de l'autre, ce qui renforce les deux requetes.

**Fichiers concernes** : index.html (section offres)

---

#### 3.7 Mettre a jour llms.txt avec un focus audit

Reformuler la description du service audit dans llms.txt :

```markdown
- Audit de conversion CRO (499 EUR, livre en 2 semaines) : rapport PDF detaille
  comprenant analyse GA4, heatmaps, session replays, 10-20 recommandations UX
  et copywriting priorisees par impact, et hypotheses de tests A/B actionnables.
```

**Fichiers concernes** : llms.txt

---

### PRIORITE 3 -- Actions a long terme, fort impact

#### 3.8 Ajouter des temoignages specifiques a l'audit

Recueillir 2-3 temoignages clients mentionnant explicitement l'audit et ses resultats :

> "L'audit a revele 3 frictions majeures sur notre page produit que nous n'avions jamais detectees. En 2 mois, notre taux de conversion est passe de 1.8% a 2.9%."
> -- Marie D., responsable e-commerce

**Pourquoi** : Les IA ponderent fortement la preuve sociale. Un temoignage avec des chiffres concrets ("+60% de conversion") est extremement citable.

**Fichiers concernes** : index.html (nouvelle section temoignages ou dans la carte audit), schema Review

---

#### 3.9 Envisager une page dediee "Audit de conversion CRO"

Si le referencement sur "audit CRO" est un objectif strategique majeur, creer une page dediee `audit-cro.html` avec :

- Un titre H1 cible : "Audit de conversion CRO : identifiez ce qui freine vos ventes"
- Une explication detaillee du processus (les 2 semaines pas a pas)
- Un exemple anonymise de rapport d'audit (captures d'ecran)
- Des resultats typiques obtenus apres implementation des recommandations
- Un CTA direct vers le formulaire de contact
- Des mots-cles longue traine : "audit CRO e-commerce", "audit conversion site vitrine", "audit UX site web"

**Avantage** : Permet un ciblage agressif sans diluer la page principale. La page dediee peut se positionner sur des dizaines de variantes longue traine.

**Inconvenient** : Maintenance supplementaire. A ne faire que si l'audit est un canal d'acquisition prioritaire.

---

#### 3.10 Proposer un exemple de rapport anonymise

Creer un PDF anonymise montrant a quoi ressemble un audit (avec vraies heatmaps floutees, recommandations typiques, format du livrable).

- Le proposer en telechargement sur la page ("Voir un exemple de rapport d'audit")
- Cela repond directement a la requete "exemple audit CRO" / "sample CRO audit report"
- Renforce la confiance avant achat

**Fichiers concernes** : nouveau fichier PDF + lien dans index.html

---

## 4. Resume -- Plan d'implementation

| # | Action | Effort | Impact SEO/GEO | Fichiers |
|---|---|---|---|---|
| 3.1 | Renommer "Audit operationnel" -> "Audit de conversion" | Tres faible | Eleve | index.html, schemas |
| 3.2 | Etoffer la description avec les livrables | Faible | Eleve | index.html |
| 3.3 | Ajouter FAQ "Que contient l'audit ?" | Faible | Eleve | index.html, schema FAQ |
| 3.4 | Integrer "audit de conversion" dans le contenu visible | Faible | Moyen-Eleve | index.html |
| 3.5 | Enrichir schema Service (duration, serviceOutput) | Faible | Moyen | index.html |
| 3.6 | Lien "diagnostic gratuit -> audit" | Faible | Moyen | index.html |
| 3.7 | Mettre a jour llms.txt | Tres faible | Moyen | llms.txt |
| 3.8 | Ajouter temoignages audit | Moyen | Eleve | index.html, schemas |
| 3.9 | Page dediee audit-cro.html | Eleve | Tres eleve | nouveau fichier |
| 3.10 | Exemple de rapport anonymise | Eleve | Eleve | nouveau PDF |

**Priorite suggeree** : 3.1 + 3.2 + 3.3 + 3.4 d'abord (effort minimal, impact immediat sur le referencement "audit CRO").
