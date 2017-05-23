# Guidelines d'intégration

## Généralités

Les noms des fichiers, les commentaires, les feuilles de style, fonctions, etc. doivent être en anglais.
Exemples: `product` pour produit, `basket` pour panier, etc.

## Conventions de nommage

Les nom des classes et id doivent être en minuscule.
Les mots composés sont séparés par des tirets.
Les noms composés des templates twig sont également séparés par des tirets.

Le nom d'un template qui affiche une ressource précise doit être le même que celui de la ressource.
Exemples :
- le template de la page de présentation d'un 'produit' doit s'appeller `product.html.twig`
- le template de la page 'panier' doit s'appeller `basket.html.twig`

## Chargement des bibliothèques

Toutes les bibliothèques tierces doivent être téléchargées en local.
Pour Bootstrap, cela permettra notamment de surcharger les variables Less.

## Carousel

Afin de rester homogène entre les différents projets, nous utilisons systématiquement la bibliothèque [slick.js](https://github.com/kenwheeler/slick/) pour tous les éléments de type carousel.
[Voir démo et utilisation de la bibliothèque](http://kenwheeler.github.io/slick#demos)

## Fonts

Les polices de caractère doivent également être téléchargée en local.

### Icones

Dans le cas où les icones d'un projet ne sont pas issues d'une bibliothèque spécialisée (ex. Bootstrap, font-awesome, icomoon), il faut les convertir en font.
La web app du site [icomoon.io](https://icomoon.io/app) permet d'effectuer cette opération.
L'intérêt ici est de bénéficier des avantages des fonts vs des images (font-size, color, fond transparent, etc.).

## Composants
### Product

La Product card est l'ensemble des éléments d'un produit présenté à l'internaute.
Elle comprend généralement l'image principale du produit, son nom, son prix, les différents bandeaux de mise en avant ('Promotion', 'Nouveauté') et un bouton de mise au panier.
D'autres éléments peuvent être ajoutés en fonction des besoins du client, par exemple la catégorie du produit ou encore sa description.

Exemple de code html :

```html
<article class="product" data-id="1_23">
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

- la classe `add-to-basket` et l'attribut `data-id` de l'élément bouton sont utilisés par javascript pour mettre à jour le panier.

- dans l'éventualité où le produit n'a pas d'image, on remplace l'élément `<img>` par : `<div class="no-image">Pas d'image</div>`.

Le style de cet élément doit alors avoir une dimension et un aspect semblables à l'emplacement qu'aurait dû occuper l'image.

### Menu principal

Le menu principal présente en général le menu des catégories et les liens vers les pages importantes.

## Bibliothèque Wizaplace

Afin de résoudre les questions qui reviennent pour chaque nouveau projet, la bibliothèque javascript Wizaplace fournit des outils simples qui peuvent venir en renfort de bibliothèques tierces comme Bootstrap.

### Reveal

Ce composant permet de cacher ou révéler un élément du DOM, un peu à la manière du composant 'dropdown' de Bootstrap.
Pour l'accessibilité, la valeur de l'attribut `aria-expanded` est mise à jour automatiquement en fonction de l'état de l'élément à cacher/révéler.
Il s'utilise de manière similaire aux composants de Bootstrap de type 'dropdown' mais propose plus d'options.
Il permet de choisir l'évènement déclencheur ("click" ou "hover") et il est également possible de paramétrer l'effet d'apparition/disparition de l'élément concerné.
```html
<div class="reveal">
    <a href="#" class="reveal-pop" aria-haspopup="true" aria-expanded="false" id="demo-id">Mon compte</a>    
    <div class="reveal-content" aria-labelledby="quick-access-user">Contenu caché par défaut.</div>
</div>
```

Pour que le système soit déclenchable, il faut minimum que :
- l'élément parent aie la classe `.reveal`,
- l'élément déclencheur aie une classe `.reveal-trigger`,
- l'élément à cacher/révéler aie la classe `.reveal-content`.

#### Les effets visuels
L'apparition du contenu peut prendre **plusieurs aspects** :
- le contenu apparaît **instantanément** (`.reveal-pop`),
- le contenu apparaît **progressivement** (`.reveal-fade`),
- le contenu apparaît progressivement **vers le bas** (`.reveal-down`),  
- le contenu apparaît progressivement et **cache les autres éléments** visibles du groupe (`.reveal-accordion`).

La classe correspondant à l'effet choisi doit être appliquée à l'élément parent du groupe (`.reveal`), par exemple `.reveal-down` :
```html
<div class="reveal reveal-down">
    <a href="#" class="reveal-pop"> [...]</a>
</div>
```

Si aucune de ces classes n'est appliquée en supplément de `.reveal`, alors **l'effet par défaut est `.reveal-pop`**.
Ce comportement est paramétrable de manière globale sur chacun des types d'évènement déclencheur, en modifiant le fichier `config.js` de la bibliothèque Wizaplace.

Les vitesses des effets de type `fade`, `down`, `accordion` sont également paramétrables via le fichier `config.js` de la bibliothèque Wizaplace.
L'unité de mesure de ces vitesses est la milliseconde.

#### Les évènements déclencheurs

Deux évènements peuvent **déclencher** l'apparition ou la disparition du contenu du groupe :
- au **clic** (`.reveal-click`) sur l'élément déclencheur (`.reveal-trigger`),
- au **survol** (`.reveal-hover`) de ce même élément.

La classe correspondant à l'évènement choisi doit être appliquée à l'élément déclencheur du groupe (`.reveal-trigger`), par exemple `.reveal-hover` :
```html
<div class="reveal">
    <a href="#" class="reveal-trigger reveal-hover" aria-haspopup="true" aria-expanded="false" id="demo-id">Mon compte</a>    
    [...]
</div>
```
Si aucune de ces classes n'est appliquée en supplément de `.reveal-trigger`, alors **l'évènement déclencheur par défaut est `.reveal-click`**.
Ce comportement est paramétrable de manière globale sur chacun des types d'effet, en modifiant le fichier `config.js` de la bibliothèque Wizaplace.
