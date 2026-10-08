# Partie 3 : Durcissement et orchestration Swarm

**Durée :** 12 h (chapitres 9 à 12) · **Acquis visés :** AA3, AA7, AA8

Cette partie optimise et sécurise vos images, puis vous fait passer d'une machine à un cluster Docker Swarm de trois nœuds. L'autonomie augmente.

| Chapitre | Contenu | Ressources |
|---|---|---|
| 9. Optimisation des images (AA7, AA3) | Construction multi-stage, BuildKit, images minimales, comparaison de taille et de temps de construction | [Cours](./ch09-optimisation-des-images/cours.md) · [Lab 9.1 : Construire avec multi-stage](./ch09-optimisation-des-images/lab-9-1-construire-avec-multi-stage.md) · [Lab 9.2 : Réduire et comparer des images](./ch09-optimisation-des-images/lab-9-2-reduire-et-comparer-des-images.md) · [Quiz](./ch09-optimisation-des-images/quiz.md) |
| 10. Sécurité des conteneurs (AA7) | Utilisateur non root, système de fichiers en lecture seule, capabilities, gestion des secrets, analyse de vulnérabilités des images | [Cours](./ch10-securite-des-conteneurs/cours.md) · [Lab 10.1 : Durcir un conteneur](./ch10-securite-des-conteneurs/lab-10-1-durcir-un-conteneur.md) · [Lab 10.2 : Analyser et corriger une image](./ch10-securite-des-conteneurs/lab-10-2-analyser-et-corriger-une-image.md) · [Quiz](./ch10-securite-des-conteneurs/quiz.md) |
| 11. Swarm : cluster et services (AA8) | Pourquoi orchestrer, architecture managers et workers, initialisation et adhésion, services répliqués et globaux, routing mesh, mise à l'échelle, maintenance d'un nœud | [Cours](./ch11-swarm-cluster-et-services/cours.md) · [Lab 11.1 : Créer un cluster Swarm](./ch11-swarm-cluster-et-services/lab-11-1-creer-un-cluster-swarm.md) · [Lab 11.2 : Déployer et mettre à l'échelle des services](./ch11-swarm-cluster-et-services/lab-11-2-deployer-et-mettre-a-l-echelle-des-services.md) · [Quiz](./ch11-swarm-cluster-et-services/quiz.md) |
| 12. Swarm : stacks et exploitation (AA8) | Réseaux overlay, stacks à partir d'un fichier Compose, configs et secrets Swarm, mises à jour progressives et retour arrière, contraintes de placement, tolérance aux pannes, comparaison avec Kubernetes | [Cours](./ch12-swarm-stacks-et-exploitation/cours.md) · [Lab 12.1 : Déployer une stack](./ch12-swarm-stacks-et-exploitation/lab-12-1-deployer-une-stack.md) · [Lab 12.2 : Mises à jour, secrets et panne d'un nœud](./ch12-swarm-stacks-et-exploitation/lab-12-2-mises-a-jour-secrets-et-panne-d-un-nud.md) · [Quiz](./ch12-swarm-stacks-et-exploitation/quiz.md) |
| **Mini-projet 3** | Application sécurisée sur un cluster Swarm | [Énoncé](mini-projet-3.md) |
