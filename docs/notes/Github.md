---
share: "true"
tags:
  - Informatique
  - Développement
  - Git
---

![[Pasted image 20240215213440.png|Pasted image 20240215213440.png]]

## Description

GitHub est un service web d'hébergement et de gestion de développement de logiciels, utilisant le logiciel de gestion de versions Git. GitHub propose des comptes professionnels payants, ainsi que des comptes gratuits pour les projets de **logiciels libres**. Le site assure également un contrôle d'accès et des fonctionnalités destinées à la collaboration comme le suivi des bugs, les demandes de fonctionnalités, la gestion de tâches et un wiki pour chaque projet.

## Fonctionnalités

GitHub est centré vers l'aspect social du développement. En plus d'offrir l'hébergement de projets avec Git, le site offre de nombreuses fonctionnalités habituellement retrouvées sur les réseaux sociaux comme les flux, la possibilité de suivre des personnes ou des projets ainsi que des graphes de réseaux pour les dépôts (en anglais repository). GitHub offre aussi la possibilité de créer un wiki et une page web pour chaque dépôt. Le site offre aussi un logiciel de suivi de problèmes (de l'anglais issue tracking system). GitHub propose aussi l'intégration d'un grand nombre de services externes, tels que l'intégration continue, la gestion de versions, badges, chats basés sur les projets, etc.

### Pull request

![[Pasted image 20240215213447.png|Pasted image 20240215213447.png]]

Les pulls requests permettent de dire aux autres que vos changements ont été publiés sur Github.

Une fois qu’un pull request est ouvert, il est possible de discuter, de revoir de potentielles modifications avec les collaborateurs et ajouter des commits de suivis avant de fusionner (merge) les changements dans le repository.

### Github flow

![[Pasted image 20240215213453.png|Pasted image 20240215213453.png]]

-          Tout ce qui est dans le **master est déployable**

-          Tous les nouveaux développements, fix, et évolutions sont créés dans des nouvelles **branches distinctes**.

-          Ces branches ont des **noms explicites** pour que les autres sachent sur quoi on travaille (ex: refactor-authentication, make-retina-avatars)

-          **Commitez régulièrement** sur cette branche localement et poussez votre travail sur la même branche sur le remote

-          Lorsque vous avez besoin de feedback ou d’aide, ou que vous pensez que la branche est prête à être intégrée, ouvrez un **pull request**

-          Lorsque quelqu’un d’autre a **validé votre travail**, vous pouvez **l’intégrer au master**

-          Lorsqu’elle est mergée et poussée sur ‘master’, elle sera déployée tout de suite

## Markdown (.md)

Les documentations des projets sont écrites en langage Markdown (fichiers .md). Ces fichiers ont l'avantage d'être facilement compréhensibles même sans intérpréteur. Ce document en question est réalisé en Markdown.