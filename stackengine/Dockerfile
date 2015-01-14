# This file creates a container that runs Database (Percona) with Galera Replication.
#
# Author: Paul Czarkowski
# Date: 08/16/2014

FROM progrium/busybox
MAINTAINER Paul Czarkowski "paul@paulcz.net"

ADD . /app
ADD https://s3.amazonaws.com/stackengine-controller/linux64/stackengine /app/bin/stackengine
ADD https://s3-us-west-2.amazonaws.com/opdemand/etcdctl-v0.4.6 /app/bin/etcdctl

RUN chmod +x app/bin/*

ENV DOCKER_HOST unix:///var/run/docker.sock
ENV PATH /app/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
VOLUME ["/var/lib/stackengine"]

# Define default command.
CMD ["/app/bin/boot"]

# Expose ports.
EXPOSE 8000 8001 8002
