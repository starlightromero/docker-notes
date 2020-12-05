# Docker

Get Help
```zsh
docker --help
```

Get help about a command
```zsh
docker [COMMANDS] --help
```

### Images

Images take a snapshot of a project.

List all images
```zsh
docker images
```

Build an image
```zsh
docker build -t [IMAGE]:[TAG] .
```

Remove an image
```zsh
docker rmi [IMAGE]:[TAG]
```

### Containers

Containers are **run** in attached mode. To run a detached container use the flag **-d**

Containers are **start** in detached mode

Use the flag **--rm** to automatically remove a container once it is stopped

Use the flag **--name** to name the container

List all running containers
```zsh
docker ps
```

List all containers
```zsh
docker ps -a
```

Get logs from a container
```zsh
docker logs [CONTAINER]
```

Run a named container in detatch mode with automatic removal on stop
```zsh
docker run -d -p [APP_PORT]:[ACCESS_PORT] --rm --name [CONTAINER] [IMAGE]:[TAG]
```

Restart a stopped container
```zsh
docker start [CONTAINER]
```

Stop a container
```zsh
docker stop [CONTAINER]
```

Remove a container
```zsh
docker rm [CONTAINER]
```

### Volumes

Volumes are managed by Docker.

Volumes persist data by **mounting** a **folder on your host machine** into containers

Volumes persist if a container is stopped or removed

A container can **write** data into a volume and **read** data from it

Anonymous volumes are deleted when the container is removed since they are recreated when the container is created.

Named volumes are kept when the container is removed.

List all volumes
```zsh
docker volume ls
```

Run a container with a named volume
```zsh
docker run -d -p [APP_PORT]:[ACCESS_PORT] --rm --name [CONTAINER] -v [VOLUME]:[CONTAINER_PATH] [IMAGE]:[TAG]
```

Remove an anonymous volume
```zsh
docker volume rm [VOLUME]
```

Remove all anonymous volumes
```zsh
docker volume prune
```

### Bind Mounts (Code Sharing)

Bind mounts are similar to volumes. However unlike volumes, bind mounts are managed by the developer.

ANON_VOLUME = Path to Docker interal folder which should not be overwritten by the bind mount (i.e. /app/node_modules)

Run a container with a bind mount.
```zsh
docker run -d -p [APP_PORT]:[ACCESS_PORT] ---rm -name [CONTAINER] -v [VOLUME]:[CONTAINER_PATH] -v [ABSOLUTE_PATH_TO_PROJECT_FOLDER]:/app -v [ANON_VOLUME] [IMAGE]:[TAG]
```

### Node Development

To use nodemon with Docker:
1. add nodemon as a dependency in package.json
2. add a start script "nodemon app.js" in package.json
3. `CDM["yarn", "start"]` in Dockerfile

*The image will need to be deleted and rebuilt after this*

### Anonymous vs Named vs Bind Mount

Anonymous Volume
```zsh
docker run -v /app/data
```

Named Volume
```zsh
docker run -v data:/app/data
```

Bind Mount
```zsh
docker run -v /path/to/code:/app/code
```

Anonymous | Named | Bind Mount
---|---|---
created specifically for a single container | not tied to a specific container | located on host file system
survives container shutdown/restart unless --rm is used | survive container shutdown/restart and removal | survive container shutdown/restart and removal
cannot be shared across containers | can be shared across containers | can be shared across containers
cannot be reused (even on the same image) | can be reused for same container (across restarts) | can be reused for same container (across restarts)

### Read Only Volumes

Volumes by default are read/write

For some volumes, particularly bind mount, you want to be able to change the source code but you don't want the container itself to be able to change the code

You can enforce this read only behavior with read only volumes

Run a container with a Read Only Bind Mount
```zsh
docker run -d -p [APP_PORT]:[ACCESS_PORT] --rm -name [CONTAINER] -v [VOLUME]:[CONTAINER_PATH] -v [ABSOLUTE_PATH_TO_PROJECT_FOLDER]:/app:ro -v [ANON_VOLUME] [IMAGE]:[TAG]
```
