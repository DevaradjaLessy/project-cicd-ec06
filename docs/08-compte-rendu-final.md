# 08 - Compte rendu final

## 1. Synthèse

Ce projet met en place une chaîne CI/CD complète pour l'entreprise fictive Catal-Log. Elle automatise la construction, le test, la publication et la promotion d'une image Docker Nginx contenant un site web statique, via GitHub Actions et GitHub Container Registry.

## 2. Fonctionnement technique

- **Commit** : un push sur le dépôt déclenche automatiquement le workflow 01-ci.yml
- **Build** : l'image Docker est construite à partir du Dockerfile
- **Test** : un conteneur est lancé et deux requêtes HTTP vérifient que le site répond
- **Publication GHCR** : lors d'un push sur main, l'image est publiée avec un tag sha- et latest
- **Validation recette** : le workflow 03-promote.yml télécharge l'image et la teste
- **Promotion production-simulee** : la même image est taguée production-simulee et poussée sans rebuild

## 3. Conteneurisation C12

Le Dockerfile utilise l'image de base nginx:alpine (légère et sécurisée) et copie le contenu du dossier site/ dans le répertoire servi par Nginx. L'image est construite de façon reproductible : le même Dockerfile produit toujours la même image à partir du même code.

Le test local a été réalisé avec Docker Desktop sur Windows :
- Build : docker build -t projet-cicd-nginx:local .
- Run : docker run -d --name test-local -p 8080:80 projet-cicd-nginx:local
- Résultat : site accessible sur http://localhost:8080

## 4. Orchestration et scaling C13

Le compose.yml décrit trois services : web (Nginx), tester (curl qui vérifie les URLs) et whoami (service secondaire). La simulation de scaling avec docker compose up --scale web=2 a lancé deux instances du service web simultanément. Cette simulation montre la coordination de conteneurs mais ne remplace pas une vraie orchestration : absence de load balancer, pas de haute disponibilité, pas de supervision.

## 5. Automatisation et sécurité C14

Les trois workflows GitHub Actions automatisent l'intégralité de la chaîne. Le GITHUB_TOKEN est utilisé pour s'authentifier à GHCR sans stocker de secret dans le code. Les permissions sont limitées au strict nécessaire. Le rollback est possible en relançant 03-promote.yml avec un ancien tag.

## 6. Production réelle

**Gestion des secrets** : en production, tous les secrets (tokens, mots de passe, clés API) doivent être stockés dans un coffre sécurisé (HashiCorp Vault, GitHub Secrets) et jamais dans le code source.

**Rollback** : identifier le digest de l'image précédente dans GHCR et relancer la promotion avec ce tag. Le digest garantit l'identité exacte de l'image.

**Sauvegarde/restauration** : sauvegarder le dépôt Git, les images GHCR, la configuration des environnements et les secrets dans un coffre externe. La restauration passe par un git clone et le rejeu des workflows.

**Éléments complémentaires** :
- Contrôle des vulnérabilités : scan des images avec Trivy à chaque build
- Séparation stricte des environnements : réseaux, secrets et accès distincts entre recette et production

## 7. Preuves

- Dépôt GitHub : https://github.com/DevaradjaLessy/project-cicd-ec06
- Run 01 CI Build et test : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/28599348170
- Run 02 Publication GHCR : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/28599350379
- Run 03 Promotion : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/28599858570
- Image GHCR : ghcr.io/devaradjalessy/project-cicd-ec06
- Tag : latest / sha-6acddaa
- Digest : sha256:c7fd9f4c087153756a09c682e6292388a51065539931af5b45171ecd191ea9d2

## 8. Difficultés et apprentissages

La principale difficulté rencontrée a été la création des fichiers sur Windows avec PowerShell, qui ajoutait des caractères parasites dans les fichiers YAML. La solution a été de générer les fichiers proprement depuis un environnement Linux.

J'ai compris techniquement comment fonctionne une chaîne CI/CD complète : la notion de pipeline automatisé, l'importance du digest pour garantir l'identité d'une image entre les environnements, et la différence entre une promotion (réutilisation d'un artefact existant) et un rebuild (nouvelle construction).
