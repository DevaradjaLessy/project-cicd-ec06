# 04 - Preuve image GHCR

## Image publiée

- Nom de l'image : ghcr.io/devaradjaLessy/project-cicd-ec06
- Tag principal : latest / sha-xxxxxxx
- Digest : A compléter après publication (sha256:...)
- Lien GHCR : https://github.com/DevaradjaLessy/project-cicd-ec06/pkgs/container/project-cicd-ec06

## Explication

Le **tag** (ex: sha-abc1234) permet d'identifier lisiblement quelle version du code correspond à l'image. Il est lié au SHA du commit Git, ce qui garantit la traçabilité entre le code source et l'image produite.

Le **digest** (ex: sha256:abc123...) est une empreinte cryptographique unique de l'image. Contrairement au tag qui peut être réattribué, le digest est immuable : il identifie exactement le contenu de l'image. C'est ce qui permet de garantir qu'on promeut en production exactement la même image qui a été testée en recette, sans aucune modification.
