# Partie 1 : Fondations

**Durée :** 12 h (chapitres 1 à 4) · **Acquis visés :** AA1 à AA3

Cette partie vous fait découvrir les conteneurs, les manipuler, construire vos propres images puis les publier dans un registre. Les travaux pratiques sont guidés pas à pas.

| Chapitre | Contenu | Ressources |
|---|---|---|
| 1. Introduction aux conteneurs (AA1) | Conteneur et machine virtuelle, namespaces et cgroups, architecture de Docker (client, daemon, containerd, runc), normes OCI, choix de l'environnement de TP | [Cours](./ch01-introduction-aux-conteneurs/cours.md) · [Lab 1.1 : Installer Docker](./ch01-introduction-aux-conteneurs/lab-1-1-installer-docker.md) · [Lab 1.2 : Premiers conteneurs](./ch01-introduction-aux-conteneurs/lab-1-2-premiers-conteneurs.md) · [Quiz](./ch01-introduction-aux-conteneurs/quiz.md) |
| 2. Cycle de vie des conteneurs (AA2) | Commandes run, ps, stop, rm, publication de ports, variables d'environnement, logs, exec, inspect, limites de ressources de base | [Cours](./ch02-cycle-de-vie-des-conteneurs/cours.md) · [Lab 2.1 : Gérer le cycle de vie](./ch02-cycle-de-vie-des-conteneurs/lab-2-1-gerer-le-cycle-de-vie.md) · [Lab 2.2 : Publier et configurer un service](./ch02-cycle-de-vie-des-conteneurs/lab-2-2-publier-et-configurer-un-service.md) · [Quiz](./ch02-cycle-de-vie-des-conteneurs/quiz.md) |
| 3. Images et Dockerfile (AA3) | Couches et système de fichiers en union, instructions du Dockerfile, build, cache de construction, tags, .dockerignore | [Cours](./ch03-images-et-dockerfile/cours.md) · [Lab 3.1 : Écrire un premier Dockerfile](./ch03-images-et-dockerfile/lab-3-1-ecrire-un-premier-dockerfile.md) · [Lab 3.2 : Cache et couches](./ch03-images-et-dockerfile/lab-3-2-cache-et-couches.md) · [Quiz](./ch03-images-et-dockerfile/quiz.md) |
| 4. Registres et distribution (AA3) | Rôle d'un registre, Docker Hub, nommage et tags, versionnage des images, registre privé | [Cours](./ch04-registres-et-distribution/cours.md) · [Lab 4.1 : Publier sur Docker Hub](./ch04-registres-et-distribution/lab-4-1-publier-sur-docker-hub.md) · [Lab 4.2 : Déployer un registre privé](./ch04-registres-et-distribution/lab-4-2-deployer-un-registre-prive.md) · [Quiz](./ch04-registres-et-distribution/quiz.md) |
| **Mini-projet 1** | Conteneuriser et publier une application web | [Énoncé](mini-projet-1.md) |
