FROM debian:9

USER root

RUN apt-get update && apt-get upgrade && apt-get install -y \
 build-essential \
 radare2 \
 gcc \
 nasm \
 gdb \
 python \
 python-pip \
 python-dev \
 vim \
 nano \
 git \
 libffi-dev \
 libssl-dev \
 libc6-i386 \
 libc6-dev-i386 \
 lsb-core

RUN git config --global user.name "ambalabanov" && \
 git config --global user.email "ambalabanov@gmail.com" && \
 git config --global core.editor "nano"

RUN pip install --upgrade pip
RUN pip install --upgrade pwntools


RUN git clone https://github.com/longld/peda.git ~/peda && \
 echo "source ~/peda/peda.py" >> ~/.gdbinit

RUN "/bin/bash"