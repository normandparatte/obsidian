---
share: true
tags:
  - Informatique
  - Développement
  - Git
---

Faire des commits régulier sur une branche dédiée à la fonctionnalité. 

Lorsque terminé :
- Mettre à jour la branche Master (Sous local, master -> Update)
- Sur notre branche, faire local, master -> Merge master into "notre branche"
- Création de la pull request
- Validation et merge soit même si personne d'autre ne contrôle

Si problème avec des fichiers Untracked files, ils peuvent être supprimés si le commit des autres fichiers a bien été fait.

Revoir Git :
- C'est quoi git ? Gestionnaire de version décentralisé. Concrètement mes fichiers sont où ? 
- C'est quoi un commit ? 
- C'est quoi une branche ? 
- Comment sont géré les conflits ? 
- C'est quoi un pull request ?

- Processus git (simplifié avec uniquement master et fonctionnalités)     
- Voir en détail comment procéder (et comment faire sur webstorm) :
	- Commit les modifications
	- Quand on veut "merge" sur master (ou une autre branche comme develop), on reprend master sur sa branche
	- On fait le Pull Request
	- On fait les corrections
	- Quand validé, on fait le merge (généralement le développeur)