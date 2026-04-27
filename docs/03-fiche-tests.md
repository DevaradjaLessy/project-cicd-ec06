# 03 - Fiche tests

## Test automatisé GitHub Actions

- Workflow concerné : 01-ci.yml
- Lien vers le run réussi : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/24985970254
- Ce qui est testé : présence des fichiers requis, syntaxe compose.yml, build Docker, réponse HTTP sur / et /version.json, présence du texte "Projet CICD"
- Résultat : Success en 24s

## Test local Docker

### Situation A - Test réalisé

Environnement : Docker Desktop sur Windows

Commandes utilisées :

```bash
docker build -t projet-cicd-nginx:local .
docker run -d --name test-local -p 8080:80 projet-cicd-nginx:local
```

Résultat observé : Le site Catal-Log s'affiche correctement sur http://localhost:8080. La page affiche le titre "Site statique Catal-Log" et le footer "Projet CICD EC06 - Etudiant-EC06 - Version 0.1.0".

## Simulation de scaling

Commande exécutée :

```bash
docker compose up -d --scale web=2
docker compose ps
```

Résultat observé :
- project-cicd-ec06-web-1 : Up (instance 1)
- project-cicd-ec06-web-2 : Up (instance 2)
- project-cicd-ec06-whoami-1 : Up (service secondaire)
- project-cicd-ec06-tester-1 : Up (service de test)

4 conteneurs ont démarré simultanément dont 2 instances du service web.

## Limites de la simulation

- Absence de vrai load balancer : les deux instances web écoutent sur le même port expose, sans répartition de charge réelle.
- Absence de haute disponibilité : si l'hôte tombe, tous les conteneurs tombent.
- Absence de supervision : aucun outil ne surveille l'état des conteneurs en temps réel.
- Dépendance à l'environnement local : la simulation ne fonctionne que sur le poste de développement.
- Docker Compose ne gère pas la persistance des sessions entre les instances.
