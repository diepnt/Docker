#
# MySQL Dockerfile
#
# https://github.com/dockerfile/mysql
#

# Pull base image.
FROM diepnt/ubuntu

# Install MySQL.
RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y mysql-server && \
  sed -i s/127.0.0.1/0.0.0.0/g /etc/mysql/my.cnf && \
  sed -i '43i#innodb config'  /etc/mysql/my.cnf && \
  sed -i '44idefault-storage-engine = innodb'  /etc/mysql/my.cnf && \
  sed -i '45iinnodb_file_per_table'  /etc/mysql/my.cnf && \
  sed -i '46icollation-server = utf8_general_ci' /etc/mysql/my.cnf && \
  sed -i '47iinit-connect = SET NAMES utf8'  /etc/mysql/my.cnf && \
  sed -i '48icharacter-set-server = utf8'  /etc/mysql/my.cnf && \
  service mysql restart && \
  mysql -uroot  -e 'CREATE DATABASE keystone;' && \
  mysql -uroot  -e "GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' IDENTIFIED BY 'KEYSTONE_DBPASS'"  && \
  mysql_install_db && \
  echo  "mysql_secure_installation <<EOF" >>/tmp/script && \
  echo " "  >> /tmp/script && \
  echo "n"  >> /tmp/script && \
  echo "y"  >> /tmp/script && \
  echo "n "  >> /tmp/script && \
  echo "y "  >> /tmp/script && \
  echo "y"  >> /tmp/script && \
  echo "y"  >> /tmp/script && \
  echo "EOF"  >> /tmp/script && \
  bash /tmp/script

# Define working directory.
WORKDIR /root
EXPOSE 3306
