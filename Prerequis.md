Le portail ALA nécessite plusieurs composants tels que Java, Tomcat et Cassandra, ainsi que des applications Web qui composent le portail ALA. 
Ces logiciels peuvent être automatiquement installés et configurés par un playbook [Ansible](http://www.ansible.com/home), un type de script développé avec le projet. Donc, si vous avez une instance Linux Ubuntu en cours d'exécution, vous pouvez utiliser les playbooks Ansible dans le projet [ala-install](https://github.com/AtlasOfLivingAustralia/ala-install) pour monter et configurer automatiquement l'instance Linux dans un portail ALA.

En plus des playbooks Ansible, si vous n'avez pas d'instance Linux prête, ou si vous voulez simplement mettre en place un nettoyage pour ce portail ALA, vous pouvez considérer les deux outils suivants pour créer une instance propre:

* [Vagrant](http://www.vagrantup.com/) : Créer et configurer une machine virtuelle pour héberger le portail ALA;
* [VirtualBox](http://www.vagrantup.com/) : le conteneur de machines virtuelles;

Le [guide d'installation](https://github.com/AtlasOfLivingAustralia/documentation/wiki/Installation) suppose que l'on veut créer une instance Linux et configurer un portail ALA à partir de zéro. Si vous voulez configurer une instance Linux existante (Ubuntu), vous pouvez aller directement à la section [Ansible](https://github.com/AtlasOfLivingAustralia/documentation/wiki/Installation#ansible) du guide d'installation. Ce didacticiel ne peut être exécuté que sur des systèmes UNIX (Linux / Mac OS X), étant donné qu'Ansible n'est pas encore disponible sur Microsoft Windows au 24 juin 2014.

En utilisant un Macintosh comme exemple, voici les étapes pour obtenir ces outils prêts à l’emploi :

1. [Télécharger Vagrant](http://www.vagrantup.com/downloads.html) et installez le paquet téléchargé.
1. [Télécharger VirtualBox](https://www.virtualbox.org/wiki/Downloads) et installez le paquet téléchargé.
1. Pour installer Ansible, le plus simple est d'installer via [homebrew](http://brew.sh/). Il est également pratique d'avoir [les outils de ligne de commande pour Mac OS X](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/) installés. Une fois prêt, les commandes suivantes vont installer Ansible:
    
        $ brew update
        $ brew install ansible

Les pré-requis serveur recommandées sont les suivants:
* Machine virtuelle avec Ubuntu 12 ou 13.
* 100 Go de stockage sur disque libre (idéalement SSD), l'indexation et le traitement des données consomme de l'espace très rapidement.
* 32 Go de RAM.
* 2 CPU.

Cependant, dans ce guide, [Vagrantfile](https://github.com/AtlasOfLivingAustralia/ala-install/blob/master/vagrant/ubuntu/Vagrantfile) déterminera les configurations de serveur pour vous.

Vous êtes maintenant prêt à commencer l'installation du portail ALA.

## Environnement testé
* Vagant 1.6.2 + VirtualBox v4.3.12 r93733 + Ansible 1.6.1 sur Mac OS X 10.8.5.