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

## Rajouter docker-compose
Installation de curl, docker compose et rajout des droits d'éxécution pour docker-compose
```shell
apt-get install -y curl
curl -L https://github.com/docker/compose/releases/download/1.19.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

## Docker volumes
Créer un volume:
```shell
docker volume create <monVolume-sansEspace>
```
Petit script pour avoir un volume et son path dans une variable:
```shell
VOLUME_PATH=$(docker volume inspect --format '{{ .Mountpoint }}' <monVolume-sansEspace>)
if [[ -z "$VOLUME_PATH" ]]; then
	docker volume create <monVolume-sansEspace>
	VOLUME_PATH=$(docker volume inspect --format '{{ .Mountpoint }}' <monVolume-sansEspace>)
	echo $VOLUME_PATH
fi
```