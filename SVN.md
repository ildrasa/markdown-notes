# SVN

## Installation
```shell
apt-get update
apt-get install subversion
```
## Mise en place d'un repository
1. Création d'un répertoire de dépôt *repository* dans /var/svn
```shell
mkdir /var/svn
chmod 755 /var/svn
chown user /var/svn
svnadmin create /var/svn/repository
```

2. Configuration des accès au repository
Dans /var/svn/repository/conf
  
  * Fichier passwd
  
  ```
  [users]
  user=user
  ```
  
  * Fichier authz
  
  ```
  # pour tout le repository
  [/]
  # n'importe qui n'a aucun droit
  * = 
  # le user *user* a les droits read et write
  user = rw
  ```

  * Fichier svnserve.conf
  
  ```
  [general]
  # user non logué n'a aucun droit
  anon-access = none
  # user authentifié a les droits write
  auth-access = write
  # definition de la gestion des password pour le repository: ici le fichier passwd précédemment modifié
  password-db = passwd
  # realm le repository *repository*
  realm = repository
  ```
  
  3. Démarrage du serveur SVN
  
  ```shell
  svnserve -d -r /var/svn
  ```