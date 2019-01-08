Il y a 4 moyens de télécharger des données sur votre portail ; chacun d'eux est expliqué sur cette page.

## Créer une ressource de données sur le site ALA

Accédez à votre interface d'administration à l'aide de l'URL suivante : <http://URL_of-you-portal/collectory/manage/list>.

Tout en bas de la page, deux fonctionnalités sont disponibles: 
1) [Add all GBIF resource](http://10.1.1.2/collectory/manage/gbifLoadCountry) pour un pays; 
2) [Upload GBIF file](http://10.1.1.2/collectory/dataResource/gbifUpload).


***


1. Cliquez sur "Upload" le fichier GBIF;
1. Trouvez le fichier sur votre bureau et cliquez sur "Upload";
1. Le résultat étant comme cette page:

![Résultat du téléchargement](/AtlasOfLivingAustralia/documentation/wiki/img/result_of_uploading.png)

Mémorisez bien l'UID : dr0 dans la première section. Cet UID sera utilisé pour l'étape suivante d'indexation et de traitement.

Lancer l'indexation et le traitement des données par rapport à la ressource de données nouvellement créée

Ceci est fait via l'interface de ligne de commande. Maintenant, naviguez vers ala-install/vagagrant/ubuntu et lancez :

    $ vagrant ssh

Ensuite, selon que le répertoire de données appartient à root, continuez le reste en tant qu'utilisateur root:

    $ sudo su

Démarrer la console biocache:

    $ biocache

Chargez, échantillonnez, procédéz, Indexez la ressource dr0 que nous venons de charger:

    biocache> ingest -dr dr0

À ce stade, consultez http://10.1.1.2/collectory/public/show/dr0 et vous pouvez voir que le site ALA a pris connaissance de ces enregistrements dans l'archive téléchargée.
![Après le téléchargement](/AtlasOfLivingAustralia/documentation/wiki/img/after.png)

Cliquez sur le bouton "view records", vous devriez être en mesure de voir la carte des enregistrements:
![Après le téléchargement](/ AtlasOfLivingAustralia/documentation/wiki/img/indexed.png)

## Ajouter toutes les ressources du GBIF pour un pays

Un nouvel outil permet de télécharger toutes les ressources du GBIF pour un pays donné. Pour ce faire, vous devez :

1. Dans le formulaire, remplissez le pays désiré, vos identifiants GBIF.org (utilisés pour vous connecter au site http://www.gbif.org/) et le nombre de ressources nécessaires.
1. Vous devriez obtenir toutes les ressources de ce pays téléchargées automatiquement avec cet outil.

## Fournisseurs de données

Les fournisseurs de données sont des organisations, des particuliers et autres institutions (comme des musées) qui donnent accès à certaines de leurs données.

Pour obtenir les données auxquelles ils ont donné accès, voici les étapes:

1. Allez sur http://ala-demo.org/collectory/manage/list, cliquez sur "View all data providers" puis sur "Add a new DataProvider". Entrez un nom et l'adresse URL de l'IPT dans la partie "entrer le nom" et cliquez sur "Check endpoint" dans la partie d'intégration IPT.
A la fin, cliquez sur "Update data resources";

1. Vous devez 'ingérer' les nouvelles données ; pour cela, allez dans le terminal et tapez :

	`$sudo biocache`   
	`biocache>ingest -a `


@todo: le dernier moyen de téléchargement de données