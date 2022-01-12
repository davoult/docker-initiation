# [Labs] Initiation à Docker

    Auteur: Sébastien DAVOULT
    Courriel: d@vou.lt
    Licence: CC-BY-4.0
    Version: 1.0

<!--- Forked from  --->

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />Ce support de formation est distribué sous la license <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

## Environnement

Chaque participant a accès à son environnement, il est composant d'une instance, voici les paramètres:

| Clé          | Valeur |
| ------------ | ------- |
| Utilisateur  |         |
| Mot de passe |         |
| Adresse IP   |         |

## 1 - Installation de Docker

Dans cet exercice, vous vous reposerez sur la documentation proposée par l'éditeur afin d'installer docker CE sur votre environnement.

[Docker Installation Guide](https://docs.docker.com/engine/install/)

- [ ] Installation du dépôt 
- [ ] Installation de *Docker Engine* et de ses utilitaires
- [ ] Permettre à votre utilisateur standard d'exécuter des commandes *docker*
- [ ] Mettre docker en démarrage automatique sur votre serveur

## 2 - Ma première application

Dans cet exercice nous allons déployer notre première application conteneurisée. Il s'agit d'un serveur Web minimaliste qui affichera simplement les informations sur notre conteneur. L'image public utilisée est : `containous/whoami` et se trouve sur le registre d'image public *Docker Hub*.

- [ ] Créer un conteneur nommé **whoami** qui utilise l'image **containous/whoami** et qui sera exposé sur le port **80** de votre machine hôte. (Pour information le serveur Web au sein de l'image écoute sur le port 80)
  - [ ]  Nom: **whoami**
  - [ ]  Image: **containous/whoami**
  - [ ]  Expose: **80:80**
- [ ] Accéder à l'interface web de votre conteneur au travers du réseau [http://IP_WAN:80](http://IP_WAN:80)


## 3 - Mon premier stockage persistant

Durant cet exercice nous allons déployer une base de données. Elle nous servira dans l'exercice suivant.

Il est important pour une base de données d'avoir un stockage persistant et non éphémère pour l'hébergement de ses données. Sinon, à chaque redémarrage de notre machine hôte, toutes nos données seront perdues.

- [ ] Création d'un conteneur nommé **mariadb**
  - [ ] Utilisant l'image **mariadb:latest**
  - [ ] Pas d'exposition du port en dehors du serveur
  - [ ] Créer une base de données dans mariaDB nommée: **wordpress**
  - [ ] Créer un utilisateur dans mariaDB nommé: **wordpress**
  - [ ] Définir le mot de passe de l'utilisateur à: **DockerRocks**


## 4 - Communication interservices

Dans cet exercice, nous allons déployer un service Wordpress et le connecter à notre base de données précédemment créée.

- [ ] Créer un conteneur nommé **wordpress**
  - [ ] Exposé sur le port **80**
  - [ ] Utilisant l'image **wordpress:latest**
  - [ ] Définir via variable d'environnement le nom d'utilisateur de la base de données
  - [ ] Définir via variable d'environnement le mot de passe de l'utilisateur de la base de données
  - [ ] Définir via variable d'environnement l'adresse du serveur de base de données
  - [ ] Définir via variable d'environnement le nom de la base de données utilisé pour y stocker les données
  - [ ] Vérifier le bon fonctionnement de l'accès web à votre application
  - [ ] Vérifier le bon fonctionnement de l'interaction entre vos services
