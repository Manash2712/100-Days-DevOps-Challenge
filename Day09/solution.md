### Solution

ssh to the DB server

As the task states mariadb service is not running, lets first start the mariadb service.
```
sudo systemctl start mariadb
```

This failed, so let's check the status of service to get more information about error.
```
sudo systemctl status mariadb
```

In this we can see the below error.
```
Process: 2280 ExecStart=/usr/libexec/mariadbd --basedir=/usr $MYSQLD_OPTS $_WSREP_NEW_CLUSTER (code=exited, status=1/FAILURE)
```

This error generally related to permission errors. So let's check the permission on data directory (/var/lib/mysql)
```
ls -ld /var/lib/mysql
```
From above check we can confirm the ownership of the data directory. The owner is root and group is mysql.
```
[peter@stdb01 ~]$ ls -ld /var/lib/mysql
drwxr-xr-x 1 root mysql 4096 Nov  6 10:48 /var/lib/mysql
[peter@stdb01 ~]$
```

Let's change the ownership of data directory to mysql:mysql
```
sudo chown -R mysql:mysql /var/lib/mysql
```

Let's try to start mariadb service now.
```
sudo systemctl start mariadb
```

Bingo!! No errors this time, lets check the status.
```
sudo systemctl status mariadb
```
The service is active and running.

