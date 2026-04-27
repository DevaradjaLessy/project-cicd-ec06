# 04 - Preuve image GHCR

## Image publiée

- Nom de l'image : ghcr.io/devaradjalessy/project-cicd-ec06
- Tag principal : latest / sha-d41aa59
- Digest : sha256:1bbab9dfa173f15292c78b70e1230f49bb756f165fe89ff7c342e7e0a7d1cbd9
- Lien run publication : https://github.com/DevaradjaLessy/project-cicd-ec06/actions/runs/24985970255
- Lien GHCR : https://github.com/DevaradjaLessy/project-cicd-ec06/pkgs/container/project-cicd-ec06

## Explication

Le **tag** (sha-d41aa59) permet d'identifier lisiblement quelle version du code correspond à l'image. Il est lié au SHA du commit Git, ce qui garantit la traçabilité entre le code source et l'image produite.

Le **digest** (sha256:1bbab9dfa173...) est une empreinte cryptographique unique de l'image. Contrairement au tag qui peut être réattribué, le digest est immuable : il identifie exactement le contenu de l'image. C'est ce qui permet de garantir qu'on promeut en production exactement la même image qui a été testée en recette, sans aucune modification.
