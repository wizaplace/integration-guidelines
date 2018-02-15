# Guidelines d'intégration

## Généralités

Le code doit être écrit en anglais. Cela inclut : les variables, fonctions, noms de fichiers, commentaires, ID et classes HTML, etc.

Exemples : `product` pour produit, `basket` pour panier, etc.

## Conventions de nommage

### Vocabulaire

Afin d'éviter l'utilisation de termes différents pour représenter la même chose, voici la liste des termes à utiliser :

- Pour les produits : `product`
- Pour les produits apparaissant dans une carte (recherche, etc.) : `product-card`
- Pour les commandes : `order`
- Pour les paniers : `basket` (ne pas utiliser `cart`)
- Pour l'espace "Mon compte" (aka "Mon profil") : `profile` (ne pas utiliser `account`)

### Fichiers

Les règles ci-dessous s'appliquent aux fichiers suivant :

- templates Twig
- fichiers Less/CSS
- fichiers JS
- assets (images, fonts, etc.)

Les noms doivent être écrit en minuscules, les noms composés doivent être séparés par des tirets (exemple : `product-card.html.twig`).

Le nom d'un template qui affiche une ressource précise doit être le même que celui de la ressource. Exemples :

- le template de la page de présentation d'un 'produit' doit s'appeller `product.html.twig`
- le template de la page 'panier' doit s'appeller `basket.html.twig`

### HTML/Less/CSS

Les nom des classes et id doivent être en minuscule. Les mots composés sont séparés par des tirets.

## Git et GitHub

Le code est hébergé sur GitHub et doit donc être livré via git et GitHub.

Les fichiers suivants ne doivent pas être commités sur le repository git :

- assets de production minifiés (CSS, JS, etc.)
- dépendances PHP, JS, etc. (les dépendances doivent être installées avec l'outil approprié : NPM ou Composer)
- fichiers de configuration de l'IDE (dossier PhpStorm, Netbeans ou autre)

Si nécessaire il est possible de les ajouter au fichier `.gitignore` pour ne pas avoir de problèmes.

## HTML/Less/CSS

Nous utilisons Less afin d'écrire le style du site. Aucun style doit être écrit en CSS directement.

### Structure de page

La structure de la page doit être basée sur [la grille Bootstrap](https://getbootstrap.com/docs/3.3/css/#grid). Afin d'exploiter correctement cette grille, il faut respecter les règles suivantes :

- ne pas surcharger les `margin` ou `padding` des classes `container`, `row` ou colonnes (`col-*`)
- ne pas utiliser des `row` ou colonnes (`col-*`) en dehors d'un `container`
- toute colonne (`col-*`) doit être directement dans un div de type `row`

### Variables

Les couleurs principales du site doivent être définies dans des variables Less afin de ne pas être dupliquées plusieurs fois.

Pour personnaliser l'apparence des composants Bootstrap, il est nécessaire de surcharger en priorité les variables définies par Bootstrap. Voir : [la liste des variables Bootstrap](https://getbootstrap.com/docs/3.3/css/#less-variables).

### Bootstrap

Bootstrap fournit [une base de composant standards](https://getbootstrap.com/docs/3.3/components/) : boutons, formulaires, tables, modals, etc.

Préférer la réutilisation des composants standards plutôt que de créer des nouvelles classes CSS lorsque cela peut être évité.

Exemples :

- utiliser le bouton standard (`btn btn-default`) autant que possible
- utiliser [les titres standards](https://getbootstrap.com/docs/3.3/css/#type) autant que possible plutôt que de créer des classes spécifiques

### Dépendances

Installer les dépendances avec NPM via le fichier `package.json`.

## JavaScript

Le code JavaScript se base sur 2 frameworks différents selon l'usage :

- VueJS lorsqu'il s'agit de dynamiser une partie de page entière (par exemple la recherche)
- jQuery lorsqu'il s'agit d'introduire un comportement très précis et ponctuel

Il est préférable d'éviter de mélanger l'utilisation des 2 frameworks dans la mesure du possible.

## Templates

### Traductions

Tous les textes du site doivent être gérés via des traductions du système de traduction Symfony. Ne pas inclure de texte directement dans les templates.

Les traductions sont définies dans le fichier `src/AppBundle/Resources/translations/messages.fr.json`.

## Assets

### Fonts

Les polices de caractères doivent être stockée dans le repository git. Ne pas utiliser de CDN.

### Icones

Dans le cas où les icones d'un projet ne sont pas issues d'une bibliothèque spécialisée (ex. Bootstrap, font-awesome, icomoon), il faut les convertir en font.

La web app du site [icomoon.io](https://icomoon.io/app) permet d'effectuer cette opération. L'intérêt ici est de bénéficier des avantages des fonts par rapport à l'utilisation d'images (font-size, color, fond transparent, etc.).

### Images

Les images doivent être enregistrées dans un format compatible web, avec des dimensions appropriées.

## PHP

La réalisation de sites fronts en se basant sur le StarterKit ne nécessite pas énormément de développements PHP. En effet le StarterKit fournit une base d'application fonctionnelle. Cependant certaines fonctionnalités ne sont pas implémentées dans le StarterKit et peuvent nécessiter du développement PHP/Symfony.

Dans les contrôleurs il est nécessaire de minimiser le nombre d'appels à l'API Wizaplace afin de ne pas allonger les temps de chargement des pages. Dans un cas normal nous visons 1 ou 2 appels API par page. Une stratégie pour éviter trop d'appels API dans les contrôleurs PHP est de déplacer certains chargements en AJAX, par exemple des mises en avant de produits sur la page d'accueil.

Le code PHP doit respecter [le standard de code](https://github.com/wizaplace/php-coding-standard) basé sur PSR-2 et le standard Symfony.

## Composants

### Carousel

Afin de rester homogène entre les différents projets, nous utilisons systématiquement la bibliothèque [slick.js](https://github.com/kenwheeler/slick/) pour tous les éléments de type carousel.
[Voir démo et utilisation de la bibliothèque](http://kenwheeler.github.io/slick#demos)

### Product card

La "Product card" est l'ensemble des éléments d'un produit présenté à l'internaute lors d'un affichage en mode grille ou liste.

Elle comprend généralement l'image principale du produit, son nom, son prix, les différents bandeaux de mise en avant ('Promotion', 'Nouveauté') et un bouton de mise au panier. D'autres éléments peuvent être ajoutés en fonction des besoins du client, par exemple la catégorie du produit ou encore sa description.

Exemple de code html :

```html
<article class="product-card" data-id="{{ product.id }}">
    {# flags #}
    <div class="flags">
        <div class="promo">Promotion</div>
        <div class="new">Nouveauté</div>
    </div>

    {# main image #}
    <div class="image">
        <img src="/crayon-laser.jpg" alt="Decription de l'image">
    </div>

    {# product details #}
    <div class="name">Crayon laser</div>
    <div class="description">Mieux que le tournevis sonique du docteur Who.</div>
    <div class="price">159,99€ TTC</div>

    <button class="add-to-basket"><i class="icon icon-basket"></i></button>
</article>
```

A noter :

- la classe `add-to-basket` du bouton et l'attribut `data-id` de l'élément `article` sont utilisés par javascript pour mettre à jour le panier.

- dans l'éventualité où le produit n'a pas d'image, on remplace l'élément `<img>` par : `<div class="no-image">Pas d'image</div>`.

Le style de cet élément doit alors avoir une dimension et un aspect semblables à l'emplacement qu'aurait dû occuper l'image.

### Menu principal

Le menu principal présente en général le menu des catégories et les liens vers les pages importantes.

### Recherche

La recherche est implémentée entièrement en VueJS et basées sur l'API de recherche.

L'appel à notre API de recherche se fait via la classe JavaScript `SearchClient` incluse dans le StarterKit.

Le comportement de la page recherche est standardisé entre nos marketplaces, il faut conserver ce comportement sauf si instruction contraire donnée par Wizaplace. Cela inclut par exemple :

- le comportement des facettes et filtres
- le stockage des filtres de recherche dans l'URL et le chargement de ceux-ci
- le comportement des filtres prix et géolocalisation (si ils existent dans les maquettes)

