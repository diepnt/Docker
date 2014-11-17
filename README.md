Docker
=======
install docker
git clone https://github.com/diepnt/Docker.git
docker build -t $service /path to service forder
keystone
=======
trước khi build edit file hosts trỏ tới mysql vd:

172.17.0.105           keystone

10.2.34.24             mysql


Glance
====
trước khi build edit file hosts trở tới mysql và keystone vd:

172.17.0.107          glance

10.2.34.24            mysql

10.2.34.24            keystone

127.0.0.107           localhost



