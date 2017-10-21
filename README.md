# Hyperledger Fabric and Hyperledger Composer sur LinuxONE

# Architecture : 
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
# Scénario

Dans ce tutoriel, nous simulerons un thermostat et une jauge de température pour nous fournir des données de température. Dans un scénario réel, cela pourrait être un capteur de température dans votre maison ou dans un immeuble de bureaux. Le capteur peut être connecté à un thermostat réel comme Nest ou d'autres appareils domestiques intelligents via l'API. Pour empêcher les membres de la famille, les colocataires, les amis ou les enfants de trop chauffer ou de faire fonctionner la climatisation, ils doivent d'abord savoir s'ils sont autorisés à ajuster le thermostat en exécutant une transaction définie dans un contrat intelligent exécuté sur Hyperledger Fabric. Le contrat vérifiera la valeur enregistrée dans le registre pour la jauge de température afin de déterminer si le réglage du thermostat est écologique. Deuxièmement, nous allons intégrer Weather.com pour vérifier les températures actuelles et ajuster le thermostat à des paramètres idéaux en fonction des termes du contrat intelligent. 
