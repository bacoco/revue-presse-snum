# Revue de presse du SNUM

Site public de la revue de presse du Service du numérique (SNUM), présenté avec le Système de design de l’État (DSFR).

- Site GitHub Pages : <https://bacoco.github.io/revue-presse-snum/>
- Dernière édition : `index.html`
- Archives : <https://bacoco.github.io/revue-presse-snum/editions/>

## Fonctionnement

La revue est préparée deux fois par semaine, le mardi et le vendredi. Le processus :

1. collecte les nouveaux articles sur le numérique, l’intelligence artificielle, la sécurité informatique, la commande publique, la vie de Bercy et les ressources humaines ;
2. vérifie les titres, dates, sources, URL et faits essentiels ;
3. supprime les doublons et regroupe les articles consacrés au même événement ;
4. produit une synthèse éditoriale avec « L’essentiel », « À retenir », « Intérêt pour le SNUM » et « À surveiller » ;
5. publie la nouvelle édition sur le site ;
6. envoie un message court contenant trois points clés et le lien vers le site.

Le scheduler et les identifiants de messagerie sont gérés en dehors de ce dépôt. Aucun secret ni adresse de diffusion ne doit être ajouté au dépôt public.

## Sources suivies

Les sources récurrentes comprennent notamment Acteurs Publics, Le Monde Pixels, economie.gouv.fr, presse.economie.gouv.fr, numerique.gouv.fr, IT for Business, Journal du Net et L’Usine Digitale. Les ressources internes ou documentaires ne sont utilisées que lorsqu’elles sont effectivement accessibles et ne doivent jamais être publiées si leur diffusion est restreinte.

## Organisation du dépôt

```text
.
├── index.html                   # dernière édition
├── styles.css                  # styles communs
├── editions/
│   ├── index.html              # sommaire des archives
│   └── YYYY-MM-DD/
│       └── index.html          # édition figée
├── .nojekyll
└── README.md
```

## Publier une nouvelle édition

1. Créer `editions/YYYY-MM-DD/index.html` avec le contenu complet de la nouvelle édition.
2. Copier cette édition dans `index.html` afin qu’elle devienne la page d’accueil.
3. Ajouter l’édition en tête de `editions/index.html`.
4. Vérifier que tous les liens externes utilisent `target="_blank"` et `rel="noopener noreferrer"`.
5. Vérifier qu’aucune information interne, donnée personnelle ou URL réservée à l’intranet n’est exposée.
6. Committer et pousser les modifications sur `main`.

Chaque commit Git conserve l’historique technique. Chaque dossier daté conserve une édition publique stable, consultable même après la publication des numéros suivants.

## Activer GitHub Pages

Dans **Settings → Pages** :

- **Source** : `Deploy from a branch`
- **Branch** : `main`
- **Folder** : `/ (root)`

Après validation, GitHub publie automatiquement les changements poussés sur `main`.

## Développement local

Le site est statique : aucun build n’est nécessaire. Ouvrir `index.html` dans un navigateur ou servir le dossier avec un serveur HTTP local suffit.

## Règles éditoriales

- 10 à 15 sujets par édition ;
- résumé factuel de 100 à 160 mots par article ;
- lien canonique et date vérifiés ;
- distinction claire entre faits, analyse et intérêt pour le SNUM ;
- aucun contenu inventé à partir d’un titre ou d’un extrait incomplet ;
- signalement des contenus payants ou inaccessibles ;
- aucune publication d’une ressource interne sans autorisation explicite.
