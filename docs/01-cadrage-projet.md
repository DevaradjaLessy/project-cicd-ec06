# 01 - Cadrage du projet

## Identité

- Nom et prénom : Etudiant-EC06
- Dépôt GitHub : https://github.com/DevaradjaLessy/project-cicd-ec06
- Date de démarrage : 2026-04-27

## Objectif

Mettre en place une chaîne CI/CD permettant de construire, tester, publier et promouvoir une image Docker Nginx contenant un site web statique pour le scénario Catal-Log.

## Contraintes du projet

- Travail individuel.
- Aucune infrastructure fournie, préparée, administrée ou maintenue par le formateur.
- Pas de serveur distant, pas de SSH, pas de cloud provider imposé.
- Les traitements principaux sont exécutés dans GitHub Actions.
- Docker local est disponible sur le poste de travail Windows personnel.
- Pas de VM personnelle disponible — les tests sont réalisés via Docker Desktop sur Windows.

## Choix personnels

- Dépôt public sur GitHub pour permettre l'accès gratuit à GHCR.
- Nommage du dépôt : project-cicd-ec06.
- Stratégie de tags : tag sha- pour la traçabilité par commit, tag latest sur la branche main.
- Tests locaux réalisés avec Docker Desktop sur Windows.
- Pas de VM personnelle : justification documentée dans la fiche tests.
