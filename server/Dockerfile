# server/Dockerfile
FROM debian:slim

# Install OpenSSH server and Vim
RUN apt-get update && apt-get install -y \
    openssh-server \
    sudo \
    vim \
    && mkdir /var/run/sshd

# Add a user
# I'll add a user in the running Docker container

# Configure SSH to allow password login
RUN echo 'PermitRootLogin no' >> /etc/ssh/sshd_config \
    && echo 'PasswordAuthentication yes' >> /etc/ssh/sshd_config

# Expose the SSH port
EXPOSE 22

# Start the SSH service
CMD ["/usr/sbin/sshd", "-D"]

