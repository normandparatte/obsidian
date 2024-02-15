---
share: "true"
tags:
  - Informatique
  - Développement
  - Web
  - CSS
---

## Propriété display
Il est possible de changer le type d'un élément vers un autre (inline ou block).
Par exemple pour un lien qui est normalement de type inline, nous pourrions le définir de type block. voici le code css relatif :
```html
a {
    display: block;
}
```
Il devient donc possible de modifier les dimensions des liens avec cet exemple.

### inline-block
Il est également possible d'attribuer le display **inline-block** afin que l'élément soit de type inline mais puisse être dimensionné (par exemple via un width) comme un block.

### none (cacher un élément)
Il est également possible de cacher un élément en attribuant le display none. Dans cet exemple les div avec la classe "secret" ne seront pas affichées : 
```html
div.secret {
    display: none;
}
```

## Propriété position
Le navigateur dispose les éléments afin qu'ils ne se superposent jamais. Ils font partie d'un flux normal. Cependant, il peut être necéssaire de changer le flux normal, par exemple pour afficher le menu, un bouton retour en haut de la page, etc.
Pour cela il existe plusieurs types de positionnements détaillés ci-dessous.

### Positionnement relatif (position: relative)
Le positionnement relatif permet d'effectuer des ajustements : l'élément est décalé par rapport à sa position initiale.
Quatre propriétés CSS permettent de définir le décalage depuis le point d'origine :
- left
- right
- top
- bottom

Par exemple, voici le code pour décaler les liens depuis le haut et la gauche (donc contre le bas et la droite) :
```html
a {
    position: relative;
    top: 6px;
    left: 10px;
}
```

### Positionnement absolu (position: absolute)
Le positionnement absolu permet de placer un élément n'importe où sur la page.
Par exemple ce code, affichera le lien en haut à gauche de la page :
```html
a {
    position: absolute;
    top: 6px;
    left: 10px;
}
```

#### Position par rapport à un autre élément
Les éléments ne se place pas forcément selon les bords de la page. En effet, Un élément absolute va se positionner par rapport au **premier élément** qu'il rencontre dans ses parents, et qui **utilise lui-même la propriété position** . Pour **placer un élément par-dessus un autre**, il faut donc que ce premier élément utilise aussi la propriété position.

Voici un exemple concret : https://codepen.io/nicolaspatschkowski/pen/QWrMwXP?editors=1100
Dans cet exemple si on enlève la position relative du parent, le titre en position absolu se positionne en fin de page et non par rapport à la bannière.

### Position unset (Réinitialiser la position)
La position unset permet d'annuler le positionnement pour un élément donné (combinaison de initial et inherit). Ce mot-clé réinitialise la propriété afin que sa valeur soit la valeur héritée depuis l'élément parent ou soit la valeur initiale (s'il n'y a pas d'héritage).

Source : https://developer.mozilla.org/fr/docs/Web/CSS/unset

### Bloquez un élément (fixed ou sticky)
Le principe est le même que pour le positionnement absolu à l'exception que l'élément reste figé au même endroit même si on descend plus bas dans la page.

Voici un code pour exemple :
```html
.sticky {
  position: sticky;
  background-color: #C2B0F9;
  margin: auto;
  top: 0;
}

.fixed {
  position: fixed;
  background-color: #CBFCB9;
  top: 0;
  left: 0;
}
```

#### Différence entre fixed et sticky
L'élément fixed reste toujours fixé sur la page tandis que sticky reste fixé uniquement quand il arrive en haut de la page via le scroll.

Voici l'exemple concret de ces deux éléments (réduire la fenêtre afin de pouvoir scroller assez) : https://codepen.io/nicolaspatschkowski/pen/dyezoyV?editors=1100

### z-index
Etant donné que certains éléments peuvent se **chevaucher**, il existe la **propriété z-index** qui  permet de définir l'**ordre de profondeur** des éléments.
L'élément ayant la valeur de z-index la **plus élevée** sera placé **par-dessus** les autres.
Par exemple, voici trois éléments en position absolute (par rapport au conteneur comme il a lui-même un attribut position).
Dans cet exemple, l'élément trois est placé en fond, suivi de deux et pour finir un est au premier plan :

```html
.conteneur {
    position: relative;
    height: 300px;
    width: 300px;
}

.une {
    background-color: #C2B0F9;
    position: absolute;
    left: 0;
    top: 90px;
    z-index: 300;
}

.deux {
    background-color: #CBFCB9;
    position: absolute;
    right: 70px;
    top: 0;
    z-index: 200;
}

.trois {
    background-color: #F2A3BB;
    position: absolute;
    right: 0;
    bottom: 20px;
    z-index: 100;
}
```

## Sources
Fiche basée sur le tutoriel OpenClassrooms : https://openclassrooms.com/fr/courses/1603881-creez-votre-site-web-avec-html5-et-css3/8061421-abordez-dautres-techniques-de-mise-en-page