Vous devez avoir un fichier Vagrant et un playbook Ansible afin de guider Vagrant et Ansible pour l'automatisation.

L'ensemble de l'installation, sur un MacBook Pro, INTEL i7 2.66Ghz (fin 2010) avec SSD, prend environ 30 minutes. Cela inclut le temps de transférer des fichiers war par Internet.

Pour les obtenir, clonez le repo ALA-install à l'adresse <https://github.com/AtlasOfLivingAustralia/ala-install>.

    $ git clone https://github.com/AtlasOfLivingAustralia/ala-install.git
    $ cd ala-install

## Vagrant

    $ cd vagrant/ubuntu/
    $ vagrant up

À ce stade, vous devriez voir une instance d'ubuntu fonctionner si vous ouvrez VirturalBox:

![VirtualBox UI](/AtlasOfLivingAustralia/documentation/wiki/img/virtual_box.png)

A la date du 28 mai 2014, vous pourriez voir "default: stdin: is not a tty" en rouge. Cela n'a aucune incidence handicapante car si vous faites:

    $ vagrant ssh

Vous pouvez vous connecter à l'instance d'ubuntu que vous venez de configurer:
![vagrant ssh](/AtlasOfLivingAustralia/documentation/wiki/img/vagrant_ssh.png)

### Problème de mémoire
En cas de problème de mémoire (insuffissante), vous pouvez modifier le fichier vagrant dans `Vagrant/ubuntu-Trusty/Vagrantfile` :

    # these machines require some memory to operate the apps
    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
    end 

Ensuite, après avoir modifié le fichier, démarrez simplement votre machine:
    
    vagrant up

## Ansible
Vous êtes maintenant prêt à configurer le serveur Ubuntu avec Ansible.
Pour exécuter le playbook Ansible:

    $ cd ../../ansible/
    $ ansible-playbook -i inventories/vagrant/demo-vagrant ala-demo.yml --private-key ~/.vagrant.d/insecure_private_key -u vagrant -s

Le playbook devrait être fini. Il pourrait y avoir quelques erreurs mineures non-bloquante. Dans ce cas, veuillez déposer un problème afin que les développeurs puissent enquêter. Merci!

![ansible finished](/AtlasOfLivingAustralia/documentation/wiki/img/ansible_finished.png)

Le portail de démonstration ALA devrait être accessible maintenant. Par commodité, comme dans le fichier Vagrantfile, le nom d'hôte est défini comme ala.vagrant.dev et il a une adresse IP 10.1.1.2. 
En ajoutant une ligne dans / etc / hosts:

    10.1.1.2  ala.vagrant.dev

... vous permettra de visiter le portail de démonstration ALA depuis la machine d'hébergement.

![vagrant ssh](/AtlasOfLivingAustralia/documentation/wiki/img/ala.vagrant.dev.png)

Toutes nos félicitations! Votre portail de démonstration ALA est opérationnel.

#### Arréter la VM
Lorsque vous êtes satisfait de l'installation de test, il est probable que vous ayez besoin d'une pause, vous devez donc arrêter la machine virtuelle. Pour faire cela:

    $ cd ../vagrant/ubuntu/
    $ vagrant halt

Cette commande arrête la machine en cours d'exécution que Vagrant gère.
Si vous voulez supprimer cette instance de test, dans le même répertoire, faites:

    $ vagrant destroy

Cela effacera la machine virtuelle et toute la configuration que vous avez faite avec Ansible.