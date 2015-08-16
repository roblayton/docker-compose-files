FROM busybox
MAINTAINER Rob Layton hire@roblayton.com

ADD ["config/registry.yml", "/data/registry.yml"]
ADD ["config/redis.conf", "/data/redis.conf"]
ADD ["config/nginx.conf", "/data/nginx.conf"]
ADD ["certs/selfsigned.crt", "/data/domain.crt"]
ADD ["certs/selfsigned.key", "/data/domain.key"]
ADD ["certs/passwd", "/data/passwd"]
