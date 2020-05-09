# 1.
_Qu'est-ce qu'une instance Virtual Machine ?

Une machine virtuelle, ou VM (Virtual Machine), est un environnement d'application ou de système d'exploitation (OS, Operating System) installé sur un logiciel qui imite un matériel dédié. Côté utilisateur final, l'interaction avec une machine virtuelle est la même qu'avec un matériel dédié.
# 2.
_Qu'est-ce qu'un VNET ?

Le réseau virtuel Azure (VNet) est le bloc de construction fondamental pour votre réseau privé dans Azure. Le réseau virtuel permet à de nombreux types de ressources Azure, telles que les machines virtuelles (VM) Azure, de communiquer de manière sécurisée entre elles, avec Internet et avec les réseaux locaux. Un réseau virtuel est similaire à un réseau traditionnel que vous utiliseriez dans votre propre centre de données, mais avec les avantages supplémentaires de l’infrastructure Azure, tels que la mise à l’échelle, la disponibilité et l’isolation.

# 3.
A quoi sert un NSG ?
Le Network Security Group correspond aux matrices de flux celle-ci s’applique sur:
Cartes réseaux/serveurs Base de données Passerelle VPN Sous réseau Tag/balise

# 4.
Quelles sont les 5 propriétés désirables du cloud ?

Les cinq caractéristiques essentielles du Cloud computing :
- Accès aux services par l'utilisateur à la demande.
- Accès réseau large bande.
- Réservoir de ressources (non localisées)
- Redimensionnement rapide (élasticité)
- Facturation à l'usage.

# 5.
Qu'est-ce que l'A/B Testing ?

L’A/B Testing est une technique qui consiste à mettre en comparaison deux versions d’une page web, d’une application, d’un e-mail ou même d’un formulaire, afin d’analyser les résultats et déterminer la version la plus performante selon l’objectif souhaité
# 6.
Comment programmer le cloud ?
Les Étapes pour programmer le cloud sont :

- Stocker les données
- Transférer les applications dans le cloud
- Disposer d’une visibilité complète
- Faire des amélioration
# 7.
Quelle est la technique pour faire un déploiement sans interruption de service ?

Faire un déploiement sans interruption de service il faut d'abord isolé les machines de productions mais aussi découper 
les versions en un plus grand nombre de livraisons de moindre taille et moins complexes à tester,
automatisant au maximum les étapes de tests et passages en production d’une nouvelle version afin de réduire les cycles,
permettant un déploiement très régulier des nouveautés.

# 8.
Qu'est-ce que le Canary release ?

Le canary release est un pattern qui permet de faire tester les dernières modifications réalisées (appelée version N+1) à une tranche de population restreinte avant de réaliser un déploiement général de cette version.

# 9.
Comment changer de taille de machine virtuelle ?
Avec une commande qui permet l'augmentation du disque dur:
- VBoxManage.exe modifyhd "D:\VirtualBox\Windows 10bis.vdi" --resize 2000. 
Ici on augmente le disque dur de 200Go.

# 10.
Qu'est-ce que le Blue/Green deployment ?
Le Blue-Green Deployment et l’exposition progressive offrent encore plus de souplesse et réduisent de façon drastique le risque de bogue en production.
Le principe de l’exposition progressive est assez simple : la nouvelle version de l’application est rendue disponible à un nombre restreint d’utilisateurs. Plus elle est stable et plus l’on est satisfait de sa réactivité, plus elle est accessible à un nombre important d’utilisateurs, jusqu’à une exposition complète à l’ensemble des utilisateurs.
# 11.
Citez deux avantages du PaaS sur le IaaS ?

Deux avantages du PaaS sur le IaaS
- Une mise en production quasi instantanée.
- Une fluidité dans l'organisation

# 12.
Quelle est la différence entre le PaaS et le Serverless ?

Les applications Serverless évoluent instantanément, automatiquement et à la demande, sans configuration supplémentaire de la part du développeur ou du fournisseur. En revanche, ce n'est pas une caractéristique intrinsèque de PaaS. Le serverless peut évoluer rapidement en faisant tourner de nouvelles instances de fonctions d'application à mesure qu'elles sont demandées. Il se réduit également rapidement en arrêtant les fonctions lorsqu'elles ne sont plus nécessaires ou lorsqu'elles ont fonctionné pendant une période de temps définie. Les applications basées sur PaaS ne peuvent pas évoluer si rapidement ou à un tel degré.

# 13.
Que veut dire Serverless ?

L'informatique sans serveur ou serverless computing est un paradigme de cloud computing dans lequel le fournisseur de serveur gère dynamiquement les ressources allouées au service client. Le terme 'sans serveur' ne signifie pas qu'il n'y a pas de serveurs impliqués. Cela signifie qu'ils sont gérés par les fournisseurs et non par les consommateurs.

# 14.
Citez les trois propriétés désirable du Serverless ?

Une application Web Serverless peut évoluer jusqu'à arrêter son activité, puis redémarrer en réponse à un événement en quelques secondes ou millisecondes. Certains fournisseurs Serverless ne facturent aux développeurs que la durée exacte d'exécution de leurs fonctions. Le temps de lancement des applications Serverless est très rapide.

# 15.
Comment s'appelle la plus petite unité de compute déployable en Serverless ?

La plus petite unité de compute déployable en Serverless est une Fonction (programme informatique).
