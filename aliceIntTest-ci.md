# AliceIntegrationTests-CI

## Description
Ceci est la description de la CI qui effectue les tests d'intégration pour le [webservice rest Alice](https://github.com/ildrasa/AliceRestApi).
Les sources des tests d'intégration d'Alice sont [ici](https://github.com/ildrasa/AliceIntegrationTests).
La CI va :
- récupérer une image docker depuis le registry docker
- démarrer un container docker à partir de l'image sur le port 5001
- builder les tests d'intégration.
- passer les tests.
- arrêter le container docker.
- détruire le container docker.

## Remarques
Si l'on ne détruit pas le container docker on ne peut pas le re-créer avec le même nom. On essaie de recycler les noms de container et de nettoyer les container inutiles après leur utilisation.

## Configuration

### General
![onglet general](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_general)

### Gestion des sources
La source est le repository GitHub des tests d'intégration d'Alice
![onglet gestion des sources](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_sources)

### Déclenchement du build
Le build est déclenché si on a commité sur le repo GitHub dans les 5 dernières minutes ou si la CI *alice* s'est déroulé, même si elle est instable car on veut une liste exhaustive des problèmes sur Alice. 
![onglet déclenchement du build](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_declenchement)

### Environnement de build
Rien de particulier

### Build
1. Le build comporte un script shell pour la récupération de l'image docker générée par la CI de build d'Alice et le lancement du container basé sur celle-ci.
![build shell docker](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_docker)

2. Le build comporte une invocation maven.
Remarques: 
  - L'option Dmaven.test.failure.ignore=true sert à ne pas arrêter la CI si les tests ne passent pas. Ce qui empêcherai l'arrêt et le nettoyage du container docker et empêcherai le bon dérouloulement des prochaine itération de la CI.
![build maven](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_maven)

### Actions post build
1. Utilisation d'un script shell pour l'arrêt et la suppression du container docker faisant tourner Alice pour les tests d'intégration.
![tomcat deploy](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_dockerStop)

2. On regarde le contenu de la console de sortie pour passer le build en instable (jaune) si les tests on échoués. Pour cela on cherche la ligne `[ERROR] There are test failures.`
![build jenkins text finder](https://github.com/ildrasa/markdown-notes/blob/master/images/aliceIntTest-ci/aliceIntTest-ci_textFinder)



