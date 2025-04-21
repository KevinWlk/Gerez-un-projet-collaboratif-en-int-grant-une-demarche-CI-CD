# Rapport CI/CD – Projet BobApp

## Objectif du pipeline

Ce projet met en place une chaîne CI/CD complète sur GitHub Actions pour automatiser les tâches suivantes :
- Vérification de la qualité du code
- Exécution des tests unitaires (Back + Front)
- Génération de rapports de couverture (JaCoCo + Karma)
- Analyse de la qualité avec SonarCloud
- Construction et publication des images Docker sur Docker Hub

---

## Étapes du workflow CI/CD (Pipeline unifié)

| Étape                      | Description                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Tests Back-end**        | Tests JUnit + JaCoCo pour couverture                                        |
| **Tests Front-end**       | Tests Angular avec Karma + code coverage                                   |
| **Analyse SonarCloud**    | Analyse statique qualité, duplication, bugs, sécurité                      |
| **Docker Back**           | Build de l'image backend Spring Boot + push Docker Hub                     |
| **Docker Front**          | Build de l'image frontend Angular + push Docker Hub                        |

---

## Nouvelle structure du workflow (avril 2025)

Depuis avril 2025, l’ensemble des étapes CI/CD est intégré dans un **seul fichier GitHub Actions**.

### Ordre de dépendance :

1. `tests-back` et `tests-front` : s'exécutent en parallèle
2. `sonarcloud` : s'exécute seulement si les tests sont OK (`needs: [tests-back, tests-front]`)
3. `build-and-push-back` & `build-and-push-front` : uniquement si SonarCloud est OK (`needs: [sonarcloud]`)

### Avantages :

- Empêche les déploiements Docker si les tests échouent
- Analyse automatique du code via SonarCloud avant toute livraison
- Pipeline unifié et maintenable

---

## KPIs proposés

| Indicateur                  | Objectif                                                                 |
|-----------------------------|--------------------------------------------------------------------------|
| **Couverture des tests**    | ≥ 70 % (objectif initial pour back et front)                             |
| **Fiabilité du code**       | Note A sur SonarCloud (0 bug critique)                                   |
| **Sécurité**                | Note A (aucune vulnérabilité)                                            |
| **Maintenabilité**          | Note A (dette technique maîtrisée)                                       |
| **Hotspots de sécurité**    | 100 % examinés                                                           |
| **Taux de duplication**     | ≤ 3 % (actuellement 0 %)                                                 |

---

## Résultats observés (métriques initiales)

| Composant       | Coverage actuel  | Bugs Blocker | Code Smells | Duplications |
|------------------|------------------|--------------|-------------|--------------|
| **Back-end**     | **72.7 %**       | **0**        | **0**       | **0.0 %**     |
| **Front-end**    | **81.5 %**       | **0**        | **0**       | **0.0 %**     |

> Résultats issus du dernier scan SonarCloud :  
> https://sonarcloud.io/summary/new_code?id=KevinWlk_Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD

> Les rapports de couverture sont également stockés dans les artefacts GitHub Actions.

---

## Recommandations

- Augmenter la couverture de tests pour tendre vers 80 % sur le front et le back
- Mettre en place un **Quality Gate personnalisé SonarCloud** pour bloquer les PR en dessous du seuil
- Suivre régulièrement la dette technique via le tableau de bord SonarCloud

---

## Liens utiles

- [Tableau de bord SonarCloud](https://sonarcloud.io/summary/new_code?id=KevinWlk_Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD)
- [Images Docker – Docker Hub](https://hub.docker.com/u/kevinwlk)
- [Workflows GitHub Actions](https://github.com/kevinwlk/Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD/actions)

---

Dernière mise à jour : 21/04/2025