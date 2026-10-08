---
title: Syllabus
template: home.html
hide:
  - navigation
  - toc
---

## Syllabus { #syllabus }

!!! info "Site en construction"
    Toutes les pages existent ; celles marquées « Under construction » sont en cours de rédaction et seront complétées au fil de l'avancement du cours.

### Fiche d'identification

| Rubrique | Description |
|---|---|
| Intitulé | Docker : conteneurisation, orchestration et industrialisation d'applications |
| Public | Master DevOps et Cloud Computing, semestre 1 |
| Volume horaire | 45 h (15 séances de 3 h : environ 15 h de cours, 30 h de TP) |
| Crédits | 3 ECTS |
| Prérequis | Linux en ligne de commande, réseau (TCP/IP, DNS), notions de développement ; aucune expérience des conteneurs requise |
| Outils de TP | Docker Engine ou Docker Desktop, au choix : Docker Desktop (Windows), Ubuntu Desktop ou Ubuntu Server (VM VMware Workstation) ; 3 VM Ubuntu pour le cluster Swarm (chapitres 11, 12 et 14) ; Docker Hub et GitHub (chapitres 4 et 13) ; voir [l'annexe Environnement de travail](annexes/environnement.md) |

### Objectif général

Concevoir, construire, distribuer, sécuriser et exploiter des applications conteneurisées avec Docker, les orchestrer avec Docker Compose et Docker Swarm, puis automatiser leur livraison par un pipeline CI/CD.

### Acquis d'apprentissage

À la fin du cours, l'étudiant est capable de :

- **AA1** : expliquer le fonctionnement des conteneurs et l'architecture de Docker (comprendre)
- **AA2** : créer, exécuter et gérer le cycle de vie des conteneurs (appliquer)
- **AA3** : construire, versionner et distribuer des images via des registres (appliquer)
- **AA4** : gérer la persistance des données et le réseau des conteneurs (appliquer)
- **AA5** : orchestrer une application multi-conteneurs avec Docker Compose (créer)
- **AA6** : superviser et diagnostiquer des conteneurs en exploitation (analyser)
- **AA7** : optimiser et sécuriser des images et des conteneurs (analyser)
- **AA8** : déployer et exploiter une application sur un cluster Docker Swarm (appliquer)
- **AA9** : automatiser la construction, les tests et la livraison par un pipeline CI/CD (créer)

### Compétences visées

=== "Savoirs"

    Conteneurs (namespaces, cgroups, normes OCI), images et couches, registres, volumes, réseaux Docker, Compose, modèle de sécurité des conteneurs, architecture de Swarm (managers, workers, services, stacks), principes CI/CD.

=== "Savoir-faire"

    Maîtrise de la ligne de commande Docker, écriture de Dockerfile et de fichiers Compose, publication d'images, diagnostic et supervision de conteneurs, durcissement et analyse de vulnérabilités, administration d'un cluster Swarm, pipelines GitHub Actions.

=== "Savoir-être"

    Rigueur et reproductibilité, esprit critique sur la sécurité, autonomie, travail en équipe, veille technologique.

### Organisation du cours

#### Partie 1 : Fondations (12 h) { #partie-1 }

[Présentation de la Partie 1](partie-1-fondations/index.md)

| Chapitre | Contenu | Ressources |
|---|---|---|
| 1. Introduction aux conteneurs (AA1) | Conteneur et machine virtuelle, namespaces et cgroups, architecture de Docker (client, daemon, containerd, runc), normes OCI, choix de l'environnement de TP | [Cours](partie-1-fondations/ch01-introduction-aux-conteneurs/cours.md) · [Lab 1.1 : Installer Docker](partie-1-fondations/ch01-introduction-aux-conteneurs/lab-1-1-installer-docker.md) · [Lab 1.2 : Premiers conteneurs](partie-1-fondations/ch01-introduction-aux-conteneurs/lab-1-2-premiers-conteneurs.md) · [Quiz](partie-1-fondations/ch01-introduction-aux-conteneurs/quiz.md) |
| 2. Cycle de vie des conteneurs (AA2) | Commandes run, ps, stop, rm, publication de ports, variables d'environnement, logs, exec, inspect, limites de ressources de base | [Cours](partie-1-fondations/ch02-cycle-de-vie-des-conteneurs/cours.md) · [Lab 2.1 : Gérer le cycle de vie](partie-1-fondations/ch02-cycle-de-vie-des-conteneurs/lab-2-1-gerer-le-cycle-de-vie.md) · [Lab 2.2 : Publier et configurer un service](partie-1-fondations/ch02-cycle-de-vie-des-conteneurs/lab-2-2-publier-et-configurer-un-service.md) · [Quiz](partie-1-fondations/ch02-cycle-de-vie-des-conteneurs/quiz.md) |
| 3. Images et Dockerfile (AA3) | Couches et système de fichiers en union, instructions du Dockerfile, build, cache de construction, tags, .dockerignore | [Cours](partie-1-fondations/ch03-images-et-dockerfile/cours.md) · [Lab 3.1 : Écrire un premier Dockerfile](partie-1-fondations/ch03-images-et-dockerfile/lab-3-1-ecrire-un-premier-dockerfile.md) · [Lab 3.2 : Cache et couches](partie-1-fondations/ch03-images-et-dockerfile/lab-3-2-cache-et-couches.md) · [Quiz](partie-1-fondations/ch03-images-et-dockerfile/quiz.md) |
| 4. Registres et distribution (AA3) | Rôle d'un registre, Docker Hub, nommage et tags, versionnage des images, registre privé | [Cours](partie-1-fondations/ch04-registres-et-distribution/cours.md) · [Lab 4.1 : Publier sur Docker Hub](partie-1-fondations/ch04-registres-et-distribution/lab-4-1-publier-sur-docker-hub.md) · [Lab 4.2 : Déployer un registre privé](partie-1-fondations/ch04-registres-et-distribution/lab-4-2-deployer-un-registre-prive.md) · [Quiz](partie-1-fondations/ch04-registres-et-distribution/quiz.md) |
| **Mini-projet 1** | Conteneuriser et publier une application web | [Énoncé](partie-1-fondations/mini-projet-1.md) |

#### Partie 2 : Données, réseau et exploitation (12 h) { #partie-2 }

[Présentation de la Partie 2](partie-2-donnees-reseau-et-exploitation/index.md)

| Chapitre | Contenu | Ressources |
|---|---|---|
| 5. Volumes et persistance (AA4) | Volumes nommés, bind mounts, tmpfs, cycle de vie des données, sauvegarde et restauration | [Cours](partie-2-donnees-reseau-et-exploitation/ch05-volumes-et-persistance/cours.md) · [Lab 5.1 : Persister des données](partie-2-donnees-reseau-et-exploitation/ch05-volumes-et-persistance/lab-5-1-persister-des-donnees.md) · [Lab 5.2 : Sauvegarder et restaurer un volume](partie-2-donnees-reseau-et-exploitation/ch05-volumes-et-persistance/lab-5-2-sauvegarder-et-restaurer-un-volume.md) · [Quiz](partie-2-donnees-reseau-et-exploitation/ch05-volumes-et-persistance/quiz.md) |
| 6. Réseau Docker (AA4) | Pilote bridge, réseaux définis par l'utilisateur, DNS interne, publication de ports, modes host et none | [Cours](partie-2-donnees-reseau-et-exploitation/ch06-reseau-docker/cours.md) · [Lab 6.1 : Réseaux et résolution DNS](partie-2-donnees-reseau-et-exploitation/ch06-reseau-docker/lab-6-1-reseaux-et-resolution-dns.md) · [Lab 6.2 : Isoler une application par réseaux](partie-2-donnees-reseau-et-exploitation/ch06-reseau-docker/lab-6-2-isoler-une-application-par-reseaux.md) · [Quiz](partie-2-donnees-reseau-et-exploitation/ch06-reseau-docker/quiz.md) |
| 7. Docker Compose (AA5) | Services, réseaux et volumes dans un fichier compose, variables et fichier .env, healthchecks, dépendances entre services | [Cours](partie-2-donnees-reseau-et-exploitation/ch07-docker-compose/cours.md) · [Lab 7.1 : Première pile Compose](partie-2-donnees-reseau-et-exploitation/ch07-docker-compose/lab-7-1-premiere-pile-compose.md) · [Lab 7.2 : Application trois niveaux avec Compose](partie-2-donnees-reseau-et-exploitation/ch07-docker-compose/lab-7-2-application-trois-niveaux-avec-compose.md) · [Quiz](partie-2-donnees-reseau-et-exploitation/ch07-docker-compose/quiz.md) |
| 8. Observabilité et dépannage (AA6) | Logs, stats, events, limites de ressources, healthchecks, démarche de diagnostic, entretien du moteur (espace disque, nettoyage) | [Cours](partie-2-donnees-reseau-et-exploitation/ch08-observabilite-et-depannage/cours.md) · [Lab 8.1 : Superviser une pile applicative](partie-2-donnees-reseau-et-exploitation/ch08-observabilite-et-depannage/lab-8-1-superviser-une-pile-applicative.md) · [Lab 8.2 : Dépanner des pannes imposées](partie-2-donnees-reseau-et-exploitation/ch08-observabilite-et-depannage/lab-8-2-depanner-des-pannes-imposees.md) · [Quiz](partie-2-donnees-reseau-et-exploitation/ch08-observabilite-et-depannage/quiz.md) |
| **Mini-projet 2** | Pile applicative persistante, cloisonnée et supervisée | [Énoncé](partie-2-donnees-reseau-et-exploitation/mini-projet-2.md) |

#### Partie 3 : Durcissement et orchestration Swarm (12 h) { #partie-3 }

[Présentation de la Partie 3](partie-3-durcissement-et-orchestration-swarm/index.md)

| Chapitre | Contenu | Ressources |
|---|---|---|
| 9. Optimisation des images (AA7, AA3) | Construction multi-stage, BuildKit, images minimales, comparaison de taille et de temps de construction | [Cours](partie-3-durcissement-et-orchestration-swarm/ch09-optimisation-des-images/cours.md) · [Lab 9.1 : Construire avec multi-stage](partie-3-durcissement-et-orchestration-swarm/ch09-optimisation-des-images/lab-9-1-construire-avec-multi-stage.md) · [Lab 9.2 : Réduire et comparer des images](partie-3-durcissement-et-orchestration-swarm/ch09-optimisation-des-images/lab-9-2-reduire-et-comparer-des-images.md) · [Quiz](partie-3-durcissement-et-orchestration-swarm/ch09-optimisation-des-images/quiz.md) |
| 10. Sécurité des conteneurs (AA7) | Utilisateur non root, système de fichiers en lecture seule, capabilities, gestion des secrets, analyse de vulnérabilités des images | [Cours](partie-3-durcissement-et-orchestration-swarm/ch10-securite-des-conteneurs/cours.md) · [Lab 10.1 : Durcir un conteneur](partie-3-durcissement-et-orchestration-swarm/ch10-securite-des-conteneurs/lab-10-1-durcir-un-conteneur.md) · [Lab 10.2 : Analyser et corriger une image](partie-3-durcissement-et-orchestration-swarm/ch10-securite-des-conteneurs/lab-10-2-analyser-et-corriger-une-image.md) · [Quiz](partie-3-durcissement-et-orchestration-swarm/ch10-securite-des-conteneurs/quiz.md) |
| 11. Swarm : cluster et services (AA8) | Pourquoi orchestrer, architecture managers et workers, initialisation et adhésion, services répliqués et globaux, routing mesh, mise à l'échelle, maintenance d'un nœud | [Cours](partie-3-durcissement-et-orchestration-swarm/ch11-swarm-cluster-et-services/cours.md) · [Lab 11.1 : Créer un cluster Swarm](partie-3-durcissement-et-orchestration-swarm/ch11-swarm-cluster-et-services/lab-11-1-creer-un-cluster-swarm.md) · [Lab 11.2 : Déployer et mettre à l'échelle des services](partie-3-durcissement-et-orchestration-swarm/ch11-swarm-cluster-et-services/lab-11-2-deployer-et-mettre-a-l-echelle-des-services.md) · [Quiz](partie-3-durcissement-et-orchestration-swarm/ch11-swarm-cluster-et-services/quiz.md) |
| 12. Swarm : stacks et exploitation (AA8) | Réseaux overlay, stacks à partir d'un fichier Compose, configs et secrets Swarm, mises à jour progressives et retour arrière, contraintes de placement, tolérance aux pannes, comparaison avec Kubernetes | [Cours](partie-3-durcissement-et-orchestration-swarm/ch12-swarm-stacks-et-exploitation/cours.md) · [Lab 12.1 : Déployer une stack](partie-3-durcissement-et-orchestration-swarm/ch12-swarm-stacks-et-exploitation/lab-12-1-deployer-une-stack.md) · [Lab 12.2 : Mises à jour, secrets et panne d'un nœud](partie-3-durcissement-et-orchestration-swarm/ch12-swarm-stacks-et-exploitation/lab-12-2-mises-a-jour-secrets-et-panne-d-un-nud.md) · [Quiz](partie-3-durcissement-et-orchestration-swarm/ch12-swarm-stacks-et-exploitation/quiz.md) |
| **Mini-projet 3** | Application sécurisée sur un cluster Swarm | [Énoncé](partie-3-durcissement-et-orchestration-swarm/mini-projet-3.md) |

#### Partie 4 : Industrialisation (9 h) { #partie-4 }

[Présentation de la Partie 4](partie-4-industrialisation/index.md)

| Chapitre | Contenu | Ressources |
|---|---|---|
| 13. Intégration continue (AA9) | Principes CI/CD, GitHub Actions, pipeline de construction, tests, publication versionnée d'une image | [Cours](partie-4-industrialisation/ch13-integration-continue/cours.md) · [Lab 13.1 : Pipeline de construction d'image](partie-4-industrialisation/ch13-integration-continue/lab-13-1-pipeline-de-construction-d-image.md) · [Lab 13.2 : Tests et publication versionnée](partie-4-industrialisation/ch13-integration-continue/lab-13-2-tests-et-publication-versionnee.md) · [Quiz](partie-4-industrialisation/ch13-integration-continue/quiz.md) |
| 14. Livraison continue (AA9, AA8) | Déploiement automatisé sur le cluster Swarm, gestion des versions, retour arrière automatisé | [Cours](partie-4-industrialisation/ch14-livraison-continue/cours.md) · [Lab 14.1 : Déploiement automatisé sur Swarm](partie-4-industrialisation/ch14-livraison-continue/lab-14-1-deploiement-automatise-sur-swarm.md) · [Lab 14.2 : Pipeline complet avec retour arrière](partie-4-industrialisation/ch14-livraison-continue/lab-14-2-pipeline-complet-avec-retour-arriere.md) · [Quiz](partie-4-industrialisation/ch14-livraison-continue/quiz.md) |
| 15. Synthèse et ouverture vers Kubernetes (AA1 à AA9) | Bilan des acquis, bonnes pratiques de bout en bout, limites de Swarm, passage vers Kubernetes | [Cours](partie-4-industrialisation/ch15-synthese-et-ouverture-vers-kubernetes/cours.md) |

#### Projet final

[Plateforme conteneurisée, sécurisée et livrée par pipeline](projet-final.md)

### Méthodes pédagogiques

Cours interactifs courts, TP guidés puis de plus en plus autonomes, études de cas de pannes, mini-projets en binôme à la fin de chaque partie, projet final en binôme avec soutenance. Les étudiants choisissent leur environnement de TP parmi trois options classées par niveau de complexité.

### Évaluation

| Modalité | Pondération |
|---|---|
| Contrôle continu : TP et quiz | 30 % |
| Mini-projets (15 %) et projet final (25 %) | 40 % |
| Examen pratique chronométré | 30 % |

### Références

- Documentation officielle Docker : [docs.docker.com](https://docs.docker.com/)
- Documentation de GitHub Actions : [docs.github.com/actions](https://docs.github.com/actions)
- Open Container Initiative : [opencontainers.org](https://opencontainers.org/)
