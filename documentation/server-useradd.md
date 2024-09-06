# Add A User to the Server

Enter the container:

```Bash
docker exec -it ssh-server-container /bin/bash
```

Add a user from within the container:

```Bash
useradd -m -s /bin/bash testuser
```

Set user password:

```Bash
echo "testusers:password" | chpasswd
```

Add user to sudoer's group:

```Bash
usermod -aG sudo testuser
```

