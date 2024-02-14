---
share: "true"
tags:
  - Développement
  - Informatique
  - Vuejs
  - Ionic
  - npm
  - Quasar
---
## npm

Installation des dépendances package-lock.json si existant sinon package.json :
```
npm install
```

Lancer l'application Vue ou Quasar
```
npm run serve
```

Compiler pour la production Vue ou Quasar
```
npm run build
```

Lints and fixes files
```
npm run lint
```

### Mise à jour des dépendances du projet
**package.json** n'indexe pas les paquets installés mais contient simplement des règles pour installer ces derniers selon une indication de version plus ou moins précise. En utilisant des numéros de version comme "latest", "~1.1.0" ou "^1.1.0", impossible de prévoir quelle sera la version exacte qui sera installée, l’exécution de npm install est donc "non-déterministe". Un comportement qui peut poser problème lorsque deux développeurs d'une même équipe se retrouvent avec deux dossiers de dépendances différents, pourtant issus du même package.json.

**package-lock.json** sert à stocker une représentation exacte des dépendances installées dans le projet à un instant T qui contient : 
-	la version exacte
-	l'url depuis laquelle elle a été installé
-	un checksum pour vérifier l'intégrité
-	les sous-dépendances

Ce qui permet d'avoir une photographie instantanée très précise des dépendances actuellement utilisées par le projet, qui sera mise à jour à chaque opération modifiant le contenu de "node_modules" ou du fichier package.json

**Mettre à jour les dépendances de votre projet** aux versions les plus récentes (**package-lock.json**) :
```
npm update
```

Si les mises à jour fonctionnent correctement, le **package.json peut également être mis à jour** :
```
npm update –save
```

### npm ci
La commande npm ci est plus stricte que la commande npm install. Si le fichier package-lock.json n'existe pas ou s'il ne contient pas les informations nécessaires pour installer les dépendances, npm ci échouera.
 
Exemple :

package-lock.json
```
{
  "dependencies": {
    "react": "^18.0.0"
  }
}
```
package.json
```
{
  "dependencies": {
    "react": "^17.0.0"
  }
}
```
Si vous exécutez la commande npm install, npm installera la version 18.0.0 de React, car c'est la version spécifiée dans le fichier package-lock.json.
Si vous exécutez la commande npm ci, npm échouera, car le fichier package-lock.json ne contient pas les informations nécessaires pour installer la version 17.0.0 de React.
En général, il est recommandé d'utiliser la commande npm install pour installer les dépendances de votre projet Node.js. La commande npm install est plus flexible que la commande npm ci et elle permettra à npm de gérer automatiquement les mises à jour des dépendances.
Cependant, si vous avez besoin d'être sûr que les mêmes dépendances sont installées sur toutes les machines, vous pouvez utiliser la commande npm ci.

## ionic

Lancer l’application :
```
cd myApp
ionic serve
Pour voir l’application sur ios et android, utiliser la commande suivante :
ionic serve -l ou ionic serve --lab
```

Désinstallation si ancienne version :
```
npm uninstall -g ionic
```

Installation de ionic :
```
npm install -g @ionic/cli
```

Création d'une application :
```
ionic start myApp tabs // blank starter, tabs starter, and sidemenu starter
```

### Création des app iOs et Android

```
ionic integrations enable capacitor
```

S'assurer que le dossier de build webDir est le bon dans capacitor.config. json
```
{
"appId": "ch.divtec.salon-metiers",
"appName": "Salon 2022",
"webDir": "dist",
"bundledWebRuntime": false
}
```

Ajout des plateformes
```
ionic cap add ios
ionic cap add android
```

Copie, mise à jour de l'app
```
# Après le build copie la nouvelle version vers iOS ou Android
ionic cap copy
# Si ajout de plugin, paramètres iOs ou Android
ionic cap sync
```

Ouvrir les app dans les IDE
```
ionic cap open ios
ionic cap open android
```