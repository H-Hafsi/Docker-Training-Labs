# Quiz du chapitre 10 : Sécurité des conteneurs

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Pourquoi l'isolation d'un conteneur est-elle moins forte que celle d'une machine virtuelle ?

- A. Parce qu'un conteneur n'a pas de système de fichiers propre
- B. Parce que les conteneurs partagent le noyau de l'hôte
- C. Parce que les conteneurs ne peuvent pas être limités en ressources
- D. Parce que les conteneurs ne disposent pas de réseau privé

??? success "Réponse"
    **B.** Les conteneurs sont des processus isolés qui partagent le noyau de l'hôte : une faille du noyau ou une mauvaise configuration peut permettre de dépasser les limites du conteneur (section 1).

**Question 2.** Quel est l'utilisateur par défaut du processus d'un conteneur, si le Dockerfile n'indique rien ?

- A. Un utilisateur anonyme sans droits
- B. L'utilisateur qui a lancé `docker run` sur l'hôte
- C. `root` (identifiant 0)
- D. Un utilisateur choisi aléatoirement

??? success "Réponse"
    **C.** Sans instruction `USER` ni option `--user`, le processus s'exécute en root dans le conteneur (section 2.1).

**Question 3.** Quelle instruction du Dockerfile fait s'exécuter la suite et le conteneur avec un utilisateur ordinaire ?

- A. `RUN user appuser`
- B. `USER appuser`
- C. `WORKDIR appuser`
- D. `EXPOSE appuser`

??? success "Réponse"
    **B.** `USER` définit l'utilisateur des instructions suivantes et du processus du conteneur ; on la place après les instructions qui exigent des droits d'administrateur (section 2.2).

**Question 4.** Que fait l'option `--read-only` de `docker run` ?

- A. Elle empêche de lire les journaux du conteneur
- B. Elle rend le système de fichiers du conteneur accessible uniquement en lecture
- C. Elle interdit toute connexion réseau
- D. Elle supprime les volumes à l'arrêt

??? success "Réponse"
    **B.** Un attaquant ne peut alors ni modifier les programmes, ni déposer de fichiers. On rouvre l'écriture aux seuls endroits nécessaires, avec `--tmpfs` ou un volume (section 3).

**Question 5.** Une application démarre avec `--read-only` puis s'arrête avec `Read-only file system`. Que faut-il faire ?

- A. Retirer `--read-only`
- B. Lancer le conteneur en `--privileged`
- C. Identifier le chemin signalé dans les journaux et le monter en écriture (`--tmpfs` ou volume)
- D. Réinstaller l'image

??? success "Réponse"
    **C.** On conserve la protection et on ouvre l'écriture uniquement à l'endroit dont l'application a besoin (section 3).

**Question 6.** Quelle est la méthode du moindre privilège pour les capabilities ?

- A. Retirer une par une les capabilities que l'on sait dangereuses
- B. Garder les capabilities par défaut
- C. Tout retirer avec `--cap-drop ALL`, puis ajouter seulement celles qui sont nécessaires
- D. Utiliser `--privileged` pour éviter les erreurs

??? success "Réponse"
    **C.** On part de zéro et on ajoute une capability à la fois, après avoir constaté qu'elle est nécessaire. `--privileged` donne au contraire toutes les capabilities (section 4.2).

**Question 7.** Pourquoi le montage du socket du moteur (`/var/run/docker.sock`) dans un conteneur est-il dangereux ?

- A. Il ralentit le conteneur
- B. Il donne au conteneur la possibilité de piloter le moteur Docker, donc un accès administrateur à l'hôte
- C. Il empêche le conteneur de démarrer
- D. Il supprime les images locales

??? success "Réponse"
    **B.** Qui contrôle le moteur Docker contrôle la machine : on peut y lancer un conteneur qui monte n'importe quel dossier de l'hôte (sections 1 et 4.3).

**Question 8.** Pourquoi un mot de passe défini avec `ENV` ou `ARG` dans un Dockerfile reste-t-il un problème, même si on le supprime ensuite ?

- A. Il ralentit la construction
- B. Il reste enregistré dans les couches et les métadonnées de l'image, visible avec `docker history` ou `docker inspect`
- C. Docker refuse de construire l'image
- D. Il est automatiquement chiffré, mais illisible

??? success "Réponse"
    **B.** Les couches sont immuables : une suppression ultérieure ne retire pas le secret des couches existantes. Un secret exposé doit être révoqué et remplacé (section 5.1).

**Question 9.** Quelle méthode recommandée fournit un mot de passe à l'image `postgres` ?

- A. `-e POSTGRES_PASSWORD=...` dans la commande, car c'est le plus simple
- B. Un fichier monté en lecture seule, lu via `POSTGRES_PASSWORD_FILE`
- C. Une instruction `ENV` dans un Dockerfile dérivé
- D. Le nom du conteneur

??? success "Réponse"
    **B.** La variable ne contient que le chemin du fichier : le secret n'apparaît ni dans `docker inspect` ni dans l'image (sections 5.2 et 5.3).

**Question 10.** Un scanner de vulnérabilités ne signale aucune faille critique dans votre image. Que peut-on en conclure ?

- A. Que l'image est sûre et ne nécessite plus d'analyse
- B. Qu'aucune faille connue de gravité critique n'a été trouvée, à la date de l'analyse et avec la base utilisée
- C. Que le conteneur ne peut pas être attaqué
- D. Que l'image n'a plus besoin d'être mise à jour

??? success "Réponse"
    **B.** Le scanner ne couvre que les failles **connues**, et de nouvelles sont découvertes en continu : il faut réanalyser régulièrement et conserver les autres protections (section 6.2).