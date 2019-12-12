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

Au lieu d'avoir un seul backbone, on a donc une suite de réseaux, les features utilisées par le reste de l'architecture étant celles données par le dernier backbone, baptisé "Lead BackBone". L'intérêt est ainsi double : non seulement on a de meilleurs performances grâce à l'ajout de plusieurs backbones, ce qui rend le tout plus puissant, mais en plus on peut toujours utiliser des modèles pré-entraînées, et faire un CBNet formé de plusieurs ResNet pré-entraînés, par exemple.

![alt text](https://raw.githubusercontent.com/triboolet/ProjetDL/master/images/cbnet_archs.png "archs")

Les auteurs du papier proposent plusieurs manières d'agencer un composite backbone : au final, lors des différents tests effectués, il apparaît que la première méthode, Adjacent Higher-Level Composition, donne les meilleurs résultats. De plus, une autre question se pose, celle du nombre de réseaux à mettre dans le composite backbone. 

![alt text](https://raw.githubusercontent.com/triboolet/ProjetDL/master/images/cbnet_numbers.png "numbers")

Après plusieurs tests, les auteurs conseillent de ne pas mettre plus de 3 réseaux, le gain en performance au-delà de ce seuil étant négligeable. 

![alt text](https://raw.githubusercontent.com/triboolet/ProjetDL/master/images/cbnet_results.png "results")

Enfin, cette table montre bien ce dont on parlait plus haut : les résultats montrent que CBNet est meilleur que l'état de l'art sur la détection d'objets, avec un gain significatif de plus d'un pourcent dans certains cas.

A noter qu'avec un tel backbone viennent des désavantages, notamment celui de la vitesse d'inférence du modèle. Le papier le mentionne, et propose même une solution avec une version améliorée du CBNet plus rapide.
