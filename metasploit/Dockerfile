# From the Kali linux base image
FROM kalilinux/kali-linux-docker

# Update and apt install programs
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y metasploit-framework 

# Post-install
RUN service postgresql start && msfdb init

# Indicate we want to expose ports 80 and 443
EXPOSE 8080/tcp 4444/tcp

# Starting DB
CMD service postgresql start

ENTRYPOINT /bin/bash
