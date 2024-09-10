# Tutorial: SSH Server in Docker - Project Guide

This project demonstrates how to build a Docker-based SSH server and client setup using Docker Compose. You can also set up a password-less login and use certificate-based authentication (Ed25519) for the SSH server.

---

## Project Setup

### 1. Initialize the Project
Create the folder structure and set up the initial project files:

```bash
cd ~/projects
mkdir docker-ssh-server
cd docker-ssh-server
mkdir documentation client server
touch client/Dockerfile
touch server/Dockerfile
touch docker-compose.yml
touch .gitignore
git init
git add .
git commit -m "Initial commit"
```

### 2. Build Docker Images
First, ensure Docker and Docker Compose are installed on your system. Then, to build and run the Docker images for the SSH server and client:

```bash
docker-compose up --build
```

### 3. Access Docker Containers

You can access the running Docker containers using:

#### Access Server:
```bash
docker exec -it ssh-server-container /bin/bash
```

#### Access Client:
```bash
docker exec -it ssh-client-container /bin/bash
```

---

## Adding a User Inside Containers

### Adding a User to the Server:
1. Access the server container:
   ```bash
   docker exec -it ssh-server-container /bin/bash
   ```
2. Set the root password:
   ```bash
   passwd
   ```
3. Add a user:
   ```bash
   useradd -m -s /bin/bash testuser
   echo "testuser:password" | chpasswd
   ```
4. Add the user to the sudo group:
   ```bash
   usermod -aG sudo testuser
   ```

### Adding a User to the Client:
1. Access the client container:
   ```bash
   docker exec -it ssh-client-container /bin/bash
   ```
2. Set the root password:
   ```bash
   passwd
   ```
3. Add a user:
   ```bash
   useradd -m -s /bin/bash clientuser
   echo "clientuser:1234" | chpasswd
   usermod -aG sudo clientuser
   ```

---

## SSH Key Setup

### 1. Generate SSH Keys on the Client
Within the client container, generate SSH keys:

#### For a more secure setup:
```bash
ssh-keygen -t ed25519 -a 101 -f ~/.ssh/id_ed25519
```

#### For a simpler setup:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### 2. Copy SSH Keys to the Server
Copy the public key to the server (replace `172.19.0.2` with your server's IP address):

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub testuser@172.19.0.2
```

### 3. SSH from Client to Server
Now, from within the client container, SSH into the server:

```bash
ssh testuser@ssh-server-container
```

Alternatively, SSH directly from the Docker host using the exposed port:
```bash
ssh testuser@host.docker.internal -p 2222
```

---

## Configure SSH Server for Certificate-based Login (Ed25519)

### 1. Generate SSH Host Keys (Server-side):
Run the following command on the SSH server to generate Ed25519 keys:
```bash
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ''
```

Ensure the key permissions are set properly:
```bash
chown root:root /etc/ssh/ssh_host_*
chmod 600 /etc/ssh/ssh_host_*
```

### 2. Update SSH Configuration:
Edit the server's `sshd_config` file to include the Ed25519 key:
```bash
vim /etc/ssh/sshd_config
```

Add the following line:
```bash
HostKey /etc/ssh/ssh_host_ed25519_key
```

Ensure the `PubkeyAcceptedAlgorithms` line includes `ssh-ed25519`:
```bash
PubkeyAcceptedAlgorithms ssh-ed25519
```

### 3. Restart SSH Service:
```bash
service ssh restart
```

### 4. Verify SSH Setup:
Check the SSH status and logs:
```bash
service ssh status
journalctl -u sshd
```

---

## Docker Orchestration Commands

### Build and Run Containers
You can start the containers in detached mode with:
```bash
docker-compose up -d
```

### Shutdown Containers
To gracefully shut down running containers:
```bash
docker-compose down
```

---

## Getting the Server Container's IP Address
You may need the SSH server's container IP for testing:

```bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ssh-server-container
```

---

## License and Contributions

This project is licensed under the **MIT License**. You are welcome to fork, modify, and tinker with the project.