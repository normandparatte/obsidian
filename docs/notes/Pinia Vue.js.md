---
share: "true"
tags:
  - Développement
  - Informatique
  - Vuejs
  - Pinia
---

Pinia est une bibliothèque de stockage ou gestionnaire d’état (« state management pattern ») pour Vue.js. Il permet de partager un état entre les composants/pages de l’application par l’intermédiaire d’une zone de stockage partagée appelée store (magasin).

Un magasin (comme Pinia) est une entité contenant l'état et la logique métier qui n'est pas liée à votre arborescence de composants. En d'autres termes, il héberge un état global. C'est un peu comme un composant qui est toujours là et que tout le monde peut lire et écrire. Il possède trois concepts, l'état (state), les getters et les actions, et l'on peut supposer que ces concepts sont l'équivalent des données, des calculs et des méthodes dans les composants.

Un magasin doit contenir des données auxquelles on peut accéder dans toute l'application. Il peut s'agir de données utilisées à plusieurs endroits, par exemple les informations sur l'utilisateur affichées dans la barre de navigation, ou de données qui doivent être conservées au fil des pages, par exemple un formulaire à plusieurs étapes.

D'autre part, il faut éviter d'inclure dans le magasin des données qui pourraient être hébergées dans un composant, par exemple la visibilité d'un élément local à une page. A noter que toutes les applications n'ont pas besoin d'accéder à un état global.

Différents avantages à utiliser Pinia (ou un store) :
- Support de Devtools
  - Suivre dans le temps les actions et mutations
  - Magasin visible dans les composants où ils sont utilisés
  - Débogage plus facile avec le voyage dans le temps
- Hot Module (Remplacement à chaud)
  - Modification des magasins sans recharger la page
  - Conserver les états pendant le développement
- Différentes fonctionnalitées grâce à des plugins avec Pinia
- Typescript et autocomplétion
- SSR (Support du rendu côté serveur)

## Installation de Pinia

Installer la dépendance de Pinia :

````js
npm install pinia
````

Créer une instance de Pinia et indiquer que notre application utilise cette instance :
````js
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'

const pinia = createPinia()
const app = createApp(App)

app.use(pinia)
app.mount('#app')
````

## Exemple rapide

Déclaration du routeur en **Setup Stores** :

````js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const name = ref('Eduardo')
  const doubleCount = computed(() => count.value * 2)
  function increment() {
    count.value++
  }

  // Tous les propriétés doivent être retournées (states, getters et actions)
  return { count, name, doubleCount, increment }
})
````
Avec l'Api de composition (Setup Stores) :
- ref() sont des states
- computed() sont des getters
- function() sont des actions

Exemple en **Options Store** :
````js
export const useCounterStore = defineStore('counter', {
  state: () => ({ count: 0, name: 'Eduardo' }),
  getters: {
    doubleCount: (state) => state.count * 2,
  },
  actions: {
    increment() {
      this.count++
    },
  },
})
````

Utilisation du store :

````js
<script setup>
import { useCounterStore } from '@/stores/counter'

// Récupération du store -> Sera créé uniquement à ce moment là
const store = useCounterStore()

setTimeout(() => {
  store.increment()
}, 1000)

// Le store est un reactive, donc pas de .value
const doubleValue = computed(() => store.doubleCount)
</script>
````

Comme le store est un reactive, il ne pas le copier ou extraire les propritétés car la réactivité serait rompu comme pour les props. Par exemple : 
````js
// Ne pas faire ça :
const { name, doubleCount } = store
````

Il est possible d'extraire les propriétés en gardant leurs réactivités en utilisant **storeToRefs**.
````js
import { storeToRefs } from 'pinia'
const store = useCounterStore()

// Récupération des refs
const { name, doubleCount } = storeToRefs(store)

// Attention les actions ne sont pas des refs
const { increment } = store
````

## State

Le state est accessible directement depuis le store en faisant store.monState.
Un nouveau state de ne peut être créer, il doit impérativement être déclaré dans le store.

Pour que le state soit compatible avec TypeScript, il faut être en compilation strict (ou noImplicitThis).
Pinia déduit automatiquement le type de l'état, il faut parfois l'aider pour les listes et les datas qui ne sont pas encore chargées

````js
// for initially empty lists
userList: [] as UserInfo[],
// for data that is not yet loaded
user: null as UserInfo | null,

interface UserInfo {
  name: string
  age: number
}
````

### Reset

Pour reset le store, utiliser la méthode reset :
````js
const store = useStore()

store.$reset()
````

Attention en setup store, il faut définir soi-même la méthode :

````js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)

  function $reset() {
    count.value = 0
  }

  return { count, $reset }
})
````