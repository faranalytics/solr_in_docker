# Solr in Docker
A Solr in Docker implementation.

## Introduction

This repository contains notes for running Solr in Docker.

## Solr In Docker on Fedora

### Install the Docker software platform.

Reference: [Install Docker Engine on Fedora](https://docs.docker.com/engine/install/fedora/)

### Create a `docker-compose.yml` file.

Reference: [Solr in Docker](https://solr.apache.org/guide/solr/latest/deployment-guide/solr-in-docker.html)

```yml
version: "3"
services:
  solr:
    image: solr:8.11.4
    ports:
      - "127.0.0.1:8983:8983"
    volumes:
      - data:/var/solr
    command:
      - solr-precreate
      - gettingstarted
volumes:
  data:
```
### Use Docker Compose to run a Solr server.

```bash
sudo docker compose up -d
```

## Docker Volumes

### List Docker volumes.
```bash
sudo ls -la /var/lib/docker/volumes
```

### List Solr cores.
```bash
sudo ls -la /var/lib/docker/volumes/solr_in_docker_data/_data/data
```

### Copy your core into the data directory.
```bash
sudo rsync -r --progress /home/null/Desktop/your-core /var/lib/docker/volumes/solr_in_docker_data/_data/data
```

### Change ownership of the core.
```bash
sudo chown -R 8983:8983 /var/lib/docker/volumes/solr_in_docker_data/_data/data/your-core
```

## The Solr UI

### Access the Solr UI in a browser.
The `docker-compose.yml` mapped `127.0.0.1:8983` on the host to the container port.  You can access the Solr server's UI using the mapped IP and port.

`http://127.0.0.1:8983/solr/#/`

## Manage Docker

### Start docker.
```bash
sudo systemctl start docker
```

### List all images.
```bash
sudo docker image ls -a
```

### List all containers.
```bash
sudo docker container ls -a
```

### Restart a container.
```bash
sudo docker container restart '<CONTAINER ID>'
```

### Remove all containers and images.
```bash
sudo docker container rm -f $(sudo docker container ls -qa); sudo docker image rm -f $(sudo docker image ls -qa)
```

### Remove all containers, images, and volumes.
```bash
sudo docker container rm -f $(sudo docker container ls -qa); sudo docker image rm -f $(sudo docker image ls -qa); sudo docker volume rm -f $(sudo docker volume ls)
```