# Brunehilde pipeline


## Description
Ceci est la description du pipeline jenkins pour Brunehilde et ses tests d'intégration
Les sources de Brunehilde sont [ici](https://github.com/ildrasa/BrunehildePythonApp).
Les sources des tests d'intégration d'Alice sont [ici](https://github.com/ildrasa/BrunehildeIntegrationTests).

Le pipeline va :
- créer une image docker avec python et les librairies pour le service et la stocke dans le docker registry local.
- récupérer l'image docker depuis le registry docker
- démarrer un container docker à partir de l'image sur le port 5002 (via docker-compose).
- démarrer un container docker avec redis (un programme qui garde des valeurs) pour simuler une base de données (via docker-compose).
- éxécuter le script de test d'intégration.
- arrêter les containers docker (via docker-compose).

## Remarques:
- Brunehilde est codé en python, comme il s'agit d'un programme de script le code n'est pas compilé; il est juste copié dans l'image docker.
- La particularité de ce build est qu'il lance plusieurs sontainers docker via la commande docker compose dans le but de monter un environnement de test complet qui n'est actif que durant les tests d'intégration. Le même système peut s'utiliser pour mettre un place un environnement de développement sur un poste développeur. Le docker registry peut alors servir à partager les images entre développeurs.

## Configuration

### General
![onglet general](https://github.com/ildrasa/markdown-notes/blob/master/images/brunehilde-pipeline/brunehilde-pipeline_general)

### Déclenchement du build
Le build est déclenché tous les soir à minuit.
![onglet déclenchement du build](https://github.com/ildrasa/markdown-notes/blob/master/images/brunehilde-pipeline/brunehilde-pipeline_declenchement)

### Pipeline
Le fichier de description du pipeline est versionné sur un repository GitHub spécifique car il n'est pas spécifique à un unique projet.
Le fichier est disponible [ici](https://github.com/ildrasa/JenkinsPipelines/blob/master/brunehilde-jenkinsfile)
![onglet pipeline](https://github.com/ildrasa/markdown-notes/blob/master/images/brunehilde-pipeline/brunehilde-pipeline_pipeline)
