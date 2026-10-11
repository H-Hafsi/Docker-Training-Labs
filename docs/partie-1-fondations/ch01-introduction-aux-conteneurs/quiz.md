# Quiz du chapitre 1 : Introduction aux conteneurs

!!! abstract "Consignes"
    Autoévaluation : 10 questions, environ 10 minutes. Chaque question a **une seule** bonne réponse. Répondez d'abord de mémoire, puis cliquez sur « Réponse » pour vérifier. En cas d'erreur, relisez la section indiquée du [cours](cours.md).

**Question 1.** Quel problème les conteneurs résolvent-ils en priorité ?

- A. Ils remplacent le matériel physique des serveurs
- B. Ils chiffrent automatiquement les données d'une application
- C. Ils permettent d'exécuter une application de la même façon d'un environnement à un autre
- D. Ils suppriment le besoin d'un système d'exploitation sur la machine

??? success "Réponse"
    **C.** Le conteneur regroupe l'application et ses dépendances dans un ensemble isolé et portable, ce qui évite le « ça marche chez moi » (section 1 du cours).

**Question 2.** Quelle affirmation décrit correctement la différence entre un conteneur et une machine virtuelle ?

- A. Un conteneur embarque son propre noyau, alors que les machines virtuelles partagent celui de l'hôte
- B. Les conteneurs partagent le noyau de l'hôte, alors que chaque machine virtuelle embarque le sien
- C. Une machine virtuelle démarre toujours plus vite qu'un conteneur
- D. Un conteneur ne peut s'exécuter qu'avec un hyperviseur

??? success "Réponse"
    **B.** Un conteneur est un processus de l'hôte qui utilise le noyau de celui-ci ; une machine virtuelle embarque un système complet, noyau compris. L'affirmation A est l'inverse de la réalité (section 2).

**Question 3.** Quel est l'effet du namespace PID sur un conteneur ?

- A. Le conteneur ne voit que ses propres processus
- B. Le conteneur ne peut pas utiliser plus d'un processeur
- C. Le conteneur reçoit sa propre adresse IP
- D. Le conteneur ne peut plus écrire dans son système de fichiers

??? success "Réponse"
    **A.** Le namespace PID isole les identifiants de processus : le premier processus du conteneur porte le numéro 1 et les processus de l'hôte ne sont pas visibles. La limitation des processeurs relève des cgroups, l'adresse IP du namespace NET (section 3).

**Question 4.** Vous voulez empêcher un conteneur d'utiliser plus de 512 Mo de mémoire. Quel mécanisme du noyau Linux est utilisé ?

- A. Le namespace MNT
- B. Le namespace USER
- C. La norme OCI
- D. Les cgroups

??? success "Réponse"
    **D.** Les cgroups mesurent et limitent les ressources consommées : processeur, mémoire, entrées-sorties, nombre de processus. Les namespaces, eux, limitent ce que le processus **voit** (section 3).

**Question 5.** Quel composant crée réellement le conteneur en s'adressant au noyau ?

- A. Le client `docker`
- B. Le daemon `dockerd`
- C. `runc`
- D. Le registre

??? success "Réponse"
    **C.** `runc` demande au noyau les namespaces et les cgroups nécessaires. Le daemon reçoit les demandes et s'appuie sur containerd, qui fait appel à `runc` (section 4).

**Question 6.** Quel est le rôle du daemon `dockerd` ?

- A. Stocker publiquement les images pour tous les utilisateurs
- B. Recevoir les demandes du client et gérer les images, les conteneurs, les réseaux et les volumes
- C. Définir le format officiel des images de conteneurs
- D. Isoler les processus à la place du noyau

??? success "Réponse"
    **B.** Le client envoie ses demandes au daemon par une API ; le daemon les exécute. Le stockage public des images est le rôle d'un registre, et le format des images est défini par les normes OCI (section 4).

**Question 7.** Quelle phrase sur les images et les conteneurs est exacte ?

- A. Une image est en cours d'exécution, alors qu'un conteneur est un modèle en lecture seule
- B. Une image ne peut servir à créer qu'un seul conteneur
- C. Les fichiers écrits par un conteneur modifient l'image dont il provient
- D. Plusieurs conteneurs peuvent être créés à partir de la même image

??? success "Réponse"
    **D.** L'image est un modèle en lecture seule ; chaque conteneur en est une instance indépendante. C'est pourquoi un fichier créé dans un conteneur n'apparaît pas dans un nouveau conteneur lancé depuis la même image (section 4 et Lab 1.2).

**Question 8.** Quel est le registre public utilisé par défaut par Docker ?

- A. Docker Hub
- B. containerd
- C. runc
- D. L'Open Container Initiative

??? success "Réponse"
    **A.** Docker Hub est le registre public par défaut. containerd et `runc` sont des composants du moteur, et l'Open Container Initiative est une organisation qui publie des normes (sections 4 et 5).

**Question 9.** Que sont les normes OCI ?

- A. Un produit commercial qui remplace Docker
- B. Une liste d'images officielles à utiliser en production
- C. Des spécifications (image, runtime, distribution) qui rendent les conteneurs portables d'un outil à un autre
- D. Un système de limitation des ressources du noyau Linux

??? success "Réponse"
    **C.** L'Open Container Initiative définit trois spécifications : le format des images, l'exécution des conteneurs et la distribution des images par les registres (section 5).

**Question 10.** Pourquoi Docker Desktop exécute-t-il le moteur dans une machine virtuelle Linux interne lorsqu'il est installé sous Windows ?

- A. Parce que Windows ne peut pas se connecter à Internet sans machine virtuelle
- B. Parce qu'un conteneur Linux a besoin d'un noyau Linux, que Windows ne fournit pas
- C. Parce que les conteneurs doivent obligatoirement avoir un hyperviseur
- D. Parce que Docker Desktop remplace containerd par une machine virtuelle

??? success "Réponse"
    **B.** Un conteneur Linux partage le noyau de son hôte : sous Windows, Docker Desktop fournit donc une machine virtuelle Linux pour héberger le moteur. Un conteneur n'a pas besoin d'hyperviseur sur un hôte Linux (section 2 et annexe Environnement).