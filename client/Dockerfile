# client/Dockerfile
FROM debian:bookworm-slim

# Install SSH client and Vim
RUN apt-get update && apt-get install -y \
    openssh-client \
    vim

# Start a bash shell (useful for manual testing)
CMD ["/bin/bash"]

