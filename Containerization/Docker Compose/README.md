<h1 align="center">
  <img src="./assets/docker-compose.png" alt="icon" height="150"></img>
  <br>
  <b>Docker compose Cheatsheet</b>
</h1>

<p align="center">Quick reference for defining and managing multi-container applications with ease and simplicity.</p>

<!-- Badges -->
<p align="center">
  <a href="https://github.com/quanblue/tech-cheatsheets/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/quanblue/tech-cheatsheets" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/quanblue/tech-cheatsheets" alt="last update" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/network/members">
    <img src="https://img.shields.io/github/forks/quanblue/tech-cheatsheets" alt="forks" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/stargazers">
    <img src="https://img.shields.io/github/stars/quanblue/tech-cheatsheets" alt="stars" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/issues/">
    <img src="https://img.shields.io/github/issues/quanblue/tech-cheatsheets" alt="open issues" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/quanblue/tech-cheatsheets.svg" alt="license" />
  </a>
</p>

<p align="center">
  <b>
    <a href="https://github.com/quanblue/tech-cheatsheets">Docker cheatsheet</a> •
    <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/Docker%20Compose%20cheatsheet/README.md">Docker Compose cheatsheet</a> •
    <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/Docker%20Swarm%20cheatsheet/README.md">Docker Swarm cheatsheet</a>
  </b>
</p>

<details open>
<summary><b>:open_book: Table of Contents</b></summary>

-  [CLI Cheatsheet](#clipboard-cli-cheatsheet)
   -  [Build Commands](#build-commands)
      -  [Config](#config)
      -  [Build](#build)
   -  [Inspect Commands](#inspect-commands)
      -  [PS](#ps)
      -  [Images](#images)
      -  [Log](#log)
      -  [Port](#port)
   -  [Interact Commands](#interact-commands)
      -  [Pull](#pull)
      -  [Push](#push)
   -  [Control Commands](#control-commands)
      -  [Start](#start)
      -  [Restart](#restart)
      -  [Pause](#pause)
      -  [Unpause](#unpause)
      -  [Stop](#stop)
      -  [Kill](#kill)
      -  [Up](#up)
      -  [Run](#run)
      -  [Scale](#scale)
   -  [Remove](#remove)
   -  [Down](#down)
   -  [Exec](#exec)
-  [Docker Compose File Cheatsheet](#clipboard-docker-compose-file-cheatsheet)
   -  [Example](#example)
   -  [Building](#building)
   -  [Port](#port-1)
   -  [Commands](#commands)
   -  [Environment Variables](#environment-variables)
   -  [Dependencies](#dependencies)
   -  [Other Options](#other-options)
   -  [Labels](#labels)
   -  [DNS Servers](#dns-servers)
   -  [Devices](#devices)
   -  [External Links](#external-links)
   -  [Healthcheck](#healthcheck)
   -  [Hosts](#hosts)
   -  [Network](#network)
   -  [External Network](#external-network)
   -  [Volume](#volume)
   -  [User](#user)
-  [Practice Lab](#memo-practice-lab)
-  [Credits](#sparkles-credits)
</details>

# :clipboard: CLI Cheatsheet

> **To view detail:** `docker-compose [COMMAND] --help`

## Build Commands

### Config

The docker-compose `config` Validate the docker-compose file and view the compose file.  
syntax: `docker-compose config [options]`

### Build

The docker-compose `build` used to create a new image using the instructions in the Dockerfile.  
syntax: `docker-compose build [options] [SERVICE...]`

## Inspect Commands

### PS

The docker-compose `ps` command list out the containers with details like status, Port mapping etc, which is declared in docker-compose file.  
syntax: `docker-compose ps [options] [SERVICE...]`

### Images

The docker-compose `images` command help to listout images used/created by the containers.  
syntax: `docker-compose images [options] [SERVICE...]`

### Log

The docker-compose `logs` command help to see the service logs.  
syntax: `docker-compose logs [options] [SERVICE...]`

### Port

The docker-compose port command print the public/network facing port for a service.  
syntax: `docker-compose port [options] SERVICE PRIVATE_PORT`

## Interact Commands

### Pull

The docker-compose `pull` command pull down the images which is specified under each service of docker-compose file from the docker hub.

syntax: `docker-compose pull [options] [SERVICE...]`

### Push

**docker-compose**

The docker-compose `push` command help you tou push the service images to Docker Hub or your own private Docker registry.
syntax: `docker-compose push [options] [SERVICE...]`

> **Note:** you must name your images with your docker hub username before pushing, this is syntax: `[DOCKER_HUB_USERNAME]/[IMAGE]:[TAG]`

**docker**

If you want using docker to push your command, you must 3 step bellow:

-  Tagging image: you must tag your images with docker hub username before pushing:  
    `docker tag [IMAGE] [DOCKER_HUB_USERNAME]/[IMAGE]:[TAG]`
-  Login to docker hub: `docker login`
-  Pushing: `docker push [DOCKER_HUB_USERNAME]/[IMAGE]:[TAG]`

## Control Commands

### Start

The docker-compose `start` command help us to start containers of a service.  
syntax: `docker-compose start [SERVICE...]`

### Restart

The docker-compose `restart` command help us to restart the services.  
syntax: `docker-compose restart [options] [SERVICE...]`

### Pause

The docker-compose `pause` command help to pause services.  
syntax: `docker-compose pause [SERVICE...]`

### Unpause

The docker-compose `unpause` command help to Unpauses paused containers of a service.  
syntax: `docker-compose unpause [SERVICE...]`

### Stop

The docker-compose `stop` command help us to stop containers in service.  
syntax: `docker-compose stop [SERVICE...]`

> **Note:** different between `Kill` and `Stop` (See detail [here](https://www.baeldung.com/ops/docker-stop-vs-kill))
>
> -  **The docker stop command stops the container gracefully and provides a `safe way out`**. If a docker stop command fails to terminate a process within the specified timeout, the Docker issues a kill command implicitly and immediately
> -  **The docker kill command terminates the entry point process abruptly. The docker kill command causes an `unsafe exit`**. In some cases, the docker container runs with the volume mounted with the host. This might result in damage to the file system if there are still pending changes in memory when the main process stops.

### Kill

The docker-compose `kill` command force stop service containers.  
syntax: `docker-compose kill [options] [SERVICE...]`

### Up

The docker-compose `up` command help you to bring up a multi-container application, which you have described in your docker-compose file.  
syntax: `docker-compose up [options] [SERVICE...]`

### Run

Run command help to run a one-time command against a service. docker-compose run will start a new container to execute the command, not executed against a running container.  
Syntax: `docker-compose run [options] SERVICE [COMMAND] [ARGS...]`

### Scale

The docker-compose `scale` sets the number of containers to run for a service.  
syntax: `docker-compose scale [SERVICE=NUMBER_OF_SERVICE...]`

> **Note:**
>
> -  **Do not name the container** to avoid errors: "Docker requires each container to have a unique name"
> -  The scale command is deprecated, instead Use the up command with the –scale flag.  
>    `docker-compose up --scale <service name> = <no of instances>`

## Remove

The docker-compose `rm` command helps to Remove stopped containers.  
syntax: `docker-compose rm [options] [SERVICE...]`

> **Note:** You must stop container before remove it

## Down

The docker-compose `down` command helps to Stop and remove containers, networks, images, and volumes (`down` = `stop` + `remove`)  
syntax: `docker-compose down [options]`

## Exec

Docker exec is used to run commands in a running container, similarly docker-compose exec runs commands in your services.  
syntax: `docker-compose exec [options] SERVICE COMMAND [ARGS...]`

# :clipboard: Docker Compose File Cheatsheet

> Refer [this](https://docs.docker.com/compose/compose-file/build/) for configuring your compose file.

## Example

```yml
# docker-compose.yml
version: "3"

services:
   web:
      build: .
      image: web-client
      depends_on:
         - server
      ports:
         - "8080:8080"
   server:
      image: akshitgrover/helloworld
      volumes:
         - "/app" # Anonymous volume
         - "data:/data" # Named volume
         - "mydata:/data" # External volume

volumes:
   data:
   mydata:
      external: true
```

## Building

```yml
# build from Dockerfile
build: .
args: # Add build arguments
   APP_HOME: app
```

```yml
# build from custom Dockerfile
build:
   context: ./dir
   dockerfile: Dockerfile.dev
```

```yml
# build from image
image: ubuntu
image: ubuntu:14.04
image: tutum/influxdb
image: example-registry:4000/postgresql
image: a4bc65fd
```

## Port

```yml
ports:
   # host:container
   - "3000" # random host:container(3000)
   - "8000:80" # host(8000):container(80)
   - "3001-3005" # random host:container range(3001-3005)
   - "9090-9091:8080-8081" # host range(9090-9091):container range(8080-8081)
   - "127.0.0.1:8002:8003" # host(8002):container(8003) and bind to 127.0.0.1
   - "6060:6060/udp" # host(6060):container(6060) restricted to UDP protocol
```

```yml
# expose ports to linked services (not to host)
expose: ["3000"]
```

## Commands

```yml
# command to execute
command: bundle exec thin -p 3000
command: [bundle, exec, thin, -p, 3000]
```

```yml
# override the entrypoint
entrypoint: /app/start.sh
entrypoint: [php, -d, vendor/bin/phpunit]
```

## Environment Variables

```yml
# environment vars
environment:
   RACK_ENV: development
```

```yml
# environment vars from file
env_file: .env
env_file: [.env, .development.env]
```

## Dependencies

```yml
# makes the `db` service available as the hostname `database`
# (implies depends_on)
links:
   - db:database
   - redis
```

```yml
# make sure `db` is alive before starting
depends_on:
   - db
```

```yml
# make sure `db` is healty before starting
# and db-init completed without failure
depends_on:
   db:
      condition: service_healthy
   db-init:
      condition: service_completed_successfully
```

## Other Options

```yml
# make this service extend another
extends:
   file: common.yml # optional
   service: webapp
```

```yml
volumes:
   - /var/lib/mysql
   - ./_data:/var/lib/mysql
```

```yml
# automatically restart container
restart: unless-stopped
# always, on-failure, no (default)
```

## Labels

```yml
services:
web:
   labels:
      com.example.description: "Accounting web app"
```

## DNS Servers

```yml
services:
web:
 dns: 8.8.8.8
 dns:
   - 8.8.8.8
   - 8.8.4.4
```

## Devices

```yml
services:
   web:
      devices:
         - "/dev/ttyUSB0:/dev/ttyUSB0"
```

## External Links

```yml
services:
   web:
      external_links:
         - redis_1
         - project_db_1:mysql
```

## Healthcheck

```yml
# declare service healthy when `test` command succeed
healthcheck:
   test: ["CMD", "curl", "-f", "http://localhost"]
   interval: 1m30s
   timeout: 10s
   retries: 3
   start_period: 40s
```

## Hosts

```yml
services:
   web:
      extra_hosts:
         - "somehost:192.168.1.100"
```

## Network

```yml
# creates a custom network called `frontend`
networks:
   frontend:
```

## External Network

```yml
# join a pre-existing network
networks:
   default:
      external:
         name: frontend
```

## Volume

```yml
# mount host paths or named volumes, specified as sub-options to a service
  db:
    image: postgres:latest
    volumes:
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"
      - "dbdata:/var/lib/postgresql/data"

volumes:
  dbdata:
```

## User

```yml
# specifying user
user: root
```

```yml
# specifying both user and group with ids
user: 0:0
```

# :memo: Practice Lab

https://github.com/QuanBlue/Docker-practice-lab


# :sparkles: Credits

-  https://devhints.io/docker-compose
-  https://docs.docker.com/compose/compose-file/build/
-  https://dockerlabs.collabnix.com/intermediate/docker-compose/


---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
