# SVN

## Installation
```shell
wget-q -O - http://pkg.jenkins-ci.org/debian-stable/jenkins-ci.org.key | apt-key add
echo "deb http://pkg.jenkins-ci.org/debian-stable binary/" > /etc/apt/sources.list.d/jenkins.list
apt-get update
apt-get install jenkins
```

## Configuration
1. Changer le port d'écoute de jenkins (default 8080) dans /etc/default/jenkins
```
HTTP_PORT = 8081
```

2. Récupérer le mod de passe admin initial dans /var/lib/jenkins/secrets/initialAdminPassword.

3. Changer le mot de passe sur <url install de jenkins>:8081

4. Rajouter les plugins suivants:
- Config File Provider Plugin
- Deploy to container Plugin
- Green Balls
- Hudson Post build task
- Maven Release Plug-in Plug-in
- ruby-runtime
- TextFinder plugin
- GitHub plugin

5. Rajouter le fichier de configuration MySettings pour référencer les serveurs pour maven (Administrer Jenkins > Configuration files)
```xml
<?xml version="1.0"?>

<settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://maven.apache.org/SETTINGS/1.0.0">

<servers>
	<server>
		<id>tomcat_debian_vm</id>
		<username>user</username>
		<password>user</password>
	</server>
  
	<server>
		<id>nexus</id>
		<username>admin</username>
		<password>admin123</password>
	</server>
</servers>

</settings>
```



