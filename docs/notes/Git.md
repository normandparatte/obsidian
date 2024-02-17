---
share: true
tags:
  - Informatique
  - Développement
  - Git
---

![[Pasted image 20240215211949.png|200]]

## Description

Git est un logiciel de gestion de versions décentralisé. C'est un logiciel libre créé par Linus Torvalds, auteur du noyau Linux, et distribué selon les termes de la licence publique générale GNU version 2. Il s’agit du logiciel de gestion de versions le plus populaire qui est utilisé par plus de douze millions de personnes. Git ne repose pas sur un serveur centralisé. C'est un outil de bas niveau, qui se veut simple et performant.

## Installation et configuration
Le plus simple est d’installer directement github car ce dernier va automatiquement configurer ssh avec la bonne adresse mail.

Sinon il est possible d’installer uniquement git et de configurer ssh via **Git Bash**.

Voici les commandes à utiliser afin de configurer ssh :
```
cd ~/.ssh

ssh-keygen -t rsa -C [your_email@example.com](mailto:your_email@example.com)
```
Cette commande va créer les fichiers _id_rsa_ and _id_rsa.pub_.

Il faut ensuite ouvrir le fichier id_rsa.pub (dans C:\Users\_Utilisateur_\.ssh\) et copier tout le contenu (la ligne entière) puis l’ajouter dans les propriétés du comptes github.

## Utilisation
![[Pasted image 20240215213043.png|450]]![[Pasted image 20240215213048.png|450]]

Créez tout de suite un gitignore pour votre projet, cela évitera de “polluer” votre répo avec des fichiers non pertinents, diminuer les risques de problèmes de configuration.

Avant de changer de branche, assurez-vous d’avoir au moins un commit existant sur la branche master ! Sinon, la branche nouvellement créée sera définie comme branche par défaut.

Pour vous prémunir contre cet inconvénient, prenez l’habitude de committer votre .gitignore et votre readme sur la branche master dès l’initialisation de votre répo.

![[Pasted image 20240215213114.png|Pasted image 20240215213114.png]]

## Branches
Création d’une nouvelle ligne de développement dans un projet. Une branche est souvent réconciliée et fusionnée (merged) avec d’autres branches pour réunir les différents efforts.

![[Pasted image 20240215213127.png|Pasted image 20240215213127.png]]

**Important** de d’abord faire le **pull de master** puis **merge master sur sa branche** puis **push de la branche**

![[Pasted image 20240215213138.png|Pasted image 20240215213138.png]]

Il peut aussi y avoir des branches d’intégrations afin de réunir des features et master dans une branche spécifique.

![[Pasted image 20240215213154.png|Pasted image 20240215213154.png]]

Ne pas utiliser Release mais le reste peut être utilisé. Develop est utile car Master pourrait par exemple être déployé automatiquement. Une branche normandTests peut aussi servir pour intégrer plusieurs fonctionnalités ensemble ou faire des tests mais elle ne sera jamais mergée vers d’autres branches.

## Gitignore
Il est possible d’exclure des fichiers de votre dépôt Git avec gitignore.

Le plus simple est de le faire localement en créant un fichier .gitignore au sein du projet Git.

La plupart du temps ce fichier est créé à la base du dépôt. Vous avez la possibilité d’en créer à n’importe quel niveau de votre projet mais cela est fortement déconseillé. Le fichier .gitignore fait partie du projet, il sera donc partager avec les autres contributeurs.

Cette méthode est utile pour demander à ignorer les fichiers en liens avec le projet, par exemples : les builds ou encore les fichiers compilés en lien avec le langage utilisé.

Exemple d’un fichier gitignore pour un petit projet :
```
.idea
target
*.iml
```
## Commandes principales

### Initialisation (init et clone)

Créé un nouveau dépôt. La branche par défaut s'appelle **master**.
```
git init
```
La commande ci-dessous permet de récupérer une copie d'un dépôt Git distant.
```
git clone adresseDuRepo
```
Cette commande correspond à :
-          Git init
-          Git remote add origin Adresse
-          Git pull origin master

### Ajout des fichiers dans la staging area (fichiers à commit)
Ajoute les fichiers souhaités pour le prochain commit. Les objets qui restent inchangés ne sont naturellement pas ajoutés.

git add . OU git add fichierSpécifique OU git add copie*

### Ajout des fichiers dans le repository
Intègre toutes les modifications apportées dans une version, un commit. Sont commités tous les fichiers qui ont été précédemment ajoutés via la commande _"add"_. A noter, qu'il est possible de **modifier le dernier commit** (bien que pas très recommandé sauf si des fichiers ont été oubliés ou que le commentaire n'était pas complet, etc) avec le paramètre _**–amend**_
```
git commit
```

### Gestion des fichiers dans le suivi de version
Pour effacer des fichiers, il faut les supprimer du suivi de version en utilisant la commande _rm_ et pour les déplacer, il faut utiliser la commande _mv_

**(Attention : supprime réellement le fichier et pas uniquement du suivi de version)**
```
git rm
git mv
```

### Gestion des branches
Permet de voir toutes les branches (sans paramètre) ou de créé une nouvelle branche de développement (avec le nom en paramètre).
```
// Permet de voir les branches
git branch

//Permet d’ajouter une branche
git branch NomDeLaBranche (-d nomBranche pour la supprimer)
```
### Fusionner des branches
Deux méthodes permettent de fusionner plusieurs branches de développement.

#### Git merge
Il faut se placer dans la branche souhaitée et choisir la branche de laquelle reprendre les modifications.
```
// Sur placer sur la branche dont on veut intégrer les modifs
Git checkout brancheDestination

// Puis reprendre les modifs de la branche choisie
git merge brancheAReprendre

// Il est aussi possible de le faire en une ligne
git merge **brancheAReprendre brancheDestination**
```

Cette commande créer un **nouveau commit** en reprenant les modifications de master dans la branche de feature.

![[Pasted image 20240215213349.png|Pasted image 20240215213349.png]]

#### Git rebase
```
// Sur placer sur la branche dont on veut intégrer les modifs
Git checkout feature

// Puis reprendre les modifs de la branche choisie
git rebase master
```

Cette commande intègre les modifications de master dans **tous les commit** de la branche feature.

![[Pasted image 20240215213358.png|Pasted image 20240215213358.png]]

#### Git Merge vs Git Rebase
En général, il est recommandé d'utiliser git merge pour les situations suivantes :
```
Lorsque vous souhaitez conserver l'historique complet du projet. Le merge crée un commit de fusion qui enregistre les modifications apportées par les deux branches. Cela permet de suivre l'historique des modifications au fil du temps.
Lorsque vous travaillez avec des branches distantes. Le merge est la méthode recommandée pour fusionner des branches distantes, car il permet de conserver l'historique des modifications apportées par les autres développeurs.
Lorsque vous souhaitez pouvoir revenir à une version antérieure du projet. Le merge permet de revenir à une version antérieure du projet en annulant le commit de fusion.
```

En revanche, il est recommandé d'utiliser git rebase pour les situations suivantes :
```
Lorsque vous souhaitez nettoyer l'historique du projet. Le rebase réécrit l'historique du projet en fusionnant les modifications de la branche source dans la branche cible. Cela permet d'obtenir une ligne de temps plus propre et plus facile à comprendre.
Lorsque vous travaillez sur une branche qui a été poussée sur une branche distante. Le rebase permet de fusionner les modifications de la branche source dans la branche cible sans créer de commit de fusion. Cela peut être utile si vous souhaitez éviter de créer des conflits avec les modifications apportées par d'autres développeurs.
```

### Serveurs distants
Pour visualiser les serveurs distants enregistrés, il faut utiliser la commande ci-dessous.
```
git remote
```
Pour ajouter un dépôt distant, il faut utiliser la commande ci-dessous. A noter que le nom est facultatif et le nom du dépôt distant par défaut est **origin**.
```
git remote add <nomDepot> <AdresseDepot>
```
### Récupérer et envoyer des données
Cette commande récupère et fusionne automatiquement une branche distante dans la branche locale. (Pour autant qu’il n’y ait pas de confits).
```
git pull
```
  
La commande _git pull_ exécute les deux commandes suivantes :
```
//Mise à jour des données du serveur
git fetch
git merge
```

Et à l'inverse la commande suivante permet de _pousser_ la brancher locale sur le serveur distant.
```
git push <DepotDistant> <Branche>

// La commande ci-dessous permet de pousser une **branche spécifique**
git push -u origin brancheSource
```

### Forcer la récupération du serveur en écrasant les fichiers locaux
Pour forcer la récupération depuis le serveur en écrasant les fichiers locaux par ceux du serveur, il faut exécuter les trois commandes suivantes.
```
// Mise à jour des données du serveur
git fetch –all

// Reset au dernier commit du serveur
git reset --hard origin/master

// Reprend toutes les modifications du serveur
git pull origin master
```

### Annuler des modifications, changer de branche et revenir dans un état donné
La commande _git checkout_ permet de changer de branche ou d'annuler les modifications d'un ou plusieurs fichiers.

```
// Change de branche
git checkout <branch> (avec -b permet de créer + changer de branche)

// Annule les modifications d''un fichier
git checkout <fichier>

// Annule toutes les modifications en cours
git checkout .
```

Attention cette opération est irréversible ! Cette commande permet d'annuler les modifications actuelles et de revenir dans la version du dernier commit !

### Revenir dans un état donné pour consultation
La commande _git checkout permet également de revenir dans l’état du commit donné pour consultation si aucun fichier n’est passé en paramètre :_
```
git checkout <commit> // revenir à l’état du commit choisi

git checkout HEAD // revenir à la dernière version
```

[[todo|todo]] n’a pas l’air de fonctionner -> Voir si correct en VSCode

La commande reset permet de revenir dans l’état d’un commit précédent puis de continuer le développement depuis cette version (le dernier commit de la branche devient celui du reset). Attention cette commande écrase tous les autre commits et est dangereuse. Il faut donc être sûr de ce qu’on fait et l’utiliser en dernier recours (Préférer la méthode **0** **1.6.11.2**).
```
git reset <commit>
```
La commande reset est utile du moment que l’on n’a pas envoyé les modifications sur le serveur. Mais une fois que les modifications ont été envoyées, nous ne serons plus autorisés à envoyer les modifications :
```
! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs
```

Dans ce cas, il faut annuler les commits souhaités en appliquant l’inverse via la commande **git revert.** Voir le chapitre suivant (**1.6.11.1** **Revenir dans l’état inverse d’un commit** ) pour plus d’informations. Voici la différence entre un checkout et un reset en image :

![[Pasted image 20240215213420.png|435]]![[Pasted image 20240215213423.png|435]]

#### Revenir dans l’état inverse d’un commit (git revert)
```
git revert HEAD
```
Cette commande va immédiatement prendre le précédent commit, créer un commit exactement inverse, et l’appliquer.

Si vous aviez : C1 — C2 — C3

Et que vous vouliez annuler C3.

Vous allez vous retrouver avec : C1 — C2 — C3 — C4.

Avec C4 comme exacte inverse de C3 (équivalent C2).

Annuler les trois derniers commits :
```
git revert HEAD~3..HEAD
```
Inverse d’un commit en particulier (donc l’annule aussi) :
```
git revert 89476e1ccb20d5d7e4b647e20c83852653b13c2f
```

#### Revenir dans l’état complet d’un commit précédent (git checkout)
La meilleure méthode pour revenir dans l’état d’un commit donné est d’utiliser git checkout avec le fichier en question ou « . » pour tous les fichiers :
```
git log // pour voir quelle version reprendre

git checkout 89476e1 . // Reprise du commit dans la version actuelle (tous les fichiers dans ce cas présent)

git add .

git commit -m « Reprise de la version complète du commit : 89476e1 Texte du commit … »
```

### Etats des fichiers, différences et historique
Cette commande permet de vérifier l'état des fichiers (untracked, unmodified, modified, staged)
```
git status
```
Cette commande permet de voir les différentes modifications entre la version actuelle et la version du dernier commit
```
git diff
```
Afin de visualiser l'historique des validations, il faut utiliser la commande suivante
```
git log
```
Cependant afin de visualiser l'historique des validations via une interface graphique, il est possible d'utiliser la commande
```
gitk
```
### Copier un repository sans faire de fork
Voici les commandes afin de cloner un repository sans faire de fork.
```
git clone --bare https://github.com/exampleuser/old-repository.git
cd old-repository.git
git push --mirror [https://github.com/exampleuser/new-repository.git](https://github.com/exampleuser/new-repository.git)
```
#### Supprimer un repository local
Cette commande permet de supprimer un repository en local.
```
cd ..
rm -rf _old-repository_.git
```

### Git Shell
Afin de pouvoir utiliser git depuis Visual Studio Code, il est possible d'ajouter git dans la variable d'environnement Path ou alors, de démarrer le terminal de git (Git Shell), de se positionner sur le répertoire de projet et de lancer l'éditeur avec la commande
```
Code .
```
## Autres
Apprendre Git en s’amusant : [https://ohmygit.org/](https://ohmygit.org/)