# ELK-CTF

## Install Packetbeat

curl -L -O https://artifacts.elastic.co/downloads/beats/packetbeat/packetbeat-6.2.2-amd64.deb

dpkg -i packetbeat-6.2.2-amd64.deb

nano /etc/packetbeat/packetbeat.yml

service packetbeat start


## Install Filebeat

curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.2.2-amd64.deb

dpkg -i filebeat-6.2.2-amd64.deb

nano /etc/filebeat/filebeat.yml

service filebeat start
