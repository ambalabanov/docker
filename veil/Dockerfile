# From the Kali linux base image
FROM kalilinux/kali-linux-docker

# Update and apt install programs
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y \
 veil

# Create known_hosts for git cloning
RUN mkdir /root/.ssh
RUN touch /root/.ssh/known_hosts
# Add host keys
RUN ssh-keyscan bitbucket.org >> /root/.ssh/known_hosts
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts

# Post-install
RUN /usr/share/veil/config/setup.sh --force --silent


# Set entrypoint and working directory
WORKDIR /root/

# Indicate we want to expose ports 80 and 443
#EXPOSE 80/tcp 443/tcp