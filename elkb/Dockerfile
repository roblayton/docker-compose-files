FROM busybox
MAINTAINER Rob Layton hire@roblayton.com

ADD ["config/elasticsearch.yml", "/usr/share/elasticsearch/config/elasticsearch.yml"]
ADD ["config/logstash.conf", "/data/logstash.conf"]
ADD ["config/kibana.yml", "/data/kibana.yml"]
ADD ["config/redis.conf", "/data/redis.conf"]
ADD ["config/nginx.conf", "/data/nginx.conf"]
ADD ["sec/htpasswd.users", "/data/htpasswd.users"]
