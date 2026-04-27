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

## Tests complémentaires

### Test 1 — Vérification du fichier version.json

```bash
curl http://localhost:8080/version.json
```

Résultat attendu :
```json
{
  "projet": "Projet CICD",
  "contexte": "EC06 - ASRC",
  "organisation": "Catal-Log",
  "auteur": "Etudiant-EC06",
  "version": "0.1.0",
  "date": "2026-04-27"
}
```

Ce test vérifie que le fichier de version est bien servi par Nginx et que les métadonnées sont correctes.

### Test 2 — Vérification des headers HTTP

```bash
curl -I http://localhost:8080/
```

Résultat attendu : HTTP/1.1 200 OK avec le header Server: nginx

Ce test vérifie que c'est bien Nginx qui sert le contenu et que la réponse est correcte.

### Test 3 — Vérification du service whoami

```bash
docker compose up -d
curl http://localhost:$(docker inspect --format='{{(index (index .NetworkSettings.Ports "80/tcp") 0).HostPort}}' project-cicd-ec06-whoami-1)/
```

Ce test vérifie que le second service whoami répond correctement, prouvant la coordination entre conteneurs.

## Limites de la simulation

- Absence de vrai load balancer : les deux instances web écoutent sur le même port expose, sans répartition de charge réelle.
- Absence de haute disponibilité : si l'hôte tombe, tous les conteneurs tombent.
- Absence de supervision : aucun outil ne surveille l'état des conteneurs en temps réel.
- Dépendance à l'environnement local : la simulation ne fonctionne que sur le poste de développement.
- Docker Compose ne gère pas la persistance des sessions entre les instances.
