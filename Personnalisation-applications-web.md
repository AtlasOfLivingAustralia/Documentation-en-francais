## Aperçu

Cette page couvrira le processus de création de style personnalisé pour l'application Web [`generic-hub`](https://github.com/AtlasOfLivingAustralia/generic-hub) Grails. Vous devriez avoir un bon niveau de connaissance en HTML et CSS ainsi qu'une compréhension de base de [Grails](http://grails.org) et [Bootstrap](http://getbootstrap.com/2.3.2). 

Liens utiles:
* [Documentation Grails] (http://grails.org/doc/2.3.x/guide/)
* [Bootstrap CSS framework] (http://getbootstrap.com/2.3.2/getting-started.html)

Les étapes de base sont:
* Forker le projet [`generic-hub`](https://github.com/AtlasOfLivingAustralia/generic-hub) et renommez-le pour refléter votre organisation
* Copiez le fichier de disposition `generic.gsp` dans un nouveau fichier (par exemple` votreOrganisation.gsp`)
* Modifier `Config.groovy` pour utiliser le nouveau fichier de mise en page
* Modifier le fichier `votreOrganisation.gsp`
* Créer des fichiers CSS personnalisés (avec des fichiers JS facultatifs)
* Ajouter un i18n personnalisé

## Fork et renommer

* Accédez à la page [`generic-hub`](https://github.com/AtlasOfLivingAustralia/generic-hub) et cliquez sur le bouton" Fork "dans le coin supérieur droit de la page. Sélectionnez le dépôt désiré et cliquez sur OK.
* Pour renommer le projet, cliquez sur l'icône "Paramètres" sur le côté droit et modifiez le nom du projet (par exemple `votreOrganisation-hub`).
* Cloner/archiver le projet sur votre PC local
* Déplacez le fichier que vous souhaitez modifier du plugin dans votre dossier grails-app

## Créer un fichier de disposition personnalisé
    cd votreOrganisation-hub/grails-app/views/layout
    cp genric.gsp votreOrganisation.gsp

## Modifier le fichier de configuration
Il existe deux mécanismes pour configurer l'application Web:
* fichier de configuration externe (fichier de propriétés) - emplacement par défaut : `/data/appName/conf/appName-config.properties`
* fichier de configuration interne de Grails sur : `/grails-app/conf/Config.groovy`

Les valeurs de configuration externes auront la priorité sur celles de Config.groovy. ala-demo utilise le fichier de configuration externe et c'est la manière recommandée de définir les valeurs de configuration.

Modifiez les variables suivantes (dans un fichier externe ou interne):

    skin.layout = 'generic'
    skin.orgNameLong = 'Generic Data Portal'
à

    skin.layout = 'votreOrganisation'
    skin.orgNameLong = 'le nom de votre organisation'

Vous pouvez pointer l'application vers une version locale de `biocache-service` en ajoutant/éditant la ligne:

    biocache.baseUrl = "http://votreOrganisation.org/biocache-service"


**Note :** si vous utilisez un fichier de propriétés externe, omettez les caractères de citation autour des chaînes de caractères.

## Modifier la disposition

Le fichier de disposition est un fichier **GSP**, qui est similaire au format de fichier Java **JSP**, avec quelques différences mineures (voir les documents Grails). Grails utilise la bibliothèque [SiteMesh](https://github.com/sitemesh/sitemesh2) pour fournir un composant HTML commun aux pages. Le hub générique (~ plugin biocache-hubs) utilise le framework CSS **Bootstrap**, il faut donc que certains éléments HTML soient présents pour que toutes les pages soient correctement affichées.

* détails à venir

## Ajouter des fichiers CSS et JS personnalisés

Grails fournit un mécanisme pour gérer les ressources statiques (CSS, JS et images), appelé le [Resources plugin](http://grails-plugins.github.io/grails-resources/), et nous vous recommandons d'utiliser cette fonctionnalité.

Les ressources sont déclarées dans le fichier `votreOrganisation-hub/grails-app/conf/ApplicationResources.groovy`, les fichiers associés étant gérés comme **modules**. Les modules peuvent dépendrent (`dependOn`) d'autres modules, ce qui permet de s'assurer que les fichiers dépendants apparaissent avant le fichier appelant (par exemple, un plugin jQuery" dépend de (`dependOn`) "jQuery et ainsi jQuery sera appliquer sur la page avant le plugin).

Le fichier de disposition contient une balise 'require' qui indique les modules requis pour toutes les pages utilisant ce fichier de mise en page particulier. Par exemple.

     <r:require modules="bootstrap2, hubCore" />

Pour ajouter un nouveau module, ajoutez simplement une référence au module:

    <r:require modules="bootstrap2, hubCore, votreOrganisation" />

puis ajoutez ce module à `ApplicationResources.groovy`:

    votreOrganisation{
        dependsOn 'bootstrap2', 'hubCore' //
        resource url: [dir:'css', file:'votreOrganisation.css']
        resource url: [dir:'js', file:'votreOrganisation.js']
    }

## Balise Grails ##

Format: `<g:tag_name option=”valeur_de_l_option” />`

La documentation du nom d'une balise : http://docs.grails.org/latest/ref/Tags/nom_de_la_balise.html

Voici une liste non-exhaustive des balises Grails avec les explications fournies :
***
>message

>Utilisez pour l'internationalisation, les propriétés du code seront dans le fichier message.properties:

>http://docs.grails.org/latest/ref/Tags/message.html
***
>link

>Ancre qui crée un lien HTML. Plus d'informations sur cette page:

>http://docs.grails.org/latest/ref/Tags/link.html
***
>if/else

>La balise logique if/else:

>http://docs.grails.org/latest/ref/Tags/if.html
>http://docs.grails.org/latest/ref/Tags/else.html
***
>actionSubmitImage

>Génère une action de soumission/d'envoi avec une entrée de type = "image":

>http://docs.grails.org/latest/ref/Tags/actionSubmitImage.html
***
>actionSubmit

>Ancre qui créera un bouton avec une action de soumission/d'envoi.
>Dans la partie action, vous pourrez changer l'action du bouton (ex: delete, sumbit, etc.) et vous pouvez avoir plusieurs actions de soumission en une seule forme:

>http://docs.grails.org/latest/ref/Tags/actionSubmit.html
***
>select

>Génère un champ select dans un formulaire:

>http://docs.grails.org/latest/ref/Tags/select.html
***
>checkbox

>Crée un champ de case à cocher dans un formulaire:

>http://docs.grails.org/latest/ref/Tags/checkBox.html
***
>hiddenField

>Ajoute un champ caché sur votre formulaire:

>http://docs.grails.org/latest/ref/Tags/hiddenField.html
***
>textArea

>Crée et remplit un champ de zone de texte sur un formulaire:

>http://docs.grails.org/latest/ref/Tags/textField.html
***
>form

>Ancre qui crée et gère un formulaire qui soumet/envoi à un contrôleur:

>http://docs.grails.org/latest/ref/Tags/form.html
***
>textField

>Crée et remplit un champ de texte d'un formulaire:

>http://docs.grails.org/latest/ref/Tags/textField.html
***

## Bootstrap 3: conseils ##

 Ajoutez le module bootstrap3 dans votre fichier `applicationRessource.groovy` en utilisant les commandes suivantes:

    bootstrap3 {
		resource url: [dir: 'bootstrap3/js', file: 'bootstrap.js', disposition: 'head']
		resource url: [dir: 'bootstrap3/css', file: 'bootstrap.css', attrs: [media: 'screen, projection, print']]
		resource url: [dir: 'bootstrap3/css', file: 'bootstrap-theme.css', attrs: [media: 'screen, projection, print']]
	}


 Télécharger Bootstrap3 : `http://getbootstrap.com/getting-started/#download`

 Ajouter ce dossier dans le dossier `web-app`

 Ajoutez bootstrap3 à votre balise `require module` dans votre fichier de mise en page

 Vous devez mettre à niveau JQuery 1.8 vers JQuery 1.11


 **Attention: Certaines fonctions sont dépréciées.**

 **Par exemple: .live() doit être changé en .on()**


 Dans le fichier de configuration, vous devez ajouter le dossier /bootstrap3/ pour avoir accès à l'image

        grails.resources.adhoc.patterns = ['/img/**', '/images/*', '/data/*', '/css/*', '/js/**', '/plugins/**', '/bootstrap3/css/**', '/bootstrap3/js/**', '/bootstrap3/fonts/**']

        grails.resources.adhoc.includes = ['/img/**', '/images/*', '/data/*', '/css/*', '/js/**', '/plugins/**', '/bootstrap3/css/**', '/bootstrap3/js/**', '/bootstrap3/fonts/**']


## Internationalisation personnalisée (i18n)

Voir la page sur wiki dédié : [[Internationalization (i18n)|Internationalization-(i18n)]]

## Exemples

Il existe un certain nombre d'applications Web personnalisées dans le dépôt [AtlasOfLivingAustralia](https://github.com/AtlasOfLivingAustralia?query=-hub) Github que vous pouvez consulter pour obtenir des idées/de l'aide pour l'habillage de votre copie de generic-hub :

* [ala-hub](https://github.com/AtlasOfLivingAustralia/ala-hub)
* [ozcam-hub](https://github.com/AtlasOfLivingAustralia/ozcam-hub)
* [obis-hub](https://github.com/AtlasOfLivingAustralia/obis-hub)
* [avh-hub](https://github.com/AtlasOfLivingAustralia/avh-hub)
* [appd-hub](https://github.com/AtlasOfLivingAustralia/appd-hub)