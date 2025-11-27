### Solution

First login to the appserver and follow below steps.

Lets start by installing nginx on the app server.
```
dnf install nginx -y
```

Install php-fpm 8.2
```
dnf module -y install php:8.2/common
```

Now fix up php-fpm so it can work with nginx and listen on the given socket.
- Open /etc/php-fpm.d/www.conf in vi
  ```
  vi /etc/php-fpm.d/www.conf
  ```
- Edit the user = and group = lines to both use nginx instead of apache
- Edit the listen = line to below
  ```
  listen = /var/run/php-fpm/default.sock
  ```
- Save and exit vi

Now fix up nginx.
- Open /etc/nginx/nginx.conf
  ```
  vi /etc/nginx/nginx.conf
  ```
- Edit it as below.
  ```
  server {
        listen       8098;
        listen       [::]:8098;
        server_name  _;
        root         /var/www/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }
  ```
 - Save and exit.
 - Edit this file (vi /etc/nginx/conf.d/php-fpm.conf) with correct unix socket.
    ```
    upstream php-fpm {
        server unix:/run/php-fpm/default.sock;
    }
    ```

  Restart php-fpm and nginx services
  ```
  systemctl restart nginx
  ```
  ```
  systemctl restart php-fpm
  ```
Run the curl test from jumphost
```
curl http://stapp01:8098/index.php 
```

 
