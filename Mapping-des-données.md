## Codes des fournisseurs

Aide pour mapper la source de données vers l'institution et / ou la collection


***

### SOLUTION 1 (_Solution utilisée sur le portail GBIF France_) :

>Télécharger le DwC-A en local

>Ouvrez le fichier de ressources en utilisant Excel

>Ajouter des filtres au fichier

>Aller à institutionCode et collectionCode

>Cliquez sur le nom de la colonne pour connaître les différents codes utilisés par cet ensemble de données

__IMPORTANT :__  fonctionne avec des ressources dont le nombre d'occurrences est inférieur au nombre maximal de lignes dans Excel (environ 1 million)

***

### SOLUTION 2:

> Vous pouvez aussi lancer l'indexation, il y a une ligne d'info avec cette information :

>INFO: [DataLoader] - Les codes d'institution actuels pour la ressource de données

>INFO: [DataLoader] - Les codes de collecte actuels pour la ressource de données

>Entrez ces codes sur votre plateforme

***

## Création du mappage

Si les providersCodes spécifiques n'existent pas, entrez-les en utilisant la page "Manage provider code" :

`http://URL_to_your_ALA_portal/providerCode/list`

Créez le mappage du fournisseur entre la ressource de données, l'institution et/ou la collection dans la page suivante :

`http://URL_to_your_ALA_portal/providerMap/list`

## Saisie des métadonnées

Remplissez les métadonnées pour la source de données nouvellement créée.

Si la dataResource est un lien vers une collection :
* si elle n'existe pas: cela crée la page de collection.
* si elle existe : cela l'ajoute à la collection de l'utilisateur enregistré pour cette dataResource

Reliez la dataResource à un établissement :
* si elle n'existe pas : cela crée la page de l'institution avec l'action de renseignement des métadonnées.
* si elle existe : cela ajoute l'institution à l'utilisateur enregistré de cette dataResource.

N'oubliez pas de revenir à la page de la dataResource pour renseigner les informations des utilisateurs enregistrés si la collection ou l'institution n'existe pas.