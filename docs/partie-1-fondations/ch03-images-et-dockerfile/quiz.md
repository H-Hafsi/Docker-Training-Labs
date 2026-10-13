# Quiz du chapitre 3 : Images et Dockerfile

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Quelle affirmation décrit correctement une image Docker ?

- A. Un conteneur en cours d'exécution
- B. Un modèle en lecture seule, formé de couches empilées
- C. Une machine virtuelle complète avec son noyau
- D. Un fichier de configuration du daemon

??? success "Réponse"
    **B.** Une image est un modèle en lecture seule composé de couches ; un conteneur en est une instance (section 1).

**Question 2.** Où sont enregistrées les données qu'un conteneur écrit pendant son exécution ?

- A. Dans la dernière couche de l'image
- B. Dans le registre
- C. Dans le Dockerfile
- D. Dans une couche d'écriture propre au conteneur, supprimée avec lui

??? success "Réponse"
    **D.** Docker ajoute une fine couche d'écriture au-dessus des couches de l'image, en lecture seule. Elle disparaît avec le conteneur, et l'image n'est pas modifiée (section 1).

**Question 3.** Quelle est la différence entre `RUN` et `CMD` dans un Dockerfile ?

- A. `RUN` s'exécute pendant la construction de l'image ; `CMD` définit la commande lancée au démarrage du conteneur
- B. `RUN` s'exécute au démarrage du conteneur ; `CMD` pendant la construction
- C. `RUN` est réservé à Linux et `CMD` à Windows
- D. Il n'y a aucune différence, les deux instructions sont interchangeables

??? success "Réponse"
    **A.** `RUN` crée une couche lors de `docker build` (installation de paquets, par exemple). `CMD` enregistre la commande par défaut exécutée quand on démarre un conteneur (section 2.2).

**Question 4.** Que fait l'instruction `EXPOSE 5000` ?

- A. Elle publie le port 5000 sur la machine hôte
- B. Elle ouvre le port 5000 dans le pare-feu de l'hôte
- C. Elle documente le port sur lequel l'application écoute, sans le publier
- D. Elle redirige le port 5000 vers le port 80

??? success "Réponse"
    **C.** `EXPOSE` est une indication pour les lecteurs de l'image. Pour joindre le service depuis l'hôte, il faut publier le port avec `-p` au lancement du conteneur (section 2.1).

**Question 5.** Que fait la commande `docker build -t monapp:1.0 .` ?

- A. Elle lance un conteneur nommé `monapp`
- B. Elle construit une image nommée `monapp` avec le tag `1.0`, à partir du contexte du dossier courant
- C. Elle télécharge l'image `monapp:1.0` depuis Docker Hub
- D. Elle supprime l'image `monapp:1.0`

??? success "Réponse"
    **B.** `-t` donne le nom et le tag, et le point final désigne le **contexte de construction**, ici le dossier courant (section 3).

**Question 6.** Vous modifiez une instruction au milieu d'un Dockerfile. Que devient le cache des instructions qui la suivent ?

- A. Elles sont réexécutées
- B. Elles restent lues dans le cache
- C. Seule l'instruction `COPY` est réexécutée
- D. Docker demande une confirmation avant de les réexécuter

??? success "Réponse"
    **A.** Dès qu'une couche est invalidée, toutes les instructions suivantes sont réexécutées. C'est pourquoi on place en premier ce qui change rarement (section 4).

**Question 7.** Pour une application Python, quel ordre d'instructions exploite le mieux le cache ?

- A. `COPY . .` puis `RUN pip install -r requirements.txt`
- B. `RUN pip install -r requirements.txt` puis `COPY requirements.txt .`
- C. `COPY . .` puis `COPY requirements.txt .`
- D. `COPY requirements.txt .`, puis `RUN pip install -r requirements.txt`, puis `COPY . .`

??? success "Réponse"
    **D.** La liste des dépendances est copiée seule : l'installation reste dans le cache tant qu'elle ne change pas, même si le code est modifié. Avec l'ordre A, chaque modification du code relance l'installation. L'ordre B échoue, car le fichier doit être copié avant d'être utilisé (section 4).

**Question 8.** Pourquoi faut-il éviter de s'appuyer sur le tag `latest` ?

- A. Docker interdit son utilisation
- B. Il télécharge toujours la plus ancienne version de l'image
- C. Il n'est que le tag par défaut et peut désigner des versions différentes au fil du temps
- D. Il rend l'image plus volumineuse

??? success "Réponse"
    **C.** `latest` n'est pas « la dernière version » : c'est le tag utilisé quand aucun tag n'est précisé. Une version explicite rend les constructions reproductibles (section 5).

**Question 9.** À quoi sert le fichier `.dockerignore` ?

- A. À exclure des fichiers du contexte de construction : construction plus rapide, image plus petite, secrets non copiés
- B. À empêcher l'exécution d'un conteneur
- C. À ignorer les erreurs pendant la construction
- D. À masquer certaines images dans la liste de `docker images`

??? success "Réponse"
    **A.** Les fichiers listés ne sont pas envoyés au daemon lors de `docker build` et ne peuvent donc pas être copiés dans l'image (section 6).

**Question 10.** Quelle commande affiche les couches d'une image et l'instruction qui a créé chacune ?

- A. `docker logs`
- B. `docker history`
- C. `docker ps`
- D. `docker port`

??? success "Réponse"
    **B.** `docker history <image>` liste les couches, de la plus récente à la plus ancienne, avec leur taille et l'instruction correspondante (section 3 et Lab 3.1).