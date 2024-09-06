# SSH from the Client to the Server

```Bash
docker exec -it ssh-client-container /bin/bash
```

```Bash
ssh testuser@ssh-server-container
```

## Altnernatively

SSH directly from the Docker host and into the Server container:

```Bash
ssh testuser@host.docker.internal -p 2222
```

## Next Step

Add SSH Ed25519 Keys (for both client and server)

