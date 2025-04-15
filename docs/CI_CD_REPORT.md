
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

Dernière mise à jour : 11/04/2025
