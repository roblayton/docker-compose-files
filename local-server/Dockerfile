FROM busybox
MAINTAINER Rob Layton hire@roblayton.com

ADD /data

ADD ["config/registry.yml", "/media/data1/docker/data/registry.yml"]
ADD ["config/redis.conf", "/media/data1/docker/data/redis.conf"]
ADD ["config/nginx.conf", "/media/data1/docker/data/nginx.conf"]
ADD ["config/sinopia.yaml", "/media/data1/docker/data/sinopia.yaml"]
ADD ["certs/selfsigned.crt", "/media/data1/docker/data/selfsigned.crt"]
ADD ["certs/selfsigned.key", "/media/data1/docker/data/selfsigned.key"]
ADD ["certs/passwd", "/media/data1/docker/data/passwd"]
