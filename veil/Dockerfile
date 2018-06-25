# From the Kali linux base image
FROM kalilinux/kali-linux-docker

# Update and apt install programs
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y \
 metasploit-framework \
 exploitdb \
 exploitdb-bin-sploits \
 nasm

# Create known_hosts for git cloning
RUN mkdir /root/.ssh
RUN touch /root/.ssh/known_hosts
# Add host keys
RUN ssh-keyscan bitbucket.org >> /root/.ssh/known_hosts
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts

# Clone git repos
RUN git clone https://github.com/EmpireProject/Empire.git /opt/empire
RUN git clone https://github.com/PowerShellMafia/PowerSploit.git /opt/powersploit
RUN git clone https://github.com/trustedsec/unicorn.git /opt/unicorn

# Post-install
RUN service postgresql start && msfdb init
RUN /opt/empire/setup/install.sh

# Update ENV
ENV PATH=$PATH:/opt/powersploit:/opt/empire:/opt/unicorn

# Set entrypoint and working directory
WORKDIR /root/

# Indicate we want to expose ports 80 and 443
EXPOSE 80/tcp 443/tcp