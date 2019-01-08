## Ingestion des ressources

### Jeux de données

***

#### Dans le cas d'une petite source de données ( < 50 000 enregistrements)

1 Connectez-vous au serveur sur lequel votre outil biocache est hébergé

2 Connectez-vous à biocache

	$ sudo biocache

3 Exécutez la ligne de commande suivante:

	$ ingest –dr <id_source_donnees>

Vous pouvez également exécuter directement sur le terminal

	$ sudo biocache ingest -dr <id_source_donnees>

__Important:__ vous n'aurez pas de log si vous ne spécifiez pas le fichier de sortie.

***

#### Dans le cas d'une grande source de données ( > 50 000 enregistrements et < 8 millions)

1 Connectez-vous au serveur sur lequel votre outil biocache est hébergé

2 Connectez-vous à biocache:

	$ sudo biocache

3 Exécutez les lignes de commande suivantes:

	$ load <id_source_donnees>
	$ process -dr <id_source_donnees>
	$ sample -dr <id_source_donnees>
	$ index -dr <id_source_donnees>

Vous pouvez également exécuter directement sur le terminal, les lignes de commande ci-dessus avec

	$ sudo biocache 

***

#### Dans le cas d'une très grande source de données (taille de l'archive DwC > 1 Go)

 1 Téléchargez une archive DwC modifiée avec 15 occurrences afin de créer l'ensemble de données dans le système.

 2 Copiez la vraie archive DwC au lieu de celui modifié dans le dossier `/collectory/upload/`

 3 Exécutez ensuite les commandes load, process et index:

	$ load <id_source_donnees>
	$ process -dr <id_source_donnees>
	$ sample -dr <id_source_donnees>
	$ index -dr <id_source_donnees>
 
 L'étape 1 est obligatoire car la bibliothèque ZipFile utilisée par le biocache-store ne peut pas ouvrir un fichier plus grand que 1 GO

 Vous devez avoir un serveur qui doit avoir au moins autant de RAM (sinon plus) que la taille de votre archive DwC.


### Toutes vos ressources

Vous pouvez exécuter une ligne de commande (en tant qu'utilisateur sudo):

	$ nohup biocache ingest -all > /tmp/load.log &

Vous pouvez exécuter trois lignes de commande différentes directement sur le terminal (en tant qu'utilisateur sudo):

	$ biocache bulk-processor load -t 7 > data/output_load.log
	$ biocache bulk-processor process -t 6 > data/output_process.log
	$ biocache bulk-processor index -ps 1000 -t 8 > /data/output_index.log

Avec l'option `-t`, vous indiquerez le nombre de CPU que vous voulez utiliser pour le processus.

Avec l'option `-ps`, vous donnerez le nombre d'occurrences par pages sur SOLR.

## Utilisation & bonnes pratiques de Biocache

@Todo: Conseils et bonnes pratiques à ajouter

@Todo: Astuces: Vous n'avez pas besoin d'entrer dans l'environnement biocache pour exécuter la ligne de commande biocache (repéré par institution/production ALA)

## Commandes pour le module spatial

@Todo : instruction à ajouter