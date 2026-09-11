# Post-mortem - rendu illisible de « L’essentiel »

Date de l’incident : 11 septembre 2026  
Dépôt : `bacoco/revue-presse-snum`  
Page concernée : page d’accueil et archive du 11 septembre 2026

## Résumé

L’édition a été publiée puis diffusée alors que les trois cartes de « L’essentiel » étaient presque illisibles. Chaque carte n’occupait qu’environ un tiers de sa propre colonne. Les lignes devenaient extrêmement étroites et les mots se cassaient verticalement.

La publication et l’envoi auraient dû être bloqués. Les contrôles automatisés avaient été exécutés, mais aucune inspection visuelle réelle de la page n’avait été faite avant l’envoi.

## Impact

- Page publique difficilement lisible.
- Lien envoyé vers une édition présentant ce défaut.
- Nécessité de plusieurs correctifs publics successifs.
- Perte de confiance dans le garde-fou annoncé.
- Aucun second courriel n’a été envoyé après la correction.

## Cause technique

La grille `.top-grid` utilisait CSS Grid avec trois pistes d’environ 392 px. Ses enfants conservaient simultanément les classes DSFR `fr-col-12 fr-col-md-4`.

À partir du point de rupture desktop, le DSFR appliquait aux enfants :

- une base flexible de 33,3333 % ;
- une largeur ou largeur maximale équivalente.

Cette largeur était calculée à l’intérieur de chaque piste CSS Grid. Les cartes mesuraient donc environ 131 px au lieu de 392 px et atteignaient environ 10 674 px de hauteur.

Un second conflit concernait l’ordre flex interne des cartes DSFR. Les paragraphes personnalisés sans ordre explicite passaient avant le titre et le résumé. « À retenir » apparaissait ainsi avant le titre, contrairement à l’ordre éditorial attendu.

## Pourquoi les contrôles n’ont pas détecté le défaut

Les vérifications se limitaient principalement à :

- la présence des éléments ;
- le nombre de `h1` ;
- les accès rapides ;
- les liens et attributs de sécurité ;
- l’absence de débordement horizontal global ;
- la présence de `auto-fit/minmax`, `min-width: 0` et `overflow-wrap`.

Ces tests étaient vrais mais insuffisants. La page n’avait pas de débordement horizontal précisément parce que le contenu se cassait dans des colonnes minuscules. Le contrôle de la largeur totale de la page a donc donné un faux sentiment de sécurité.

Aucune capture de la section « L’essentiel » n’avait été examinée avant l’envoi. La validation annoncée comme visuelle ne l’était pas réellement.

## Corrections

1. Neutralisation ciblée des contraintes de largeur DSFR sur les enfants directs de `.top-grid`.
2. Conservation des classes DSFR dans le HTML, avec surcharge limitée au composant éditorial.
3. Largeur des trois cartes portée d’environ 131 px à environ 392 px sur le bureau testé.
4. Hauteur ramenée d’environ 10 674 px à environ 1 238 px.
5. Ordre visuel explicite : tag, source/date, titre, résumé, « À retenir », « Intérêt pour le SNUM », lien.
6. Ajout de `word-break: break-word` en complément de `overflow-wrap`.
7. Versionnement de l’URL de `styles.css` pour empêcher le cache GitHub Pages de conserver l’ancienne feuille.
8. Correction du compteur d’articles affiché, de 11 à 12.
9. Vérification par capture réelle de la page GitHub Pages corrigée.
10. Aucun nouvel envoi de courriel.

## Preuves après correction

Sur la page publique contrôlée :

- trois cartes alignées horizontalement ;
- largeur mesurée : environ 392 px par carte ;
- hauteur mesurée : environ 1 238 px ;
- largeur du document égale à celle de la zone d’affichage, sans débordement horizontal ;
- feuille chargée : `styles.css?v=900a347` ;
- ordre calculé des éléments : 1 à 7, conforme à l’ordre éditorial ;
- compteur affiché : 12 articles.

Commits correctifs principaux :

- `70051d941f5718287f06e8331129cccd596b1dd8` - neutralisation de la largeur DSFR ;
- `900a3476b0fc0c177f45be6b905da12e0a28dc63` - ordre de lecture ;
- `313faaf41e10276e30b17ceb30634fbfba5eb6c3` et `62109ec86bb4238754ba8a53bd0d06e244d8583b` - activation initiale du correctif ;
- `9af7f19075d64eeef42823bc1e6f7b023f812011` et `126f8058175f52d59856554a13e04678f3f951b5` - activation de l’ordre corrigé.

## Prévention

La planification a été modifiée pour imposer deux barrières visuelles :

### Avant publication

Le candidat doit être rendu dans un navigateur réel et examiné à partir de captures desktop, mobile et zoom 200 %. Les largeurs, hauteurs et styles calculés des cartes doivent être contrôlés. L’indisponibilité d’un navigateur produit `VISUAL_PREFLIGHT_UNAVAILABLE` et interdit commit, publication et envoi.

### Après déploiement

La page GitHub Pages réellement servie doit être ouverte avec Agent Browser. La feuille CSS effectivement chargée, l’ordre vertical, les dimensions et les captures doivent être revérifiés. Tout échec interdit le courriel.

Un contrôle anti-doublon arrête aussi l’exécution avec `ALREADY_COMPLETE` lorsqu’une édition de la date courante existe déjà.

## Planification

L’exécution inutile du vendredi 11 septembre à 8 h a été neutralisée. La prochaine occurrence est fixée au mardi 15 septembre 2026 à 8 h, fuseau Europe/Paris. La récurrence mardi et vendredi est conservée.
