# 06 - Preuve promotion production-simulee

## Promotion

- Workflow concerné : 03-promote.yml
- Environnement GitHub : production-simulee
- Tag source : latest
- Tag cible : production-simulee
- Lien du run : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/24986405520

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
sha256:1bbab9dfa173f15292c78b70e1230f49bb756f165fe89ff7c342e7e0a7d1cbd9

Cela prouve que le contenu de l'image n'a pas changé entre la recette et la production-simulee. La promotion s'est terminée en 12s avec le statut Success.
