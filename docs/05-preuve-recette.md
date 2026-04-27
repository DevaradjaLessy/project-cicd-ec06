# 05 - Preuve recette simulée

## Workflow de validation recette

- Workflow concerné : 03-promote.yml
- Environnement GitHub : recette
- Tag source validé : latest
- Digest observé : sha256:1bbab9dfa173f15292c78b70e1230f49bb756f165fe89ff7c342e7e0a7d1cbd9
- Lien du run : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/24986405520

## Résultat

Lors de la validation recette, le workflow a téléchargé l'image depuis GHCR sans la reconstruire, lancé un conteneur et effectué deux tests HTTP :
- GET http://127.0.0.1:8080/ → réponse 200 OK
- GET http://127.0.0.1:8080/version.json → réponse 200 OK

La validation recette s'est terminée en 11s avec le statut Success. Le digest de l'image a été affiché dans le résumé du run pour prouver que c'est bien la même image que celle publiée.
