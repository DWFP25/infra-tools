FROM ubuntu:22.04

# Update package lists and install necessary packages
RUN apt-get update && apt-get install -y \
    sudo \
    vim \
    openssh-server

# Set root password
RUN echo 'root:password' | chpasswd

# Configure SSH server
RUN mkdir /var/run/sshd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

# Create user and configure for SSH
RUN useradd -m -d /home/don don
RUN echo 'don:password' | chpasswd
RUN chsh -s /bin/bash don
RUN sudo -u don mkdir -m 700 /home/don/.ssh
RUN sudo -u don touch /home/don/.ssh/authorized_keys
RUN sudo -u don chmod 644 /home/don/.ssh/authorized_keys
RUN echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIExjcnIlWqGiFB2zaoEi9XhCVoAkD7enACMrcJ1gm/VV don@fundingpips.com" >> /home/don/.ssh/authorized_keys


# Expose the SSH port
EXPOSE 22

# Start SSH service
ENTRYPOINT ["/usr/sbin/sshd", "-D", "-e"]