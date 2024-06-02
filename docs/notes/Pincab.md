---
share: true
revision: false
MOC:
  - "[[MOC_Perso_Projet|MOC_Perso_Projet]]"
tags:
  - Pincab
  - Flipper
---
---
share: true
revision: false
MOC:
  - "[[MOC_Perso_Projet|MOC_Perso_Projet]]"
tags:
- Pincab
- Flipper
---
# Pincab

## Matos
24" pouces - Ecran IPS - Huawei Ad80Hw
Sono 5.1 Trust GTX 658 Tytan 5.1
10x Bouton non lumineux
Bouton Credit "Insert coin" lumineux (LED ne sera pas branchée)
Câbles boutons + cosses
Carte KL25Z (pour boutons + nudge et tilt)
2x Ventilo + grille (Molex vers pin car pas assez de prise sur l'alim)
Câble jack pour musique
Rallonge USB double pour insertion bois
Grande rallonge électrique pour brancher le tout
Bois
Verre

### PC

Intel : i7-4790K 4x4.0GHZ. max. 1 x 4,4GHz 1150 8MB CACHE
Ventirad : Scythe Mugen4
Carte graphique : Nvidia GeForce GTX970 4,0GB DDR5 RAM
RAM : Corsair Vengeance 32GB (4x8GB) DDR3 1333MHz CL9
Disque : Kingston Now SSD V 300 240GB 2.5", MLC, SATA3 6Gb/s, lesen 450MB/s, schreiben 450MB/s
Disque 2 : 4,0TB Seagate Desktop SSHD 3.5" SATA-III
Carte mère : ASUS H87M-E
Lecteur CD : Blu-Ray-Combo LG CH08LS10 8x, SATA, LightScribe
Carte son : Onbord, 8 -Channel High Definition Audio CODEC
Carte réseau Wifi : Wireless Lan: Linksys WMP600N: WLAN-N PCI-Adapter 300n
Lecteur de carte : Kartenlesegerät (card reader) multi format
Alimentation : Corsair CX600W ATX 12V V2.3 & EPS 12V 2.01 / 40A / effi. 80% / 12 cm
Boitier : Sharkoon T9 Value

## Utilisation des boutons
2x Flippers Bouton 28mm vissable Gold Leaf - Orange
2x Magna Bouton 28mm vissable Gold Leaf - Jaune
launchBouton 28mm vissable Gold Leaf - Orange
start Bouton 28mm vissable Gold Leaf - Orange
Coin Bouton spécial INSERT COIN
Au millieu, 3 boutons noir (Extraball, PAUSE + Instruction, Quitter)
Allumage PC 28mm vissable Gold Leaf - Noir

Voir si possible de exit depuis pinup puis éteindre PC donc avec le même bouton :
- exit Bouton 28mm vissable Gold Leaf - Noir
- eteindre propre Bouton 28mm vissable Gold Leaf - Noir

Voir si possible de regrouper ces deux :
- Pause Bouton 28mm vissable Gold Leaf - Noir
- Instruction Bouton 28mm vissable Gold Leaf - Noir

Volume -> Inutile car j'ai une télécommande pour la sono si besoin
Allumage CM -> Parfois possible sur allumage secteur dans le BIOS

## Logiciels
### Windows

- Laisser l'orientation en paysage car la plupart des tables et logiciels sont prévus comme ça (plus facile)
- Se connecter automatiquement (win+R, netplwiz, décocher mot de passe obligatoire pour le compte en question)
- Pinvol + Pinup dans le démarrage automatique (mettre raccourci dans %appdata%\Roaming\Microsoft\Windows\Start Menu\Programs\Startup)
- Configurer la sono 5.1 dans windows
- Fond écran noir + masquer les icones du bureau + réduire auto la barre des tâches quand pincab prêt
- Enlever la connexion internet quand pincab prêt (évite les MAJ de Windows)
- Désactiver UAC (via FULLCAB)
- Désactiver MAJ + Exceptions (via FULLCAB)
- Installation des prérequis et runtime (via FULLCAB)

### FULLCAB
Fullcab est un logiciel amateur permettant de lancer l'installation et la configuration de presque tous les logiciels nécessaires pour le pincab. Il faut l'installer en premier (d'abord désactiver uac + mettre en exclusion de l'antivirus pour ne pas avoir de problèmes).

### Visual Pinball 10 (VPX)
Logiciel utilisé pour l'émulation des flippers, utilise également Visual PinMAME (l'émulateur des ROMS pour les vraies flippers).

Afin d'afficher les tables en vertical sur l'écran par défaut, il faut cocher **Use always FS backdrop settings** dans les paramètre video de VPX.

#### Gestion des tables
Les **tables** téléchargées sont au format .vpx. Ce fichier peut directement être copié dans le répertoire Tables de visualpinball.
Lors du lancement de la table, une erreur apparaît qu'il manque la rom (pour les vraies tables). Prendre note de la **ROM** et la télécharger en ligne. Il faut ensuite copier le zip de la ROM dans le répertoire de VPinMAME, dossier Roms.
Les **scores, crédits et autres informations** de la ROM sont stockées dans le **répertoire NVRAM de VPinMAME**. Le dossier du nom de la ROM en question peut être supprimé afin de réinitialiser les scores et autres informations.
Certaines **modifications de la ROM** sont possibles, **gestion du volume, DMD, etc**. Pour ça, il faut modifier le registre correspondant (Win+R, HKEY_CURRENT_USER/Software/Freeware/VisualPinMame puis dossier de la ROM).

#### Gestion du DMD
Pour afficher les DMD correctement, il faut **configurer** pour chaque table directement **dans la rom (sur le registre correspondant)**. Toutefois afin de configurer toutes les ROMS en même temps, il est possible d'utiliser **setDMD**.
Pour finir afin de **tourner de 90° le DMD**, il faut modifier directement le code de la table sous VPX, rechercher "rol" et changer la ligne de ****"rol") = 0 à "rol") = 1****

Le format du DMD est de 1:4.
Voici les paramètres utilisés pour un positionnement en bas en haut centre sur mon écran 1920x1080 :
 - offset X : 1780
 - offset Y : 260
 - height : 140
 - width : 560

#### Gestion du TILT
Afin de gérer le Tilt via une KL25Z, il faut tout d'abord choisir le sens dans lequel est installé la KL25Z directement dans les réglages de cette dernière (La sensibilité elle reste à 1 dans les réglages).

Comme un fera un vrai nudge, il faut supprimer le nudge visuel en mettant la valeur à 0 dans les paramètres visuels de VPX.

Puis toujours sous VPX, sous réglage, nudge, il faut cocher :
- Enable Analog Nudge
- Enable Nudge Filter
- Tilt sensitivity

Le Tilt sensitivity doit être entre 1 et 100 et est propre à chaque installation.
Il faut simplement tester la sensibilité et adapter selon le ressenti.
Pour ma part, ce dernier est réglé à **900**.

Pour finir X-Gain and Y-Gain sont le supplément donné pour le nudge. Encore une fois, cela dépend de la configuration et doit être configurer selon le ressenti. Pour ma part, X-Gain : 125% et Y-Gain : 150%.

Une fois les paramètres changés, il faut **quitter complétement VPX** et le relancer sinon les modifications ne sont pas prises en compte.

### Pinscape -> Gestion de la KL25Z
Faire les branchements selon schéma ci-dessous (aussi visible depuis pinscape) :
![[Pasted image 20240325222104.png|Pasted image 20240325222104.png]]

Le sens de la kl25z doit être choisi dans les réglages.
Les boutons sont configurés et testé sous boutons ou joystick depuis le menu principal.

### Pinvol -> Gestion du volume par table

Pinvol permet de gérer le volume directement table par table via un raccourci clavier (voir le raccourci clavier sous l'onglet "Table Keys".
Il faut également lancer Pinvol au démarrage de Windows (raccourci dans %appdata%\Roaming\Microsoft\Windows\Start Menu\Programs\Startup).

Dans les préférences audio de VPX, le volume **pour toutes les tables** peut être géré en choisissant le volume de la musique et le volume des effets.
**Il ne faut pas changer ces volumes** et les laisser à 100%.

Le volume peut être choisi dans la ROM donc dans le registre du pinball correspondant.
**Il ne faut pas changer ce volume** et le laisser à 100%.

Pour gérer le volume des tables (**ratio effets et musique**), il faut régler sur **chaque table sous VPX**, le volume des effets et le volume de la musique. Ceci se trouve dans la partie de droite sous l'onglet Properties, Sound Effect Volume et Music Volume.
Si le ratio n'est toujours pas bon ou qu'un effet est trop fort, il est possible de changer son par son directement sous Table, Sound Manager.
Pour finir, il est également possible de changer le son de la musique via les options de la ROM : https://montetoncab.fr/faq-regler-le-son-des-tables-son-rom/

Attention : Modifier le son viaPreferences -> Audio Options, modifie le ratio pour toutes les tables donc ne pas gérer via cette option ou une fois pour toutes les tables

Ensuite, il faut lancer la table et régler directement le volume général de la table grâce aux raccourcis clavier de Pinvol.

### PinUP Popper (configuration et lancement automatique choix des tables)

Pour la configuration sur un seul écran comme dans mon cas, le backglass correspond au playfield (prendre un printscreen et mettre dans le répertoire approprié).
Pour la vidéo de loading, pinvol ne gère le son qu'une fois la table lancée. Il faut donc télécharger la vidéo souhaitée depuis la configuration de pinup et ensuite supprimer le son de la vidéo.


## Procédure Nouvelle table
- [ ] Téléchargement de la table
- [ ] Téléchargement de ROM associée
- [ ] Lancer la table en mode interactif et régler correctement la caméra
- [ ] Changer le code de la table par ("rol") = 1 OU le registre de la table (rol à 1)
- [ ] Lancer SetDMD et faire Install Roms and Update
- [ ] Régler le volume de la musique dans PinVOL
- [ ] Ajuster le ration volume musique et effets dans les paramètres de la table
- [ ] Ajouter dans le menu pinpup (voir détail sous pinup)

Pour régler la caméra :
 - XY Rotation : 270
 - Inclination : 9
 - Field of view : 30
 - Layback : 57
 - Régler X/Y Scale
 - Régler X/Y Offset

## Montage bois
![[Pasted image 20240326075411.png|Pasted image 20240326075411.png]]

## Sites utiles
https://montetoncab.fr/