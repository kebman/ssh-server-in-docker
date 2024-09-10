# Docker SSH Server and Client Setup

This project provides a simple Docker-based setup for running and testing an SSH server and client. It consists of two services: one for the SSH server and another for the client, allowing easy interaction between them.

## Project Structure

```
. 
├── client/ # Docker build context for the SSH client 
├── server/ # Docker build context for the SSH server
├── documentation/ # Other documentation, tutorials and help
├── docker-compose.yml # Docker Compose file to orchestrate the services 
└── README.md # This file
```

## How to Use

1. **Clone the repository:**

```bash
   git clone https://github.com/kebman/ssh-server-in-docker.git
   cd ssh-server-in-docker
```

2. Build and start the containers:

```Bash
docker-compose up --build
```

3. Access the SSH server: Once the containers are up, the SSH server is exposed on port `2222` (mapped to the default SSH port `22`). You can connect to the server from the client container or your local machine using:

```Bash
ssh user@localhost -p 2222
```

Replace `user` with the actual username you add in the Docker container.

## Configuration

- The SSH server is built on top of Debian Bookworm Slim with OpenSSH installed.
- Password authentication is enabled, but root login is disabled for security.
- The SSH server's default port (22) is mapped to port 2222 on the host.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contributing

Feel free to fork this repository or tinker with the code! Contributions are always welcome. If you make improvements or changes, consider submitting a pull request.

---

Made with ❤️ by [kebman](https://github.com/kebman)
