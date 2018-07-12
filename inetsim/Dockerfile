FROM debian:wheezy-slim

RUN apt-get update && \
    apt-get install -y wget && \
    echo "deb http://www.inetsim.org/debian/ binary/" > /etc/apt/sources.list.d/inetsim.list && \
    wget -O - http://www.inetsim.org/inetsim-archive-signing-key.asc | apt-key add - && \
    apt-get update && \
    apt-get install -y inetsim
	
EXPOSE 21 25 53 53/udp 80 110 443 

WORKDIR /opt/inetsim/

CMD ["inetsim"]