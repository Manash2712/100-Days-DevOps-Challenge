### Solution

LAMP Stack is a group of open-source software that is typically installed together to enable a server to host dynamic web apps. 

Full form of LAMP:

 - L: Linux Operating Systems
 - A: Apache Web Server
 - M: MySQL/MariaDB Database
 - P: Php

Lets start by installing apache httpd and php on all the appservers. Follow below steps on each of app servers.

- Step 1: Login to app server.
  ```
  ssh tony@stapp01
  ```

- Step 2: Install httpd and php along with dependencies.
  ```
  yum install -y httpd php php-mysqli
  ```

- Step 3: Edit httpd config to listen on port 8088, open the config file with file editor and search for _Listen 80_ and replace it by _Listen 8088_.
  ```
  vi /etc/httpd/conf/httpd.conf 
  ```

- Step 4: Start and enable httpd service.
  ```
  systemctl start httpd
  ```
  ```
  systemctl enable httpd
  ```

Configurations on app servers is done, now lets start to work on database server. Log in to DB server.
```
ssh peter@stdb01
```

Install mariadb on the server.
```
yum install mariadb-server
```

Start and enable mariadb service.
```
systemctl start mariadb
```
```
systemctl enable mariadb
```

Now login to the mysql command line using below.
```
mysql -u root
```

Noww in the mysql command line run below command to create a database with name _kodekloud_db1_.
```
CREATE DATABASE kodekloud_db1;
```

Now lets create user.
```
CREATE USER 'kodekloud_gem'@'%' IDENTIFIED BY 'BruCStnMT5';
```

Grant the kodekloud_gem user all privileges to the database created.
```
GRANT ALL ON kodekloud_db1.* TO 'kodekloud_gem'@'%';
```

Use below command to reload the grant tables.
```
FLUSH PRIVILEGES;
```

Now click on the _App_ button to test the connection.
