# 04 - Preuve image GHCR

## Image publiée

- Nom de l'image : ghcr.io/devaradjalessy/project-cicd-ec06
- Tag principal : latest / sha-6acddaa
- Digest : sha256:c7fd9f4c087153756a09c682e6292388a51065539931af5b45171ecd191ea9d2
- Lien run publication : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/28599350379
- Lien GHCR : https://github.com/DevaradjaLessy/project-cicd-ec06/pkgs/container/project-cicd-ec06

## Explication

Le **tag** (sha-6acddaa) permet d'identifier lisiblement quelle version du code correspond à l'image. Il est lié au SHA du commit Git, ce qui garantit la traçabilité entre le code source et l'image produite.

Le **digest** (sha256:c7fd9f4c...) est une empreinte cryptographique unique de l'image. Contrairement au tag qui peut être réattribué, le digest est immuable : il identifie exactement le contenu de l'image. C'est ce qui permet de garantir qu'on promeut en production exactement la même image qui a été testée en recette, sans aucune modification.
