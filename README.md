Docker
=======
keystone
=======
Sau khi build config hosts trỏ tới mysql vd:
====
172.17.0.104    keystone
====
10.2.34.24      mysql
====
Glance
Sau khi build config hosts trở tới mysql và keystone vd:
172.17.0.107    glance
10.2.34.24      mysql
10.2.34.24      keystone
127.0.0.107     localhost

