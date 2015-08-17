FROM busybox
MAINTAINER Rob Layton hire@roblayton.com

ADD /data

ADD ["config/registry.yml", "/data/registry.yml"]
ADD ["config/redis.conf", "/data/redis.conf"]
ADD ["config/nginx.conf", "/data/nginx.conf"]
ADD ["config/sinopia.yaml", "/data/sinopia.yaml"]
ADD ["certs/selfsigned.crt", "/data/selfsigned.crt"]
ADD ["certs/selfsigned.key", "/data/selfsigned.key"]
ADD ["certs/passwd", "/data/passwd"]
