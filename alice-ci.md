# Alice-CI

## Description
Ceci est la description de la CI qui gère le webservice rest Alice.
Les sources d'Alice sont [ici](https://github.com/ildrasa/AliceRestApi).
La CI va :
- builder le service Alice en un war.
- passer les tests unitaires.
- déployer le war du service sur nexus.
- déployer le war sur un serveur tomcat de démonstration.
- créer une image docker avec un tomcat ayant le webservice installé et la stocke dans le docker registry local.
- lancer la CI des tests d'intégration d'Alice.

## Configuration

### General
![onglet general](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_general)

### Gestion des sources
La source est le repository GitHub d'Alice
![onglet gestion des sources](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_sources)

### Déclenchement du build
Le build est déclenché si on a commité sur le repo GitHub dans les 5 dernières minutes.
![onglet déclenchement du build](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_declenchement)

### Environnement de build
Rien de particulier

### Build
1. Le build comporte une invocation maven.
Remarques: 
  - Comme le plugin nexus pour jenkins ne fonctionne pas avec nexus 3.x c'est la tâche deploy de maven qui envoie le war généré sur le nexus.
  - L'option Dmaven.test.failure.ignore=true sert à ne pas arrêter la CI si les tests ne passent pas. Ce qui mettrai la CI broken, ce qui n'est pas le cas, l'appli est *fonctionnelle* mais instable... ou le test est juste incorrect, ça s'est déjà vu.
![build maven](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_maven)

2. Le build comporte un script shell pour l'image docker qui servira aux tests d'intégration.
![build shell docker](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_docker)

### Actions post build
1. Déploiement du war sur le serveur tomcat de démonstration
![tomcat deploy](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_tomcat)

2. On regarde le contenu de la console de sortie pour passer le build en instable (jaune) si les tests on échoués. Pour cela on cherche la ligne `[ERROR There are test failures.`
![build jenkins text finder](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_textFinder)

3. On lance la CI de tests d'intégration d'Alice. On la lance même si le build est instable (un test unitaire raté n'empêche pas de tester l'intégration avec les autres composants). Différence entre le métier interne et l'interraction avec l'environnement.
![déclenchement CI de tests d'intégration](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-ci_lancementSuivant)





