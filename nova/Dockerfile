#
# keystone dockerfile
#

# Pull base image.
FROM diepnt/ubuntu

# Install keystone
  RUN \
  #apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y nova-api nova-cert nova-conductor nova-consoleauth nova-novncproxy nova-scheduler python-novaclient supervisor && \
  echo 'rpc_backend = rabbit'  >> /etc/nova/nova.conf && \
  echo 'rabbit_host = keystone' >>  /etc/nova/nova.conf && \
  echo 'rabbit_password = RABBIT_PASS' >> /etc/nova/nova.conf && \
  echo 'my_ip = nova_controller' >> /etc/nova/nova.conf && \
  echo 'vncserver_listen = nova_controller' >>  /etc/nova/nova.conf && \
  echo 'vncserver_proxyclient_address = nova_controller' >> /etc/nova/nova.conf && \
  echo 'auth_strategy = keystone'  >> /etc/nova/nova.conf && \
  echo '[database]' >> /etc/nova/nova.conf && \
  echo 'connection = mysql://nova:NOVA_DBPASS@mysql/keystone' >> /etc/nova/nova.conf && \
  echo '[keystone_authtoken]'  >> /etc/nova/nova.conf  && \
  echo 'auth_uri = http://keystone:5000' >> /etc/nova/nova.conf  && \
  echo 'auth_host = keystone'  >> /etc/nova/nova.conf  && \
  echo  'auth_port = 35357' >> /etc/nova/nova.conf  && \
  echo  'auth_protocol = http' >> /etc/nova/nova.conf  && \
  echo 'admin_tenant_name = service' >>  /etc/nova/nova.conf  && \
  echo 'admin_user = nova' >> /etc/nova/nova.conf  && \
  echo 'admin_password = NOVA_PASS' >> /etc/nova/nova.conf
  sed -i '17i[program:nova-api]' /etc/supervisor/supervisord.conf && \
  sed -i '18icommand=/usr/bin/nova-api' /etc/supervisor/supervisord.conf && \
  sed -i '19i[program:nova-cert]' /etc/supervisor/supervisord.conf && \
  sed -i '20icommand=/usr/bin/nova-cert' /etc/supervisor/supervisord.conf && \
  sed -i '21i[program:nova-consoleauth]' /etc/supervisor/supervisord.conf && \
  sed -i '22icommand=/usr/bin/nova-consoleauth' /etc/supervisor/supervisord.conf && \
  sed -i '23i[program:scheduler]' /etc/supervisor/supervisord.conf && \
  sed -i '24icommand=/usr/bin/nova-scheduler' /etc/supervisor/supervisord.conf && \
  sed -i '25i[program:nova-conductor]' /etc/supervisor/supervisord.conf && \
  sed -i '26icommand=/usr/bin/nova-conductor' /etc/supervisor/supervisord.conf && \
   sed -i '27i[program:novncproxy]' /etc/supervisor/supervisord.conf && \
  sed -i '28icommand=/usr/bin/nova-novncproxy' /etc/supervisor/supervisord.conf && \
  rm /var/lib/nova/nova.sqlite && \
  /etc/init.d/supervisor start


# Define working directory.
WORKDIR /root

# Define default command.
CMD ["/usr/bin/supervisord", "-n"]
# Expose ports.
EXPOSE 8774
