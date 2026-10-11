# Quiz du chapitre 2 : Cycle de vie des conteneurs

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Que fait la commande `docker run` ?

- A. Elle télécharge seulement l'image
- B. Elle crée un conteneur sans le démarrer
- C. Elle crée un conteneur, le démarre, et télécharge l'image si elle est absente
- D. Elle redémarre un conteneur arrêté

??? success "Réponse"
    **C.** `docker run` enchaîne la création et le démarrage, et télécharge l'image au besoin. La création seule relève de `docker create`, et le redémarrage d'un conteneur existant de `docker start` (section 1).

**Question 2.** Pourquoi un conteneur s'arrête-t-il tout seul après avoir affiché un message ?

- A. Son processus principal s'est terminé
- B. Docker arrête tout conteneur après 10 secondes
- C. Aucun port n'a été publié
- D. L'image utilisée est en lecture seule

??? success "Réponse"
    **A.** Un conteneur vit aussi longtemps que son processus principal : dès que celui-ci se termine, le conteneur s'arrête (section 2). Le délai de 10 secondes concerne seulement l'arrêt demandé par `docker stop`.

**Question 3.** Après `docker stop web`, quelle affirmation est exacte ?

- A. Le conteneur `web` est supprimé
- B. Le conteneur `web` existe toujours et peut être redémarré avec `docker start`
- C. Le nom `web` est de nouveau disponible pour un autre conteneur
- D. L'image utilisée par `web` est supprimée

??? success "Réponse"
    **B.** Un conteneur arrêté existe encore, avec son nom : seul `docker rm` le supprime. Le nom `web` reste donc pris tant que le conteneur n'est pas supprimé (sections 1 et 3).

**Question 4.** Vous ouvrez un terminal dans le conteneur `web` avec `docker exec -it web sh`, puis vous tapez `exit`. Que devient le conteneur `web` ?

- A. Il est supprimé
- B. Il est arrêté
- C. Il redémarre
- D. Il continue de tourner, car son processus principal n'a pas changé

??? success "Réponse"
    **D.** Le shell lancé par `docker exec` est un processus supplémentaire. Le processus principal du conteneur (nginx, par exemple) n'est pas concerné par `exit` (section 6 et Lab 2.1).

**Question 5.** Que signifie l'option `-p 8080:80` ?

- A. Le port 80 de l'hôte est redirigé vers le port 8080 du conteneur
- B. Les ports 8080 et 80 du conteneur sont ouverts
- C. Le port 8080 de l'hôte est redirigé vers le port 80 du conteneur
- D. Le port 8080 du conteneur est redirigé vers le port 80 d'un autre conteneur

??? success "Réponse"
    **C.** La forme générale est `-p <port hôte>:<port conteneur>` : le premier nombre désigne l'hôte, le second le conteneur (section 4).

**Question 6.** Quel est l'effet de `-p 127.0.0.1:8082:80` ?

- A. Le service n'est accessible que depuis la machine locale
- B. Le service est accessible depuis toutes les machines du réseau
- C. Le conteneur est limité à un seul processeur
- D. Le port 80 de la machine 127.0.0.1 est publié sur le conteneur

??? success "Réponse"
    **A.** En préfixant le port par `127.0.0.1`, la publication est restreinte à l'hôte lui-même (section 4).

**Question 7.** Vous voulez lancer deux conteneurs nginx, dont le port interne est 80, sur la même machine. Quelle publication de ports fonctionne ?

- A. `-p 80:80` pour les deux conteneurs
- B. `-p 8080:80` pour l'un et `-p 8081:80` pour l'autre
- C. `-p 8080:80` pour les deux conteneurs
- D. `-p 80:8080` pour les deux conteneurs

??? success "Réponse"
    **B.** Chaque conteneur a son propre réseau, donc le port 80 interne ne pose pas de problème. En revanche, un port de l'**hôte** ne peut être utilisé que par un seul conteneur : il faut deux ports d'hôte différents (section 4).

**Question 8.** Pourquoi est-il déconseillé de transmettre un mot de passe réel avec l'option `-e` ?

- A. Docker refuse les variables qui contiennent un mot de passe
- B. Les variables ne sont lues qu'au redémarrage du conteneur
- C. Les variables sont chiffrées et l'application ne peut pas les lire
- D. Les variables sont visibles avec `docker inspect` par quiconque a accès à Docker

??? success "Réponse"
    **D.** Une variable d'environnement n'est pas un coffre-fort : elle apparaît dans la configuration du conteneur, visible avec `docker inspect`. Le chapitre 10 présente de meilleures pratiques (section 5).

**Question 9.** Un conteneur lancé en arrière-plan n'apparaît pas dans `docker ps`. Quel est le bon premier réflexe ?

- A. Lancer `docker ps -a` pour voir son état, puis `docker logs` pour lire son message
- B. Réinstaller Docker
- C. Supprimer l'image et la télécharger de nouveau
- D. Redémarrer la machine

??? success "Réponse"
    **A.** Le conteneur s'est probablement arrêté : `docker ps -a` montre son état et son code de sortie, et `docker logs` affiche ce que son processus principal a écrit avant de s'arrêter (section 6 et Lab 2.2).

**Question 10.** Quelle option limite la mémoire qu'un conteneur peut utiliser ?

- A. `--cpus 0.5`
- B. `-p 256`
- C. `--memory 256m`
- D. `-e MEMOIRE=256m`

??? success "Réponse"
    **C.** `--memory` plafonne la mémoire grâce aux cgroups. `--cpus` limite le processeur, `-p` publie un port, et `-e` définit une variable d'environnement que Docker n'interprète pas comme une limite (section 7).