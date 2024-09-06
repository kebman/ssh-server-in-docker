# Add A User

General advice on how to add a user in a Docker container.

You'll want to do this when starting the server container in this project.


## `useradd` options

When creating a user with the `useradd` command, several options and flags can be used:

`-d /home/user`: Specifies the home directory for the user. 
If not specified, a default home directory is created based on the username.

`-s /bin/bash`: Sets the user's default shell. 
- `/bin/bash` is a common shell, but you can use `/bin/sh`, `/bin/zsh`, etc.

`-g root`: Specifies the primary group for the user. 
- In this case, it's set to the root group. 
- If not provided, a new group with the same name as the user is created.

`-G sudo`: Specifies additional groups for the user. 
- The user is added to the sudo group, which gives them sudo privileges.

`-u 1000`: Specifies the user ID (UID) for the user. 
- If not provided, a default UID is assigned.

`-r`: Creates a system user. 
- Usually means a user without a home directory and typically used for system services. 
- This flag is not used in the provided Dockerfile.

## Example

Here’s a simplified example of how you might create a user inside a running container:

Enter the container:

```Bash
docker run -it --rm debian:slim /bin/bash
```

Add a user in the container:

```Bash
useradd -m -s /bin/bash -u 1001 myuser
```

Here’s what each flag does:

`-m`: Creates the user’s home directory if it does not exist.
`-s /bin/bash`: Sets /bin/bash as the default shell for the user.
`-u 1001`: Assigns UID 1001 to the user. You can choose any available UID.

Add the user to the *Sudoers Group*:

```Bash
usermod -aG sudo myuser
```

Exit and save the changes to a new Docker image:

```Bash
docker commit <container_id> my-new-image
```

