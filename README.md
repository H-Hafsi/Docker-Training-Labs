# Docker : conteneurisation, orchestration et industrialisation d'applications : site de cours

Site MkDocs Material publié sur GitHub Pages : `https://H-Hafsi.github.io/Docker-Training-Labs/` (casse du compte en minuscules).
Les pages marquées « Under construction » sont des squelettes à compléter ; `AVANCEMENT.md` suit l'état de chaque page.

## Structure

```
mkdocs.yml                  configuration, navigation (nav), textes de la bannière
requirements.txt            dépendances
overrides/home.html         page d'accueil (bannière)
docs/index.md               syllabus
docs/partie-N-.../          index.md, chNN-.../ (cours.md, lab-N-M-....md, quiz.md), mini-projet-N.md
docs/annexes/               pages annexes
docs/assets/css/extra.css   charte graphique (variables en tête de fichier)
docs/assets/img/            logo, bannière, images
modeles/                    modèles de pages (non publiés)
AVANCEMENT.md               suivi de rédaction (non publié)
.github/workflows/deploy.yml  publication automatique
```

## Prévisualiser

```bash
pip install -r requirements.txt
mkdocs serve        # http://127.0.0.1:8000
```

## Publier sur GitHub Pages

1. Créer le dépôt sur GitHub (public) et pousser le contenu **à la racine** du dépôt, dossier `.github` compris. Branche `main`.
2. `Settings`, puis `Pages`, puis **Source : GitHub Actions**.
3. Onglet **Actions** : attendre les deux coches vertes (`build`, `deploy`). En cas d'échec lié à Pages non activé : `Re-run all jobs`.
4. Si `git push` est rejeté (le dépôt contient déjà un commit) : `git pull origin main --allow-unrelated-histories --no-rebase -X ours`, puis `git push -u origin main`.

## Ajouter ou modifier un contenu

Après chaque modification : `mkdocs serve` pour vérifier, puis `git add -A`, `git commit`, `git push`.
La construction utilise `mkdocs build --strict` : un lien cassé ou une page absente de `nav` fait échouer la publication.

### Compléter une page « Under construction »
1. Ouvrir le fichier et remplacer son contenu (supprimer le bloc `Under construction`) en suivant le modèle dans `modeles/`.
2. Passer son statut à `Terminé (v1)` dans `AVANCEMENT.md`. Aucun autre changement n'est nécessaire.

### Ajouter un lab à un chapitre existant
1. Copier `modeles/modele-lab.md` vers `docs/partie-X-.../chNN-.../lab-N-M-titre.md` (M = numéro suivant dans le chapitre).
2. Déclarer la page dans `mkdocs.yml` (section `nav`), sous le chapitre.
3. Ajouter le lien dans la liste « Ressources du chapitre » de `cours.md` du chapitre.
4. Ajouter le lien dans le tableau de `docs/partie-X-.../index.md`.
5. Ajouter le lien dans le tableau de la partie dans `docs/index.md` (syllabus).
6. Ajouter une ligne dans `AVANCEMENT.md`.

### Ajouter un quiz, un mini-projet ou une annexe
- **Quiz :** `modeles/modele-quiz.md` vers `chNN-.../quiz.md` ; mêmes étapes 2 à 6 (lien dans `cours.md`, index de la partie, syllabus, `nav`).
- **Mini-projet :** `modeles/modele-mini-projet.md` vers `docs/partie-X-.../mini-projet-N.md` ; `nav`, index de la partie, syllabus.
- **Annexe :** nouveau fichier dans `docs/annexes/` ; déclarer dans `nav`.

### Ajouter un chapitre
1. Créer le dossier `docs/partie-X-.../chNN-titre/` avec `cours.md` (modèle `modele-cours.md`) et ses labs.
2. Déclarer le chapitre et ses pages dans `nav`.
3. Ajouter une ligne dans le tableau de l'index de la partie et dans le tableau du syllabus (`docs/index.md`).
4. Mettre à jour les volumes horaires de la partie et du syllabus si nécessaire, puis `AVANCEMENT.md`.

### Ajouter une partie
1. Créer le dossier `docs/partie-N-titre/` avec un `index.md`.
2. Déclarer la partie dans `nav`, ajouter sa section dans `docs/index.md`.
3. Ajouter ses chapitres comme ci-dessus.

### Renommer ou supprimer une page
Modifier ou retirer toutes ses références : `nav`, liens dans `cours.md`, index de la partie, syllabus, `AVANCEMENT.md`.

### Ajouter une image
Déposer le fichier dans `docs/assets/img/` (WebP ou JPEG optimisé, moins de 300 Ko, droits vérifiés) puis l'insérer avec `![Description](chemin/relatif/vers/assets/img/image.webp)`.
Pour un schéma, préférer un bloc Mermaid dans la page.

### Changer le style
- Couleurs : variables au début de `docs/assets/css/extra.css`.
- Logo : remplacer `docs/assets/img/logo-iset.svg` (provisoire) et, si l'extension change, mettre à jour `mkdocs.yml` (`logo`, `favicon`) et `overrides/home.html`.
- Bannière : `docs/assets/img/banniere.svg`.
- Textes et chiffres de la bannière : section `extra.matiere` de `mkdocs.yml`.

## Bonnes pratiques
- Pas de corrigés ni de notes enseignant dans ce dépôt public : les garder dans un dépôt privé séparé.
- Ajouter un fichier `LICENSE` (par exemple Creative Commons).
