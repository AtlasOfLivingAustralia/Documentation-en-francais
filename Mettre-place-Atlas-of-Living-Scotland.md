# Configurer Atlas of Living Scotland

L'Atlas of Living Scotland a été configuré en utilisant une sélection de scripts [ansible](http://www.ansible.com/).
La plupart de ces scripts se trouvent dans le dépôt Atlas of Living Autralia (ALA) [ala-install](http://github.com/atlasoflivingaustralia/ala-install).

Ici sera présenté un exemple d'une configuration système qui est bien plus avancé que le playbook ala-demo, en mettant en place beaucoup plus de composants dans le système.

Certains playbooks additionnels ont été utilisé dans le dépôt pour la configuration du système. 
Les inventaires ansibles qui ont été utilisés sont dans un dépôt privé.


## Pour commencer

Pour éviter une tape de clavier fastidieuse, définissez un alias Unix comme indiqué sur le fichier PEM que vous allez utilisé sur les machines virtuelles :

```
export alias ansible-als='ansible-playbook --private-key ~/.ssh/XXXXXXXXX.pem -u ubuntu -s'
```

## Playbooks Ansible utilisé pour configurer le système

### Installer le registry (collectory)

La ligne suivante va configurer le registry principal, the collectory, pour le système.

```
ansible-als -i inventories/registry.als.scot ala-install/ansible/collectory.yml
```

### Installer le backend d'occurrence (la base de données biocache)

```
ansible-als -i inventories/occurrence-db.als.scot ala-install/ansible/biocache-backend.yml
```

### Installer le service d'images

Installer les services d'image et le backend de la base de données.

```
ansible-als -i inventories/images.als.scot ala-install/ansible/image-service.yml
```

### Installer le Service d'Authentification Centrale (CAS)

Installer le composant d'authentification de signature unique.

```
ansible-als -i inventories/auth.als.scot ala-install/ansible/auth-standalone.yml
```

### Installer les observations

Installer le composant ad-hoc pour les observations.

```
ansible-als -i inventories/ecodata.als.scot ala-install/ansible/ecodata.yml 
ansible-als -i inventories/sightings.als.scot ala-install/ansible/pigeonhole-standalone.yml 
```

### Le serveur d'index

Le script suivant va configurer SOLR sur un serveur autonome.

```
ansible-als -i inventories/index.als.scot ala-install/ansible/solr-standalone.yml 
```

### Page web des espèces & Interface Utilisateur (BIE)

Le script suivant va configurer les pages espèces et les services web sur un serveur autonome.

```
ansible-als -i inventories/species-ws.als.scot ala-install/ansible/bie-index.yml 
ansible-als -i inventories/species.als.scot ala-install/ansible/bie-hub.yml 
```

### Services web Biocache & Interface Utilisateur

Ce script configure les pages de recherche d'occurrences et les services Web sur un serveur autonome.
```
ansible-als -i inventories/records-ws.als.scot ala-install/ansible/biocache-service.yml 
ansible-als -i inventories/records.als.scot ala-install/ansible/biocache-hub.yml 
```

### Installer la version du Royaume-Unis (UK) de l'index de correspondance des noms

Ce script installe l'index de nom sur les machines via les index de noms lucene. Cela inclura les services Web biocache, l'outil de listes et quelques autres composants.

```
ansible-als -i inventories/name-index als-install/ansible/name-index.yml 
```