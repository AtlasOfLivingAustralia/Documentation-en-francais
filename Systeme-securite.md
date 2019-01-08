Dans cette section, nous verrons les categories suivantes :
* Restrictions de page avec ala-auth-plugin
* Restrictions de page en utilisant Apache2 et htpasswd
* Restrictions de page en utilisant Ansible

## Les restrictions de page avec ala-auth-plugin ##

Voir la page suivante : https://github.com/AtlasOfLivingAustralia/ala-auth-plugin 

@Todo : étapes pour configurer le plugin

## Restrictions de page en utilisant Apache2 et htpasswd ##

D'abord, vous devez créer un fichier pour les utilisateurs et les mots de passe :

    $ sudo touch /usr/local/apache/password

Ensuite, créez un mot de passe pour l'utilisateur nom_utilisateur: 

    $ sudo htpasswd -c /usr/local/apache/password <nom_utilisateur>

Modifiez le fichier de configuration Apache2 (pour chaque page dont vous souhaitez restreindre l'accès) :

    <Location "/manage/gbifLoadCountry”>
    AuthType Basic
    AuthName "Authentication Required"
    AuthUserFile "/usr/local/apache/password"
        Require valid-user
        Order allow,deny
        Allow from all
    </Location>

## Restrictions de page en utilisant Ansible ##

@Todo : étapes ou lien vers une autre page wiki