# Glossaire

Ce glossaire définit les termes du cours, classés par ordre alphabétique. La colonne **Chapitre** indique où le terme est présenté ou utilisé pour la première fois de façon significative : relisez ce chapitre pour le contexte et des exemples. Les termes anglais couramment utilisés dans les outils sont donnés entre parenthèses.

!!! tip "Comment l'utiliser"
Cherchez un terme avec la fonction de recherche du site, ou parcourez la lettre qui vous intéresse. Pour les sigles, voir la dernière section.

## A

| Terme                              | Définition                                                                                                        | Chapitre |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------- |
| **Action** (GitHub Actions)        | Composant réutilisable appelé dans une étape d'un workflow avec `uses` (par exemple `actions/checkout`).          | 13       |
| **Alias réseau** (_network alias_) | Nom supplémentaire par lequel un conteneur est joignable sur un réseau défini par l'utilisateur.                  | 6        |
| **Auto-guérison** (_self-healing_) | Capacité de Swarm à recréer une tâche arrêtée, défaillante ou perdue avec son nœud, pour revenir à l'état désiré. | 11, 12   |

## B

| Terme          | Définition                                                                                                                                                          | Chapitre |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Bind mount** | Montage d'un dossier ou d'un fichier de l'hôte dans un conteneur.                                                                                                   | 5        |
| **Bridge**     | Pilote réseau qui relie des conteneurs d'un même hôte. Le réseau `bridge` par défaut ne résout pas les noms ; un réseau bridge défini par l'utilisateur les résout. | 6        |
| **BuildKit**   | Moteur de construction d'images de Docker : constructions parallèles, cache amélioré, construction en plusieurs étapes.                                             | 9        |
| **Buildx**     | Interface de la ligne de commande vers BuildKit, utilisée notamment par les actions Docker dans les pipelines.                                                      | 13       |

## C

| Terme                        | Définition                                                                                                                              | Chapitre |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Cache de construction**    | Réutilisation des couches inchangées lors d'un `docker build`. Dans un pipeline, un cache partagé entre exécutions peut être configuré. | 3, 13    |
| **Capabilities** (capacités) | Droits fins du noyau Linux que l'on peut accorder à un processus ; on retire celles dont un conteneur n'a pas besoin.                   | 10       |
| **cgroups**                  | Mécanisme du noyau Linux qui limite et mesure les ressources (mémoire, processeur) d'un groupe de processus.                            | 1        |
| **Client Docker** (CLI)      | Commande `docker`, qui envoie ses ordres au démon.                                                                                      | 1        |
| **Compose**                  | Outil qui décrit une application multi-conteneurs dans un fichier (`compose.yaml`) et la démarre avec une commande.                     | 7        |
| **Config Swarm**             | Objet du cluster qui contient des données non sensibles, montées sous forme de fichier dans les tâches ; immuable.                      | 12       |
| **Conteneur**                | Processus isolé par les namespaces et limité par les cgroups, qui partage le noyau de l'hôte.                                           | 1        |
| **containerd**               | Composant qui gère le cycle de vie des conteneurs pour le démon Docker ; également utilisé par Kubernetes.                              | 1, 15    |
| **Contrainte de placement**  | Règle qui limite les nœuds où une tâche peut s'exécuter (rôle, nom d'hôte, étiquette).                                                  | 12       |
| **Contexte de construction** | Ensemble des fichiers envoyés au démon lors d'un `docker build` ; filtré par `.dockerignore`.                                           | 3        |
| **Couche** (_layer_)         | Élément en lecture seule d'une image, créé par une instruction du Dockerfile. Les couches se partagent et se mettent en cache.          | 3        |

## D

| Terme                                             | Définition                                                                                                                | Chapitre |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Démon** (_daemon_, `dockerd`)                   | Service qui reçoit les ordres du client et gère images, conteneurs, réseaux et volumes.                                   | 1        |
| **Déploiement continu** (_continuous deployment_) | Automatisation allant jusqu'au déploiement en production, sans validation humaine.                                        | 13, 14   |
| **Digest**                                        | Identifiant d'une image calculé à partir de son contenu : deux tags qui portent le même digest désignent la même image.   | 4, 13    |
| **Docker Hub**                                    | Registre public de référence, où l'on publie et télécharge des images.                                                    | 4        |
| **Dockerfile**                                    | Fichier qui décrit, instruction par instruction, comment construire une image.                                            | 3        |
| **`.dockerignore`**                               | Fichier qui liste ce que `docker build` ne doit pas envoyer au démon.                                                     | 3        |
| **Drain** (vidange)                               | Disponibilité d'un nœud Swarm qui n'accepte plus de tâches : les tâches existantes sont déplacées. Sert à la maintenance. | 11       |

## E

| Terme                      | Définition                                                                                                                              | Chapitre |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Environnement** (GitHub) | Cible de déploiement nommée (`production`) à laquelle on peut rattacher des secrets et des règles de protection, comme une approbation. | 14       |
| **Étape** (_step_)         | Commande ou action d'un job d'un workflow.                                                                                              | 13       |
| **Événement** (_event_)    | Ce qui déclenche un workflow : `push`, `pull_request`, tag, lancement manuel.                                                           | 13       |

## F

| Terme                | Définition                                                                                                                        | Chapitre |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Fichier de stack** | Fichier au format Compose, complété par une section `deploy`, qui décrit une application déployée sur Swarm.                      | 12       |
| **Fork**             | Copie d'un dépôt GitHub dans un autre compte. Les workflows lancés depuis un fork n'ont pas accès aux secrets du dépôt d'origine. | 13       |

## G

| Terme              | Définition                                                      | Chapitre |
| ------------------ | --------------------------------------------------------------- | -------- |
| **Service global** | Service Swarm qui exécute une tâche sur chaque nœud du cluster. | 11       |

## H

| Terme           | Définition                                                                                                                          | Chapitre |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Healthcheck** | Commande que Docker exécute régulièrement dans un conteneur pour déterminer son état de santé (`starting`, `healthy`, `unhealthy`). | 7, 8     |
| **Host** (mode) | Mode réseau où le conteneur partage la pile réseau de l'hôte, sans isolation réseau.                                                | 6        |
| **Hôte**        | Machine qui exécute Docker et les conteneurs.                                                                                       | 1        |

## I

| Terme                                                   | Définition                                                                                                              | Chapitre |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | -------- |
| **Image**                                               | Modèle en lecture seule, composé de couches, à partir duquel on crée des conteneurs.                                    | 3        |
| **Image de base**                                       | Image indiquée par `FROM`, sur laquelle une image est construite.                                                       | 3        |
| **Image minimale**                                      | Image réduite à ce qui est nécessaire à l'exécution (base légère, ou image vide `scratch` avec un exécutable autonome). | 9        |
| **Intégration continue** (_continuous integration_, CI) | Pratique qui construit et teste automatiquement le code à chaque modification.                                          | 13       |
| **Interne** (réseau, `--internal`)                      | Réseau sans accès vers l'extérieur de l'hôte, utilisé pour isoler la base de données.                                   | 6        |

## J

| Terme   | Définition                                                          | Chapitre |
| ------- | ------------------------------------------------------------------- | -------- |
| **Job** | Ensemble d'étapes d'un workflow qui s'exécutent sur un même runner. | 13       |

## L

| Terme                                          | Définition                                                                                        | Chapitre |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------- |
| **Lecture seule** (_read-only_)                | Option qui monte le système de fichiers du conteneur en lecture seule.                            | 10       |
| **Livraison continue** (_continuous delivery_) | Pipeline qui prépare une version prête à déployer ; une personne déclenche la mise en production. | 13, 14   |

## M

| Terme                                              | Définition                                                                                                        | Chapitre |
| -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------- |
| **Manager**                                        | Nœud Swarm qui conserve l'état du cluster, accepte les commandes d'administration et décide du placement.         | 11       |
| **Mise à jour progressive** (_rolling update_)     | Remplacement des tâches d'un service par lots, sans interruption.                                                 | 12       |
| **Moindre privilège**                              | Principe selon lequel un conteneur reçoit uniquement les droits nécessaires.                                      | 10       |
| **Multi-stage** (construction en plusieurs étapes) | Dockerfile à plusieurs `FROM` : on construit dans une étape et l'on ne copie que le résultat dans l'image finale. | 9        |

## N

| Terme             | Définition                                                                                              | Chapitre |
| ----------------- | ------------------------------------------------------------------------------------------------------- | -------- |
| **Namespaces**    | Mécanisme du noyau Linux qui isole les ressources vues par un processus (processus, réseau, fichiers…). | 1        |
| **Nœud** (_node_) | Machine membre d'un cluster Swarm, manager ou worker.                                                   | 11       |
| **None** (mode)   | Mode réseau où le conteneur n'a aucune connexion réseau.                                                | 6        |
| **Non root**      | Exécution d'un processus par un utilisateur sans privilèges d'administrateur (instruction `USER`).      | 10       |

## O

| Terme                                 | Définition                                                                                                                        | Chapitre |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **OCI** (_Open Container Initiative_) | Organisation qui définit les normes ouvertes pour les images et les environnements d'exécution de conteneurs.                     | 1        |
| **OOM** (_out of memory_)             | Arrêt d'un processus par le noyau lorsqu'il dépasse sa limite de mémoire ; un conteneur arrêté ainsi se termine avec le code 137. | 8        |
| **Overlay**                           | Pilote réseau qui relie des conteneurs répartis sur plusieurs nœuds d'un cluster.                                                 | 12       |

## P

| Terme                    | Définition                                                                                                                                             | Chapitre |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- |
| **Pipeline**             | Suite d'étapes automatisées exécutées dans un ordre fixé (construire, tester, analyser, publier, déployer).                                            | 13       |
| **Placement**            | Choix du nœud sur lequel une tâche s'exécute.                                                                                                          | 12       |
| **Port publié**          | Port d'un conteneur rendu accessible sur un port de l'hôte (`-p`). Les conteneurs d'un même réseau utilisent le port du conteneur, non le port publié. | 2, 6     |
| **Publication** (_push_) | Envoi d'une image vers un registre.                                                                                                                    | 4        |
| **Pull request**         | Proposition de modification d'un dépôt GitHub, qui peut déclencher un workflow.                                                                        | 13       |

## Q

| Terme      | Définition                                                                               | Chapitre |
| ---------- | ---------------------------------------------------------------------------------------- | -------- |
| **Quorum** | Nombre de managers dont la majorité doit être disponible pour que le cluster fonctionne. | 11       |

## R

| Terme                           | Définition                                                                                                             | Chapitre |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | -------- |
| **Réplique**                    | Tâche d'un service répliqué ; le nombre de répliques est fixé par `replicas`.                                          | 11, 12   |
| **Registre** (_registry_)       | Service qui stocke et distribue des images.                                                                            | 4        |
| **Retour arrière** (_rollback_) | Retour d'un service à sa configuration ou à sa version précédente, manuel ou automatique.                              | 12, 14   |
| **Routing mesh**                | Mécanisme de Swarm qui rend un port publié accessible par n'importe quel nœud, quelle que soit la position des tâches. | 11       |
| **Runner**                      | Machine qui exécute les jobs d'un workflow. Hébergé par GitHub, ou auto-hébergé sur votre propre machine.              | 13, 14   |
| **runc**                        | Composant qui crée effectivement les conteneurs en s'appuyant sur le noyau.                                            | 1        |

## S

| Terme                        | Définition                                                                                                                   | Chapitre |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Scratch**                  | Image vide, base des images minimales contenant un seul exécutable autonome.                                                 | 9        |
| **Secret de dépôt** (GitHub) | Valeur chiffrée enregistrée dans les paramètres d'un dépôt, lue par un workflow avec `secrets.NOM`.                          | 13       |
| **Secret Swarm**             | Objet chiffré du cluster qui contient une donnée sensible, monté en mémoire sous `/run/secrets/` dans les tâches ; immuable. | 10, 12   |
| **Service** (Swarm)          | Description de l'état désiré d'une application (image, nombre de répliques, ports) que Swarm maintient.                      | 11       |
| **Stack**                    | Ensemble de services, réseaux, configs et secrets déployés à partir d'un fichier de stack.                                   | 12       |
| **Surface d'attaque**        | Ensemble des points par lesquels une attaque est possible ; on la réduit avec moins de composants et moins de droits.        | 9, 10    |
| **Swarm** (Docker Swarm)     | Mode d'orchestration intégré à Docker, qui gère un cluster de machines.                                                      | 11       |

## T

| Terme                            | Définition                                                                                                                          | Chapitre |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | -------- |
| **Tâche** (_task_)               | Unité d'exécution d'un service Swarm : un conteneur, placé sur un nœud.                                                             | 11       |
| **Tag** (balise)                 | Étiquette d'une version d'une image (`1.0.1`). Un tag **mobile** (`latest`) change ; un tag de version ou d'empreinte est immuable. | 3, 4, 13 |
| **Test de fumée** (_smoke test_) | Test minimal qui vérifie que le conteneur démarre et répond.                                                                        | 13       |
| **tmpfs**                        | Stockage en mémoire de l'hôte monté dans un conteneur, perdu à son arrêt.                                                           | 5        |
| **Trivy**                        | Outil d'analyse de vulnérabilités d'images, utilisé dans ce cours dans un conteneur.                                                | 10, 13   |

## U

| Terme                                    | Définition                                                                                    | Chapitre |
| ---------------------------------------- | --------------------------------------------------------------------------------------------- | -------- |
| **Union** (système de fichiers en union) | Technique qui superpose les couches d'une image pour présenter un système de fichiers unique. | 3        |

## V

| Terme                          | Définition                                                                                                       | Chapitre |
| ------------------------------ | ---------------------------------------------------------------------------------------------------------------- | -------- |
| **VIP** (adresse IP virtuelle) | Adresse stable d'un service Swarm sur un réseau overlay, qui répartit les connexions entre les tâches.           | 12       |
| **Volume** (nommé)             | Espace de stockage géré par Docker, indépendant du cycle de vie du conteneur. Sur Swarm, il est local à un nœud. | 5, 12    |
| **Vulnérabilité**              | Faille connue d'un composant logiciel, classée par gravité (par exemple `HIGH`, `CRITICAL`).                     | 10       |

## W

| Terme        | Définition                                                                     | Chapitre |
| ------------ | ------------------------------------------------------------------------------ | -------- |
| **Worker**   | Nœud Swarm qui exécute les tâches, sans prendre part aux décisions du cluster. | 11       |
| **Workflow** | Processus automatisé décrit dans un fichier YAML de `.github/workflows/`.      | 13       |

## Y

| Terme    | Définition                                                                                  | Chapitre |
| -------- | ------------------------------------------------------------------------------------------- | -------- |
| **YAML** | Format de fichier basé sur l'indentation, utilisé par Compose, les stacks et les workflows. | 7        |

## Sigles

| Sigle     | Signification                                                                                              |
| --------- | ---------------------------------------------------------------------------------------------------------- |
| **CI/CD** | Intégration continue / livraison continue (ou déploiement continu)                                         |
| **CLI**   | _Command-Line Interface_, interface en ligne de commande                                                   |
| **CRI**   | _Container Runtime Interface_, interface standard entre Kubernetes et le moteur d'exécution des conteneurs |
| **OCI**   | _Open Container Initiative_                                                                                |
| **OOM**   | _Out Of Memory_                                                                                            |
| **VIP**   | _Virtual IP_, adresse IP virtuelle                                                                         |
| **YAML**  | Format de données lisible, basé sur l'indentation                                                          |
