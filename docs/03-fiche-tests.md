# 03 - Fiche tests

## Test automatisé GitHub Actions

- Workflow concerné : 01-ci.yml
- Lien vers le run réussi : A compléter après exécution
- Ce qui est testé : présence des fichiers requis, syntaxe compose.yml, build Docker, réponse HTTP sur / et /version.json, présence du texte "Projet CICD"
- Résultat : A compléter après exécution

## Test local Docker

### Situation A - Test réalisé

Environnement : Docker Desktop sur Windows

Commandes utilisées :

```bash
docker build -t projet-cicd-nginx:local .
docker run --rm -p 8080:80 projet-cicd-nginx:local
```

Puis dans un navigateur : http://localhost:8080

Résultat observé : A compléter après test local

## Simulation de scaling

Commande exécutée :

```bash
docker compose up -d --scale web=2
docker compose ps
```

Résultat observé : A compléter après exécution

## Limites de la simulation

- Absence de vrai load balancer : les deux instances web écoutent sur le même port expose, sans répartition de charge réelle.
- Absence de haute disponibilité : si l'hôte tombe, tous les conteneurs tombent.
- Absence de supervision : aucun outil ne surveille l'état des conteneurs en temps réel.
- Dépendance à l'environnement local : la simulation ne fonctionne que sur le poste de développement.
- Docker Compose ne gère pas la persistance des sessions entre les instances.
