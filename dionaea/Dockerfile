FROM ubuntu:16.04

COPY build.sh /build/bin/

RUN /bin/bash /build/bin/build.sh && \
    groupadd --gid 1000 dionaea && \
    useradd -m --uid 1000 --gid 1000 dionaea && \
    chown -R dionaea:dionaea /opt/dionaea/var && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        p0f \
        supervisor && \
    rm -rf /opt/dionaea/etc/dionaea && \
    apt install wget -y && \
    wget "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.1.0-amd64.deb" && \
    dpkg -i filebeat*.deb && \
    rm -rf filebeat*.deb && \
    rm -rf /build /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get clean
	
COPY supervisor/*.conf /etc/supervisor/conf.d/
COPY conf /opt/dionaea/etc/dionaea
COPY conf/filebeat.yml /etc/filebeat/filebeat.yml

RUN chmod go-w /etc/filebeat/filebeat.yml

EXPOSE 21 42 53 53/udp 69/udp 80 135 443 445 1433 1723 1883 1900/udp 3306 5060 5060/udp 5061 11211

CMD ["/usr/bin/supervisord", "--nodaemon", "-c", "/etc/supervisor/supervisord.conf"]
