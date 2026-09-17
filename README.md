# Revue de presse du SNUM

Site public de la revue de presse du Service du numérique (SNUM), présenté avec le Système de design de l’État (DSFR).

- Site GitHub Pages : <https://bacoco.github.io/revue-presse-snum/>
- Dernière édition : `index.html`
- Archives : <https://bacoco.github.io/revue-presse-snum/editions/>

## Fonctionnement

La revue est préparée deux fois par semaine, le mardi et le vendredi. Le processus :

1. collecte les nouveaux articles dans les rubriques Numérique, Intelligence artificielle (IA), Commande publique, Ressources humaines et Vie de Bercy ;
2. vérifie les titres, dates, sources, URL et faits essentiels ;
3. supprime les doublons et regroupe les articles consacrés au même événement ;
4. produit une synthèse éditoriale avec « L’essentiel », « Mots-clés », « À retenir », « Intérêt pour le SNUM » et « À surveiller » ;
5. publie la nouvelle édition sur le site ;
6. envoie un message court contenant trois points clés et le lien vers le site.

La cybersécurité, les données, le cloud et les autres sujets connexes sont classés dans ces rubriques. Les ressources documentaires ne sont utilisées que lorsqu’elles sont réellement accessibles et publiables.

Le scheduler et les identifiants de messagerie sont gérés en dehors de ce dépôt. Aucun secret ni adresse de diffusion ne doit être ajouté au dépôt public.

## Sources suivies

Privilégier les médias français généralistes et économiques, notamment Le Monde et Les Echos, puis les médias français pertinents. Compléter avec Acteurs Publics, IT for Business, Journal du Net, L’Usine Digitale, economie.gouv.fr, presse.economie.gouv.fr, numerique.gouv.fr et d’autres sources officielles ou spécialisées utiles.

Seuls les articles intégralement accessibles au public sans abonnement sont retenus. Un titre, un extrait ou une page nécessitant un abonnement, un login payant ou un essai payant ne suffit pas. Aucune information restreinte ne doit être publiée.

## Organisation du dépôt

```text
.
├── index.html                   # dernière édition ou révision publiée
├── styles.css                  # styles communs
├── editions/
│   ├── index.html              # sommaire des archives
│   └── YYYY-MM-DD/
│       ├── index.html          # édition initiale figée
│       └── revision-N/
│           └── index.html      # correction explicitement demandée
├── comptes-rendus/
├── accessibilite/
├── mentions-legales/
├── plan-du-site/
├── .nojekyll
└── README.md
```

## Publier une nouvelle édition

1. Lire la dernière édition et son compte rendu. Une édition déjà publiée ou diffusée à la date courante arrête la production automatique : `ALREADY_COMPLETE`.
2. Créer `editions/YYYY-MM-DD/index.html` avec le contenu complet de la nouvelle édition.
3. Copier cette édition dans `index.html` afin qu’elle devienne la page d’accueil.
4. Ajouter l’édition en tête de `editions/index.html`.
5. Vérifier le HTML, les liens internes, les accès rapides, le titre unique, le pied de page et les indications de nouvelle fenêtre.
6. Vérifier qu’aucune information interne, adresse de diffusion ou URL réservée à l’intranet n’est exposée.
7. Committer et pousser les modifications sur `main`, sans supprimer ni réécrire les anciennes éditions.
8. Vérifier la publication réelle avant l’envoi, puis conserver un compte rendu distinguant les preuves et les limitations.

Chaque commit Git conserve l’historique technique. Chaque dossier daté conserve une édition publique stable, consultable même après la publication des numéros suivants.

### Correction éditoriale ponctuelle

Une demande explicite du propriétaire peut autoriser une correction et un renvoi uniques. Conserver l’édition initiale ; créer `editions/YYYY-MM-DD/revision-N/index.html`, actualiser l’accueil et le sommaire des archives, puis vérifier la publication. Contrôler les messages envoyés pour cette révision avant tout nouvel envoi. Ne pas présenter une révision éditoriale comme une nouvelle collecte. Cette exception n’autorise jamais un renvoi automatique lors des exécutions suivantes.

## Activer GitHub Pages

Dans **Settings → Pages** :

- **Source** : `Deploy from a branch`
- **Branch** : `main`
- **Folder** : `/ (root)`

Après validation, GitHub publie automatiquement les changements poussés sur `main`.

## Développement local

Le site est statique : aucun build n’est nécessaire. Ouvrir `index.html` dans un navigateur ou servir le dossier avec un serveur HTTP local suffit.

## Règles éditoriales

Format synthétique applicable à partir du 17 septembre 2026 :

- 10 à 15 sujets par édition, sans remplir artificiellement une rubrique ;
- trois synthèses courtes dans « L’essentiel », et non trois analyses longues ;
- pour chaque synthèse et chaque article : un titre bref, une seule phrase factuelle de 25 mots maximum, puis « Mots-clés » avec 3 à 5 termes ou expressions courts ;
- « À retenir » et « Intérêt pour le SNUM » : une phrase de 15 mots maximum chacun ;
- préserver les chiffres, dates, populations et réserves indispensables, sans accumulation de subordonnées ;
- supprimer les sous-titres génériques ou de comptage sous les rubriques, tels que « sujets structurants pour le SNUM » ou « sujets retenus » ;
- ne pas afficher de compte d’articles ou de sources près du titre de l’édition ; conserver ces volumes dans le compte rendu ;
- lien canonique et date vérifiés, distinction claire entre faits et implications proposées ;
- aucun contenu inventé à partir d’un titre ou d’un extrait incomplet ;
- exclure les contenus payants ou inaccessibles intégralement et documenter ces exclusions ;
- « À surveiller » : formulations courtes et concrètes ;
- aucun badge « Revue publique » et aucune donnée de diffusion dans le dépôt.

## Exigences DSFR et RGAA

La préservation du DSFR et de l’accessibilité RGAA est une exigence de publication. Une régression détectée doit être corrigée avant diffusion ; l’absence de navigateur de prévisualisation ne bloque pas à elle seule la publication.

- les gabarits utilisent les composants et classes du DSFR ; les personnalisations CSS ne doivent pas neutraliser le focus, les contrastes ou le redimensionnement ;
- chaque page propose des accès rapides vers le contenu et le pied de page ; chaque édition ajoute l’accès au menu `#navigation` ;
- chaque page possède un seul `h1`, une structure de titres cohérente et des liens explicites ;
- les liens ouverts dans une nouvelle fenêtre utilisent `target="_blank"`, `rel="noopener noreferrer"` et une indication textuelle accessible ;
- les pages d’accessibilité, le schéma pluriannuel, le plan d’actions et le plan du site sont conservés ;
- les contrôles automatiques ne remplacent jamais l’audit manuel RGAA ;
- sans audit complet, valide et publié, conserver « Accessibilité : non conforme » ;
- les tags non interactifs utilisent `p.fr-tag`, les colonnes `fr-grid-row` et `fr-col-*` ;
- CSS et scripts module/nomodule : DSFR 1.15.2 ; référentiel RGAA 4.1.2 ;
- la grille `.top-grid` conserve `auto-fit/minmax`, `min-width: 0` et la rupture des mots ;
- les espacements personnalisés restent des multiples de 4 px ; préférer les utilitaires DSFR ;
- dans le header et le footer, utiliser le tiret simple « - » ;
- conserver les liens Accessibilité, Mentions légales, Données personnelles, Gestion des cookies, Plan du site et Archives.
