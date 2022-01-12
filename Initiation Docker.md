# Initiation à Docker

    Auteur: Sébastien DAVOULT
    Courriel: d@vou.lt
    Licence: CC-BY-4.0
    Version: 1.0

<!--- Forked from  --->

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />Ce support de formation est distribué sous la license <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

## Qu’est-ce que Docker ?

### Docker, le programme

Docker est un moteur d'exécution de conteneurs publié sous licence Apache 2.0 en **2013**. Le programme fonctionne en tant que service sur Linux, Windows ou Mac, mais reste principalement utilisé sous plateforme GNU/Linux. Le processus tournant en tant qu’utilisateur Root, il n'est pas recommandé de permettre à un utilisateur standard d'utiliser un CLI Docker, il pourrait s'élever root sur la machine hôte sans difficulté.

``` bash
docker exec -u root -it <container-id> /bin/bash
```

### Docker, l'entreprise

En 2017, Docker publie sa première version destinée aux entreprises, Docker EE était née et par la même occasion *Docker Entreprise*.
Le modèle était simple, une version *Docker CE* possédant toutes les fonctionnalités de base et une version *Docker EE* pour avoir accès à des fonctionnalités en mode SaaS ou encore du support aux entreprises.

Mais le passage d'un mode pleinement communautaire à un modèle Entreprise est compliqué, l'équilibre est souvent fragile, en voyant la solution se monétiser une grande partie de la communauté quitta le projet.

Je conseille l'article si dessous de *Chris SHORT* qui **explique pourquoi Docker est mort**:

[Article: Docker inc. is dead](https://chrisshort.net/docker-inc-is-dead/)

En 2019, **Mirantis** rachète les services à destination des entreprises de Docker.

### Docker, le concept

Docker a défini tout un concept permettant de définir, de construire et d'exécuter une application. Nous retrouvons notamment:

- **Dockerfile**, un fichier manifeste décrivant les dépendances et le fonctionnement de notre application
- **Layers**, Chaque instruction présente dans un *Dockerfile* va engendrer la création d'une couche qui pourra être réutilisée par un autre conteneur.
- **MVC des OPS**, La conteneurisation applicative apporte une séparation entre le système, l'application et les données persistantes.
- **Tout est éphémère**, Tu souhaites apporter une modification à ton application conteneurisée ? Il faudra tuer, puis supprimer ton conteneur afin qu'un nouveau soit reprovisionné incluant la modification applicative.
- **Mono Process**, Un conteneur ne devrait inclure qu'un seul processus(PID 0).

## Un peu d'histoire

La conteneurisation existe depuis longtemps et a pris de nombreuses formes. 

### Chroot (1979)
Sa forme la plus primaire *chroot* permet l'isolation d'un utilisateur dans un répertoire et de pouvoir réaliser tout un ensemble d'actions sans impacter l'ensemble du système. Toutefois, ce mécanisme est très basic, vous ne retrouverez pas de gestion du réseau.

### OpenVZ (2005)

Les premières versions d’OpenVZ étaient des Chroot amélioré, Nous retrouvions en plus, une exposition réseau et la possibilité de partager les périphériques (/dev/) et d'y imposer quelques limitations sur les consommations de ressources.
C'est une solution qui a longtemps été utilisée par les Cloud Providers en France, OVH, Online.net pour leurs offres *VPS*.

### LXC (2008)

*Linux Conteneurs* a été la première technologie à utiliser les *cgroups* et les *namespaces* qui ont été pour l'occasion intégrés au noyau GNU/linux. LXC a démocratisé la **conteneurisation système**. Cette technologie était très utilisée, nous utilisions des archives *.tar.gz* qui comportaient une arborescence et de programmes (/, /bin, /tmp, etc ...) et nous étions isolé en son sein. Nous avions également une gestion réseau nous permettant d'exposer nos services vers l'extérieur.

Mais les problèmes de sécurité dans la solution, tel que la possibilité de s'élever root sur la machine hôte depuis un conteneur ont freiné sont adoption.

### Docker (2013)

Docker a révolutionné la conteneurisation en créant la notion de **conteneurisation applicative**. Jusqu'en 2013, les conteneurs n'étaient que de simples systèmes de fichiers exposés sur le réseau, puis nous avons vu arriver les notions de:
- Immuabilité
- Idempotence
- Méthode déclarative

Mais tout comme LXC, Docker était mal vu pour sa sécurité. En effet, le moteur exécutant les conteneurs était lancé depuis un utilisateur avec pouvoir (root) facilitant ainsi l'exploitation de failles. C'est ainsi que d'autres solutions ont ainsi vu le jour (podman, cri-o, containerd, ...)

## Comment fonctionne Docker

La technologie Docker utilise le noyau Linux et des fonctions de ce noyau, telles que les groupes de contrôle cgroups et les espaces de noms, pour séparer les processus afin qu'ils puissent s'exécuter de façon indépendante. Cette indépendance reflète l'objectif des conteneurs : exécuter plusieurs processus et applications séparément les uns des autres afin d'optimiser l'utilisation de votre infrastructure tout en bénéficiant du même niveau de sécurité que celui des systèmes distincts.

Les outils de conteneurs, y compris Docker, sont associés à un modèle de déploiement basé sur une image. Il est ainsi plus simple de partager une application ou un ensemble de services, avec toutes leurs dépendances, entre plusieurs environnements. Docker permet aussi d'automatiser le déploiement des applications (ou d'ensembles de processus combinés qui forment une application) au sein d'un environnement de conteneurs.

Ces outils conçus sur des conteneurs Linux (d'où leur convivialité et leur singularité) offrent aux utilisateurs un accès sans précédent aux applications, la capacité d'accélérer le déploiement, ainsi qu'un contrôle des versions et de l'attribution des versions.

Source: [RedHat.com What is Docker](https://www.redhat.com/fr/topics/containers/what-is-docker)

## Comment installer Docker

[Install Docker Engine](https://docs.docker.com/engine/install/)

## Docker, le Kit de survie

| Commande                            | Description                              |
| ----------------------------------- | ---------------------------------------- |
| docker ps                           | Affiche les conteneurs                   |
| docker ps -a                        | Affiche les conteneurs également éteints |
| docker build                        | Permets la construction d'images         |
| docker exec -it <container> /bin/sh | Permets l'interaction avec le container  |
| docker rm                           | Permets la suppression d'un container    |
| docker rmi                          | Permets la suppression d'une image       |
| docker images                       | Liste les images                         |
| docker logs -f <container>          | Visualisation des journaux               |
