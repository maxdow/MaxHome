# MaxHome
Projet de domotique personnelle DIY à bas coût


##Présentation
### Pourquoi un système de plus ?
Il existe déjà de nombreux système domotiques, ouverts ou non. N'ayant pas trouvé de système idéal pour mon usage, j'ai donc décidé de m'en construire un "from scratch". Les motivations principales sont avant tout le **plaisir** d'apprendre et la **passion**. 

Ma contrainte de base est le coût. C'est ce qui me gène le plus dans la domotique actuelle (payer une ampoule 80€ non merci ! )

Ce projet est un projet personnel qui n'a pas pour but une commercialisation ni une distribution massive. Il reste néanmoins accessible et open-source mais il n'y a aucun support de prévu . C'est en quelque sorte un grand bac à sable pour jouer avec des problématiques hardware, radio, software, interface, serveur...

### Technologies employées

 - Principalement du **javascript** pour le serveur et l'interface.
 - La passerelle et les modules dit "hardware" sont codés  en **C à l'aide des librairies Arduino**
 - La base de donnée (configuration + données ) est en **SQLite**

Les différentes parties seront détaillées dans la documentation mais peuvent tout à fait évoluer en cours de route.

##Objectif(s)

 - Créer un système de domotique permettant de monitorer et contrôler un environnement d'habitat.
 - Le rendre le plus modulable possible pour être modifié et amélioré
   dans le future
 - Explorer les pistes de commande vocal
 - Rendre le système autonome ( scénarios, apprentissages )
 - **Se faire plaisir**

##Historique
( photos à venir )
### V3
Après avoir testé des modules nrf24 j'ai décidé d'opter pour des modules un peu plus cher ( moins de 5€) mais beaucoup plus efficace , les rfm69. J'ai choisit d'utiliser la bande des 868Mhz . Quelques protocoles domotique commencent à l'utiliser mais il est interessant sur un point particulier à mon avis, cette fréquence est assez peu polluée ( entre le 433Mhz et le wifi à 2.4Ghz) . On profite aussi d'un meilleur débit même si ce n'est pas un soucis dans mon cas. La pénétration ainsi que la portée est sensé être moins importante qu'avec le 433Mhz mais reste plus que convenable pour un usage local ( maison + petit jardin ) . Pour finir, du fait du changement de fréquence, les antennes sont 2 fois moins grandes que pour du 433Mhz ( 8.2cm pour du 1/4 d'onde contre 16cm avec le 433Mhz) .
#### Problèmes ( déjà ) 
Le principal soucis vient du fait qu'ils fonctionnent en 3.3V et que toutes mes précédentes cartes sont faites pour du 5V. Après quelques tests en mode bidouille, j'obtiens néanmoins une excellente réception. En plus ces modules intègrent un certain nombre de fonctionnalités interessantes et la librairie de lowpowerlab fournie une gestion du ACK efficace et qui fait ses preuves lors de mes essais.

Cependant, devant la complexité grandissante des cartes, le prototypage semble de plus en plus contraignant ( avec des risques de se retrouver avec des courts circuits comme avec la V1).

### V2
Finalement j'ai opté pour des cartes toutes faites pour les microcontrolleur , des arduino pro mini. Ils embarquent tout ce qu'il faut pour faire fonctionner la puce et les pattes sont accessibles ( le coût reste très faible de l'ordre de 2.50€) .
J'ai également revu les schéma de carte tout en restant dans le prototypage.
Niveau serveur / interface, grosse amélioration avec un processus de build et une interface permettant la gestion et la création de modules en ligne.

#### Problèmes
Les problèmes ( comme la V1) ont été surtout du fait de la radio. Même en ayant testé des antennes dipoles maison , la communication est assez sensible. Après de nombreuses recherches , ces modules peut cher sont aussi assez peu efficaces surtout sans soins particulier ( plan de masse, antenne de bonne qualité). Ils nécessitent en plus une gestion de la transmission. Il existe [une librairie pour Arduino](http://www.airspayce.com/mikem/arduino/RadioHead/) qui fait ça très bien .
Le build mis en place devenait finalement assez lourd et la gestion des callback de plus en plus complexe. De plus j'avais envie d'intégrer un système de plugin , il fallait donc revoir l'organisation du serveur.


### V1
J'ai commencé à réfléchir pour mettre en place ce projet peu de temps après l'acquisition d'une maison. Le soucis étant d'insérer une domotique sur un habitat existant. Les premiers essais hardware ont été fait sur des plaques de prototypage avec des composants trouvé dans les tiroirs . J'avais à ma disposition quelques ATMEGA ( 8 32 et 164p ) .
La communication radio était en 433Mhz avec ces modules ebay à bas prix. 

#### Problèmes
Les soucis sont assez vite arrivé à cause des problèmes de connexions sur les cartes. Je devais reprogrammer souvent les microcontrôleurs et je me suis souvent retrouvé face à un élément non reconnu. En bref bcp de temps perdu à trouver le court circuit ! 
