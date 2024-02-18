---
share: true
tags:
  - Informatique
  - Développement
  - Web
  - Javascript
---
[[To do|To do]] faire le tour du cours gitbook
[[To do|To do]] JSHint

## Déclaration
Dans une balise script.
Mettre le code dans un fichier séparer grâce à l'attribut src :
```javascript
<script src="./js/script.sj"/></script>
```
Mettre la balise juste avant la fin du body sinon on ne peut pas utiliser les éléments du  DOM (par exemple via un querySelector).

```javascript
console.log()
```
Permet d'afficher un élément dans la console notamment pour debugger.

Pour indiquer au navigateur de ne pas corriger automatiquement les petites erreurs, il est possible d'utiliser la commande use strict en début de fichier.
```javascript
"use strict";
```
Ce use strict permet par exemple d'indiquer qu'une variable n'a pas été déclarer, etc. Ceci permet d'être plus précis et éviter des erreurs d'interprétation du navigateur.

Des **commentaires** peuvent être ajoutés grâce à // ou /* */.
```javascript
//initialize buttons

/*
  initialize buttons
*/
```

## Généralités
### Variables
#### Conventions
- Nom des variables en camelCase :  nomClient
- Une variable doit porter un nom représentatif de ce qu'elle contient
- majuscule les constantes contenant des valeurs : const AGE_MAX = 33; 
- minuscule les constantes contenant des références  : const ids = [12, 44];

Les variables JavaScript ne sont pas typées ! On peut donc initialiser une variable avec un entier puis lui affecter une chaîne de caractères sans déclencher d’erreur.

#### let et var
**let** pour déclarer les variables (remplace **var** qui posait des problèmes notamment pour le debuggage).
**let** permet de déclarer une variable dont la portée est celle du bloc courant.
**var**  quant à lui, permet de définir une variable globale ou locale à une fonction (sans distinction des blocs utilisés dans la fonction) :

```javascript
// Avec var
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // c'est la même variable !
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

// Avec let
function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // c'est une variable différente
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
```

Les variables peuvent être directement initilalisées. Exemple :
```javascript
let gold=50;
```

#### const
**const** pour déclarer les constantes notamment si on récupère des éléments du DOM via un querySelector.

```javascript
// Variables
var personneNom = "Dinateur";
let personneAge = 22;

// Constantes
const URL = "http://kode.ch";
const AGE_MAX = 65;
const langues = ['FR','EN'];
const personne = { age: 20 };
```

#### Tableaux
Les variables peuvent contenir **plusieurs éléments** en utilisant un **tableau** :
```javascript
let inventory = ["stick", "dagger", "sword"];
```

La propriété **length** permet de retourner le nombre d'éléments d'un tableau.
La fonction **shift** permet de **retirer** et de **retourner** le **premier** élément d'un tableau 
#### Objets
Des objets peuvent être créés et contenir autant de propriétés que nécessaires. Les valeurs peuvent être des fonctions comme goStore, goCave et fightDragon dans cet exemple :
```javascript
const locations = [
  {
    name: "town square",
    "button text": ["Go to store", "Go to cave", "Fight dragon"],
    "button functions": [goStore, goCave, fightDragon],
    text:"You are in the town square. You see a sign that says \"Store\"."
  }
];
```

### Fonctions

En JS, les fonctions sont la base de toutes interactions.
Des fonctions peuvent être définies à l'aide du mot clé function.
Si on ne spécifie pas de valeur de retour à une fonction, elle retournera undefined.

```javascript
function citationLeia() {
  console.log("La force est forte en moi.");
}

// Affecte la fonction citationLeia() au click du bouton
document.querySelector("#button").addEventListener("click", citationLeia);
```
En JavaScript, afin d'**affecter la fonction** bonjour() et **non son résultat**, on n'ajoute pas les parenthèses après le nom de la fonction.
- Element.onclick = bonjour;  affecte la fonction bonjour().
- Element.onclick = bonjour();  affecte le **résultat** de la fonction bonjour().

#### Fonctions anonymes
En JavaScript, les fonctions sont des objets, on peut donc stocker des fonctions dans une variable.
Les fonctions peuvent être passées directement en paramètre d'une autre fonction.
Comme ces fonctions n'ont pas de nom, elles sont dites "anonymes" :
```javascript
// Variante avec fonction anonyme
document.querySelector("#button").addEventListener("click", function() {
  alert("Plutôt embrasser un Wookie");
});
```
Une fonction anonyme peut également être simplifié depuis ES6 (ECMAScript 6) en se passant du mot clé function (et des accolades s'il n'y a qu'une instruction).
```javascript
// Variante avec fonction fléchée (arrow function)
document.querySelector("#button").addEventListener("click", () => alert("Plutôt embrasser un Wookie"));
```

## Manipulation du DOM

Le DOM peut être manipulé directement en javascript en utilisant l'objet **document**.

### querySelector
Une méthode pour récupérer des éléments dans le DOM est **querySelector()**.
querySelector permet de récupérer le permier élément en utilisant les sélecteurs CSS.
Par exemple pour récupérer le premier h1 de la page :
```javascript
const h1 = document.querySelector("h1");
```
Pour récupérer la liste de tous les éléments correspondant aux sélecteurs spécifiés, il faut utiliser querySelectorAll à la place.
```javascript
const listeH1 = document.querySelectorAll("h1");
```

### innerText
**innerText**  est une propriété représentant le contenu textuel « visuellement rendu » d'un nœud. 
Proche de **textContent** qui retourne également le contenu des balises scripts et style.

Le contenu d'un balise (d'un noeud) peut donc être modifié à l'aide de innerText :
```javascript
function goTown() {
  button1.innerText = "Go to store";
  button2.innerText = "Go to cave";
  button3.innerText = "Fight dragon";
}
```

### Modification du css
Il est possible de changer le css directement en JS.
Pour ça, utiliser la propriété style d'un objet récupérer par un querySelector (ou plusieurs par un querySelectorAll) :
```javascript
const monsterStats = document.querySelector("#monsterStats");
monsterStats.style.display = "block";
```

## Ecouter des événements

Les événements permettent de déclencher une fonction pour une action spécifique, comme par exemple le clic ou le survol d'un élément, le chargement du document HTML ou encore l'envoi d'un formulaire.

Présentation des événements : https://divtec.gitbook.io/javascript/javascript/dom-introduction/evenements

Page complète de tous les événements : https://www.w3schools.com/jsref/dom_obj_event.asp

Il existe deux méthodes différentes pour écouter les événements, on-event et addEventListener.
Il vaut mieux utiliser **addEventListener** que on-event, car addEventListener() **permet d'ajouter plusieurs écouteurs pour un même événement** sur un même élément. Cela est utile pour les bibliothèques et les modules qui doivent pouvoir écouter les événements de manière indépendante.
De plus cette méthode est compatible avec les anciens navigateurs et est également plus performante (car elle utilise une API native au lieu d'une API spécifique à HTML comme on-event).

### on-event
Les gestionnaires d'événements "on-event" sont nommées selon l'événement lié : onclick, onkeypress, onfocus, onsubmit, etc. (voir la liste complète : https://www.w3schools.com/tags/ref_eventattributes.asp)

On peut scpécifier un "on-event" pour un événement particulier de différentes manières :
- Avec un attribut HTML : <button onclick="bonjour()">
- En utilisant la propriété correspondante en JavaScript : Element.onclick = bonjour;

Exemple de code :
```javascript
function citationLeia() {
  alert("Plutôt embrasser un Wookie");
}

// Affecte la fonction citationLeia() au click du bouton
document.querySelector('button').onclick = citationLeia;

// Variante avec fonction anonyme
document.querySelector('button').onclick = function() {
  alert("Plutôt embrasser un Wookie");
};

// Variante avec fonction fléchée (arrow function)
document.querySelector('button').onclick = () => alert("Plutôt embrasser un Wookie");
```

### addEventListener
La méthode addEventListener() permet de définir une fonction à appeler chaque fois que l'événement spécifié est détecté sur l'élément ciblé.
```javascript
ElementCible.addEventListener("nomEvenement", nomFonction);
```
```javascript
function citationLeia() {
  console.log("La force est forte en moi.");
}

// Affecte la fonction citationLeia() au click du bouton
document.querySelector("#button").addEventListener("click", citationLeia);

// Variante avec fonction anonyme
document.querySelector("#button").addEventListener("click", function() {
  alert("Plutôt embrasser un Wookie");
});

// Variante avec fonction fléchée (arrow function)
document.querySelector("#button").addEventListener("click", () => alert("Plutôt embrasser un Wookie"););
```

Il est également possible de supprimer l'écoute d'un événement en utilisant **removeEventListener**.
Il faut une commande removeEventListener pour chaque fonction que l'on souhaite retirer.

```javascript
myDIV.removeEventListener("mousemove", myFunction1);
myDIV.removeEventListener("mousemove", myFunction2);

// Simplifié par un tableau
myDIV.removeEventListener("mousemove", [myFunction1, myFunction2]);
```

Sinon il est possible de supprimer toutes les fonctions d'un événement donné grâce à la fonction **removeAllEventListeners**.
```javascript
myDIV.removeAllEventListeners("mousemove");
```

### Ajouter un événement à une liste d'éléments
```javascript
// Récupère tous les éléments de type button
const boutons = document.querySelectorAll("button");

// Parcours ces éléments et change la classe "rouge"
for (let bouton of boutons) {
   bouton.addEventListener("click", function(event) {
      bouton.classList.toggle("rouge");
   });
}
```

### event et target
Un objet event est automatiquement passé comme premier paramètre de la fonction affectée à un événement. Pour le récupérer il suffit d'ajouter un paramètre à la fonction liée. Le nom de ce paramètre est libre mais on le nomme régulièrement event ou plus simplement e.

On appelle "cible" l'objet ou 'élément qui a envoyé l'événement. Pour récupérer la cible on utiliser la propriété target de l'événement.

```javascript
<button>Bouton 1</button>
<button>Bouton 2</button>
<button>Bouton 3</button>

<script>
// Récupère les boutons du document
const boutons = document.querySelectorAll("button");
// Parcrours les boutons
for(let bouton of boutons){
  // Ajoute événement click avec une fonction avec paramètre event
  bouton.addEventListener("click", function(event) {
    // Récupère l'élément qui a envoyé l'événement, la cible
    let cible = event.target;
    // Modifie la taille du texte de la cible
    cible.style.fontSize = "2em";
});
}
</script>
```
## Divers
### Nombre aléatoire
L'objet Math en javascript contient des propriétés et méhtodes static concernant des fonctions mathématiques. Une de ces fonctions est **math.random()** qui retourne un nombre entre 0 (inclus) et 1 (exclu).
Voici donc comment l'utiliser :
```javascript
Math.floor(Math.random() * <NOMBRE_MAX>) + <NOMBRE_MIN>;
```
Voici un exemple pour avoir un nombre entre 1 (compris) et 5 (compris) :
```javascript
Math.floor(Math.random() * 5) + 1;.
```

## Sources
Cours javascript divtec : https://divtec.gitbook.io/javascript/
Tutoriel jeu rpg de https://www.freecodecamp.org/
Documentation W3School : https://www.w3schools.com/
Site de mozilla : https://developer.mozilla.org/fr/docs/Web/