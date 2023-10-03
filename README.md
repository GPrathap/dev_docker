# Dogtooth docker container 

## Prerequisites

* docker, docker compose, nvidia-docker container toolbox 
* (Optional) WSLg

## Getting started

```bash
git clone git@github.com:GPrathap/dogtooth_bot.git
cd git@github.com:GPrathap/dogtooth_bot.git
docker-compose build --no-cache
docker-compose up -d
docker-compose exec dogtooth_core bash
```

### docker-compose

```bash
docker-compose stop
```

```bash
docker-compose down
```

```bash
docker-compose exec --user root dogtooth_core bash
```

### Inside the docker container 
#### set up github ssh key 
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent 

#### set up the environment 
    mkdir -p /home/developer/dogtooth_ws/src 
    cd /home/developer/dogtooth_ws/src 
    git clone git@github.com:GPrathap/aoc_gazebo_dogtooth.git 
    mv aoc_gazebo_dogtooth Dogtooth
    cd ../
    colcon build 
    source ~/.bashrc 

