# Add A User to the Server

Enter the container:

```Bash
docker exec -it ssh-server-container /bin/bash
```

Make sure you add the root user's password first:

```Bash
passwd
```

Then add a user from within the container:

```Bash
useradd -m -s /bin/bash testuser
```

Set user password:

```Bash
echo "testuser:password" | chpasswd
```

Add user to sudoer's group:

```Bash
usermod -aG sudo testuser
```

