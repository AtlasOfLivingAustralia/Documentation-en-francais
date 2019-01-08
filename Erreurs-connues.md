# Gérer CorruptSSTableException

## Procédure

Si vous rencontrez cette exception lors du chargement ou du traitement des données, suivez les instructions ci-dessous :

* faire un instantané avec ``nodetool snapshot occ``
* arrêter le service avec ``service cassandra stop``
* lancé ``sstablescrub occ occ`` - ceci identifie et laisse la table corrompue intacte
(la commande précédente doit été exécutée en tant que sudo):
* ``chown -R cassandra:cassandra /data/cassandra/data/occ/occ``
* déplacer la table corrompue dans le répertoire de sauvegarde
* ``nodetool repair occ``