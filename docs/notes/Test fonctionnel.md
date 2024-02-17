---
share: true
tags:
  - Informatique
  - Développement
  - Test
---

# Description
Les tests fonctionnels permettent de contrôler que les fonctionnalités de l'application soit implémentées et fonctionnelles.
Il permettent également de tester les différentes erreurs possibles et les résultats attendu en cas d'erreur.
Si possible, les tests doivent être réalisés avant de développer l'application, dès que la maquette de l'application est disponible.

# Etablir la liste des tests fonctionnel

Il est nécessaire de commencer par établir la liste des tests que nous souhaitons réaliser.

# Exemple d'une fiche fonctionnel

## Cas de test : Login sur l'application

### Objectif
Vérifier que le processus de login fonctionne correctement.

### Préconditions
1. Assurez-vous que l'application est installée.
2. L'utilisateur dispose d'un compte valide.

### Étapes

| N°  | Action                                       | Description                                                          | Résultat attendu                                                                | Test validé | Résultat obtenu / Remarque                                 |
| --- | -------------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ----------- | ---------------------------------------- |
| 1   | Ouvrir l'application                         | Lancez l'application depuis l'écran d'accueil du périphérique.       | L'application s'ouvre sans erreurs                                              | Oui         |                                          |
| 2   | Accéder à l'écran de login                   | Appuyez sur le bouton "Se connecter" pour accéder à l'écran de login | L'écran de login s'affiche correctement                                         | Oui         |                                          |
| 3   | Saisir les informations                      | Saisir nom d'utilisateur et mot de passe                             | Les informations sont saisies sans problème                                     | Oui         |                                          |
| 4a  | Connexion valide                             | Appuyez sur le bouton de connexion pour soumettre les informations   | L'utilisateur est vers l'écran principal de l'application                       | Oui         |                                          |
| 4b  | Connexion invalide : Champ manquant          | Appuyez sur le bouton de connexion pour soumettre les informations   | Le champ vide est indiqué et un message d'erreur est affiché                    | Non         | Le champ n'est pas indiqué               |
| 4c  | Connexion invalide : Donnée invalide         | Appuyez sur le bouton de connexion pour soumettre les informations   | L'application doit empêcher l'accès et afficher des messages d'erreur           | Oui         |                                          |
| 5   | Clic Mot de passe oublié ?                   | Clic sur le lien Mot de passe oublié                                 | La page doit afficher le champ du mail et pré saisir si le mail était indiqué   | Non         | Le mail n'est pas repris automatiquement |
| 6   | Clic Valider : Réinitialiser le mot de passe | Clic sur Valider pour réinitialiser le mot de passe                  | Un message est affiché et l'utilisateur doit recevoir des instructions par mail | Non         | Pas de message                           |

