# Quiz du chapitre 9 : Optimisation des images

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Parmi ces conséquences, laquelle est un avantage d'une image plus légère, du point de vue de la sécurité ?

- A. Elle démarre toujours plus vite
- B. Elle contient moins de composants susceptibles d'avoir des failles
- C. Elle ne peut plus être attaquée
- D. Elle n'a plus besoin de mises à jour

??? success "Réponse"
    **B.** Chaque paquet ou outil présent dans l'image peut contenir une faille ; en retirer réduit la surface d'attaque, sans la supprimer (section 1).

**Question 2.** Quelle commande détaille la taille de chaque couche d'une image ?

- A. `docker images`
- B. `docker history image:tag`
- C. `docker stats image:tag`
- D. `docker top image:tag`

??? success "Réponse"
    **B.** `docker history` liste les couches et leur taille ; `docker images` ne donne que le total (section 2).

**Question 3.** Une image contient ces deux instructions : `RUN apt-get update && apt-get install -y curl` puis, séparément, `RUN rm -rf /var/lib/apt/lists/*`. Que dire de sa taille ?

- A. La seconde instruction supprime les fichiers de l'image : la taille diminue
- B. Les listes de paquets restent dans la couche de la première instruction : la taille ne diminue pas
- C. L'image ne peut pas être construite
- D. La seconde instruction rend l'image plus grosse

??? success "Réponse"
    **B.** Les couches sont immuables : la suppression dans une couche ultérieure masque les fichiers sans les retirer. Il faut nettoyer dans la même instruction `RUN` (section 2.1).

**Question 4.** Quelle est la particularité de l'image `scratch` ?

- A. Elle contient une distribution minimale avec un shell
- B. Elle est une image vide : aucun fichier hormis ce que vous y copiez
- C. Elle contient uniquement le compilateur Go
- D. Elle ne peut être utilisée qu'avec Python

??? success "Réponse"
    **B.** `scratch` ne contient rien : elle convient aux programmes autonomes (binaires statiques), sans shell ni certificats (sections 3 et 4.4).

**Question 5.** Quel risque présente le passage à une image `alpine` sans test ?

- A. Les images Alpine sont interdites par Docker
- B. Alpine utilise une autre bibliothèque C : certaines dépendances ne fonctionnent pas ou sont à recompiler
- C. Alpine ne peut pas exécuter de programmes Python
- D. Alpine est toujours plus lente à construire

??? success "Réponse"
    **B.** La bibliothèque C d'Alpine (musl) diffère de celle de Debian : il faut tester l'application dans l'image choisie (section 3).

**Question 6.** Quelle est la bonne définition d'un Dockerfile multi-stage ?

- A. Un Dockerfile exécuté en plusieurs fois, dans plusieurs conteneurs
- B. Un Dockerfile avec plusieurs `FROM`, dont seule la dernière étape forme l'image finale
- C. Un Dockerfile qui construit plusieurs images à la fois
- D. Un Dockerfile qui utilise plusieurs registres

??? success "Réponse"
    **B.** Chaque `FROM` démarre une étape. Une étape peut copier des fichiers d'une étape précédente ; seule la dernière devient l'image finale (section 4.1).

**Question 7.** Quelle instruction copie un fichier produit par l'étape `build` vers l'étape courante ?

- A. `COPY --from=build /serveur /serveur`
- B. `ADD build:/serveur /serveur`
- C. `RUN copy build /serveur`
- D. `FROM build /serveur`

??? success "Réponse"
    **A.** `COPY --from=nom` copie des fichiers depuis une étape précédente identifiée par son nom (section 4.2).

**Question 8.** Pourquoi compile-t-on un programme Go avec `CGO_ENABLED=0` avant de le placer sur `scratch` ?

- A. Pour accélérer la compilation
- B. Pour obtenir un programme statique, sans dépendance à la bibliothèque C du système
- C. Pour que le programme se connecte à Internet
- D. Pour réduire la mémoire utilisée à l'exécution

??? success "Réponse"
    **B.** Un programme statique se suffit à lui-même ; il peut s'exécuter sur une image qui ne contient aucune bibliothèque, comme `scratch` (section 4.3).

**Question 9.** Quelle option de `docker build` permet de construire seulement jusqu'à l'étape nommée `build` ?

- A. `--stage build`
- B. `--only build`
- C. `--target build`
- D. `--from build`

??? success "Réponse"
    **C.** `--target` arrête la construction à l'étape indiquée (section 4.6).

**Question 10.** Pour choisir entre deux images de base, que faut-il mesurer ?

- A. Uniquement la taille de l'image
- B. La taille, la durée de construction, et surtout le bon fonctionnement de l'application
- C. Uniquement la durée de téléchargement
- D. Rien : l'image la plus petite est toujours la meilleure

??? success "Réponse"
    **B.** Une image plus petite qui ne fait pas fonctionner l'application, ou qui est plus difficile à exploiter, n'est pas un progrès : on décide d'après des mesures et des tests (section 6).