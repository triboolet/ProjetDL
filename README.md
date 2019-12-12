# Projet Deep Learning
## Andrii Kovalenko & François Philipps

L'objectif de ce projet est l'exploration d'architectures de détection d'objets et l'application à un dataset d'images d'avions bruitées, fournies par l'ONERA.
Pour cela, nous utilisons [Detectron2](https://github.com/facebookresearch/detectron2), l'outil de FAIR basé sur Pytorch permettant d'utiliser de nombreuses architectures de détection d'objets.

# Présentation de CBNet

[CBNet] (pour Composite BackBone Network) est une récente architecture pour la détection d'objets à l'état de l'art sur le dataset COCO. L'idée est de modifier une partie des architectures déjà existantes : le réseau Backbone.

![alt text](https://raw.githubusercontent.com/triboolet/ProjetDL/master/images/faster_rcnn.png "Faster RCNN")

Voici ci-dessus un schéma du Faster-RCNN. On voit bien que les boîtes englobantes sont extraites à partir des features maps données par un premier réseau convolutionnel : toute l'architecture dépend des résultats de ce réseau, d'où son nom de "backbone". Celui-ci est généralement un réseau pré-entraîné, par exemple VGG16 ou un ResNet entraînés sur ImageNet. Ainsi, il est déjà capable d'extraire des caractéristiques et il ne reste plus qu'à apprendre les autres parties de l'architecure, comme le RPN pour un Faster-RCNN.
CBNet va donc remplacer ce backbone network par plusieurs backbones, afin d'améliorer les performances.

![alt text](https://raw.githubusercontent.com/triboolet/ProjetDL/master/images/cbnet.png "CBNet")

Au lieu d'avoir un seul backbone, on a donc une suite de réseaux, les features utilisées par le reste de l'architecture étant celles données par le dernier backbone, baptisé "Lead BackBone". 




