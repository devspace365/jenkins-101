# jenkins-101
## Easy jenkins installation on docker


# Installation
## Pull the latest jenkins built from the docker hub
```
docker pull jenkins/jenkins

```

## Create the network 'jenkins'
```
docker network create jenkins
```

## Run the Container
### MacOS / Linux
```
docker run --name jenkins-server --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  jenkins/jenkins
```

### Windows
```
docker run --name jenkins-server --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 jenkins/jenkins
```


## Get the Password
```
docker exec jenkins-server cat /var/jenkins_home/secrets/initialAdminPassword
```

## Connect to Jenkins
```
https://localhost:8080/
```

## Installation Reference:
https://www.jenkins.io/doc/book/installing/docker/
