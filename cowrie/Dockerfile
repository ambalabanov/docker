FROM ubuntu:16.04

# Fix uid/gid to 1000 for shared volumes
RUN groupadd -r -g 1000 cowrie && \
    useradd -r -g 1000 -d /cowrie -m -g cowrie cowrie

RUN export DEBIAN_FRONTEND=noninteractive; \
    apt-get update && \
    apt-get install -y \
        -o APT::Install-Suggests=false \
        -o APT::Install-Recommends=false \
      python-pip \
      libssl-dev \
      libmpc-dev \
      libffi-dev \
      build-essential \
      libpython-dev \
      python2.7-minimal \
      git \
      virtualenv \
      python-virtualenv \
      python-setuptools \
      supervisor \
      wget
RUN wget "https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-6.1.0-amd64.deb" && \
    dpkg -i filebeat*.deb
RUN su - cowrie -c "\
      git clone http://github.com/micheloosterhof/cowrie /cowrie/cowrie-git && \
      cd /cowrie/cowrie-git && \
        virtualenv cowrie-env && \
        . cowrie-env/bin/activate && \
        pip install --upgrade cffi && \
        pip install --upgrade pip && \
        pip install --upgrade setuptools && \
        pip install -r ~cowrie/cowrie-git/requirements.txt" && \
    # Remove all the build tools to keep the image small.
    export DEBIAN_FRONTEND=noninteractive && \
    apt-get remove -y --purge \
      git \
      python-pip \
      python-setuptools \
      libmpfr-dev \
      libssl-dev \
      libmpc-dev \
      libffi-dev \
      build-essential \
      libpython-dev \
      python3.4* && \
    # Remove any auto-installed depends for the build and any temp files and package lists.
    apt-get autoremove -y && \
    dpkg -l | awk '/^rc/ {print $2}' | xargs dpkg --purge && \
    apt-get clean && \
    rm -rf filebeat*.deb && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
COPY supervisor/*.conf /etc/supervisor/conf.d/
WORKDIR /cowrie/cowrie-git
EXPOSE 2222 2223
CMD ["/usr/bin/supervisord", "--nodaemon", "-c", "/etc/supervisor/supervisord.conf"]
