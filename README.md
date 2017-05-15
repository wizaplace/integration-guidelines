# integration-guidelines

## Conventions de nommage

Les nom des classes et id doivent être en minuscule.
Les mots composés sont séparés par des tirets.

## Chargement des bibliothèques

Toutes les bibliothèques tierces doivent être téléchargées en local.
Pour Bootstrap, cela permettra notamment de surcharger les variables.


## Carousel :

Afin de rester homogène entre les différents projets, nous utilisons systématiquement la bibliothèque [slick.js](https://github.com/kenwheeler/slick/) pour tous les éléments de type carousel.
[Voir démo et utilisation de la bibliothèque](http://kenwheeler.github.io/slick#demos)

## Font icons :

Dans le cas où les icones d'un projet ne sont pas issues d'une bibliothèque spécialisée (ex. Bootstrap, font-awesome, icomoon), il faut les convertir en font.
La web app du site [icomoon.io](https://icomoon.io/app) permet d'effectuer cette opération.
L'intérêt ici est de bénéficier des avantages des fonts vs des images (font-size, color, fond transparent, etc.).


## Product :

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
- la classe `add-to-basket` et l'attribut `data-id` de l'émément bouton sont utilisés par javascript pour mettre à jour le panier.

- dans l'éventualité où le produit n'a pas d'image, on remplace l'élément `<img>` par : `<div class="no-image">Pas d'image</div>`.
Le style de cet élément doit alors avoir une dimension et un aspect semblables à l'emplacement qu'aurait dû occuper l'image.

## Menu principal

Le menu principal présente en général le menu des catégories et les liens vers les pages importantes.

### Menu des catégories
TODO: Créer un template de départ -> html / JS et LESS

## Structure des répertoires
TODO
