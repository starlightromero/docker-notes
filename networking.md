# Networking

* Case 1: Container to WWW Communication (works out of the box)
  * API Request
* Case 2: Container to Local Host Machine Communication
  * Connecting to a database (MongoDB)
  * host.docker.internal
* Case 3: Container to Container Communication
  * Another container which contains a SQL Database
  * Another container which contains the back-end
  * Another container which contains the front-end

Each container should only hold one thing

*Within each network, all containers can communicate with each other and IPs are automatically resolved*

Network command
```zsh
--network [NETWORK]
```

List all networks
```zsh
docker network ls
```

*You must create a network before running. Unlike volumes, Docker does not automatically create new networks for you when running a container*

Create a network
```zsh
docker network create [NETWORK]
```

Run a container with a network
```zsh
docker run -d --name [CONTAINER] --network [NETWORK] [IMAGE]
```

Remove a network
```zsh
docker network rm [NETWORK]
```

Remove all networks
```zsh
docker network prune
```

### Drivers

Networks support different types of "Drivers" which influence the behavior of the Network

The default driver is the "bridge" driver which is the most commonly used. With a bridge driver, Containers can find each other by name if they are in the same Network

The driver can be set when a Network is created by adding the --driver option

* host: For standalone containers, isolation between container and host system is removed (i.e. they share localhost as a network)
* overlay: Multiple Docker daemons (i.e. Docker running on different machines) are able to connect with each other. Only works in "Swarm" mode which is a dated / almost deprecated way of connecting multiple containers
* macvlan: You can set a custom MAC address to a container - this address can then be used for communication with that container
* none: All networking is disabled.
* Third-party plugins: You can install third-party plugins which then may add all kinds of behaviors and functionalities
