<h1 align="center">
  <img src="./assets/docker-swarm-logo.png" alt="icon" height="150"></img>
  <br>
  <b>Docker Swarm Cheatsheet</b>
</h1>

<p align="center">Quick reference for orchestrating containerized applications in a distributed environment at scale.</p>

<!-- Badges -->
<p align="center">
  <a href="https://github.com/QuanBlue/Tech-Cheatsheets/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/QuanBlue/Tech-Cheatsheets" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/QuanBlue/Tech-Cheatsheets" alt="last update" />
  </a>
  <a href="https://github.com/QuanBlue/Tech-Cheatsheets/network/members">
    <img src="https://img.shields.io/github/forks/QuanBlue/Tech-Cheatsheets" alt="forks" />
  </a>
  <a href="https://github.com/QuanBlue/Tech-Cheatsheets/stargazers">
    <img src="https://img.shields.io/github/stars/QuanBlue/Tech-Cheatsheets" alt="stars" />
  </a>
  <a href="https://github.com/QuanBlue/Tech-Cheatsheets/issues/">
    <img src="https://img.shields.io/github/issues/QuanBlue/Tech-Cheatsheets" alt="open issues" />
  </a>
  <a href="https://github.com/QuanBlue/Tech-Cheatsheets/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/QuanBlue/Tech-Cheatsheets.svg" alt="license" />
  </a>
</p>

<p align="center">
  <b>
      <a href="https://github.com/QuanBlue/Tech-Cheatsheets">Home page</a> •
      <a href="https://github.com/QuanBlue/Tech-Cheatsheets/tree/main/Container%20Orchestration">Container Orchestration page</a>
  </b>
</p>

<details open>
<summary><b>:open_book: Table of Contents</b></summary>

-  [Definition](#light_bulb-definition)
   -  [Scaling](#scaling)
   -  [Load Balancing:](#load-balancing)
-  [CLI cheatsheet](#clipboard-cli-cheatsheet)
   -  [Initialization and Management](#initialization-and-management)
   -  [Nodes Management](#nodes-management)
      -  [Handling nodes](#handling-nodes)
      -  [Labelling nodes](#labelling-nodes)
   -  [Service Management](#service-management)
      -  [Inspect](#inspect)
      -  [Control](#control)
   -  [Stack Management](#stack-management)
      -  [Inspect](#inspect-1)
      -  [Control](#control-1)
   -  [Secrets Management](#secrets-management)
      -  [Inspect](#inspect-2)
      -  [Control](#control-2)
-  [Create Docker VPS](#nut_and_bolt-create-docker-vps)
-  [Practice Lab](#memo-practice-lab)
-  [Contributors](#busts_in_silhouette-contributors)
-  [Credits](#sparkles-credits)
-  [License](#scroll-license)
-  [Related Projects](#link-related-projects)
</details>

# :light_bulb: Definition

In summary, Docker Swarm provides the orchestration and management capabilities to deploy and scale services (replicas) across a cluster of nodes, allowing you to efficiently manage and run containerized applications.

```lua
                    +-----------------------------------+
                    |       Docker Swarm Cluster        |
                    +-----------------------------------+
                             |              |
            +------------------------+------------------------+
            |                        |                        |
    +----------------+      +------------------+      +---------------+
    |     Node 1     |      |    Node Manager  |      |     Node 2    |
    +----------------+      +------------------+      +---------------+
            |                                                 |
       +---------+                                       +---------+
       | Stack 1 |                                       | Stack 2 |
       +---------+                                       +---------+
            |                                                 |
      +-----------+                                  +------------------+
      | Service 1 |                                  |                  |
      +-----------+                           +-----------+      +-----------+
                                              | Service 1 |      | Service 2 |
                                              +-----------+      +-----------+
                                                  |
                                 +----------------+----------------+
                                 |                |                |
                          +------------+    +------------+        ...
                          | Replica 1  |    | Replica 2  |
                          +------------+    +------------+
```

<p align="center">
  <i>Figure 1. Docker Swarm Cluster structure</i>
</p>

<details open>
<summary><b>The concept in Docker Swarm</b></summary>

-  **Docker Swarm Cluster:** It is a group of Docker nodes (machines) that are connected and managed as a single entity using Docker Swarm. The cluster provides high availability and scalability for running containerized applications.

-  **Node:** A node refers to a machine (physical or virtual) that is part of the Docker Swarm Cluster. Nodes can be either a manager or a worker.

   -  **Manager Node:** Manager nodes are responsible for managing the cluster and coordinating various activities such as scheduling services, maintaining cluster state, and handling swarm management commands.

   -  **Worker Node:** Worker nodes are responsible for running the containers and executing the tasks assigned to them by the manager nodes. They do not participate in the management of the cluster.

-  **Stack:** A stack in Docker Swarm is a way to organize and manage a group of services that are related to each other and need to be deployed together. Stacks are defined using a Compose file (YAML) that describes the services, networks, and other configurations.

-  **Service:** A service is a definition of the desired state for a replicated application or microservice. It represents a single task or a set of tasks that Docker Swarm manages and schedules onto worker nodes. Services can be scaled up or down, load balanced, and updated with rolling updates. Services may defined within stacks.

-  **Replica:** A replica represents an instance of a service that is running on a worker node. Docker Swarm schedules and distributes replicas across multiple nodes to provide high availability and load balancing for the services.

-  **Container:** A container is an isolated and lightweight runtime environment that encapsulates an application and its dependencies. It is an instance of an image and runs as a replica of a service on a worker node.

</details>

<details open>
<summary><b>Importance features</b></summary>

### Scaling

-  Scaling refers to increasing or decreasing the number of replicas (instances) of a service running in the Docker Swarm Cluster.
-  Docker Swarm makes it easy to scale services horizontally by adding or removing replicas, allowing you to handle increased traffic or distribute the workload.
-  Scaling can be done manually or automatically based on predefined rules or metrics.
-  When scaling a service, Docker Swarm automatically distributes the replicas across available worker nodes in the cluster to ensure load balancing and fault tolerance.

### Load Balancing:

-  Load balancing is the process of distributing incoming network traffic across multiple replicas of a service to evenly distribute the workload.
-  Docker Swarm provides built-in load balancing functionality to automatically distribute traffic among replicas of a service.
-  The ingress load balancer in Docker Swarm routes incoming requests to the appropriate service and replica, distributing the load evenly across all available replicas.
-  Load balancing in Docker Swarm ensures that the traffic is efficiently distributed and prevents any single replica or node from being overloaded.
-  Load balancing is transparent to the client, and requests are automatically routed to healthy replicas without the need for any manual configuration.

Together, scaling and load balancing in Docker Swarm enable you to handle increased traffic, improve availability, and ensure optimal resource utilization across the cluster. This allows you to scale your applications easily and efficiently while maintaining high performance and availability.

</details>

# :clipboard: CLI cheatsheet

## Initialization and Management

Initialize a Docker Swarm on the current Docker host:

```sh
docker swarm init
```

Get token:

```sh
# Get token to join workers
docker swarm join-token worker

# Get token to join new manager
docker swarm join-token manager
```

Join a Docker host to an existing Swarm:

```sh
docker swarm join --token <token> <manager-ip>:<manager-port>
```

Leave the Swarm:

```sh
docker swarm leave
```

Unlock

```sh
 # Unlock a manager host after docker daemon restart when autolock is on
docker swarm unlock

# Print key needed for 'unlock'
docker swarm unlock-key
```

## Nodes Management

### Handling nodes

List all nodes in the Swarm:

```sh
docker node ls
```

Remove a node from the Swarm:

```sh
docker node rm <node-id>
```

Promote a worker node to a manager node:

```sh
docker node promote <node-id>
```

Demote a manager node to a worker node:

```sh
docker node demote <node-id>
```

### Labelling nodes

List node labels

```sh
docker node inspect <node> | grep Labels -C5
```

Add node label

```sh
docker node update --label-add <key>=<value> <node>
```

Remove node label

```sh
docker node update --label-rm <key> <node>
```

## Service Management

### Inspect

List all services in the Swarm:

```sh
docker service ls
```

Inspect details of a service:

```sh
docker service inspect <service-name>
```

### Control

Create a new service in the Swarm:

```sh
docker service create --name <service-name> <image> [command]
```

Scale a service to a specified number of replicas:

```sh
docker service scale <service-name>=<replicas>
```

Update a service with new configuration:

```sh
docker service update <service-name> [options]
```

Remove a service from the Swarm:

```sh
docker service rm <service-name>
```

## Stack Management

### Inspect

List all stacks in the Swarm:

```sh
docker stack ls
```

Inspect details of a stack:

```sh
docker stack inspect <stack-name>
```

List services in a stack:

```sh
docker stack services <stack-name>
```

List tasks in a stack:

```sh
docker stack ps <stack-name>
```

### Control

Deploy a stack from a Compose file:

```sh
docker stack deploy -c <compose-file> <stack-name>
```

Remove a stack from the Swarm:

```sh
docker stack rm <stack-name>
```

## Secrets Management

### Inspect

List all secrets in the Swarm:

```sh
docker secret ls
```

Inspect details of a secret:

```sh
docker secret inspect <secret-name>
```

### Control

Create a secret:

```sh
echo "mysecret" | docker secret create <secret-name> -
```

Remove a secret from the Swarm:

```sh
docker secret rm <secret-name>
```

# :nut_and_bolt: Create Docker VPS

Create Docker VPS to deploy Docker Swarm

-  [Docker-VPS](https://github.com/QuanBlue/Docker-VPS)
-  [Init Docker Swarm lab](https://github.com/QuanBlue/Docker-practice-lab/tree/master/Intermediate/docker%20swarm/Lab%20%231%3A%20Init%20and%20Manage%20Docker%20Swarm)

# :memo: Practice Lab

https://github.com/QuanBlue/Docker-practice-lab

# :busts_in_silhouette: Contributors

<a href="https://github.com/QuanBlue/Tech-Cheatsheets/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=QuanBlue/Tech-Cheatsheets" />
</a>

Contributions are always welcome!

# :sparkles: Credits

-  https://lzone.de/cheat-sheet/Docker%20Swarm
-  https://chat.openai.com/
-  Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)

# :scroll: License

Distributed under the MIT License. See <a href=".https://github.com/QuanBlue/Tech-Cheatsheets/blob/main/LICENSE">`LICENSE`</a> for more information.

# :link: Related Projects

-  <u>[**Docker cheatsheet**](https://github.com/QuanBlue/Tech-Cheatsheets)</u>: Quick reference guide for commonly used Docker commands and operations.
-  <u>[**Docker Compose cheatsheet**](https://github.com/QuanBlue/Tech-Cheatsheets/blob/master/Docker%20Compose%20cheatsheet/README.md)</u>: Quick reference for managing multi-container applications.

---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
