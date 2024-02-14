---
share: "true"
---
#Développement #Informatique #Vuejs

Créer une application monopage avec Vue + Vue Router est vraiment simple. Avec Vue.js, nous concevons déjà notre application avec des composants. En ajoutant vue-router dans notre application, tout ce qu'il nous reste à faire est de relier nos composants aux routes, et de laisser vue-router faire le rendu.

Tutoriel : https://v3.router.vuejs.org/fr/guide/#javascript (provenant de la version anglaise du tuto : https://router.vuejs.org/guide/)

## Installation

```
npm install vue-router
```

## Router-view et Router-link

Au lieu des balises "a", nous utilisons un composant personnalisé : **router-link** afin de créer les liens.
Ceci permet à vue de changer d'URL sans recharger la page.

**router-view** permet d'afficher le composant correspondant à l'URL. Il peut être mis n'importe ou dans le template afin de s'adapter au layout.

Exemple :
```html
<div id="app">
  <h1>Hello App!</h1>
  <p>
    <!-- use the router-link component for navigation. -->
    <!-- specify the link by passing the `to` prop. -->
    <!-- `<router-link>` will render an `<a>` tag with the correct `href` attribute -->
    <router-link to="/">Go to Home</router-link>
    <router-link :to="{name: 'about'}">Go to About</router-link>
  </p>
  <!-- route outlet -->
  <!-- component matched by the route will render here -->
  <router-view></router-view>
</div>
```

## Création du router
Pour créer un router, il faut définir les routes dans un fichier. Pour cela, déclarer les composants devant être chargés selon l'URL et définir les routes puis créer le router :

```js
import { createRouter, createWebHashHistory } from '@ionic/vue-router';

import Home from '../views/Accueil.vue'

const routes = [
  {
    path: '/',
    redirect: '/accueil'
  },
  {
    path: '/accueil',
    name: 'accueil',
    component: Home, //component: import('../views/Accueil.vue') fonctionnerait aussi
  },
  {
    path: '/blog',
    name: 'blog',
    component: () => import('../views/Blog.vue')
  },
  {
    path: '/informations',
    name:'informations',
    component:  () => import('../views/Informations.vue')    
  }
]

const router = createRouter({
  history: createWebHashHistory(process.env.BASE_URL),
  routes
})

export default router
```

Puis indiquer que l'application Vue utilise le router :
```js
import router from './router';

const app = createApp(App)
  .use(router);

router.isReady().then(() => {
  app.mount('#app');
});
```

En injectant le routeur, nous y avons accès à travers this.\$router.
Nous avons également accès à la route courante derrière this.$route depuis n'importe quel composant :

```js
<script setup>
import { computed } from 'vue'
import { useRoute, useRouter } from 'vue-router'

// Fonction pour revenir en arrière ou naviguer vers la page d'accueil
const goBack = () => {
  if (window.history.length > 1) {
    $router.go(-1)
  } else {
    $router.push('/')
  }
}

// Calcul de la propriété 'username'
const route = useRoute()
const username = computed(() => route.params.username)
</script>
```

### Chargement à la volée (lazy-loading)

Pendant la construction d'applications avec un empaqueteur (« bundler »), le paquetage JavaScript peut devenir un peu lourd, et donc cela peut affecter le temps de chargement de la page. Il serait plus efficace si l'on pouvait séparer chaque composant de route dans des fragments séparés, et de les charger uniquement lorsque la route est visitée.

En combinant la fonctionnalité de composant asynchrone (opens new window) de Vue et la fonctionnalité de scission de code (opens new window) de webpack, il est très facile de charger à la volée les composants de route.
Le simple fait d'utiliser un import dynamique dans le routeur permet d'activer le lazy-loading de la page.
Par exemple, lieu d'indiquer :
```js
  {
    path: '/blog',
    name: 'blog',
    component: import('../views/Blog.vue')
  }
```
Nous utilisons "() =>" afin de ne charger la page que lorsque cette dernière est appelée :
```js
  {
    path: '/blog',
    name: 'blog',
    component: () => import('../views/Blog.vue')
  }
```

En général, c'est une bonne idée de toujours utiliser l'import dynamique pour les routes.

## Concordance dynamique de route (paramètres)

Vous allez très souvent associer des routes avec un motif donné à un même composant. Par exemple nous pourrions avoir le composant User qui devrait être rendu pour tous les utilisateurs mais avec différents identifiants. 
Il est donc possible de passer un segment dynamique (des paramètres) à la route via ":" :
```js
  {
    path: '/utilisateur/:id',
    name: 'utilisateur',
    component: () => import('../views/PageUtilisateur.vue')
  }
```
La valeur du segment dynamique est exposée via this.$route.params dans tous les composants :
```html
    <div>Utilisateur {{ $route.params.id }}</div>
```
Il est également possible d'avoir plusieurs segments. Par exemple /utilisateur/:username/billet/:post_id renvoie l'objet suivant au travers de \$route.params { username: 'evan', post_id: 123 }.

## Routes nommées

Au lieu d'utiliser le lien en dur, il est possible d'utiliser le nom de la route.
Ceci permet par exemple de changer les liens de l'application sans avoir à changer toute l'application.
Il faut bien sûr avoir donner des noms aux routes via la propriété name.

Le code de router-link en dur était :
```html
<router-link to="/about">Go to About</router-link>
```

Ce même code devient :

```html
<router-link :to="{name: 'about'}">Go to About</router-link>
```

Attention aux **":"** devant to.

Il est également possible de passer des paramètres :
```html
<router-link :to="{name: 'utilisateur', params: { userId: 123 }}">Profil utilisateur</router-link>
```
Cette même navigation peut être faite en js :
```js
router.push({ name: 'utilisateur', params: { userId: 123 }})
```
Dans les deux cas, le routeur va naviguer vers le chemin **/utilisateur/123**.

## Navigation dans le code

En complément de l'utilisation de \<router-link> pour créer des balises ancres pour la navigation déclarative, nous pouvons le faire en JS.

L'argument peut être une chaine de caractère représentant un chemin, ou un objet de description de destination :

```js
// chaine de caractère représentant un chemin
router.push('home')

// objet
router.push({ path: 'home' })

// route nommée
router.push({ name: 'user', params: { userId: 123 }})

// avec une requête « query » résultant de `/register?plan=private`
router.push({ path: 'register', query: { plan: 'private' }})
```

Voici comment revenir à la page suivante ou précédente :
```js
// avancer d'une entrée, identique à `history.forward()`
router.go(1)

// retourner d'une entrée en arrière, identique à `history.back()`
router.go(-1)
```
## Routes imbriquées (childrens)
Il est très commun que les segments d'URL correspondent à une certaine structure de composants imbriqués.

Pour faire le rendu de composants à l'intérieur des balises imbriquées, nous avons besoin d'utiliser l'option children dans la configuration du constructeur de VueRouter :
```js
const router = new VueRouter({
  routes: [
    { path: '/utilisateur/:id', component: User,
      children: [
        // `UserHome` va être rendu à l'intérieur du `<router-view>` de `User`
        // quand `/utilisateur/:id` concorde
        { 
            path: '', 
            component: UserHome
        },
        {
          // `UserProfile` va être rendu à l'intérieur du `<router-view>` de `User`
          // quand `/utilisateur/:id/profil` concorde
          path: 'profil',
          component: UserProfile
        },
        {
          // `UserPosts` va être rendu à l'intérieur du `<router-view>` de `User`
          // quand `/utilisateur/:id/billets` concorde
          path: 'billets',
          component: UserPosts
        }
      ]
    }
  ]
})
```

## Vues nommées

Parfois vous avez besoin d'afficher différentes vues en même temps plutôt que de les imbriquer, c.-à-d. créer un affichage avec une vue sidebar et une vue main par exemple.

Au lieu d'avoir une seule balise de vue, vous pouvez en avoir une multitude et donner à chacune d'entre elles un nom. Un router-view sans nom aura comme nom par défaut : default.
```html
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>
```
Une vue est rendue en utilisant un composant, donc de multiples vues nécessitent de multiples composants pour une même route. Assurez-vous d'utiliser l'option components (avec un s) :
```js
const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]
})
```

Il est également possible d'utiliser les vues nommées imbriquées.
Pour en savoir plus : https://v3.router.vuejs.org/fr/guide/essentials/named-views.html#vues-nommees-imbriquees

## Intercepteurs de navigation (evénements de navigations)

A noter que l'on peut déclencher des événements avant ou après avoir changer de page.
Pour en savoir plus, voir le chapitre intercepteurs de navigation du tutoriel : https://v3.router.vuejs.org/fr/guide/advanced/navigation-guards.html