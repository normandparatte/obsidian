---
share: true
tags:
  - Informatique
  - gestionnaireDePaquets
  - Applications
  - Windows
---

## Commandes principales

Obtenir la liste des logiciels installés :
`choco list -i`

(-i permet également de voir les logiciels non installés par Chocolatey)

Installer un programme :
`choco install nom-du-package`

Mettre à jour un programme :
`choco upgrade nom-du-package`

Mettre à jour tous les programmes :
`choco upgrade all`

Rechercher un package :
`choco search nom-du-package`

Désinstaller un package :
`choco uninstall nom-du-package`

Nettoyer les fichiers temporaires de choco :

1) Installer via choco le programme choco-cleaner

`choco install choco-cleaner`

2) Lancer la commande :

`choco-cleaner`