L'indexation des noms a lieu pendant la phase de "traitement" de l'ingestion. Si une liste de contrôle personnalisée/nationale est requise, un nouvel index de nom peut être créé.

## Playbook nameindexer-standalone.yml

En supposant que vous ayez une instance du portail ALA qui soit en cours d'exécution, lorsque vous ayez besoin d'utiliser votre propre index de noms ou de mettre à jour l'index de noms existant, vous souhaitez l'exécuter séparément afin de ne pas interrompre le service en cours.

Donc, comme dans le tutoriel de construction d'un index de nom personnalisé, nous partons d'une boîte Ubuntu vanilla vagrant.

    $ cd ala-install/vagrant/ubuntu
    $ vagrant status

À ce stade, si vous avez une boîte vagrant en cours d'exécution, pensez à la détruire et à en commencer une nouvelle.

    $ vagrant destroy
    $ vagrant up

Assurez-vous que la boîte virtuelle est opérationnelle et que vous pouvez vous connecter :

    $ vagrant ssh

Maintenant, exécutez le playbook pour créer l'instance qui va construire nameindexes :

    $ cd ../../ansible
    $ ansible-playbook -i inventories/vagrant nameindexer-standalone.yml --private-key ~/.vagrant.d/insecure_private_key -u root

Endroit où les sources de nom sont stockées:

    $ cd /data/lucene/sources

Regardez dans le dossier cible avant d'indexer les noms :

    $ ls /data/lucene

Il ne doit y avoir qu'un seul répertoire 'sources'.

Maintenant, pour créer un index de nom :

    $ sudo nameindexer -dwca /data/lucene/sources/dwca-col-mammals

(A la date du 23/07/2014, le propriétaire par défaut de /data est root ; vous devez donc utiliser l'instruction sudo pour lancer le nameindexer.)

Notez que le 'dwca-col-mammals' est un dossier extrait de l'archive dwca-col-mammals.zip. Si vous travaillez sur votre propre liste de contrôle au format DwC-A, assurez-vous de l'extraire avant de lancer le nameindexer. Tapez `$ nameindexer -help` pour plus d'information.

Tester la recherche pour voir si l'index de nom a été construit avec succès:

    $ sudo nameindexer -testSearch "Macropus rufus"

vous devez voir :

    Search for name
    ID: 6863103
    GUID: urn:lsid:catalogueoflife.org:taxon:d9f7aefa-29c1-102b-9a4a-00304854f820:col20120124
    Classification: "(Desmarest, 1822)",Animalia,Chordata,Mammalia,Diprotodontia,Macropodidae,Macropus
    Scientific name: Macropus rufus
    Authorship: (Desmarest, 1822)
    Rank: SPECIES
    Synonym: null
    Match type: exactMatch

Cela confirmera que vous avez un index fonctionnel.

Après avoir exécuté la commande suivante (une fois les instructions ci-dessus effectuées), `$ ls /data/lucene`, vous verrez deux nouveaux répertoires:

    namematching
    nmload-tmp
Pour utilisez le nouveau index de nom, vous pouvez compresser ces deux répertoires, puis décompresser et remplacer le même qui est situé sur votre site de production. L'étape suivante consisterait à mettre à jour l'index Solr d'occurrence pour utiliser ce nouvel index de noms.

Pour seulement quelques jeux de données ayant un nombre plutôt petit d'enregistrement (<~ 5m), vous exécuteriez simplement:

    biocache> index -dr [druid]

Mais si c'est plus que ça, vous devrais faire :

    biocache> bulk-processor

## Formats de liste de contrôle pris en charge

@Todo : Texte à ajouter (avec images ?) 

## À propos des homonymes

L'indexation des noms recherche, par défaut, dans `/data/lucene/sources/IRMNG_DWC_HOMONYMS` pour analyser les homonymes. Si vous avez d'autres homonymes à détecter, exécutez `nameindexer` avec le drapeau` -irmng` et pointez vers votre propre homonyme DwC-A que vous avez extrait.

Pour éviter une erreur d'indexation d'homonyme évidente, vous pouvez fournir des indicateurs de taxonomie dans le Collectory-hub lorsque vous modifiez les métadonnées des ressources de données en fournissant un indice de taxinomie. L'URL serait `/collectory/dataResource/edit/[druid]?page=%2Fshared%2FeditTaxonomyHints`. (Remplacez [druid] par le vôtre.)