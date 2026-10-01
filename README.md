# veille-masques-residences

Outil de veille pour le projet de masques brodés de Cécile Kretschmar : repérage de résidences artistiques (théâtre masqué), suivi des candidatures et alertes automatiques sur les nouveaux appels à candidature.

**Site en ligne :** https://ja1000m.github.io/veille-masques-residences/

## Ce que c'est

Un site statique à page unique (`index.html`), sans dépendance ni build, hébergé via GitHub Pages. Toutes les données (plateformes, résidences, mots-clés, flux RSS) sont codées en dur dans des tableaux JavaScript au sein du fichier — il n'y a pas de base de données ni de backend.

## Structure du fichier

Tout tient dans **`index.html`** : HTML, CSS et JavaScript dans un seul fichier, organisé en sections commentées (chercher les blocs `/* ===== ... ===== */` ou `<!-- ===== VUE ... ===== -->`).

Le site comporte 5 onglets (définis par les boutons `<nav class="tabs">`, un par `<section class="view" id="view-...">`) :

1. **Plateformes** — plateformes de repérage classées par zone géographique, avec les résidences du projet retrouvées sur chacune et leur statut.
2. **Répertoire résidences** — fiches des résidences identifiées, avec statut (ouvert / à surveiller / fermé) et recherche.
3. **Grille de sélection** — grille de notation (0–3 par critère, total sur 27) à dupliquer pour évaluer une résidence candidate.
4. **Veille** — mots-clés suggérés pour les alertes Google et méthode de mise en place de la veille.
5. **Alertes RSS** — flux Google Alerts branchés sur les mots-clés de veille, affichés bruts (non filtrés) via l'API `rss2json`.

Une bulle flottante (`#status-alert`) signale en haut de page les résidences passées en appel ouvert depuis la dernière visite.

## Comment éditer

Pas d'installation ni de build : ouvrir `index.html` dans un éditeur, modifier le tableau JS concerné, enregistrer, committer.

Tableaux de données à connaître (recherche par nom dans le fichier) :
- `RSS_FEEDS` — liste des flux Google Alerts (voir ci-dessous)
- données des plateformes, résidences, mots-clés et grille — dans les blocs JS correspondant à chaque vue

### Ajouter une alerte RSS

1. Créer l'alerte sur [google.com/alerts](https://www.google.com/alerts).
2. Choisir **« Livrer par : Flux RSS »**.
3. Copier le lien du flux.
4. Ajouter une entrée dans le tableau `RSS_FEEDS` (fin du fichier, avant les fonctions `buildRssItem` / `renderRSS`) :
   ```js
   { name: "libellé de l'alerte", url: "https://www.google.com/alerts/feeds/.../..." }
   ```
   Veiller à bien fermer le tableau avec `];` après la dernière entrée.

### Vérifier avant de committer

Après toute modification du JS, vérifier la syntaxe avant de pousser (par exemple en extrayant le contenu de la balise `<script>` et en lançant `node --check` dessus), pour éviter de casser l'ensemble du site avec une erreur de syntaxe.

## Déploiement

Le site se déploie automatiquement via GitHub Pages à chaque push sur `main` (voir l'onglet **Deployments** du dépôt pour le statut). Après un push, compter quelques minutes avant que le site public reflète le changement — le cache de `raw.githubusercontent.com` peut aussi retarder la vérification du contenu brut pendant quelques dizaines de secondes.

## Mise à jour mi-2026

Les statuts de résidences sont vérifiés mi-2026 sauf mention contraire sur chaque fiche — toujours reconfirmer sur le site source avant toute candidature.
