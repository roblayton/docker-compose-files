FROM busybox
MAINTAINER Rob Layton hire@roblayton.com

ADD ["config/registry.yml", "/data/registry.yml"]
ADD ["config/redis.conf", "/data/redis.conf"]
ADD ["config/nginx.conf", "/data/nginx.conf"]
ADD ["certs/selfsigned.crt", "/data/selfsigned.crt"]
ADD ["certs/selfsigned.key", "/data/selfsigned.key"]
ADD ["certs/selfsigned.crt", "/etc/docker/certs.d/192.168.99.102:443/ca.crt"]
ADD ["certs/passwd", "/data/passwd"]
