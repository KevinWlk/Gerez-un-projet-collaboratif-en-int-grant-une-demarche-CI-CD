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
| **Back-end**     | à compléter %    | 0            | à compléter | à compléter %|
| **Front-end**    | à compléter %    | 0            | à compléter | à compléter %|

> Ces résultats proviennent du dernier scan SonarCloud (voir [lien vers le projet](https://sonarcloud.io/dashboard?id=KevinWlk_Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD))  
> Les rapports de couverture sont également stockés dans les artefacts GitHub Actions.

---

## Analyse des retours utilisateurs (Notes & Avis)

| Commentaire utilisateur | Problème détecté |
|--------------------------|------------------|
| "Impossible de poster une suggestion de blague" | Bug sur le front (bouton qui plante) |
| "Bug post vidéo non corrigé depuis 2 semaines" | Pas de gestion de backlog / tests non automatisés |
| "Je ne reçois plus rien depuis une semaine" | Problème possible côté back (cron / scheduler ?) |
| "Site supprimé de mes favoris" | Dégradation de l’expérience utilisateur |

---

## Problèmes identifiés à traiter en priorité

1. **Corriger les bugs bloquants côté front** (boutons non fonctionnels)
2. **Améliorer la réactivité face aux remontées de bugs**
   - Mettre en place une gestion de backlog + test automatique sur PR
3. **Ajouter des tests de bout en bout (E2E)** pour sécuriser les fonctionnalités critiques
4. **Améliorer les logs et monitoring** pour éviter les interruptions non détectées côté back

---

## Recommandations

- **Renforcer la couverture de tests** pour atteindre au moins 80 % (front et back)
- **Mettre en place un Quality Gate SonarCloud personnalisé** pour bloquer les PR en dessous du seuil de couverture
- **Suivre l’évolution de la dette technique** via les dashboards SonarCloud
- **Ajouter une étape de pré-production avec `docker-compose` + test E2E**

---

## Lien utiles

- [SonarCloud du projet](https://sonarcloud.io/dashboard?id=KevinWlk_Gerez-un-projet-collaboratif-en-int-grant-une-demarche-CI-CD)
- [Conteneurs Docker sur Docker Hub](https://hub.docker.com/u/kevinwlk)
- [GitHub Actions du projet](https://github.com/kevinwlk/ton-repo/actions)

Dernière mise à jour : 11/04/2025
