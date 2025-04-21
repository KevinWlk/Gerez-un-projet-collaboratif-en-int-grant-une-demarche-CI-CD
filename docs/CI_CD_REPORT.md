# Rapport CI/CD – Projet BobApp

## Objectif du pipeline

Ce projet met en place une chaîne CI/CD complète sur GitHub Actions pour automatiser les tâches suivantes :
- Vérification de la qualité du code
- Exécution des tests unitaires
- Génération de rapports de couverture
- Analyse SonarCloud
- Publication d’images Docker sur Docker Hub

---

## Étapes du workflow CI/CD

| Étape                       | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| **Tests Back-end**         | Lancement des tests JUnit sur le back avec JaCoCo pour générer le coverage |
| **Tests Front-end**        | Lancement des tests Angular avec Karma + couverture                        |
| **Analyse SonarCloud**     | Vérifie les bugs, duplications, complexité et dettes techniques             |
| **Docker Back**            | Build de l’image Spring Boot et push vers Docker Hub                       |
| **Docker Front**           | Build de l’image Angular et push vers Docker Hub                           |

---

## Nouvelle structure du workflow (avril 2025)

Depuis la refonte d’avril 2025, les jobs de tests **back** et **front** sont devenus **des prérequis** obligatoires pour les jobs de construction Docker.

Cela est rendu possible grâce à l’utilisation de la directive `needs: [tests-back, tests-front]`, ce qui permet de garantir que :

- Les tests unitaires passent **avant** tout build Docker.
- En cas d’échec de test, **aucun déploiement Docker ne se produit.**

| Job GitHub Actions        | Dépendances                      |
|---------------------------|----------------------------------|
| `tests-back`              | -                                |
| `tests-front`             | -                                |
| `build-and-push-back`     | `tests-back`, `tests-front`      |
| `build-and-push-front`    | `tests-back`, `tests-front`      |

Cette amélioration sécurise les livraisons en production et renforce la fiabilité du pipeline.

---

## KPIs proposés

| Indicateur                 | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| **Coverage minimal**       | Minimum 70 % de couverture de tests unitaires (back + front)                |
| **Zéro bug “blocker”**     | Aucune anomalie critique détectée par SonarCloud                            |

---

## Résultats observés (métriques initiales)

| Composant       | Coverage actuel  | Bugs Blocker | Code Smells | Duplications |
|------------------|------------------|--------------|-------------|--------------|
| **Back-end**     | **72.7 %**       | **0**        | **0**       | **0.0 %**     |
| **Front-end**    | **81.5 %**       | **0**        | **0**       | **0.0 %**     |

> Ces résultats proviennent du dernier scan SonarCloud :  
> [Accéder au tableau de bord](https://sonarcloud.io/summary/new_code?id=KevinWlk_Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD)

> Les rapports de couverture sont également stockés dans les artefacts GitHub Actions.

---

## Recommandations

- **Renforcer la couverture de tests** pour maintenir >80 % (front et back)
- **Mettre en place un Quality Gate SonarCloud personnalisé** pour bloquer les PR en dessous du seuil de couverture
- **Suivre l’évolution de la dette technique** via les dashboards SonarCloud
- **Ajouter une étape de pré-production avec `docker-compose` + test E2E**

---

## Liens utiles

- [Tableau de bord SonarCloud](https://sonarcloud.io/summary/new_code?id=KevinWlk_Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD)
- [Conteneurs Docker sur Docker Hub](https://hub.docker.com/u/kevinwlk)
- [GitHub Actions du projet](https://github.com/kevinwlk/Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD/actions)

Dernière mise à jour : 21/04/2025