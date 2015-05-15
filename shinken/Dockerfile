# Shinken Docker installation using pip (latest)
FROM        debian:wheezy
MAINTAINER  Rohit Gupta

# Install Shinken, Nagios plugins, nginx, and supervisord
RUN         apt-get update && apt-get install -y python-pip \
                python-pycurl \
                python-cherrypy3 \
                python-paramiko \
                nagios-plugins \
                libsys-statistics-linux-perl \
                nginx \
                openssh-server \
                ntp \
                libssl-dev \
                rsyslog \
                rsyslog-doc \
                collectd \
                collectd-utils \
                supervisor && \
                apt-get -y autoremove && \
                apt-get clean
RUN         useradd --create-home shinken && \
                pip install shinken influxdb && \
                update-rc.d -f shinken remove

# Install snmp
RUN             apt-get update && apt-get install -y snmpd


# Install shinken modules from shinken.io
RUN         su - shinken -c 'shinken --init' && \
                su - shinken -c 'shinken install webui' && \
                su - shinken -c 'shinken install auth-htpasswd' && \
                su - shinken -c 'shinken install sqlitedb' && \
                su - shinken -c 'shinken install pickle-retention-file-scheduler' && \
                su - shinken -c 'shinken install booster-nrpe' && \
                su - shinken -c 'shinken install linux-snmp' && \
                su - shinken -c 'shinken install ssh' && \
                #su - shinken -c 'shinken install collectd' && \
                su - shinken -c 'shinken install mod-influxdb'

## Install collectd module
#ADD             https://github.com/shinken-monitoring/mod-collectd/archive/master.tar.gz /usr/src/
#RUN             tar xvf /usr/src/master.tar.gz && \
                #mv mod-collectd-master/module /var/lib/shinken/modules/mod-collectd

# Install check_nrpe plugin
ADD         nrpe-2.15.tar.gz /usr/src/
RUN         cd /usr/src/nrpe-2.15/ && \
                ./configure --with-nagios-user=shinken --with-nagios-group=shinken --with-nrpe-user=shinken --with-nrpe-group=shinken --with-ssl=/usr/bin/openssl --with-ssl-lib=/usr/lib/x86_64-linux-gnu && \
                make all && \
                make install-plugin && \
                mv /usr/local/nagios/libexec/check_nrpe /usr/lib/nagios/plugins/check_nrpe && \
                cd / && \
                rm -rf /usr/src/nrpe-2.15

# Configure nginx
ADD         shinken/shinken_nginx.conf /etc/nginx/sites-available/shinken_nginx.conf
RUN         mkdir -p /var/log/nginx && \
                rm -f /etc/nginx/sites-enabled/default && \
                ln -sf /etc/nginx/sites-available/shinken_nginx.conf /etc/nginx/sites-enabled/shinken_nginx.conf && \
                update-rc.d -f nginx remove && \
                echo "daemon off;" >> /etc/nginx/nginx.conf

# Configure Shinken modules
ADD         shinken/shinken.cfg /etc/shinken/shinken.cfg
ADD         shinken/broker-master.cfg /etc/shinken/brokers/broker-master.cfg
ADD         shinken/poller-master.cfg /etc/shinken/pollers/poller-master.cfg
ADD         shinken/scheduler-master.cfg /etc/shinken/schedulers/scheduler-master.cfg
ADD         shinken/receiver-master.cfg /etc/shinken/receiver/receiver-master.cfg
ADD         shinken/arbiter-master.cfg /etc/shinken/receiver/arbiter-master.cfg
ADD         shinken/webui.cfg /etc/shinken/modules/webui.cfg
#ADD         shinken/collectd.cfg /etc/shinken/modules/collectd.cfg
ADD         shinken/influxdb.cfg /etc/shinken/modules/influxdb.cfg
#ADD         shinken/linux-snmp.cfg /etc/shinken/packs/linux-snmp/commands.cfg
ADD         custom_configs/hosts/localhost.cfg /etc/shinken/hosts/localhost.cfg
ADD         snmp/snmp.conf /etc/snmp/snmp.conf
ADD         snmp/snmpd.conf /etc/snmp/snmpd.conf
ADD         collectd/collectd.conf /etc/collectd/collectd.conf
RUN         mkdir -p /etc/shinken/custom_configs /usr/local/custom_plugins && \
                ln -sf /etc/shinken/custom_configs/htpasswd.users /etc/shinken/htpasswd.users && \
                ln -s /usr/lib/nagios/plugins/utils.pm /var/lib/shinken/libexec/utils.pm

# Copy extra NRPE plugins and fix permissions
ADD         extra_plugins/* /usr/lib/nagios/plugins/
RUN         cd /usr/lib/nagios/plugins/ && \
                chmod a+x * && \
                chmod u+s check_apt restart_service check_ping check_icmp check_fping apt_update

# Define mountable directories
VOLUME      ["/etc/shinken/custom_configs", "/usr/local/custom_plugins"]

# configure supervisor
ADD         supervisor/conf.d/* /etc/supervisor/conf.d/

# Expost port 80 (nginx)
EXPOSE  80

# Default docker process
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf", "-n"]
