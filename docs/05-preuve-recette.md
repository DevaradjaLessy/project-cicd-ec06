# 05 - Preuve recette simulée

## Workflow de validation recette

- Workflow concerné : 03-promote.yml
- Environnement GitHub : recette
- Tag source validé : latest
- Digest observé : sha256:c7fd9f4c087153756a09c682e6292388a51065539931af5b45171ecd191ea9d2
- Lien du run : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/28599858570

## Résultat

Lors de la validation recette, le workflow a téléchargé l'image depuis GHCR sans la reconstruire, lancé un conteneur et effectué deux tests HTTP :
- GET http://127.0.0.1:8080/ → réponse 200 OK
- GET http://127.0.0.1:8080/version.json → réponse 200 OK

La validation recette s'est terminée en une dizaine de secondes avec le statut Success. Le digest de l'image a été affiché dans le résumé du run pour prouver que c'est bien la même image que celle publiée.
