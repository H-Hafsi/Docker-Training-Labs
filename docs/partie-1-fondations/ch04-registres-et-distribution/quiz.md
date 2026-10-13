# Quiz du chapitre 4 : Registres et distribution

!!! abstract "Consignes"
Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Quel est le rôle d'un registre ?

- A. Exécuter des conteneurs
- B. Construire des images à partir d'un Dockerfile
- C. Stocker des images et les distribuer
- D. Isoler les processus d'un conteneur

??? success "Réponse"
**C.** Un registre stocke les images et les distribue à ceux qui les demandent. La construction relève de `docker build`, l'exécution du moteur Docker (section 1).

**Question 2.** Que fait la commande `docker push` ?

- A. Elle envoie une image locale vers un registre
- B. Elle télécharge une image depuis un registre
- C. Elle supprime une image du registre
- D. Elle construit une image à partir d'un Dockerfile

??? success "Réponse"
**A.** `docker push` envoie l'image vers un registre ; `docker pull` fait l'opération inverse (section 1).

**Question 3.** Quelle est l'écriture complète de `nginx:1.27-alpine` ?

- A. `hub.docker.com/nginx:1.27-alpine`
- B. `library/docker.io/nginx:1.27-alpine`
- C. `docker.io/nginx/library:1.27-alpine`
- D. `docker.io/library/nginx:1.27-alpine`

??? success "Réponse"
**D.** Le nom complet suit la forme `registre/espace-de-noms/dépôt:tag`. Ici, le registre par défaut est `docker.io` (Docker Hub) et l'espace de noms des images officielles est `library` (section 2).

**Question 4.** Dans le nom `localhost:5000/monapp:1.0`, quelle partie désigne le registre ?

- A. `monapp`
- B. `localhost:5000`
- C. `1.0`
- D. `monapp:1.0`

??? success "Réponse"
**B.** L'adresse du registre figure au début du nom. `monapp` est le dépôt et `1.0` le tag (section 2).

**Question 5.** Pourquoi faut-il exécuter `docker tag monapp:1.0 monutilisateur/monapp:1.0` avant de publier l'image sur Docker Hub ?

- A. Pour compresser l'image
- B. Pour chiffrer l'image
- C. Pour que son nom commence par votre espace de noms
- D. Pour télécharger l'image sur la machine

??? success "Réponse"
**C.** Docker Hub range les images par espace de noms : sans le nom de votre compte, l'envoi serait refusé. `docker tag` ajoute un nom à l'image existante sans la copier (section 3).

**Question 6.** Pourquoi préfère-t-on un jeton d'accès au mot de passe du compte pour `docker login` ?

- A. Un jeton a des droits limités et peut être révoqué sans changer le mot de passe du compte
- B. Un jeton rend le téléchargement des images plus rapide
- C. Docker Hub interdit l'usage du mot de passe avec Docker
- D. Un jeton chiffre les images publiées

??? success "Réponse"
**A.** Un jeton peut être créé pour un usage précis et révoqué à tout moment, par exemple en cas de fuite. Il ne change rien à la vitesse ni au chiffrement des images (section 3.1).

**Question 7.** Vous corrigez un bogue de la version `1.4.2`, sans ajouter de fonctionnalité. Quelle est la nouvelle version selon le versionnage sémantique ?

- A. `2.0.0`
- B. `1.5.0`
- C. `1.4.0`
- D. `1.4.3`

??? success "Réponse"
**D.** Une correction d'anomalie incrémente le numéro de **correctif**. Le numéro mineur augmente pour une nouvelle fonctionnalité compatible, le numéro majeur pour un changement incompatible (section 4.1).

**Question 8.** Quelle affirmation sur les tags et les digests est exacte ?

- A. Un tag désigne toujours la même image, quoi qu'il arrive
- B. Un digest désigne toujours la même image, alors qu'un tag peut être réaffecté à une autre
- C. Un digest est le nom lisible d'une version
- D. Deux images différentes peuvent avoir le même digest

??? success "Réponse"
**B.** Le digest est une empreinte du contenu de l'image : il est immuable. Un tag est un nom que le propriétaire du dépôt peut faire pointer vers une autre image (section 4.3).

**Question 9.** Quelle commande lance un registre privé pour un TP ?

- A. `docker run -d -p 5000:5000 nginx`
- B. `docker registry start`
- C. `docker run -d --name registre -p 5000:5000 registry:2`
- D. `docker push registre`

??? success "Réponse"
**C.** Docker fournit l'image officielle `registry`, qu'on lance comme n'importe quel conteneur en publiant son port 5000 (section 5.2). La commande `docker registry` n'existe pas.

**Question 10.** Pourquoi Docker refuse-t-il par défaut d'utiliser, depuis une autre machine, un registre qui fonctionne sans chiffrement ?

- A. Il exige HTTPS pour tout registre autre que `localhost`, sauf déclaration explicite dans la configuration du daemon
- B. Un registre ne peut être utilisé que depuis la machine qui l'héberge
- C. Le port 5000 est réservé à un usage interne de Docker
- D. Les images ne peuvent pas être envoyées dans un registre privé

??? success "Réponse"
**A.** Docker accepte de communiquer sans chiffrement avec `localhost`, mais exige HTTPS pour les autres registres. Pour un TP, on peut déclarer le registre comme « non sécurisé » ; en production, on le protège par TLS (section 5.3 et Lab 4.2).
