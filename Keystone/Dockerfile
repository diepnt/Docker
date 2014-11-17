#
# keystone dockerfile
#

# Pull base image.
FROM diepnt/ubuntu

# Install keystone
ADD hosts /etc/hosts
ADD script /tmp/script
  RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y keystone rabbitmq-server supervisor && \
  sed -i '609iconnection = mysql://keystone:KEYSTONE_DBPASS@mysql/keystone'  /etc/keystone/keystone.conf && \
  sed -i '14iadmin_token = ADMIN_TOKEN' /etc/keystone/keystone.conf  && \
  sed -i '15ilog_dir = /var/log/keystone' /etc/keystone/keystone.conf  && \
  sed -i '17i[program:keystone]' /etc/supervisor/supervisord.conf && \
  sed -i '18icommand=/usr/bin/keystone-all' /etc/supervisor/supervisord.conf && \
  rm /var/lib/keystone/keystone.db && \
  service supervisor start && \
  bash /tmp/script && \
  supervisorctl restart keystone


# Define working directory.
WORKDIR /root

# Define default command.
CMD ["/usr/bin/supervisord", "-n"]
# Expose ports.
EXPOSE 5000 35357 5672

