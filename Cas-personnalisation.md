Il est possible d'avoir plusieurs applications Web avec une interface utilisateur personnalisée et d'afficher des données pour un Hub particulier en utilisant un seul serveur principal.

Étapes de base
* Créer et configurer le hub dans le collectory-hub
* Configurer l'application Web pour afficher les enregistrements du nouveau hub
* Configurer les champs de facet
* Liste des cas de personnalisation (application web générique-hub)

## Étapes de bases

### Créer et configurer le hub dans le collectory-hub

Dans l'interface d'administration de collectory-hub, recherchez l'option *View all data hubs*, vous pouvez ajouter à cet endroit un nouveau DataHub. Modifiez le nom et toute autre information requises.
Dans la section **Members**, ajoutez l'identifiant des institutions, des collections et des ressources de données qui appartiennent au Hub. C'est l'information qui apparaîtra dans l'application web.

### Configurer l'application Web pour afficher les enregistrements du nouveau hub

Recherchez l'UID du hub que vous avez déjà créé dans l'interface d'administration de Collectory-hub.
Dans le fichier de configuration de l'application Web (grails-app/conf/config.groovy), ajoutez la propriété avec l'UID approprié.

    biocache.queryContext = "data_hub_uid:dh1"

### Configurer les champs de facet 

Les variables de configuration commençant par `facets.` sont responsables de ceci :

* **`facets.include`** - liste de champs séparés par des virgules à inclure (habituellement seulement les champs qui ne sont pas dans l'ensemble par défaut spécifié par` ${biocache.baseUrl}/search/facets`)
* **`facets.exclude`** - liste des champs à exclure séparés par des virgules. c'est-à-dire les champs du jeu par défaut que vous ne voulez pas voir apparaître
* **`facets.hide`** - liste de champs séparés par des virgules qui seraient inclus dans la colonne à facettes, que vous voulez cacher (c'est-à-dire non cochés dans le menu déroulant  "customise filters"). Ces champs seront affichés si l'utilisateur modifie les paramètres d'affichage par défaut et choisit de les activer.

Notez que vous pouvez également modifier **l'ensemble par défaut** des facettes, mais cela est défini dans l'application **biocache-service**, également via config vars (je pense). Vous pouvez également changer la façon dont les facettes sont **regroupées** ensemble (voir `${biocache.baseUrl}/search/grouped/facets`).

## Liste des cas de personnalisation (application web générique-hub)

Pour ajouter un cas, créez un nouvel élément de liste ci-dessous et liez-le à un nouveau fichier Markdown préfixé par 'case-'.

### [[Espagne|http://datos.gbif.es/generic-hub/]]

* Liste des personnalisations spécifiques dans le portail de données du GBIF Spain:

> 1.  Personnalisations générales :

> 2.  Personnalisation de Biocache-hub :

> 3.  Personnalisation de Collectory-hub :

### [[France|http://portail.gbif.fr/]]

* Liste des personnalisations spécifiques dans le portail de données du GBIF France :

> 1. Personnalisations générales :

> * Le menu est ajouté dans le fichier de disposition; layoutBody: appelle les autres dispositions pour afficher la page. De cette façon, les couches en-tête et pied de page sont les même sur tout le site.


> * ajouté 2 filtres à la page publique de collecte-hub: paléontologie et champignons.

> Voici les fichiers (sur le dossier de l'application web) où les modifications sont faites:

>https://github.com/gbiffrance/gbiffrance-collectory/blob/master/web-app/css/generic.css#L874 - Lines 874-882

>https://github.com/gbiffrance/gbiffrance-collectory/blob/master/web-app/js/map.js#L980 - Lines 980-982