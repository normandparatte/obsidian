---
share: "true"
tags:
  - Informatique
  - Développement
  - CSS
  - Web
---

Tout d'abord, définir un conteneur contenant tout nos éléments à mettre sous forme de grille :
```html
<div class="conteneur">
    <div class="box">🐸 Élément 1</div>
    <div class="box">🦊 Élément 2</div>
    <div class="box">🦄 Élément 3</div>
    <div class="box">🐶 Élément 4</div>
    <div class="box">🐨 Élément 5</div>
    <div class="box">🐒 Élément 6</div>
    <div class="box">🦆 Élément 7</div>
    <div class="box">🐙 Élément 8</div>
    <div class="box">🐋 Élément 9</div>
</div>
```
 
Afin de pouvoir gérer chaque élément individuellement, si besoin, mettre une classe spécifique sur les éléments :
```html
 <div class="conteneur">
    <div class="box une">🐸 Élément 1</div>
    <div class="box deux">🦊 Élément 2</div>
    <div class="box trois">🦄 Élément 3</div>
    <div class="box quatre">🐶 Élément 4</div>
    <div class="box cinq">🐨 Élément 5</div>
    <div class="box six">🐒 Élément 6</div>
    <div class="box sept">🦆 Élément 7</div>
    <div class="box huit">🐙 Élément 8</div>
    <div class="box neuf">🐋 Élément 9</div>
</div>
```

## Propriétés du conteneur
### display: grid
Pour indiquer que le conteneur réagit comme **une grille**, il faut utiliser la propriété : **display: grid;**
### grid-template-columns et  grid-template-rows
Pour définir le nombre et la taille des colonnes et des lignes, il faut utiliser les propriétés **grid-template-columns** et  **grid-template-rows**.
Le nombre de valeurs pour les propriétés des colonnes et des lignes définissent respectivement le nombre de colonnes et de lignes.

### gap (espacement)
Comme pour les flexbox, un espacement constant peut être mis en place via la propriété **gap**

### Unité fr (fraction units)
A cause des espacements et marges entre les éléments de la grille il n'est pas facile ou aisé d'utiliser des pourcentages.
C'est pourquoi pour définir des parts de largeur dans les colonnes, il faut utiliser l'unité des fraction units soit "fr".

### Exemple complet
Voici le code pour une grille avec une colonne centrale deux fois plus grande que les autres colonnes (dont la hauteur des lignes change) et avec un espacement :
```css
.conteneur {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    grid-template-rows: 50px 100px 200px;
    grid-gap: 10px;
}
```

## Propriété d'un élément
En ayant défini des classes distinctes pour chaque élément, il est possible de définir une taille précise.
Pour cela, il faut indiquer un point de départ et d'arrivée (colonnes et lignes) grâce à **grid-column-start**, **grid-column-end**, **grid-row-start** et **grid-row-end**.

### Exemples
Par exemple, pour une grille avec trois colonnes, voici le code pour que l'élément 1 prenne toute la largeur :
```css
.une {
    grid-column-start: 1;
    grid-column-end: 4;
}
```
Ce code peut être abrégé :
```css
.une {
    grid-column: 1 / 4;
}
```
**Attention :** Le grid grid-column-end est bien a **4** car il faut indiquer l'élément avant lequel il faut s'arrêter (donc colonne de fin +1).

Voici le code pour un élément qui commence sur la **ligne** 2 et fini sur la ligne 3 :
```css
.deux {
    grid-row-start: 2;
    grid-row-end: 4;
}
```
Ce code peut être abrégé :
```css
.deux {
    grid-row: 2 / 4;
}
```
**Attention :** De même que grid-column-end, la valeur est bien à 4 car il faut indiquer l'élément avant lequel il faut s'arrêter (donc ligne de fin +1).

## Sources
Openclassroom : https://openclassrooms.com/fr/courses/1603881-creez-votre-site-web-avec-html5-et-css3/8061410-decouvrez-les-bases-de-css-grids



























