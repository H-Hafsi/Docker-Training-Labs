# Lab 2.1 : Gérer le cycle de vie

| | |
|---|---|
| **Durée** | 60 min |
| **Niveau** | Guidé |
| **Prérequis** | [Lab 1.2 : Premiers conteneurs](../ch01-introduction-aux-conteneurs/lab-1-2-premiers-conteneurs.md), cours du [chapitre 2](cours.md) |
| **Acquis visés** | AA2 |

!!! abstract "Objectifs"
    - Faire passer un conteneur par tous ses états : créé, en cours d'exécution, arrêté, supprimé
    - Constater le lien entre un conteneur et son processus principal
    - Lire les journaux d'un conteneur et exécuter une commande dedans
    - Lire l'état et le code de sortie d'un conteneur avec `docker inspect`

## Contexte et schéma

Vous manipulez quatre conteneurs aux comportements différents pour observer leur cycle de vie.

| Conteneur | Image | Comportement |
|---|---|---|
| `web` | `nginx:1.27-alpine` | Serveur web, reste en cours d'exécution |
| `court` | `alpine:3.20` | Affiche un message puis se termine |
| `erreur` | `alpine:3.20` | Se termine avec un code d'erreur |
| `boucle` | `alpine:3.20` | Écrit l'heure chaque seconde, sans fin |

```mermaid
flowchart LR
  I["Image"] -- "create" --> C["Créé"]
  C -- "start" --> R["En cours<br/>d'exécution"]
  R -- "stop" --> S["Arrêté"]
  S -- "start" --> R
  S -- "rm" --> X["Supprimé"]
```

## Étapes

### Étape 1 : Créer un conteneur sans le démarrer

```bash
docker create --name web nginx:1.27-alpine
docker ps -a
docker inspect --format '{{.State.Status}}' web
```

`docker create` crée le conteneur mais ne le démarre pas. `docker ps` seul n'affiche rien, car il ne liste que les conteneurs en cours d'exécution ; `docker ps -a` montre `web` avec le statut `Created`.

!!! success "Point de contrôle"
    - [ ] `docker ps -a` affiche `web` avec le statut `Created`
    - [ ] `docker inspect` affiche `created`

### Étape 2 : Démarrer le conteneur

```bash
docker start web
docker ps
docker inspect --format '{{.State.Status}}' web
```

!!! success "Point de contrôle"
    - [ ] `docker ps` affiche `web` avec un statut commençant par `Up`
    - [ ] `docker inspect` affiche `running`

### Étape 3 : Observer un conteneur dont le processus se termine

Lancez deux conteneurs dont le processus principal s'arrête de lui-même :

```bash
docker run --name court alpine:3.20 echo "Bonjour depuis un conteneur"
docker run --name erreur alpine:3.20 sh -c "exit 3"
docker ps -a
```

Le premier affiche son message puis s'arrête. Le second ne produit rien et s'arrête avec une erreur. Lisez leur état et leur **code de sortie** :

```bash
docker inspect --format '{{.State.Status}} {{.State.ExitCode}}' court
docker inspect --format '{{.State.Status}} {{.State.ExitCode}}' erreur
```

Un code de sortie `0` indique une fin normale ; toute autre valeur signale une erreur.

!!! success "Point de contrôle"
    - [ ] `court` est à l'état `exited` avec le code `0`
    - [ ] `erreur` est à l'état `exited` avec le code `3`
    - [ ] Dans `docker ps -a`, ces deux conteneurs apparaissent avec un statut `Exited`

### Étape 4 : Lire les journaux

Lancez un conteneur qui écrit l'heure chaque seconde :

```bash
docker run -d --name boucle alpine:3.20 sh -c 'while true; do date; sleep 1; done'
docker logs --tail 5 boucle
```

Suivez ensuite les journaux en continu :

```bash
docker logs -f boucle
```

Arrêtez le suivi avec `Ctrl+C` : le conteneur, lui, continue de tourner.

!!! success "Point de contrôle"
    - [ ] `docker logs --tail 5` affiche les cinq dernières lignes
    - [ ] Avec `-f`, de nouvelles lignes apparaissent chaque seconde
    - [ ] Après `Ctrl+C`, `docker ps` montre toujours `boucle` à l'état `Up`

### Étape 5 : Exécuter une commande dans un conteneur

Utilisez `web`, qui tourne :

```bash
docker exec web ls /usr/share/nginx/html
docker exec -it web sh
```

Dans le terminal ouvert, exécutez `ps`, puis `exit`.

Vérifiez que le conteneur n'est pas arrêté :

```bash
docker ps
```

!!! success "Point de contrôle"
    - [ ] La première commande liste des fichiers de la page d'accueil de nginx
    - [ ] `ps` dans le conteneur montre le processus `nginx`
    - [ ] Après `exit`, `web` est toujours `Up`

### Étape 6 : Arrêter et redémarrer

Arrêtez `web`, puis `boucle`, en observant la durée de chaque commande :

```bash
docker stop web
docker stop boucle
docker ps -a
```

Un conteneur arrêté de façon normale a un code de sortie bas ; un conteneur arrêté de force, comme `boucle`, a un code plus élevé. Comparez :

```bash
docker inspect --format '{{.State.Status}} {{.State.ExitCode}}' web
docker inspect --format '{{.State.Status}} {{.State.ExitCode}}' boucle
```

Redémarrez `web` :

```bash
docker start web
docker restart web
docker ps
```

!!! info "Pourquoi `boucle` est-il plus long à arrêter ?"
    `docker stop` demande au processus principal de s'arrêter proprement et attend, par défaut, jusqu'à 10 secondes avant de l'arrêter de force. Le programme lancé dans `boucle` ne réagit pas à cette demande : Docker doit donc attendre la fin du délai. nginx, lui, s'arrête immédiatement.

!!! success "Point de contrôle"
    - [ ] `docker stop boucle` a pris nettement plus de temps que `docker stop web`
    - [ ] `docker inspect` affiche un code de sortie différent pour `boucle` et pour `web`
    - [ ] Après `docker restart`, `web` est de nouveau `Up`

### Étape 7 : Supprimer les conteneurs

Essayez de supprimer `web`, qui tourne encore :

```bash
docker rm web
```

Docker refuse : il faut d'abord arrêter le conteneur, ou forcer la suppression :

```bash
docker rm -f web
```

Supprimez ensuite les trois autres :

```bash
docker rm court erreur boucle
docker ps -a
```

!!! success "Point de contrôle"
    - [ ] Docker a refusé `docker rm web` tant que le conteneur tournait
    - [ ] `docker ps -a` n'affiche plus aucun des quatre conteneurs du lab

## Questions de réflexion

??? question "Pourquoi `court` est-il arrêté alors que personne ne l'a arrêté ?"
    Son processus principal (`echo`) s'est terminé après avoir affiché son message. Un conteneur vit aussi longtemps que son processus principal.

??? question "Pourquoi `exit` dans `docker exec -it web sh` n'arrête-t-il pas le conteneur `web` ?"
    Le shell lancé par `docker exec` est un processus **supplémentaire**. Le processus principal du conteneur reste nginx, qui continue de tourner.

??? question "Quelle information le code de sortie apporte-t-il lors d'un diagnostic ?"
    Il indique si le processus principal s'est terminé normalement (0) ou en erreur (autre valeur), ce qui oriente la lecture des journaux avec `docker logs`.

## Dépannage

| Symptôme | Pistes |
|---|---|
| `The container name "/web" is already in use` | Un conteneur `web` existe déjà (peut-être celui du Lab 1.2) : supprimez-le avec `docker rm -f web` |
| `docker logs` n'affiche rien | Le conteneur n'a rien écrit : vérifiez avec `docker ps -a` que vous interrogez le bon conteneur |
| `docker exec` renvoie `container ... is not running` | Le conteneur est arrêté : démarrez-le avec `docker start` |
| `docker stop boucle` semble bloqué | C'est normal : Docker attend jusqu'à 10 secondes avant l'arrêt forcé |
| Sous PowerShell, la commande de `boucle` est rejetée | Vérifiez les guillemets simples autour de `while true; do date; sleep 1; done` |

## Nettoyage et reprise

Si un conteneur du lab subsiste :

```bash
docker rm -f web court erreur boucle
```

Les noms absents provoquent un message d'erreur sans gravité.

## Retour au chapitre

[Chapitre 2 : Cycle de vie des conteneurs](cours.md) · Lab suivant : [Lab 2.2 : Publier et configurer un service](lab-2-2-publier-et-configurer-un-service.md)