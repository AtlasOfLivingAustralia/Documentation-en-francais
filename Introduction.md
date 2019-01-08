# Internationalisation (i18n)

Grails utilise les standard Java pour [fournir l'internationalisation](http://grails.org/doc/latest/guide/i18n.html) - utilisant pour cela messages.properties et la [librairie tag g:message](http://grails.org/doc/latest/ref/Tags/message.html) à utiliser dans les pages GSP. La détection de la langue peut être déclenchée par le navigateur en fournissant une valeur **locale** ou en fournissant un paramètre de requête supplémentaire nommé **lang**. Exemple : ajouter `?lang=es` a une URL de requête.

Le client webapp (generic-hub par exemple) hérite de certaines propriétés d'internationalisation du plugin **biocache-hubs**, qui à son tour, hérite d'autres propriétés de **biocache-service** (via un [appel webservice](biocache.ala.org.au/ws/facets/i18n). Les propriétés i18n personnalisées peuvent être ajoutées/remplacées en incluant le fichier de messages approprié. Une liste complète des traductions des codes i18n (et anglais) peut être consultée sur : 

[http://localhost:8080/generic-hub/messages/i18n/messages_en-US.properties](http://localhost:8080/generic-hub/messages/i18n/messages_en-US.properties)

__Warning__ : Il y a des différences entre la structuration de phrase anglaise et celle française (même problème pour  la structuration de phrase espagnole)
Pour éviter ce problème, vous devez effectuer des modifications directement dans le code et créer de nouveaux termes dans messages.properties

## Fichier de propriétés i18n 

Les fichiers Grails i18n peuvent être trouvés dans :

    /grails-app/i18n

et suivez la convention de nommage Java de `messages_xx_XX.properties`. La communauté ALA est désireuse d'avoir des contributions pour des traductions non-anglaises, soit via des demandes d'extraction vers le projet biocache-hubs, soit en nous envoyant un fichier patch ou des fichiers de propriétés individuels.

Dans cette page vous avez les instructions pour faire la configuration correcte du plugin lang-selector dans votre module.

Maintenant, nous allons supposer que vous voulez installer et configurer ce plugin dans generic-hub.

1) Vous devez inclure dans la section des plugins de BuildConfig.grovy ce code:

    runtime ":lang-selector:0.3"

 2) Après cela, vous pouvez ajouter la balise à votre gsp. Par exemple, vous pouvez l'inclure dans les sections d'en-tête de /grails-app/views/laouts/generic.gsp pour voir le sélecteur de langue dans toutes les vues de votre module generic-hub. 

    <ul class="nav pull-right">
       <li class="dropdown">
           <a class="dropdown-toggle" data-toggle="dropdown" href="#">Language<b class="caret"></b></a>
           <ul class="dropdown-menu">
               <li><langs:selector langs="ca"/></li>
               <li><langs:selector langs="en"/></li>
               <li><langs:selector langs="es"/></li>
           </ul>
       </li>
    </ul>

3) Vous pouvez éventuellement ajouter cette propriété à /grails-app/conf/Config.groovy pour indiquer au plugin quel drapeau est associé à quelle langue:

    com.mfelix.grails.plugins.langSelector.lang.flags = 
                                                    ["es":"es",
                                                     "en":"gb",
                                                     "fr":"fr",
                                                     "da":"dk",
                                                     "de":"de",
                                                     "it":"it",
                                                     "ja":"jp",
                                                     "nl":"nl",
                                                     "ru":"ru",
                                                     "th":"th",
                                                     "zh":"cn",
                                                     "pt":"pt",
                                                     "ca":"catalonia"]
   
Vous pouvez également le faire dans le module collectory-hub.

Maintenant, nous allons supposer que vous ne voulez pas avoir de drapeaux, peut-être pour plus d'accessibilité ou pour d'autres raisons. Dans ce cas, vous devez modifier le code de ce plugin. Pour ce faire, vous devez télécharger le plugin, en l'appelant localement dans /grails-app/BuildConfig.groovy, et vous devez modifier /lang-selector-0.3/grails-app/views/langSelector/_selector.gsp :

BuildConfig.groovy:

    grails.plugin.location.'lang-selector' = "plugins/lang-selector-0.3"


_selector.gsp:

    <div id="lang_selector">
    <span style="color:white"><g:message code="1" default="|"/></span>
	<g:each in="${flags.keySet().sort() }" var="lang">
		<a href="${ uri + lang }" title="${message(code:'tittle.lang_link')}">
			<span class="lang_flag ${ lang==selected.toString()? selected_class : not_selected_class }" style="margin-left: 14px;">
			<g:if test="${flags[lang] == 'catalonia'}">
			        <g:message code="1" default="Català"/>
			</g:if>
			<g:if test="${flags[lang] == 'gb'}">
			        <g:message code="1" default="English"/>
			</g:if>

			<g:if test="${flags[lang] == 'es'}">
			        <g:message code="1" default="Español"/>
			</g:if>
			<%--<img alt="" src="${resource(plugin:'langSelector',dir:'images/flags/png',file:flags[lang]+'.png') }" border="0">--%>
			</span>
		</a>
		<span style="color:white"><g:message code="1" default="|"/></span>
	</g:each>
</div>