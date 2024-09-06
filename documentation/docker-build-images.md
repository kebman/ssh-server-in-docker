# Build Docker Images

Build the server and client images from `docker-compose.yml`

```Bash
docker-compose up --build
```

## Access

When the images are built and running, you can enter them from the host with the following commadnds:

### Client

```Bash
docker exec -it ssh-client-container /bin/bash
```

### Server

```Bash
docker exec -it ssh-server-container /bin/bash
```

From there you can run regular Debian Linux commands, from within the respective container.
