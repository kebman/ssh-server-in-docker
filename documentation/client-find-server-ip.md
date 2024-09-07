# Find Server Container's IP

```Bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ssh-server-container
```
## Server IP

172.19.0.2
