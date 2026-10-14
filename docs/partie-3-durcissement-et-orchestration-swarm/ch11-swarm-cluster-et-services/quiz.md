# Quiz du chapitre 11 : Swarm : cluster et services

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Quel besoin un orchestrateur comme Swarm satisfait-il, et pas Docker Compose utilisé sur une seule machine ?

- A. Décrire une application dans un fichier
- B. Maintenir une application disponible malgré la panne d'une machine
- C. Construire des images
- D. Publier des ports

??? success "Réponse"
    **B.** Sur une seule machine, la panne de celle-ci arrête tout. Un orchestrateur gère plusieurs machines et recrée les conteneurs ailleurs en cas de panne (section 1).

**Question 2.** Quel est le rôle d'un manager dans un cluster Swarm ?

- A. Exécuter uniquement les conteneurs d'application
- B. Conserver l'état du cluster, accepter les commandes d'administration et décider du placement
- C. Stocker les images
- D. Fournir l'accès à Internet aux workers

??? success "Réponse"
    **B.** Les managers conservent et répliquent l'état du cluster et prennent les décisions. Les workers exécutent les tâches (section 2).

**Question 3.** Pourquoi choisit-on un nombre impair de managers ?

- A. Parce que Docker refuse un nombre pair
- B. Pour que la majorité (le quorum) reste disponible malgré des pannes, avec le moins de machines possible
- C. Pour que chaque worker ait un manager attitré
- D. Pour accélérer les services

??? success "Réponse"
    **B.** Le cluster fonctionne si la majorité des managers est disponible : 3 managers tolèrent 1 panne, comme 4, avec une machine de moins (section 2.1).

**Question 4.** Sur quelle machine exécute-t-on `docker node ls` ?

- A. Sur n'importe quel nœud
- B. Uniquement sur un worker
- C. Uniquement sur un manager
- D. Sur une machine extérieure au cluster

??? success "Réponse"
    **C.** Les commandes d'administration du cluster ne fonctionnent que sur un manager ; un worker répond qu'il n'est pas un manager (section 2).

**Question 5.** Que représente le jeton affiché par `docker swarm init` et demandé par `docker swarm join` ?

- A. Le mot de passe du compte Docker Hub
- B. Un secret qui autorise une machine à rejoindre le cluster
- C. Un identifiant de conteneur
- D. Le nom du service

??? success "Réponse"
    **B.** Quiconque possède le jeton et peut joindre le port 2377 du manager peut rejoindre le cluster : il est secret, et se renouvelle avec `--rotate` (section 3.2).

**Question 6.** Quelle est la différence entre un service répliqué et un service global ?

- A. Le service global tourne uniquement sur les managers
- B. Le service répliqué a un nombre fixe de tâches ; le service global a une tâche par nœud
- C. Le service global ne peut pas publier de port
- D. Il n'y a aucune différence

??? success "Réponse"
    **B.** En mode global (`--mode global`), Swarm place une tâche sur chaque nœud, y compris ceux ajoutés plus tard (section 5).

**Question 7.** Un service de 3 répliques perd un conteneur supprimé à la main. Que fait Swarm ?

- A. Rien : l'état du service est figé
- B. Il supprime le service
- C. Il crée une nouvelle tâche pour revenir à 3 répliques
- D. Il demande une confirmation à l'administrateur

??? success "Réponse"
    **C.** Swarm compare en permanence l'état réel à l'état désiré et corrige l'écart : c'est la boucle de réconciliation (section 2.2 et 5.1).

**Question 8.** Pourquoi un service créé avec une image construite uniquement sur le manager échoue-t-il sur les workers ?

- A. Les workers ne peuvent pas exécuter d'images
- B. Chaque nœud télécharge lui-même l'image depuis un registre, et l'image locale du manager n'y est pas
- C. Le manager interdit de partager les images
- D. Le service doit être global

??? success "Réponse"
    **B.** Les images doivent être accessibles à tous les nœuds : on les publie dans un registre (section 4.3).

**Question 9.** Un service publie le port 8080. Que se passe-t-il quand on envoie une requête à un nœud qui n'exécute aucune tâche de ce service ?

- A. La requête est refusée
- B. La requête est transmise à une tâche du service grâce au routing mesh
- C. Le nœud démarre automatiquement une tâche
- D. La requête est mise en attente indéfiniment

??? success "Réponse"
    **B.** Le port publié est ouvert sur tous les nœuds ; le routing mesh redirige la requête vers une tâche du service et répartit la charge (section 6).

**Question 10.** Vous mettez un nœud en `drain`, puis, après la maintenance, en `active`. Que devient la charge ?

- A. Les tâches déplacées reviennent automatiquement sur ce nœud
- B. Le nœud reçoit de nouvelles tâches mais ne reprend pas automatiquement les anciennes
- C. Le service est supprimé
- D. Le nœud devient manager

??? success "Réponse"
    **B.** Avec `drain`, les tâches sont recréées ailleurs ; Swarm ne rééquilibre pas automatiquement au retour du nœud. On peut modifier le nombre de répliques pour redistribuer (section 7).