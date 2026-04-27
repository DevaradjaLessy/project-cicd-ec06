# 07 - Sécurité minimale

## Permissions GitHub Actions

Les permissions sont limitées au strict nécessaire pour chaque workflow :

- **01-ci.yml** : `contents: read` — lecture seule du dépôt, aucune écriture nécessaire pour le build et le test.
- **02-publish-ghcr.yml** : `contents: read, packages: write` — lecture du dépôt et écriture sur GHCR pour publier l'image.
- **03-promote.yml** : `contents: read, packages: write` — lecture du dépôt et écriture sur GHCR pour promouvoir l'image.

Limiter les permissions réduit la surface d'attaque : si un workflow est compromis, il ne peut pas modifier le dépôt ou accéder à des ressources non nécessaires.

## Gestion des secrets

Aucun secret ne doit être stocké dans le code source car le dépôt est public et lisible par tous. Un mot de passe ou token dans le code serait immédiatement exposé.

Le **GITHUB_TOKEN** est un token temporaire généré automatiquement par GitHub pour chaque exécution de workflow. Il n'est jamais écrit dans le code, il est injecté via `${{ secrets.GITHUB_TOKEN }}`. Il expire à la fin du run.

En production réelle, les éléments suivants devraient être placés dans GitHub Secrets ou un coffre de secrets (ex: HashiCorp Vault) :
- Credentials d'un registre d'images privé
- Clés d'API de services externes
- Variables d'environnement sensibles (mots de passe BDD, tokens...)

## Rollback

Pour revenir à une version précédente :
1. Identifier le tag ou digest de l'image précédente dans GHCR (ex: sha-abc1234)
2. Relancer le workflow 03-promote.yml en saisissant ce tag comme source_tag
3. Le workflow va tester cette ancienne image en recette puis la promouvoir en production-simulee sans rebuild

Le digest garantit qu'on redéploie exactement la même image qu'avant, octet pour octet.

## Sauvegarde / restauration

Éléments à sauvegarder :
- **Dépôt GitHub** : code source, workflows, documentation — exportable via git clone
- **Images GHCR** : les images publiées avec leurs tags et digests
- **Configuration des environnements** GitHub (recette, production-simulee)
- **Secrets GitHub** : noter les valeurs dans un coffre sécurisé externe

Pour restaurer : cloner le dépôt, reconfigurer les environnements et secrets, puis relancer les workflows.

## Deux éléments complémentaires

### 1. Contrôle des vulnérabilités
En production, il faudrait scanner l'image Docker avec un outil comme Trivy ou Grype à chaque build pour détecter les failles connues dans les dépendances et l'image de base Nginx.

### 2. Séparation stricte des environnements
Les environnements recette et production-simulee doivent être totalement isolés : réseaux séparés, secrets distincts, accès restreints. Une modification en recette ne doit jamais impacter la production.
