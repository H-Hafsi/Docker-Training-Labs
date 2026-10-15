# Quiz du chapitre 14 : Livraison continue

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Quelle étape la livraison continue ajoute-t-elle au pipeline du chapitre 13 ?

- A. La construction de l'image
- B. Le déploiement sur le cluster, suivi d'une vérification et, si besoin, d'un retour arrière
- C. L'écriture du Dockerfile
- D. La création du compte Docker Hub

??? success "Réponse"
    **B.** Le chapitre 13 s'arrête à la publication de l'image. La livraison continue y ajoute le déploiement, la vérification du résultat et le retour arrière (section 1).

**Question 2.** Pourquoi préfère-t-on `docker stack deploy` à `docker service update --image` pour un déploiement normal ?

- A. Parce qu'il est plus rapide
- B. Parce qu'il applique tout le fichier de stack, qui reste la référence de l'état désiré
- C. Parce qu'il ne nécessite pas d'image publiée
- D. Parce qu'il supprime automatiquement les anciennes versions de Docker Hub

??? success "Réponse"
    **B.** Avec `docker stack deploy`, le fichier versionné reste la référence : secrets, réseaux et limites sont appliqués avec la version. Avec `docker service update`, le service peut diverger du fichier (section 2).

**Question 3.** Dans un fichier de stack, que produit `image: monimage:${TAG:?La variable TAG est obligatoire}` si la variable `TAG` n'est pas définie ?

- A. Le déploiement utilise le tag `latest`
- B. Le déploiement utilise une chaîne vide
- C. Le déploiement échoue avec le message indiqué
- D. Le déploiement lit la valeur dans le fichier `.env`

??? success "Réponse"
    **C.** La syntaxe `${VARIABLE:?message}` provoque une erreur si la variable est absente, ce qui empêche un déploiement sans version. De plus, `docker stack deploy` ne lit pas le fichier `.env` : la variable doit être exportée dans le shell (section 2.1).

**Question 4.** Pourquoi un runner hébergé par GitHub ne peut-il pas déployer sur un cluster de machines virtuelles locales ?

- A. Parce que Swarm refuse les connexions de GitHub
- B. Parce que ces machines sont sur un réseau privé, inaccessible depuis Internet
- C. Parce que les runners hébergés n'ont pas Docker
- D. Parce que les runners hébergés ne peuvent exécuter que des tests

??? success "Réponse"
    **B.** Le runner hébergé s'exécute sur Internet et ne peut pas joindre une machine sans adresse publique (section 3).

**Question 5.** Comment un runner auto-hébergé reçoit-il ses jobs ?

- A. GitHub se connecte au runner par un port ouvert sur votre machine
- B. Le runner contacte GitHub par une connexion sortante pour demander du travail
- C. Les jobs sont copiés à la main sur la machine
- D. Le runner interroge Docker Hub

??? success "Réponse"
    **B.** Le runner initie la connexion vers GitHub : aucun port entrant n'est nécessaire, ce qui convient aux réseaux privés (section 3).

**Question 6.** Pourquoi déconseille-t-on d'associer un runner auto-hébergé à un dépôt public ?

- A. Parce que les dépôts publics n'ont pas de workflows
- B. Parce que le runner est plus lent avec un dépôt public
- C. Parce que GitHub ne permet pas d'installer de runner dans ce cas
- D. Parce que n'importe qui pourrait proposer du code qui s'exécuterait sur votre machine avec les droits du runner

??? success "Réponse"
    **D.** Le runner exécute le code des workflows sur votre machine, avec les droits de Docker, donc de fait ceux de l'administrateur. Il ne doit exécuter que du code de confiance (section 3).

**Question 7.** Le déploiement se termine sans erreur. Pourquoi faut-il encore vérifier l'application ?

- A. Parce que la commande de déploiement ne fait que lancer la mise à jour, dont le résultat n'est pas garanti
- B. Parce que Docker Hub peut avoir supprimé l'image
- C. Parce que le déploiement s'exécute toujours deux fois
- D. Parce que le runner ne conserve pas les journaux

??? success "Réponse"
    **A.** `docker stack deploy` déclenche la mise à jour, qui se poursuit dans le cluster. Seule une vérification du comportement du service montre que l'application fonctionne (section 7).

**Question 8.** Une mise à jour échoue : les nouvelles tâches ne démarrent pas, et Swarm revient seul à l'ancienne version (`failure_action: rollback`). Le pipeline contient une vérification qui envoie seulement une requête à l'application. Que peut-il arriver ?

- A. Le pipeline échoue forcément
- B. Le pipeline passe, car l'ancienne version répond encore : la vérification doit aussi contrôler la version en service et l'état de la mise à jour
- C. Le pipeline supprime le service
- D. Le pipeline republie l'image

??? success "Réponse"
    **B.** L'ancienne version répond, donc la vérification de la réponse réussit alors que la nouvelle version n'est pas en service. Il faut contrôler la **version** et l'**état de la mise à jour** (sections 7 et 8).

**Question 9.** Après un retour arrière automatique, pourquoi faut-il aussi intervenir dans Git ?

- A. Parce que Git doit être redémarré
- B. Parce que le retour arrière efface l'historique
- C. Parce que le retour arrière répare le cluster mais pas le dépôt, qui contient toujours la version défectueuse et la réinstallerait au prochain déploiement
- D. Parce que Docker Hub synchronise ses tags avec Git

??? success "Réponse"
    **C.** On annule ou corrige le commit fautif pour que le dépôt, le fichier de stack et le cluster décrivent de nouveau le même état (section 8).

**Question 10.** À quoi sert la règle `concurrency` d'un workflow de déploiement ?

- A. À accélérer le déploiement
- B. À répartir les tâches entre plusieurs runners
- C. À chiffrer les secrets
- D. À empêcher que deux déploiements s'exécutent en même temps sur la même stack

??? success "Réponse"
    **D.** Avec un groupe de concurrence, un second déploiement attend la fin du premier. Sans cela, deux opérations simultanées sur la même stack donneraient un état imprévisible (sections 4 et 5).

!!! tip "Pour aller plus loin"
    Si plusieurs réponses sont fausses, refaites le [Lab 14.1](lab-14-1-deploiement-automatise-sur-swarm.md) (runner, variable de version, déclenchement) ou le [Lab 14.2](lab-14-2-pipeline-complet-avec-retour-arriere.md) (pipeline complet, vérification, retour arrière).