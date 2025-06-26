# Examen GIT - Gestion de Version d'un Mini-Site Statique

Ce dépôt contient le projet de l'examen GIT, consistant en la gestion de version d'un mini-site web statique. L'objectif principal était de démontrer la maîtrise des bonnes pratiques Git, incluant la gestion des branches, les fusions, et la résolution de conflits, en suivant une stratégie de branchement spécifique.

## 1. Stratégie de Branchement

Pour ce projet, une stratégie de branchement inspirée de Git Flow a été adoptée, adaptée aux besoins d'un projet de petite envergure mais exigeant une rigueur dans la collaboration et l'intégration.

Voici les branches utilisées et leur rôle :

* **`main`**:
    * **Rôle :** Branche de production stable. Elle ne contient que le code entièrement testé, validé et prêt pour le déploiement. Chaque fusion dans `main` représente une version livrable du site.
    * **Flux :** Seules les fusions depuis `dev` sont autorisées.

* **`dev`**:
    * **Rôle :** Branche d'intégration globale. C'est ici que toutes les fonctionnalités développées et testées individuellement sont regroupées avant d'être considérées pour la mise en production. Elle représente l'état le plus à jour du projet stable.
    * **Flux :** Reçoit les fusions des branches `test/*`.

* **`feature/*`**: (Exemples : `feature/html-structure`, `feature/css-theme`, `feature/js-interactions`)
    * **Rôle :** Branches de développement pour chaque nouvelle fonctionnalité ou tâche spécifique. Chaque fonctionnalité est isolée sur sa propre branche pour éviter d'interférer avec le reste du développement.
    * **Flux :** Créées à partir de `dev`. Une fois la fonctionnalité développée et testée unitairement, elle est fusionnée dans `test/frontend`.

* **`test/frontend`**:
    * **Rôle :** Branche dédiée aux tests d'intégration front-end. Toutes les fonctionnalités `feature/*` sont d'abord fusionnées ici pour unifier le travail et s'assurer de la cohérence visuelle et fonctionnelle avant d'être poussées vers `dev`. Cela permet d'isoler les problèmes d'intégration sans perturber la branche `dev`.
    * **Flux :** Reçoit les fusions des branches `feature/*`. Une fois les tests concluants, elle est fusionnée dans `dev`.

**Résumé du Flux de Travail :**

`feature/*` (développement d'une fonctionnalité)

`test/frontend` (intégration et tests front-end)
 
`dev` (intégration globale et stabilisation)

`main` (version stable et production)

## 2. Étapes Suivies et Commandes Git Utilisées

Ce projet a été développé en suivant les étapes clés ci-dessous, en utilisant les commandes Git pertinentes pour gérer l'historiqu les branches.

### 2.1. Initialisation du Projet et du Dépôt

1.  **Création du répertoire projet :**
    ```bash
    mkdir mon-mini-site
    cd mon-mini-site
    ```
2.  **Initialisation du dépôt Git :**
    ```bash
    git init
    ```
3.  **Création des fichiers initiaux (`index.html`) :**
    ```bash
    touch index.html
    # Ajout du contenu HTML de base via éditeur
    ```
4.  **Premier commit :**
    ```bash
    git add .
    git commit -m "Initialisation du projet et ajout de la structure HTML de base"
    ```

### 2.2. Configuration des Branches Initiales et Liaison GitHub

1.  **Création de la branche `dev` :**
    ```bash
    git branch dev
    ```
2.  **Basculement sur `dev` :**
    ```bash
    git switch dev
    ```
3.  **Ajout du dépôt distant GitHub :**
    ```bash
    git remote add origin [URL_DE_VOTRE_DEPOT_GITHUB]
    ```
4.  **Premier push des branches `dev` et `main` vers GitHub :**
    ```bash
    git push -u origin dev
    git push -u origin main
    ```

### 2.3. Développement et Intégration des Fonctionnalités

Pour chaque fonctionnalité (`html-structure`, `css-theme`, `js-interactions`), le cycle suivant a été répété :

1.  **Création et basculement sur la branche `feature/nom-de-la-feature` (depuis `dev`) :**
    ```bash
    git switch dev
    git branch feature/[nom-de-la-feature]
    git switch feature/[nom-de-la-feature]
    ```
2.  **Développement de la fonctionnalité :**
    * Modification/création des fichiers (ex: `index.html`, `services.html`, `contact.html` pour `html-structure`; `style.css` pour `css-theme`; `script.js` pour `js-interactions`).
    * **Commits réguliers :**
        ```bash
        git add .
        git commit -m "Description concise de la fonctionnalité ajoutée/modifiée"
        ```
    * **Push de la branche de fonctionnalité vers GitHub :**
        ```bash
        git push -u origin feature/[nom-de-la-feature]
        ```
3.  **Fusion dans `test/frontend` :**
    * **Basculement sur `test/frontend` (création si première fois) :**
        ```bash
        git switch dev # Ou restez sur dev si vous voulez la créer à partir de dev
        git branch test/frontend # Si n'existe pas encore
        git switch test/frontend
        ```
    * **Fusion de la branche de fonctionnalité :**
        ```bash
        git merge feature/[nom-de-la-feature]
        ```
    * **Gestion des conflits (si nécessaire) :**
        * Modification des fichiers en conflit.
        * `git add [fichier-en-conflit]`
        * `git commit` (pour finaliser la fusion)
    * **Tests d'intégration front-end.**
    * **Push de `test/frontend` vers GitHub :**
        ```bash
        git push origin test/frontend
        ```
4.  **Intégration dans `dev` :**
    * **Basculement sur `dev` :**
        ```bash
        git switch dev
        ```
    * **Fusion de `test/frontend` :**
        ```bash
        git merge test/frontend
        ```
    * **Gestion des conflits (si nécessaire) :** (Même procédure que ci-dessus)
    * **Push de `dev` vers GitHub :**
        ```bash
        git push origin dev
        ```

### 2.4. Finalisation et Déploiement

1.  **Validation finale de la branche `dev`.**
2.  **Basculement sur `main` :**
    ```bash
    git switch main
    ```
3.  **Fusion de `dev` dans `main` :**
    ```bash
    git merge dev
    ```
4.  **Push de `main` vers GitHub :**
    ```bash
    git push origin main
    ```

## 3. Lien du Dépôt GitHub

Vous pouvez consulter l'intégralité du code et l'historique des commits à l'adresse suivante :

[https://github.com/votre-nom-utilisateur/nom-de-votre-depot-github](https://github.com/votre-nom-utilisateur/nom-de-votre-depot-github)

---

**Nom de l'étudiant :** [Votre Nom Complet]
**Date :** [Date de soumission, ex: 26 Juin 2025]
