# Docker Cheatsheet

### Docker Installation Instructions for Ubuntu (>= 14.04)

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

# Start the Docker service as root.
$ sudo su -
$ service docker start

# Exit root (ctrl + d)
```

### Useful Commands

#### `docker login [-u <your-username> -p <your-password>] [SERVER]`

Log into a Docker registry.

If no username nor password is specified, you will be prompted to enter them in your terminal.

If no server is specified, the default is defined by the daemon (usually [Docker Hub](https://hub.docker.com/)).

---

#### `docker build [-t <name:tag>] <path-to-dockerfile>`

Build a Docker image based on a Dockerfile.

If no `name:tag` is specified, you may add it later.

---

#### `docker run [-d/-it] [--name=<cont-name>] [-p <host-port:cont-port>] [--link=<other:alias> ] <img-name:tag> [cmd]`

Creates and runs a container out of the specified image.

If the image is not found locally, Docker will proceed to download it from a Docker registry.

If no tag is specified, then it defaults to `latest`.

Optional:

- `d`: detached mode.
- `it`: interactive mode.
- `name`: name given to the container.
- `p`: port mapping from host to container.
- `link`: links the container to another one. An entry is created under `/etc/hosts` with `alias`.
- `cmd`: the container's process or application to be executed. If the Dockerfile has an `ENTRYPOINT` specified, then `cmd` become its arguments. If it has (or not) a `CMD` specified, then these substitute it.

Other optional commands:

- `e`: set an environment variable (example: `-e TOKEN=example-token`).
- `cpu-shares`: proportion (out of 1024) of the CPU assigned to the container (example: `--cpu-shares=256`).
- `memory`: maximum amount of memory assigned to the container (example: `--memory=1g`).
- `v`: mounts the specified volume (example: `-v /example-volume`).
- `volumes-from`: mounts the volumes of the specified container into the current container (example: `--volumes-from=example-container`)
- `P`: maps all exposed ports of the container to random high-number ports of the host.
- `H`: point to another host (example: `-H tcp://<ip>:<port>`).

---

#### `docker stop <container>`

Stops the specified container.

---

#### `docker start <container>`

(Re)starts the specified stopped container.

---

#### `docker ps [-a]`

See the list of every running Docker container.

Optional:

- `a`: includes the stopped containers.

---

#### `docker rm [-f] [-v] <container>`

Destroys the specified container.

Optional:

- `f`: force.
- `v`: destroys the container's volumes too.

---

#### `docker-enter <container>`

Get shell access to a running container.

---

#### `docker exec [-it] <container> <command>`

Runs a command in the specified container.

Optional:

- `it`: runs the command in interactive mode.

---

#### `docker attach <container>`

Attaches the terminal to a running container's PID 1 process in order to view its ongoing output or to control it interactively.

You can detach from a container and leave it running using the `CTRL + p + q` key sequence, only if it was started in interactive mode.

---

#### `docker inspect <container/image>`

Inspects the specified container or image.

---

#### `docker logs [-f] <container>`

Shows the logs of the container.

Optional:

- `f`: follows the logs in real-time.

---

#### `docker top <container>`

See the top running processes of the specified container.

---

#### `docker pull [-a] <image-name:tag>`

Pulls the specified image from a Docker registry.

If no tag is specified, then it defaults to `latest`.

Optional:

- `a`: will pull all tags of the specified image.

---

#### `docker tag <image-id> <your-repository:tag>`

Tags the specified image.

---

#### `docker push <your-repository:tag>`

Pushes the specified image to its repository.

---

#### `docker images [name] [--tree]`

See the list of all local Docker images.

Optional:

- `name`: list all images with that name but different tags.
- `tree`: see the layer composition of each image shown.

---

#### `docker commit <container> <name>`

Builds an image from a container.

---

#### `docker rmi [-f] <image>`

Removes the specified image.

Optional:

- `f`: force.

---

#### `docker port <container>`

See how ports are mapped between the container and the host.

---

#### `docker stats $(docker ps | awk '{if(NR>1) print $NF}')`

See the memory usage of all running containers.

---

### Docker Compose Installation Instructions for Ubuntu (>= 14.04)

```sh
# Verify that you have pip3 installed.
# pip3: python package manager.
$ which pip3

# If pip3 is not installed, do so.
$ sudo apt-get -y install python3-pip

# Download and install docker-compose.
$ sudo pip3 install docker-compose
```

### Useful Commands

#### `docker-compose build`

Build every image specified in your `docker-compose.yml`.

---

#### `docker-compose pull`

Pull every image specified in your `docker-compose.yml`.

---

#### `docker-compose up [-d] <name>`

Create containers and run them in detached mode according to what is specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every container specified in your `docker-compose.yml`.

If there are images which have not been pulled/built, they will be pulled/built before creating their containers.

Optional:

- `d`: runs the containers in detached mode.

---

#### `docker-compose stop <name>`

Stops containers specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every container specified in your `docker-compose.yml`.

---

#### `docker-compose rm <name>`

Removes stopped containers specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every stopped container specified in your `docker-compose.yml`.

---

#### `docker-compose logs [--follow] <name>`

Shows the logs of the containers specified in your `docker-compose.yml`.

If no name is specified, the action will be applied to every container specified in your `docker-compose.yml`.

Optional:

- `follow`: follows the logs in real-time.

---

#### `docker-compose exec <name> <command>`

Runs a command in the specified container, present in your `docker-compose.yml`.

---
