# Quiz du chapitre 13 : Intégration continue

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Quelle est la différence entre la livraison continue et le déploiement continu ?

- A. Aucune : ce sont deux noms du même processus
- B. La livraison continue prépare une version prête à déployer, et une personne déclenche la mise en production ; le déploiement continu déploie automatiquement
- C. Le déploiement continu ne comporte pas de tests
- D. La livraison continue ne concerne que les applications sans conteneur

??? success "Réponse"
    **B.** Dans les deux cas, la construction, les tests et la publication sont automatisés. La différence tient à la mise en production : volontaire dans la livraison continue, automatique dans le déploiement continu (section 1.1).

**Question 2.** Dans quel ordre place-t-on habituellement les étapes d'un pipeline de construction d'image ?

- A. Publier, tester, construire
- B. Tester, publier, construire
- C. Construire, tester, analyser, publier
- D. Analyser, publier, construire, tester

??? success "Réponse"
    **C.** On construit l'image, on la contrôle (tests, analyse de vulnérabilités), puis on ne publie que si tout a réussi. Les contrôles rapides sont placés en premier pour échouer tôt (section 2).

**Question 3.** Où se trouvent les fichiers qui décrivent les workflows GitHub Actions ?

- A. Dans le dossier `.github/workflows/` du dépôt
- B. Dans les paramètres du compte Docker Hub
- C. À la racine du dépôt, dans un fichier `Dockerfile`
- D. Sur le runner, dans le dossier `/etc/actions`

??? success "Réponse"
    **A.** Un workflow est un fichier YAML placé sous `.github/workflows/` dans le dépôt : il est versionné avec le code (section 3).

**Question 4.** Qu'est-ce qu'un job dans un workflow GitHub Actions ?

- A. Un message envoyé à l'équipe après l'exécution
- B. Une action publiée par la communauté
- C. Un ensemble d'étapes exécutées sur un même runner
- D. Le nom du fichier du workflow

??? success "Réponse"
    **C.** Un job regroupe des étapes qui s'exécutent sur une même machine. Les jobs d'un workflow sont indépendants, sauf déclaration d'une dépendance avec `needs` (sections 3 et 4.1).

**Question 5.** Un premier job construit l'image `app:test` sur un runner hébergé par GitHub. Un second job du même workflow cherche cette image avec `docker run app:test`. Que se passe-t-il ?

- A. Elle est disponible, car les deux jobs appartiennent au même workflow
- B. Elle est disponible seulement si le second job déclare `needs`
- C. Elle n'est pas disponible : chaque job s'exécute sur un runner neuf
- D. Elle est téléchargée automatiquement depuis Docker Hub

??? success "Réponse"
    **C.** Un runner hébergé est une machine neuve à chaque job. La déclaration `needs` règle l'**ordre** des jobs, pas le partage des fichiers ou des images : il faut publier l'image, la transmettre ou la reconstruire (sections 3 et 4.1).

**Question 6.** Quel rôle joue l'option `--fail` de `curl` dans un test de fumée ?

- A. Elle ralentit la requête
- B. Elle renvoie un code de sortie non nul si le serveur répond par une erreur HTTP, ce qui fait échouer l'étape
- C. Elle affiche les journaux du conteneur
- D. Elle relance automatiquement le conteneur

??? success "Réponse"
    **B.** Une étape échoue dès qu'une commande renvoie un code différent de zéro. Avec `--fail`, une réponse `4xx` ou `5xx` produit un tel code (section 6.2).

**Question 7.** Que vérifie un test de fumée du conteneur que ne vérifie pas un test unitaire exécuté hors conteneur ?

- A. Que le code de chaque fonction est correct
- B. Que l'image construite démarre et répond (bon port, bonnes dépendances, bonne commande de démarrage)
- C. Que le dépôt est public
- D. Que les secrets sont chiffrés

??? success "Réponse"
    **B.** Le test unitaire contrôle le code ; le test de fumée contrôle l'**image** telle qu'elle sera exécutée (section 6.2).

**Question 8.** Où doit-on enregistrer le jeton d'accès Docker Hub utilisé par le pipeline ?

- A. Dans le fichier du workflow, pour que tout le monde puisse le relire
- B. Dans le `Dockerfile`
- C. Dans un fichier `.env` versionné
- D. Dans les secrets du dépôt GitHub, lu dans le workflow avec `${{ secrets.NOM }}`

??? success "Réponse"
    **D.** Les secrets de dépôt sont chiffrés et ne figurent pas dans les fichiers. On utilise un jeton d'accès plutôt que le mot de passe du compte, car il a des droits limités et se révoque facilement (section 7).

**Question 9.** Pourquoi les workflows déclenchés par une `pull_request` issue d'un fork n'ont-ils pas accès aux secrets du dépôt ?

- A. Parce que les forks n'ont pas de runner
- B. Parce que le code de la pull request est celui d'un tiers : il pourrait lire et divulguer les secrets
- C. Parce que GitHub ne gère pas les secrets pour les dépôts publics
- D. Parce que les secrets expirent à chaque pull request

??? success "Réponse"
    **B.** Donner les secrets à un code non relu serait dangereux. C'est pourquoi on ne publie qu'à partir d'un `push` sur la branche principale ou d'un tag du dépôt (section 7).

**Question 10.** Pourquoi déploie-t-on une image désignée par un tag de version ou d'empreinte de commit plutôt que par `latest` ?

- A. Parce que `latest` est interdit par Docker Hub
- B. Parce qu'un tag de version est plus court à écrire
- C. Parce que `latest` désigne une image qui change : on ne sait pas quelle version tourne et on ne peut pas revenir à une version précise
- D. Parce que `latest` ne peut pas être téléchargé par Swarm

??? success "Réponse"
    **C.** `latest` est un tag mobile. Un tag de version (`1.0.0`) ou d'empreinte (`sha-…`) est immuable et traçable : il rend mises à jour et retours arrière reproductibles (section 8.1).

!!! tip "Pour aller plus loin"
    Si plusieurs réponses sont fausses, refaites le [Lab 13.1](lab-13-1-pipeline-de-construction-d-image.md) (workflow, secrets, publication) ou le [Lab 13.2](lab-13-2-tests-et-publication-versionnee.md) (tests, analyse, tags de version).