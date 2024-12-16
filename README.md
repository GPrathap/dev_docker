# Development docker container 

## Prerequisites

* docker, docker compose, nvidia-docker container toolbox 
* (Optional) WSLg
* If you have GPU uncomment the following in the docker-compose.yml
    ```deploy:
      resources:
        reservations:
           devices:
             - capabilities: [gpu]
             -  count: all
## Getting started

```bash
git clone git@github.com:GPrathap/dev_docker.git
cd dev_docker_docker
git checkout main
docker-compose build --no-cache
docker-compose up -d
docker-compose exec dev_core bash
```

### docker-compose

```bash
docker-compose stop
```

```bash
docker-compose down
```

```bash
docker-compose exec --user root dev_core bash
```

### Inside the docker container 

#### set up github ssh key 
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent 

