# Hyperledger Fabric and Hyperledger Composer sur LinuxONE

Original english version : https://github.com/IBM/hyperledger-fabric-on-linux-one
### Architecture : 
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/FlowDiagram.png)

À travers ce tutoriel, vous allez devoir : 

* Demander un accès à LinuxONE Community Cloud
* Créer votre invité Linux sur la plateform LinuxONE Community Cloud
* Mettre en place et vérifier votre environnement blockchain
* Créer un projet blockchain sur HyperLedger Composer
* Intéragir avec la blockchain via des applications tierces avec le Composer Rest Server et NodeRed
    
# Présentation de l'application

Ce tutoriel blockchain est destiné à vous donner une compréhension de base de la façon dont un développeur interagirait avec Hyperledger Fabric en utilisant Hyperledger Composer. Dans ce tutoriel, vous utiliserez une interface utilisateur basée sur un navigateur pour modifier le code blockchain, tester votre code et déployer vos modifications. Vous apprendrez également comment la technologie IBM peut prendre le code et générer des API pour permettre l'intégration des applications via une interface REST.

Ce tutoriel sera divisé en trois parties:

# Partie 1 - Configurer votre LinuxONE Community Cloud guest
* Demander l'accés à [LinuxONE Community Cloud]
* Créer votre LinuxONE guest
* Mettre en place votre Linux guest pour l'Hyperledger Fabric et l'Hyperledger Composer
* Vérifier l'installation d'Hyperledger Fabric et d'Hyperledger Composer

   [LinuxONE Community Cloud]: <https://github.com/IBM/hyperledger-fabric-on-linux-one#request-access-to-linuxone-community-cloud>
 
# Partie 2 - Créer une application blockchain et générer l'API
* Importer les composants de votre application blockchain
* Créer votre application blockchain
* Tester votre code
* Déployer l'application sur Hyperledger Fabric
* Générer l'API depuis votre application blockchain

# Partie 3 - Utiliser votre API Blockchain avec NodeRED
* Importer votre flow sur sur NodeRED
* Intéragir avec la blockchain grâce à votre dashboard

# Workshop 
### Scénario

Dans ce tutoriel, nous simulerons un thermostat et une jauge de température pour nous fournir des données de température. Dans un scénario réel, cela pourrait être un capteur de température dans votre maison ou dans un immeuble de bureaux. Le capteur peut être connecté à un thermostat réel comme Nest ou d'autres appareils domestiques intelligents via l'API. Pour empêcher les membres de la famille, les colocataires, les amis ou les enfants de trop chauffer ou de faire fonctionner la climatisation, ils doivent d'abord savoir s'ils sont autorisés à ajuster le thermostat en exécutant une transaction définie dans un contrat intelligent exécuté sur Hyperledger Fabric. Le contrat vérifiera la valeur enregistrée dans le registre pour la jauge de température afin de déterminer si le réglage du thermostat est écologique. Deuxièmement, nous allons intégrer Weather.com pour vérifier les températures actuelles et ajuster le thermostat à des paramètres idéaux en fonction des termes du contrat intelligent. 

# Partie 1 - Demander l'accés à LinuxONE Community Cloud

Dans cette partie du tutoriel, nous allons demander l'accès à LinuxONE Community Cloud, établir un invité SLES, lancer un script d'installation et vérifier l'installation.

### Demander l'accès à LinuxONE Community Cloud
1- Dans un navigateur, se rendre sur https://developer.ibm.com/linuxone/ .
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/CommunityCloudPage.png)

2- Cliquer sur "Start your trial now". 
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/StartNow.png)

3- Compléter les champs requis sur la page et cliquer sur "Request your trial". 
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/GuestApplication.png)

4- Vous allez arriver sur cette page. Appuyer sur "Sign In"
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/SignIn.png)

5- Consulter vos e-mails pour vérifier que vous avez reçu un mail de confirmation similaire à celui-ci. Vous allez avoir besoin du User Id et du password qui sont dans le mail.
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/RegistrationConfirmationEmail.png)

### Créer votre invité LinuxONE

6- Retour sur votre navigateur, entrer vos User Id et votre mot de passe puis cliqué sur " Sign In ".
- Note : Une fois connecté, vous pouvez changer votre mot de passe en cliquant sur votre nom d'utilisateur en haut à droite et en séléctionnant " account settings " 

![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/SignInUserIDPW.png)

7- Depuis la page d'accueil d'IBM LinuxONE Community Cloud, séléctionner " Manage Instance " dans la partie Virtual Servers, en dessous d'Infrastructure. 
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/VirtualServers.png)

8- Appuyer sur "create". 
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/Create.png)

9- Renseigner les informations suivantes : 
- Séléctionner General purpose VM pour le type
- Entrer un nom d'instance — DJBlockchain
- Entrer une description
- Séléctionner SLES12 SP2 pour l'image.
- Séléctionner LinuxONE-Medium pour le serveur.

![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/LinuxONEFields.png)

10- Scroller vers le bas. En dessous de "Select a SSH Key Pair" , cliquer sur Create. 
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/CreateKeyPair.png)

11- Dans la pop-up, entrer un nom pour la clé SSH puis cliquer sur " Create a new key pair"
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/KeyPairName.png)

12- Selon votre ordinateur, vous allez peut être recevoir une fenetre vous demandant de sauvegarder le fichier.
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/SaveFile.png)

13- Séléctionner maintenant votre clé SSH.
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/SelectDJBlockchain.png)

14- Vérifier les informations et cliquer sur Create
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/CreateGuest.png)

15- Regarder le statut de la machine, la phase de démarrage passe par plusieurs étapes : 
* Networking
* Spawning 
* Active

/!\ Noter l'IP, nous en aurons besoin un peu plus tard
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/StartedGuest.png)

16- Depuis l'invite de commande de votre ordinateur, se rendre dans le dossier ou se trouve votre clé SSH
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/DownloadDirectory.png)

17- Modifier les permissions de la clé privée en entrant chmod 600 DJBlockchain.pem
![N|Solid](https://github.com/IBM/hyperledger-fabric-on-linux-one/raw/master/images/SSHKeyPermissions.png)

