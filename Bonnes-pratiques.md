## Architecture d'une page du wiki

Une nouvelle page doit respecter les règles suivantes :

- L'en-tête 1 n'est pas utilisé, vous devez commencer par l'en-tête 2 (##)

- Le mode d'édition doit être dans "Markdown"

- Le wiki est trié par thèmes donc avant de créer ou éditer une page, assurez-vous que les informations que vous souhaitez ajouter sont dans la bonne section

- Si une documentation spécifique d'un aspect du projet ALA existe déjà sur Github, il suffit de pointer cette documentation spécifique avec un lien dans la bonne page de la section wiki (voir [Image service](https://github.com/AtlasOfLivingAustralia/documentation/wiki/Image-service) ou [ALA4R](https://github.com/AtlasOfLivingAustralia/documentation/wiki/ALA4R) par exemple).

- Sur vos pages, si il y a des instuctions, incluez au moins une capture d'écran pour chaque partie.

- Lorsqu'il y a trop d'informations sur une page, créez une table des matières de la page.
Une table des matières est seulement composée d'un lien vers les parties différente de la page.

- Si vous souhaitez réorganiser le wiki en déplaçant des pages entre les sections ou pour ajouter/supprimer une section, veuillez d'abord contacter le responsable de la documentation (Caviere Fabien, GBIF France: caviere@gbif.fr)

Si vous avez des questions sur le wiki, n'hésitez pas à contacter le responsable de la documentation

## Règles d'édition
	
- Toujours spécifier un "Edit Message". De cette façon, d'autres personnes comprendront plus facilement vos modifications
	
## Règles de formage de texte

- Préfixé le titre de vos parties avec '## '
	
- Préfixé le titre de vos sections avec '### '
	
- Préfixé le titre de vos paragraphes avec '#### '
	
- Ne pas oublier d'ajouter 4 espaces ou une tabulation avant toute ligne de code

- Lorsque vous voulez afficher plusieurs solutions, utilisez le modèle suivant: :
	
	***

	### SOLUTION 1 :
 
	>texte

	>texte

	***
	
	### SOLUTION 2 :
 
	>texte

	>texte

	***

- Pour la page de la section "Portails en production", respecter la structure suivante :
 1) une introduction : mettre des informations comme
   + les métadonnées sur le développement du portail (nombre de développeurs et temps accordé au portail par exemple)
   + la structure qui héberge le portail
   + l'architecture du portail
   + qui, quoi, comment, quand et où
   + des stats
   + spécification
 2) un diagramme
 3) les principaux points locaux à ce portail