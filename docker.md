# docker

## Installation
```shell
apt-get update
apt-get install -y apt-transport-https ca-certificates wget software-properties-common
wget htttps://download.docker.com/linux/debian/gpg | apt-key add gpg
echo "deb [arch=amd64] htpps://download.docker.com/linux/debian $(lsb_release -cs stable" | tee -a /etc/apt/sources.list.d/docker.list
apt-get update
apt-get install -y docker-ce
```
## Démarrage de docker
```shell
systemctl start docker
```

## Rajouter des user pour utiliser docker
Rajout des users jenkins et user.
```shell
groupadd docker
usermod -aG docker user jenkins
```

## Démarrer docker registry
Avec jenkins on va utiliser un registry pour stocker les images des machines utilisées pour les tests d'intégration d'un projet.
```shell
docker run -d -p 5000:5000 --restart=always --name registry registry:2
```