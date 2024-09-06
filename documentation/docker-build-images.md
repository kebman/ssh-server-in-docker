# Build Docker Images

Build the server and client images from `docker-compose.yml`

```Bash
docker-compose up --build
```

## Check Logs and Exit

Now check the logs (right in the terminal you started the build) and check for errors.

When you're done, hit `Ctrl + C` or `Ctrl + Break` to end the Docker Orchestration Session.

## Re-start in the Background

You can then re-start the containers in detached mode (i.e. in the background) with:

```Bash
docker-compose up -d
```

See `docker-run-containers.md` for more. [[docker-run-containers]]
