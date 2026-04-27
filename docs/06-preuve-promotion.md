# 06 - Preuve promotion production-simulee

## Promotion

- Workflow concerné : 03-promote.yml
- Environnement GitHub : production-simulee
- Tag source : A compléter après exécution
- Tag cible : production-simulee
- Lien du run : A compléter après exécution

## Point essentiel

La promotion réutilise une image existante. Elle ne reconstruit pas l'image. Les commandes utilisées sont :

```bash
docker pull ghcr.io/devaradjaLessy/project-cicd-ec06:latest
docker tag  ghcr.io/devaradjaLessy/project-cicd-ec06:latest \
            ghcr.io/devaradjaLessy/project-cicd-ec06:production-simulee
docker push ghcr.io/devaradjaLessy/project-cicd-ec06:production-simulee
```

## Preuve sans rebuild

Le workflow ne contient aucune étape docker build. Il effectue uniquement un pull, un tag et un push. Le digest de l'image production-simulee est identique au digest de l'image source, ce qui prouve que le contenu n'a pas changé.
