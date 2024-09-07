# Add A User to the Client Container

Enter the Client container:

```Bash
docker exec -it ssh-client-container /bin/bash
```

Make sure you set the root user's password first:

```Bash
passwd
```

Then add a user from within the container:

```Bash
useradd -m -s /bin/bash clientuser
```

Set user password:

```Bash
echo "clientuser:1234" | chpasswd
```

Add user to sudoer's group:

```Bash
usermod -aG sudo clientuser
```

