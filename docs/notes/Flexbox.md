---
share: true
tags:
  - Informatique
  - Développement
  - CSS
  - Web
---

Flexbox est une manière plus moderne afin de mettre en page des éléments que l'ancienne méthode float (bien que pour certains cas précis, float peut toujours être utilisé).

## Utilisation
Utiliser un container contenant les éléments :
```html
<div class="container">
<div class="element element1">Élément 1</div>
<div class="element element2">Élément 2</div>
<div class="element element3">Élément 3</div>
</div>
```

Propriété flex que l'on applique au conteneur :
```css
.container {
    display: flex;
}
```

## Récap des propriétés les plus utiles
- **flex-direction** - Donnez une direction
- **flex-wrap** - Retournez à la ligne
- **justify-content** - Alignement sur l'axe principal
- **align-items** - Alignement sur l'axe secondaire
- **align-content** - Alignement des blocs sur plusieurs lignes
- **gap** : Espace entre les éléments

## **flex-direction** (Donnez une direction)

Flexbox permet d'agencer ces éléments dans le sens que l'on veut. Avec **flex-direction**, on peut les positionner verticalement ou encore les inverser. Cette propriété CSS peut prendre les valeurs suivantes :
- **row**  : organisés sur une ligne (par défaut) ;
- **column**  : organisés sur une colonne ;
- **row-reverse**  : organisés sur une ligne, mais en ordre inversé ;
- **column-reverse**  : organisés sur une colonne, mais en ordre inversé.

Exemple :
```css
.container {
    display: flex;
    flex-direction: column;
}
```

## **flex-wrap** (Retournez à la ligne)

Par défaut, les blocs essaient de rester sur la même ligne s'ils n'ont pas la place, quitte à "s'écraser",  et provoquer parfois des anomalies dans la mise en page (certains éléments pouvant dépasser de leur conteneur). Si vous voulez, vous pouvez demander à ce que les blocs aillent à la ligne lorsqu'ils n'ont plus la place, avec flex-wrap.

Voilà les différentes valeurs de **flex-wrap** :
- **nowrap**  : pas de retour à la ligne (par défaut) ;
- **wrap**  : les éléments vont à la ligne lorsqu'il n'y a plus la place ;
- **wrap-reverse**  : les éléments vont à la ligne, lorsqu'il n'y a plus la place, en sens inverse.

Exemple :
```css
.container {
    display: flex;
    flex-wrap: wrap;
}
```

## Alignez les éléments sur un axe

Les éléments sont organisés par défaut de manière horizontale. Mais ils peuvent être organisés de manière verticale. Selon le choix que vous faîtes, ça va définir ce qu'on appelle l'axe principal. Il y a aussi un axe secondaire :
- si vos éléments sont organisés horizontalement, l'axe secondaire est l'axe vertical
- si vos éléments sont organisés verticalement, l'axe secondaire est l'axe horizontal

### **justify-content** (Axe principal)

Pour changer leur alignement, on va utiliser **justify-content**, qui peut prendre ces valeurs :
- **flex-start**: alignés au début (par défaut) ;
- **flex-end**: alignés à la fin ;
- **center**: alignés au centre ;
- **space-between**: les éléments sont étirés sur tout l'axe (il y a de l'espace entre eux) ;
- **space-around**: idem, les éléments sont étirés sur tout l'axe, mais ils laissent aussi de l'espace sur les extrémités.

Exemple :
```css
.container {
    display: flex;
    justify-content: flex-start:
}
```

Exemple en ligne : https://codepen.io/nicolaspatschkowski/pen/OJZgZqB?editors=1100

### **align-items** (Axe secondaire)

Si nos éléments sont placés dans une direction horizontale (ligne), l'axe secondaire est... vertical. Et inversement : si nos éléments sont dans une direction verticale (colonne), l'axe secondaire est horizontal.

La propriété **align-items** permet de changer leur alignement sur l'axe secondaire, grâce aux valeurs :
- **stretch**: les éléments sont étirés sur tout l'axe (valeur par défaut) ;
- **flex-start**: alignés au début ;
- **flex-end**: alignés à la fin ;
- **center**: alignés au centre ;
- **baseline**: alignés sur la ligne de base (semblable à flex-start).

Exemple :
```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

Le **centrage vertical et horizontal** peut être obtenu très facilement :
```css
.container {
    display: flex;
}

.element {
    margin: auto;
}
```

## **align-content** (Blocs sur plusieurs lignes)

Si vous avez **plusieurs lignes** dans votre Flexbox, vous pouvez choisir comment celles-ci seront réparties avec align-content.

Voyons voir comment les lignes se répartissent différemment avec la nouvelle propriété **align-content** que je voulais vous présenter. Elle peut prendre ces valeurs :
- **stretch** (par défaut) : les éléments s'étirent pour occuper tout l'espace ;
- **flex-start** : les éléments sont placés au début ;
- **flex-end** : les éléments sont placés à la fin ;
- **center** : les éléments sont placés au centre ;
- **space-between** : les éléments sont séparés avec de l'espace entre eux ;
- **space-around** : idem, mais il y a aussi de l'espace au début et à la fin.

## Modification d'un élément précis

### order
Parfois, inverser l'ordre de la rangée ou la colonne ne suffit pas. Dans ces cas, on peut appliquer la propriété order à des éléments individuels. Par défaut, les éléments ont une valeur de 0, mais on peut utiliser cette propriété pour changer la valeur à un entier positif ou négatif.

Exemple :
```css
.element2 {
    order:-3;
}
```

### align-self
Cette propriété accepte les mêmes valeurs que align-items, mais s'applique seulement à l'élément ciblé.

## Jeu pour s'entraîner
Avec les différentes propriétés, il faut replacer les grenouilles sur les nénuphars : https://flexboxfroggy.com/#fr

## Sources
Fiche basée sur le tutoriel OpenClassrooms : https://openclassrooms.com/fr/courses/1603881-creez-votre-site-web-avec-html5-et-css3/8061384-faites-votre-mise-en-page-avec-flexbox