FROM busybox
MAINTAINER Rob Layton hire@roblayton.com

ADD ["config/registry.yml", "/media/data1/docker/registry.yml"]
ADD ["config/redis.conf", "/media/data1/docker/redis.conf"]
ADD ["config/nginx.conf", "/media/data1/docker/nginx.conf"]
ADD ["config/sinopia.yaml", "/media/data1/docker/sinopia.yaml"]
ADD ["certs/selfsigned.crt", "/media/data1/docker/selfsigned.crt"]
ADD ["certs/selfsigned.key", "/media/data1/docker/selfsigned.key"]
ADD ["certs/passwd", "/media/data1/docker/passwd"]
