# Utility Container

A container which only contain an environment and not an application.

Executes/Appends custom command

Execute a command in a running container
```zsh
docker exec -it [CONTAINER] [CMD]
```

Override the default container command
```zsh
docker run -it [CONTAINER] [CMD]
```

Limit avalible terminal commands in Dockerfile
```Docker
ENTRYPOINT ["[CMD]"]
```
