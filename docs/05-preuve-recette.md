# 05 - Preuve recette simulée

## Workflow de validation recette

- Workflow concerné : 03-promote.yml
- Environnement GitHub : recette
- Tag source validé : A compléter après exécution
- Digest observé : A compléter après exécution
- Lien du run : A compléter après exécution

## Résultat

Lors de la validation recette, le workflow télécharge l'image depuis GHCR sans la reconstruire, lance un conteneur et effectue deux tests HTTP :
- GET http://127.0.0.1:8080/ → réponse 200 OK
- GET http://127.0.0.1:8080/version.json → réponse 200 OK

Le digest de l'image est affiché dans le résumé du run pour prouver que c'est bien la même image que celle publiée.
