# Docker-Cheatsheet

## Instalation instructions for Ubuntu (>= 14.04)
```sh
# Verify that you have wget installed.
# wget: computer program that retrieves content from web servers.
$ which wget

# If wget is not installed, do so.
$ sudo apt-get update
$ sudo apt-get install wget

# Download and install Docker.
$ wget -qO- https://get.docker.com/ | sh

# Create a Docker group and add your user.
$ sudo usermod -aG docker $(whoami)

# Verify that yoy have pip3 installed.
# pip3: python package manager.
$ which pip3

# If pip3 is not installed, do so.
$ sudo apt-get -y install python3-pip

# Download and install docker-compose.
$ sudo pip3 install docker-compose

# Start the Docker service as root.
$ sudo su -
$ service docker start

# Exit root (ctrl + d)
```

## Useful commands

#### `docker login -u <your-username> -p <your-password> [SERVER]`

Log into a Docker registry.

If no username nor password is specified, you will be prompted to enter them
in your terminal

If no server is specified, the default is defined by the daemon (usually [Docker Hub](https://hub.docker.com/)).

---

#### `docker build -t <your-repository:tag> <path-to-dockerfile>`

Build a Docker image based on a Dockerfile.

If no repository:tag is specified, you may add it later.

---

#### `docker tag <id> <your-repository:tag>`

Tags the specified image.

---

#### `docker push <your-repository:tag>`

Push the specified image to its repository.

---

#### `docker images`

See the list of all Docker images in your machine.

---

#### `docker rmi -f <id>`

Remove images which are not being used.

---

#### `docker ps -a`

See the list of every Docker containers (running and not running).

---

#### `docker rm -f <id>`

Remove containers which are not running.

---

#### `docker stats $(docker ps | awk '{if(NR>1) print $NF}')`

See the memory usage of all running containers.

---

#### `docker-compose build`

Build every image specified in your `docker-compose.yml`.

---

#### `docker-compose pull`

Pull every image specified in your `docker-compose.yml`.

---

#### `docker-compose up -d <name>`

Create containers and run them in detached mode according to what is specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every container specified in your `docker-compose.yml`.

If there are images which have not been pulled/built, they will be pulled/built before creating their containers.

---

#### `docker-compose stop <name>`

Stop containers specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every container specified in your `docker-compose.yml`.

---

#### `docker-compose rm <name>`

Remove stopped containers specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every stopped container specified in your `docker-compose.yml`.

---

#### `docker-compose logs <name>`

See the logs of the containers specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every container specified in your `docker-compose.yml`.

---

#### `docker-compose run <name> <command>`

Runs a command in the specified container, present in your `docker-compose.yml`.

---
