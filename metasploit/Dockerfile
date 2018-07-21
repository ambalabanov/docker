FROM kalilinux/kali-linux-docker

RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y && apt-get install -y metasploit-framework 

RUN service postgresql start && msfdb init

ENTRYPOINT /bin/bash
