---
share: "true"
tags:
  - Développement
  - Informatique
  - Vuejs
---

Vue (/vjuː/ à prononcer comme en anglais: view) est un framework JavaScript qui se repose sur les standards HTML, CSS et JavaScript. Il propose une manière efficace de déclarer des composants pour la construction d'interfaces utilisateur, qu'elles soient simples ou complexes.

**Rendu déclaratif** : Vue s'appuie sur le standard HTML avec une syntaxe de type template qui permet de décrire de manière déclarative la structure HTML tout en étant basée sur un état JavaScript.
**Réactivité** : Vue traque automatiquement tout changement d'état JavaScript et met à jour efficacement le DOM en cas de changement.

## Options API ou Composition API
Choix : **Composition API**

Avec l'**API Options**, nous définissons la logique d'un composant en utilisant un objet d'options telles que data, methods, et mounted. Les propriétés définies par les options sont exposées sur this dans les fonctions, qui pointe sur l'instance du composant.
Avec l'**API de Composition**, nous définissons la logique d'un composant à l'aide de fonctions API importées. **Dans les SFC, l'API de Composition est généralement utilisée avec < script setup>**. L'attribut setup est une indication qui permet à Vue d'effectuer des transformations au moment de la compilation, ce qui nous permet d'utiliser l'API de Composition avec moins de code nécessaire aux déclarations.

L'API Options est centrée sur le concept d'une "instance de composant" tandis que l'API de Composition est centrée sur la déclaration de variables d'état réactives directement dans la portée d'une fonction, et sur la composition de l'état de plusieurs fonctions pour gérer la complexité.

Pour l'apprentissage, choisissez le style qui vous semble le plus facile à comprendre. La plupart des concepts fondamentaux sont partagés entre les deux styles. Vous pourrez toujours choisir l'autre style plus tard.

Exemple Composition API :
```js
<script setup>
import { ref } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Apprendre le HTML', done: true },
  { id: id++, text: 'Apprendre le JavaScript', done: true },
  { id: id++, text: 'Apprendre Vue', done: false }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>
```

Exemple Options API pour le même fonctionnement :
```js
<script>
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      hideCompleted: false,
      todos: [
        { id: id++, text: 'Apprendre le HTML', done: true },
        { id: id++, text: 'Apprendre le JavaScript', done: true },
        { id: id++, text: 'Apprendre Vue', done: false }
      ]
    }
  },
  computed: {
    // ...
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    }
  }
}
</script>
```

## HTML ou SFC

Choix : **SFC**

SFC regroupe html, css et js dans un même fichier vue.
la séparation des responsabilités ne signifie pas séparation des types de fichiers.
Dans le développement d'interfaces utilisateur modernes, nous avons constaté qu'au lieu de diviser la base de code en trois énormes couches qui s'entrecroisent, il est beaucoup plus logique de les diviser en composants faiblement couplés et de les composer. À l'intérieur d'un composant, son template, sa logique et ses styles sont intrinsèquement couplés, et leur regroupement rend le composant plus cohérent et plus facile à maintenir.

## réactif, texte dynamique (ref, {{ }})
```html
<script setup>
import { ref } from 'vue'

const counter = ref({ count: 0 })
const message = ref('Hello World!')
</script>

<template>
  <h1>{{ message }}</h1>
  <p>Count à: {{ counter.count }}</p>
</template>
```
ref créer un objet qui expose la valeur interne sous une propriété .value
A noter que la valeur (.value) est automatiquement récupérée dans le template.
Nous ne devons pas faire : ~~{{ message.value }}~~

Il est également possible d'utiliser une expression javascript :
```js
{{ message.split('').reverse().join('') }}
```

## Liaisons d'attributs (v-bind, :)
```html
<div v-bind:id="dynamicId"></div> -> abrégée <div :id="dynamicId"></div>
```

Exemple :
```html
<script setup>
import { ref } from 'vue'

const titleClass = ref('avertissement')
</script>

<template>
  <h1 :class="titleClass">Passez moi en rouge</h1>
</template>

<style>
.avertissement {
  color: orange;
}
.erreur {
  color: blue;
}
</style>
```

## Gestion des évènements (v-on, @)
```html
<button v-on:click="increment"></button> abrégé <button @click="increment"></button>
```

Exemple
```html
<script setup>
import { ref } from 'vue'

const count = ref(0)

// Incrémente jusqu'à 10 et recommence
function increment() {
  if(count.value<10){
  	count.value++; 
  }else{
    count.value=0;
  }
}
</script>

<template>
  <button @click="increment">count à: {{ count }}</button>
</template>
```

## Champs de formulaire (v-model)

Pour les champs de formulaire, par exemple un input, il faut :
- Lier l'attribut avec :id (v-bind:id)
- Utiliser l'événement de input via @input="onInput"
- Faire la fonction onInput pour réaffecter le text

La directive **v-model** permet de faire tout cela avec uniquement cette directive.

Voici l'exemple sans v-model :

```html
<script setup>
import { ref } from 'vue'

const text = ref('')

function onInput(e) {
  text.value = e.target.value
}
</script>

<template>
  <input :value="text" @input="onInput" placeholder="Tapez ici">
  <p>{{ text }}</p>
</template>
```

Puis le code refactorisé à l'aide de la directive :

```html
<script setup>
import { ref } from 'vue'

const text = ref('')
</script>

<template>
  <input v-model="text" placeholder="Tapez ici">
  <p>{{ text }}</p>
</template>
```
Tous les champs des formulaires sont simplifiés avec v-bind : https://fr.vuejs.org/guide/essentials/forms.html

## Rendu conditionnel (v-if, v-else)
Vue permet d'afficher un élément ou non à l'aide de la directive v-if et v-else.

```html
<script setup>
import { ref } from 'vue'

const awesome = ref(true)

function toggle() {
  awesome.value = !awesome.value
}
</script>

<template>
  <button @click="toggle">basculer</button>
  <h1 v-if="awesome">Vue est génial!</h1>
  <h1 v-else>Oh non 😢</h1>
</template>
```

## Parcours de liste (v-for)
La directive **v-for** est utilisé pour parcouris un tableau.
Un id doit être indiqué via **:key** afin de permettre à vue de retrouver le bon objet dans le tableau

```html
<li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
</li>
```

Exemple complet :
```html
<script setup>
import { ref } from 'vue'

// donne à chaque todo un id unique
let id = 0

const newTodo = ref('')
const todos = ref([
  { id: id++, text: 'Apprendre le HTML' },
  { id: id++, text: 'Apprendre le JavaScript' },
  { id: id++, text: 'Apprendre Vue' }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Ajouter une tâche</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>
```

## Propriétés calculées (computed)

Réactif à partir d'autres propriétés en utilisant l'option computed
Il est possible de **créer une réf calculée qui calcule sa .value en fonction d'autres sources de données réactives**.

Pour ça :
- import { ref, **computed** } from 'vue'
- Puis :
```html
const filteredTodos = computed(() => {
  // Retourne le calcul en fonction d'une autre source de donnée dans filteredTodos
})
```

Exemple complet :
```html
<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Apprendre le HTML', done: true },
  { id: id++, text: 'Apprendre le JavaScript', done: true },
  { id: id++, text: 'Apprendre Vue', done: false }
])

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
  
const filteredTodos = computed(() => {
  // retourne les todos filtrés en fonction de
  // `todos.value` et `hideCompleted.value`.
  
  	if(hideCompleted.value){
    	return todos.value.filter((t) => t.done == false;
    }else{
      return todos.value;
    }
  }                            
})
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Ajouter une tâche</button>
  </form>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Afficher toutes' : 'Cacher complétées' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
```
Pour finir, on change le for sur filteredTodos au lieu de todos

## Cycle de vie et refs de template

Différents cycle de vie : https://fr.vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram

Pour travailler manuellement avec le DOM, il faut mettre l'attribut spécial ref sur la balise :
```html
<p ref="pElementRef">hello</p>
```

Pour accéder à la ref, nous devons déclarer une référence avec le nom correspondant, initialisé à null :
```js
const pElementRef = ref(null)
```

La ref sera accessible seulement après être montée.
Voici le code pour récupérer cette ref via **this.$refs** :

```js
import { onMounted } from 'vue'

onMounted(() => {
  pElementRef.value.textContent = 'monté!'
})
```
## Observateurs (watch, watchEffect)

Nous pouvons réaliser, grâce a des observateurs, des **effets de bord de manière réactive** lors de changement (ajoute un propre comportement).

Voici l'exemple d'une fonction qui se déclenche lors du changement de la variable count.
```js
import { ref, watch } from 'vue'

const count = ref(0)

watch(count, (newCount) => {
  // oui, console.log() est un effet de bord
  console.log(`new count is: ${newCount}`)
})
```

Voici un autre exemple utilisant watch. Lorsque todoId est modifié, les données sont actualisées grâce à fetchData().
```html
<script setup>
import { ref, watch } from 'vue'

const todoId = ref(1)
const todoData = ref(null)

async function fetchData() {
  todoData.value = null
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  todoData.value = await res.json()
}

fetchData()

watch(todoId, fetchData)
</script>

<template>
  <p>Id de la liste de tâches : {{ todoId }}</p>
  <button @click="todoId++">Récupérer la prochaine liste de tâches</button>
  <p v-if="!todoData">Chargement...</p>
  <pre v-else>{{ todoData }}</pre>
</template>
```
Ceci évite de redéfinir une nouvelle fonction qui incrémente todoId et qui appelle fetchData qui serait équivalent dans ce cas précis. Toutefois il faudrait penser également à refaire ce processus si le changement de todoId se fait ailleurs. La maintenance et l'évolution sont donc plus facile.

### watchEffect

watchEffect() nous permet d'effectuer des effets de bord immédiatement tout en traquant automatiquement les dépendances réactives de cet effet.

Voici un exemple avec watch :

```js
const todoId = ref(1)
const data = ref(null)

watch(todoId, async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  data.value = await response.json()
}, { immediate: true })
```

Et le même exemple réécrit avec watchEffect :

```js
watchEffect(async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  data.value = await response.json()
})
```

## Composants

### Différence entre composant et vue

Techniquement, il n'y a pas de différence entre un composant dans components et un composant dans views. Les deux sont des composants Vue.js qui peuvent être utilisés pour réutiliser du code et de la logique. Toutefois, cette distinction est utile pour organiser le code et rendre l'application plus facile à comprendre et à maintenir.
Les composants dans components sont généralement utilisés pour réutiliser du code et de la logique qui ne sont pas spécifiques à une vue particulière. Les composants dans views sont généralement utilisés pour créer des vues spécifiques à une page ou à un écran.

**Un composant** est un élément réutilisable

Un composant est un élément qui peut être utilisé dans plusieurs vues. Il contient généralement sa propre logique et ses propres données. Par exemple, un composant pourrait être utilisé pour créer un bouton, une liste ou une boîte de dialogue.

**Une vue** est un élément qui est rendu par le routeur

Une vue est un élément qui est rendu par le routeur. Elle représente une page ou une section de votre application. Par exemple, une vue pourrait être utilisée pour afficher la page d'accueil, la page de profil ou la page de contact.

**Exemple** : Quiz de trois page avec un header commun. Création des trois pages sous views et le header sous components.

### Composant local

Voici un simple composant qui contient simplement un titre :
```html
<template>
  <h2>Un composant enfant!</h2>
</template>
```

Pour l'importation :

1) Importer le composant enfant :
```html
<script setup>
import ChildComp from './ChildComp.vue'
</script>
```

2) Insérer le composant dans la page :
```html
<template>
  <ChildComp />
</template>
```

Ceci est une importation au niveau local du composant.
Le composant importé n'est pas disponible aux enfants du composant en question.

### Composant global
Il est également possible d'enregistrer le composant au niveau global de l'application.
Ceci permet de l'utiliser dans le template de n'importe quel composant de cette application.
Attention à ne les utiliser que quand c'est nécessaire et ne pas en abuser de la même manière que les variables globales.

En général, il est préférable d'utiliser des composants locaux lorsque vous n'avez besoin d'utiliser le composant que dans un petit nombre de composants. Cela permet de réduire la taille de votre application et d'améliorer ses performances. Vous pouvez utiliser des composants globaux lorsque vous avez besoin d'utiliser le composant dans tous les composants de votre application. Cela peut être utile pour les composants de base, tels que des composants d'interface utilisateur ou des composants de logique métier.

1 - Rendre les composants disponible dans l'application :
```js
import { createApp } from 'vue'

const app = createApp({})

app.component(
  // le nom enregistré
  'MyComponent',
  // l'implémentation
  {
    /* ... */
  }
)
```
2 - Enregistrer les fichiers importés :

```js
import MyComponent from './App.vue'

app.component('MyComponent', MyComponent)
```
3 - Utiliser le composant dans le template de n'importe quel composant de cette application :
```html
<!-- cela fonctionnera dans n'importe quel composant de l'application -->
<ComponentA/>
<ComponentB/>
<ComponentC/>
```

### Donner un nom au composant
Afin de faciliter le développement et obtenir les noms des composants via Vue Devtools, il faut attribuer un nom aux composant :
```js
<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'NomComposant'
})
</script>
```
### Passer des données à un composant enfant (Props)
Un composant enfant peut accepter des données venant du parent via des props.
Déclarer les props que le composant accepte, sous **forme d'objet** :
```html
<!-- Dans ChildComp.vue -->
<script setup>
const props = defineProps({
  msgEnfant: String
})
</script>
```

Egalement possible sous **forme de tableau** :
```html
<!-- Dans ChildComp.vue -->
<script setup>
const props = defineProps(['msgEnfant'])
</script>
```
Entre les deux, préférer la forme d'objet pour documentation et avertissement si on passe le mauvais type.

Le parent peut passer la prop comme les attributs :
```html
<ChildComp msgEnfant="Voici mon message" />
```
Bien sûr, cette valeur peut être dynamique via une v-bind par exemple :
```html
<ChildComp :msgEnfant="messageAPasser" />
```
Il est aussi possible de passer toutes les propriétés d'un objet en utilisant v-bind (et pas :) :
```html
<BlogPost v-bind="post" />
```
Equivalent à cette ligne si l'objet a deux propriétés :
```html
<BlogPost :id="post.id" :title="post.title" />
```

Généralement, on aura même un tableau dans le composant parent dont nous voudrons un composant pour chaque élément, dans ce cas nous utiliseront un v-for :
```js
const posts = ref([
  { id: 1, title: 'My journey with Vue' },
  { id: 2, title: 'Blogging with Vue' },
  { id: 3, title: 'Why Vue is so fun' }
])
```
```html
<BlogPost
  v-for="post in posts"
  :key="post.id"
  :title="post.title"
 />
```

#### Validation des props
Il est également possible de spécifier des validations pour les props tel que les types autorisés, si le champ est obligatoire, etc.
Voici différents exemples :
```js
defineProps({
  // Contrôle de type de base
  //  (les valeurs `null` et `undefined` autoriseront tous les types)
  propA: Number,
  // Plusieurs types possibles
  propB: [String, Number],
  // Chaîne de caractères requise
  propC: {
    type: String,
    required: true
  },
  // Nombre avec une valeur par défaut
  propD: {
    type: Number,
    default: 100
  },
  // Objet avec une valeur par défaut
  propE: {
    type: Object,
    // Les valeurs par défaut d'un objet ou d'un tableau doivent être renvoyées à partir
    // d'une fonction factory. La fonction reçoit les props bruts
    // reçus par le composant en tant qu'argument.
    default(rawProps) {
      return { message: 'hello' }
    }
  },
  // Fonction de validation personnalisée
  propF: {
    validator(value) {
      // La valeur doit correspondre à l'une de ces chaînes de caractères
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // Fonction avec une valeur par défaut
  propG: {
    type: Function,
    // Contrairement aux valeurs par défaut d'un objet ou d'un tableau, il ne s'agit pas d'une fonction
    // factory - il s'agit d'une fonction servant de valeur par défaut
    default() {
      return 'Default function'
    }
  }
})
```

#### Provide et Inject (Props drilling)

A noter que si nous voulons accéder à des informations d'un composant parent depuis un composant profondément imbriqué, nous devrions passer la même prop sur toute la chaîne composants parents. Même si un intermédiaire ne l'utilise pas, il doit le déclarer et le transmettre, ce qui est compliqué à gérer, c'est le props drilling.

Pour régler ce problème, on peut utiliser Provide et Inject. Pour en savoir plus : https://fr.vuejs.org/guide/components/provide-inject.html


### Écouter des événements (Emits)
En plus de recevoir des props, un composant enfant peut également émettre des événements vers le parent.
```html
<script setup>
// déclare les événements émis
const emit = defineEmits(['responseFromChild'])

// emit avec un argument
emit('responseFromChild', "hello à partir de l'enfant")
</script>
```
Le parent peut écouter les événements émis par l'enfant en utilisant v-on :
```html
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const childMsg = ref("Pas encore de message de l'enfant")
</script>

<template>
  <ChildComp @response-from-child="(msg) => childMsg = msg" />
  <p>{{ childMsg }}</p>
</template>
```
Les événements émis par les composants ne se propagent pas au delà de leur parent direct.
S'il est nécessaire de communiquer entre des composants frères ou profondément imbriqués, il faut utiliser une solution de gestion d'état global (magasin ou store comme Pinia).

### Arguments d'événement
Il est possible de passer des arguments avec des événements :
```html
<button @click="$emit('increaseBy', 1)">
  Increase by 1
</button>
```
Lors de l'écoute de l'événement, utiliser une fonction fléchée comme écouteur :
```html
<MyButton @increase-by="(n) => count += n" />
```
Ou utiliser directement une fonction :
```html
<MyButton @increase-by="increaseCount" />
```
```js
function increaseCount(n) {
  count.value += n
}
```

### Validation des événements

Semblable à la validation de type de prop, un événement émis peut être validé s'il est défini avec la syntaxe utilisant un objet au lieu d'un tableau.

Dans cet exemple, deux emit, un sans validation et le second avec :
```html
<script setup>
const emit = defineEmits({
  // Pas de validation
  responseFromChild: null,

  // Validation de l'événement soumis
  submit: ({ email, password }) => {
    if (email && password) {
      return true
    } else {
      console.warn('Invalid submit event payload!')
      return false
    }
  }
})
```

function submitForm(email, password) {
  emit('submit', { email, password })
}
</script>

### Distribution de contenu (Slots)
Le composant parent peut également transmettre du template à l'enfant.
```html
<ChildComp>
  <h1>Contenu à transmettre dans un h1 pour l'exemple</h1>
</ChildComp>
```
Dans le composant enfant, le code de la balise slot sera affecté par ce template de code. Si aucun code n'est passé, alors le contenu de slot sera affiché.
```html
<template>  
  <slot>Contenu par défaut s'il n'a pas de slot via le parent</slot>
</template>
```

Exemple complet en passage un message à l'enfant via un slot :

```html
<script setup>
import { ref } from 'vue'
import ChildComp from './ChildComp.vue'

const msg = ref('depuis le parent')
</script>

<template>
  <ChildComp>Message: {{ msg }}</ChildComp>
</template>
```

Les slots peuvent être nommés pour ainsi avoir plusieurs slots par composants :
```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```
Puis on utilise **v-slot** ou la syntaxe abrégée pour attribuer le bon slot depuis le parent :
```html
<BaseLayout>
  <template v-slot:header>
    <!-- contenu pour le slot header -->
  </template>
</BaseLayout>
```
Syntaxe abrégée pour trois slots :

```html
<BaseLayout>
  <template #header>
    <h1>Here might be a page title</h1>
  </template>

  <template #default>
    <p>A paragraph for the main content.</p>
    <p>And another one.</p>
  </template>

  <template #footer>
    <p>Here's some contact info</p>
  </template>
</BaseLayout>
```

A noter que default est le slot par défaut et correspond donc au contenu figurant dans BaseLayout sans indication du slot :
```html
<BaseLayout>
  <template #header>
    <h1>Here might be a page title</h1>
  </template>

  <!-- slot par défaut implicite -->
  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template #footer>
    <p>Here's some contact info</p>
  </template>
</BaseLayout>
```

### Composants dynamiques (:is)
​Parfois, il peut être utile d'alterner dynamiquement entre des composants, comme dans une interface avec des onglets.
Cela est rendu possible par l'élément <component> de Vue avec l'attribut spécial :is :
```html
<!-- Le composant change lorsque currentTab change -->
<component :is="tabs[currentTab]"></component>
```
Dans l'exemple ci-dessus, la valeur passée à :is peut contenir au choix :
- une chaîne de caractères représentant le nom d'un composant enregistré, OU
- le véritable objet composant importé
Vous pouvez également utiliser l'attribut is pour créer des éléments HTML classiques.
Lorsqu'on alterne entre plusieurs composants avec <component :is="...">, seul celui sélectionné par :is reste monté. On peut forcer les composants inactifs à rester "en vie" grâce au composant intégré <KeepAlive> (https://fr.vuejs.org/guide/built-ins/keep-alive.html).
A voir si c'est plus interessant de garder le composant monté avec keepalive que de recréer le composant quand nécessaire. Sauf cas spécifique, on utilise pas le keepalive.

### v-model du composant

v-model peut être utilisé sur un composant pour implémenter une liaison à double sens.
Pour en savoir plus : https://fr.vuejs.org/guide/components/v-model.html

### Composants asynchrones

Dans des applications de taille importante, il est parfois judicieux de diviser l'application en plus petits morceaux et ne charger un composant depuis le serveur que lorsque cela est nécessaire. Pour rendre cela possible, Vue a une fonction defineAsyncComponent.

Pour en savoir plus : https://fr.vuejs.org/guide/components/async.html

## Composables

Dans le contexte des applications Vue, **un "composable" est une fonction** qui exploite la Composition API de Vue pour **encapsuler et réutiliser une logique avec état**.

Lors de la création d'applications frontend, nous devons souvent **réutiliser de la logique** pour les tâches courantes. Par exemple, nous pouvons avoir besoin de formater des dates à de nombreux endroits, on extrait une fonction réutilisable pour cela. Cette fonction de formatage encapsule la logique sans état : elle prend des arguments et renvoie immédiatement la sortie attendue.

En revanche, **la logique avec état implique la gestion d'un état qui change au fil du temps**. Un exemple simple serait de suivre la position actuelle de la souris sur une page.

Nous pouvons extraire la logique dans un fichier externe, en tant que fonction composable (par convention Un composable commence toujours par useXXX) :

```js
// mouse.js
import { ref, onMounted, onUnmounted } from 'vue'

// par convention, les noms de fonctions composables commencent par "use"
export function useMouse() {
  // état encapsulé et géré par le composable
  const x = ref(0)
  const y = ref(0)

  // un composable peut mettre à jour son état géré au fil du temps.
  function update(event) {
    x.value = event.pageX
    y.value = event.pageY
  }

  // un composable peut également s'accrocher au cycle de vie de son composant
  // propriétaire pour configurer et démonter les effets secondaires.
  onMounted(() => window.addEventListener('mousemove', update))
  onUnmounted(() => window.removeEventListener('mousemove', update))

  // expose l'état géré comme valeur de retour
  return { x, y }
}
```
```js
Et voici comment il peut être utilisé dans les composants :

<script setup>
import { useMouse } from './mouse.js'

const { x, y } = useMouse()
</script>

<template>Mouse position is at: {{ x }}, {{ y }}</template>
```

La logique de base reste identique que si nous aurions mis le code dans les composants nécessaires, il faut simplement la déplacer dans une fonction externe et de renvoyer l'état qui devrait être exposé. La même fonctionnalité useMouse() peut désormais être utilisée dans n'importe quel composant.

La partie intéressante des composables est que vous pouvez également les imbriquer : une fonction composable peut appeler une ou plusieurs autres fonctions composables. Cela nous permet de composer une logique complexe à l'aide de petites unités isolées, de la même manière que nous composons une application entière à l'aide de composants.

Pour en savoir plus : https://fr.vuejs.org/guide/reusability/composables.html

## Directives personnalisées

Nous avons introduit deux formes de code réutilisable dans Vue : les composants et les composables. Les composants sont les principaux éléments de construction, alors que les composables sont axés sur la réutilisation de la logique d'état.

Les directives personnalisées, quant à elles, sont principalement destinées à réutiliser la logique qui implique un accès de bas niveau au DOM sur des éléments simples.

Une directive personnalisée se définit comme un objet contenant des hooks du cycle de vie, similaires à ceux d'un composant. Les hooks reçoivent l'élément auquel la directive est liée.

Voici un exemple d'une directive qui met le focus sur un champ de saisie lorsque l'élément est inséré dans le DOM par Vue :

```js
<script setup>
// active v-focus dans les templates
const vFocus = {
  mounted: (el) => el.focus()
}
</script>

<template>
  <input v-focus />
</template>
```

Cette directive est plus utile que l'attribut autofocus car elle ne fonctionne pas uniquement au chargement de la page - elle fonctionne également lorsque l'élément est inséré dynamiquement par Vue.

Il est également courant d'enregistrer globalement des directives personnalisées au niveau de l'application :
```js
const app = createApp({})

// rendre v-focus utilisable dans tous les composants
app.directive('focus', {
  /* ... */
})
```

Pour en savoir plus : https://fr.vuejs.org/guide/reusability/custom-directives.html

## Utilisation de fichier
Pour utiliser un fichier notamment une image dans notre application Vue, il y a plusieurs possibilités.

L'image est recherchée depuis la racine :
````html
<img src="images/my-image.jpg" alt="My image">
````
L'image est recherchée dans le dossier courant :
````html
<img src="./images/my-image.jpg" alt="My image">
````
L'image est recherchée dans le dossier src/images de l'application Vue.js.
@ fait référence au dossier src de votre application Vue.js :
````html
<img src="@/images/my-image.jpg" alt="My image">
````
Vous devez utiliser le symbole @ lorsque vous voulez spécifier le chemin vers le dossier racine de l'application. Par exemple, pour spécifier le chemin vers le fichier CSS style.css qui est situé dans le dossier racine de l'application.


~ fait référence au chemin relatif depuis le dossier en cours
````html
<img src="~assets/my-image.jpg" alt="My image">
````
Le symbole ~ est utilisé pour spécifier le chemin relatif vers un dossier ou un fichier à partir du dossier courant. Il est souvent utilisé pour spécifier le chemin vers des ressources qui sont situées dans un sous-dossier du dossier courant.


