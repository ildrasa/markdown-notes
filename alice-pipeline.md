# Alice pipeline


## Description
Ceci est la description du pipeline jenkins pour Alice et ses tests d'intégration
Les sources d'Alice sont [ici](https://github.com/ildrasa/AliceRestApi).
Les sources des tests d'intégration d'Alice sont [ici](https://github.com/ildrasa/AliceIntegrationTests).

Le pipeline va :
- builder le service Alice en un war.
- passer les tests unitaires.
- créer une image docker avec un tomcat ayant le webservice installé et la stocke dans le docker registry local.
- récupérer l'image docker depuis le registry docker
- démarrer un container docker à partir de l'image sur le port 5001
- builder les tests d'intégration.
- passer les tests.
- arrêter le container docker.
- détruire le container docker.

## Remarques:
- Dans le projet alice, un test échoue; l'objectif est de voir que si test ne passe pas la pipeline entière est instable(contrairement aux CI habituelles pas besoin de faire un findtext en post build pour passer en instable).
- Un certain nombre de plugins ne sont pas disponibles mais on est plus limité par les différentes étapes par rapport aux CI classiques car les stages sont non typés.


## Configuration

### General
![onglet general](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-pipeline/alice-pipeline_general)

### Déclenchement du build
Le build est déclenché tous les soir à minuit.
![onglet déclenchement du build](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-pipeline/alice-pipeline_declenchement)

### Pipeline
Le fichier de description du pipeline est versionné sur un repository GitHub spécifique car il n'est pas spécifique à un unique projet.
Le fichier est disponible [ici](https://github.com/ildrasa/JenkinsPipelines/blob/master/alice-jenkinsfile)
![onglet pipeline](https://github.com/ildrasa/markdown-notes/blob/master/images/alice-pipeline/alice-pipeline_pipeline)
