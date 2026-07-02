# 06 - Preuve promotion production-simulee

## Promotion

- Workflow concerné : 03-promote.yml
- Environnement GitHub : production-simulee
- Tag source : latest
- Tag cible : production-simulee
- Lien du run : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/28599858570

## Point essentiel

La promotion réutilise une image existante. Elle ne reconstruit pas l'image. Les commandes utilisées sont :

```bash
docker pull ghcr.io/devaradjalessy/project-cicd-ec06:latest
docker tag  ghcr.io/devaradjalessy/project-cicd-ec06:latest \
            ghcr.io/devaradjalessy/project-cicd-ec06:production-simulee
docker push ghcr.io/devaradjalessy/project-cicd-ec06:production-simulee
```

## Preuve sans rebuild

Le workflow ne contient aucune étape docker build. Il effectue uniquement un pull, un tag et un push. Le digest de l'image production-simulee est identique au digest de l'image source :
sha256:c7fd9f4c087153756a09c682e6292388a51065539931af5b45171ecd191ea9d2

Cela prouve que le contenu de l'image n'a pas changé entre la recette et la production-simulee. La promotion s'est terminée en quelques secondes avec le statut Success.
