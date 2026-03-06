# Infinity LP — Landing Pages sectorielles haute performance

> Templates de landing pages HTML statiques optimisées pour la génération de leads qualifiés par verticale métier (BTP, Santé, Juridique, Automobile…).

---

## Pourquoi ce projet

Les TPE/PME de secteurs traditionnels (bâtiment, santé, droit, auto) cherchent un prestataire digital sur Google. Ces landing pages sont conçues pour une seule chose : **transformer ce trafic en leads qualifiés** avec le meilleur ratio performance/effort de déploiement possible.

Chaque LP est un fichier HTML unique, autonome, sans framework, sans build, sans dépendance serveur. On le pose sur un domaine, c'est en ligne.

---

## Principes de conception

### Stratégie d'acquisition

La structure de chaque page suit un tunnel de persuasion éprouvé, pensé pour du B2B local :

1. **Hero avec identification immédiate** — Visuel métier (artisan, praticien…), headline orienté douleur, preuve sociale chiffrée au-dessus de la ligne de flottaison.
2. **Problème nommé** — Trois pain points concrets du persona cible, formulés dans son langage. L'objectif est que le visiteur se dise "c'est exactement mon cas".
3. **CTA intermédiaire** — Premier point de conversion après la phase d'identification. Ramène au formulaire.
4. **Comment ça marche** — Processus en 3 étapes avec timeline. Lève le doute sur l'engagement en temps et en effort.
5. **Offre détaillée** — Le "combo gagnant" décomposé en briques (site, fiche Google, SEO IA) pour que le prospect comprenne ce qu'il achète.
6. **Preuve sociale** — Témoignages avec métriques vérifiables, statistiques globales.
7. **CTA intermédiaire** — Deuxième point de conversion après la démonstration de valeur.
8. **Pricing indicatif** — Ancrage tarifaire ("à partir de X€/mois"). Qualifie les leads en amont et rassure sur le budget.
9. **FAQ** — Traitement systématique des objections : engagement, délais, compétences, différenciation.
10. **Formulaire final** — Avec nudge d'urgence calibré et réassurances (données sécurisées, rappel sous 24h, zéro spam).

La page intègre **7 points de conversion** répartis sur le scroll : nav fixe, hero, 2 CTA bands, fin des sections "méthode" et "offre", pricing, formulaire. Le visiteur n'est jamais à plus d'un demi-écran d'un CTA. Une **barre sticky** apparaît après le hero et disparaît quand le formulaire entre dans le viewport.

### Copywriting

Le wording est rédigé en langage métier, pas en jargon marketing. Un artisan du BTP lit "maçon", "chantier", "devis" — pas "optimisation omnicanale". Les headlines utilisent la structure **douleur → bénéfice** et le ton est direct, sans bullshit.

---

## Optimisations SEO

### Balises & méta

| Élément | Détail |
|---|---|
| `<title>` | Mot-clé principal en tête, services explicités, marque en fin. ~55 caractères. |
| `<meta description>` | Les 3 piliers de l'offre + chiffre clé + CTA. ~155 caractères. Optimisée pour le CTR en SERP. |
| `<link rel="canonical">` | URL canonique unique par LP. |
| `<meta robots>` | `index, follow` explicite. |
| Open Graph | `og:title`, `og:description`, `og:image` (1200×630), `og:locale` fr_FR, `og:type` website. |
| Twitter Card | `summary_large_image` avec title, description, image. |

### Hiérarchie des Hn

```
H1 — Headline hero (unique par page)
  H2 — Titre de chaque section (Problème, Méthode, Offre, Témoignages, Pricing, FAQ, Formulaire)
    H3 — Sous-éléments (cards problème, étapes, services, questions FAQ)
```

Aucun heading orphelin. Les CTA bands utilisent des `<p><strong>` et non des `<h3>` pour ne pas casser la hiérarchie. Chaque `<section>` est liée à son H2 via `aria-labelledby`.

### Schema.org (JSON-LD)

Quatre schémas dans un `@graph` unique :

- **LocalBusiness** — Nom, adresse, téléphone, horaires, coordonnées GPS, zone de couverture, priceRange.
- **Service** — Description de l'offre, type de service, tarif avec `billingDuration: P1M`.
- **FAQPage** — Questions/réponses de la page. Éligible au rich snippet FAQ en SERP.
- **WebPage** — URL canonique, langue, rattachement à l'organisation.

### Sémantique HTML5

- `<main>` englobant tout le contenu principal.
- `<section>` par bloc thématique avec `aria-labelledby`.
- `<aside>` pour les éléments complémentaires (trust bar, CTA bands, sticky CTA).
- `<ol>` pour les étapes ordonnées.
- `<article>` pour les cards autonomes (problèmes, services).
- `<blockquote>` + `<footer>` + `<cite>` pour les témoignages.
- `<nav aria-label="...">` pour chaque zone de navigation (header, footer).
- Image hero en `<img>` réel (pas en `background-image`) avec `alt` descriptif, `width`/`height` explicites, `fetchpriority="high"`.

---

## Optimisations performance

### Philosophie

Pas de scroll reveal, pas de contenu masqué en attendant un IntersectionObserver. **Tout le contenu est visible instantanément.** Les animations sont réservées au hero (au-dessus de la fold, déjà chargé) et sont purement cosmétiques.

### Détail des optimisations

| Optimisation | Impact |
|---|---|
| **Fichier unique** | Zéro requête HTTP supplémentaire (pas de CSS/JS externe). Un seul document à parser. |
| **Google Fonts non-bloquant** | Chargement via `media="print" onload="this.media='all'"` + `<noscript>` fallback. Ne bloque pas le first render. |
| **Preconnect** | `fonts.googleapis.com`, `fonts.gstatic.com`, `images.unsplash.com` — économise ~200ms de DNS+TLS. |
| **Image hero optimisée** | `loading="eager"`, `fetchpriority="high"`, `width`/`height` explicites (évite le CLS). |
| **Transitions explicites** | Aucun `transition: all`. Chaque transition cible uniquement les propriétés animées (`background`, `transform`, `box-shadow`). |
| **`translate3d`** | Toutes les transformations utilisent `translate3d()` pour forcer le compositing GPU. |
| **`contain: layout style paint`** | Sur les cards interactives — isole les repaints au scope de l'élément. |
| **Scroll listener debounce** | Sticky CTA via `requestAnimationFrame` — un seul recalcul par frame au lieu de 60+ par seconde. |
| **Passive listeners** | `{ passive: true }` sur tous les scroll listeners. |
| **SVG inline** | Icônes en SVG inline — pas de requêtes icon font, pas de FOIT, contrôle total du style. |

---

## Accessibilité (WCAG 2.1 AA)

| Critère | Implémentation |
|---|---|
| **Skip link** | "Aller au contenu principal" visible au focus clavier, cible `<main id="contenu-principal">`. |
| **Contrastes** | Texte muted ≥ 4.6:1 sur fond clair. Recalculé avec des valeurs plus sombres que les defaults. |
| **Labels de formulaire** | Chaque `<input>` et `<select>` a un `<label>` associé via `for`/`id` (classe `.sr-only` pour le visuel). Attributs `autocomplete` sur nom, email, téléphone. |
| **Formulaire** | Balise `<form>` avec `aria-label`, `method`, `action`. Bouton `<button type="submit">`. |
| **FAQ** | `aria-expanded` sur chaque bouton, `aria-controls` pointant vers le panneau, `role="region"` sur les réponses. Toggle géré en JS. |
| **SVG décoratifs** | `aria-hidden="true"` sur tous les SVGs non-signifiants. |
| **Navigation** | `<nav aria-label="Navigation principale">` et `<nav aria-label="Liens légaux">`. |
| **Focus visible** | `:focus-visible` avec outline amber 3px + offset 2px sur tous les éléments interactifs. |
| **Reduced motion** | `@media (prefers-reduced-motion: reduce)` désactive toutes les animations. |

---

## Personnalisation

### Ce qui change par verticale

La page est conçue comme un template duplicable. Pour créer une nouvelle LP sectorielle, il suffit de modifier les zones suivantes :

**Wording & copywriting** — Le headline hero, les pain points, les descriptions de service, les témoignages et le vocabulaire métier. Tout est en clair dans le HTML, aucune abstraction. Chercher/remplacer "BTP" par "Santé", "chantier" par "cabinet", "devis" par "rendez-vous" couvre 80% du travail.

**FAQ** — La section FAQ est volontairement simple à éditer. Chaque question/réponse est un bloc HTML autonome :

```html
<div class="faq-item">
  <button class="faq-q" aria-expanded="false" aria-controls="faq-X">
    Votre question ici ?
    <!-- icône toggle -->
  </button>
  <div class="faq-a" id="faq-X" role="region">
    <p>Votre réponse ici.</p>
  </div>
</div>
```

Dupliquer un bloc pour ajouter une question, supprimer pour en retirer. Penser à mettre à jour le Schema.org FAQPage en parallèle dans le `<script type="application/ld+json">` du `<head>`.

**Pricing** — Le tarif affiché ("à partir de 149€/mois") et les éléments inclus dans la liste sont en dur dans le HTML. Modifier le montant, ajouter ou retirer des lignes dans `<ul class="pricing-includes">`, et mettre à jour le `price` dans le schema Service.

**Données Schema.org** — Le bloc JSON-LD dans le `<head>` contient les données structurées. À adapter par verticale : nom du service, description, type de service, témoignages si ajoutés au schema.

**Assets** — L'image hero (actuellement via Unsplash) et les couleurs CSS (variables dans `:root`). Le design system est entièrement piloté par les custom properties — changer `--amber` change tous les accents de la page d'un coup.

### Ce qui ne change pas

La structure du tunnel de conversion, le CSS, le JS, le système d'icônes SVG, l'architecture SEO et les mécaniques d'accessibilité. C'est le socle commun à toutes les LP.

---

## Stack

```
HTML5 · CSS3 (custom properties) · Vanilla JS
Google Fonts (DM Sans + Space Mono)
reCAPTCHA v3 (côté formulaire)
```

Aucun framework. Aucun build. Aucune dépendance npm. Le fichier HTML est le livrable.

---

## Déploiement

```bash
# C'est littéralement ça :
scp btp-infinity.html user@server:/var/www/btp-infinity.fr/index.html
```

Compatible avec n'importe quel hébergement capable de servir un fichier HTML : Apache, Nginx, Netlify, Cloudflare Pages, GitHub Pages, S3 + CloudFront.

---

## Structure des fichiers

```
infinity-lp/
├── btp-infinity.html        # LP BTP (template de référence)
├── sante-infinity.html      # LP Santé (à créer par duplication)
├── juri-infinity.html        # LP Juridique (à créer par duplication)
├── car-infinity.html         # LP Automobile (à créer par duplication)
└── README.md
```

---

## Checklist de personnalisation

Pour chaque nouvelle LP sectorielle :

- [ ] Dupliquer le fichier HTML de référence
- [ ] Adapter le `<title>` et la `<meta description>` avec les mots-clés de la verticale
- [ ] Mettre à jour l'URL `<link rel="canonical">`
- [ ] Modifier les balises Open Graph et Twitter Card (title, description, image, url)
- [ ] Remplacer le wording hero (headline, sous-titre, eyebrow)
- [ ] Adapter les 3 pain points de la section Problème
- [ ] Réécrire les descriptions du Combo Gagnant pour le secteur
- [ ] Modifier les témoignages (nom, métier, ville, verbatim, métrique)
- [ ] Ajuster le tarif et les éléments inclus dans le Pricing
- [ ] Réécrire les questions/réponses de la FAQ
- [ ] Mettre à jour le JSON-LD complet (LocalBusiness, Service, FAQPage)
- [ ] Remplacer l'image hero par un visuel métier
- [ ] Adapter le champ `source` du formulaire pour le routage CRM
- [ ] Tester les contrastes si les couleurs sont modifiées
- [ ] Valider le Schema.org via le Rich Results Test de Google

---

*Projet initié par l'équipe R&D de Futur Digital — Caen, France.*
