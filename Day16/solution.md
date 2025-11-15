### Solution

This task involves configuring a load balancer using nginx for a high traffic web application. So lets start by logging in to the load balancer server.

```
ssh loki@stlb01
```

Now install nginx on the load balancer server.
```
sudo yum install nginx -y
```

Now lets start and enable the nginx services.
```
sudo systemctl start nginx
```
```
sudo systemctl enable nginx
```

Now let's check the apache httpd service status and port on which it is running on all the app servers. Login to the app server and run below command to check the port.
```
sudo systemctl status httpd
sudo ss -tulnp | grep nginx
```

Now lets edit the nginx config file (/etc/nginx/nginx.conf), to configure the load balancing. Inside the config file add below content.
```
sudo vi /etc/nginx/nginx.conf
```


```
upstream app_servers {
  server 172.16.238.10:5003;
  server 172.16.238.11:5003;
  server 172.16.238.12:5003;
}

server {
  listen       80;
  listen       [::]:80;
  server_name  _;
  root /usr/share/nginx/html;

  location /{
    proxy_pass http://app_servers;
  }

  # Load configuration files for the default server block.
  include /etc/nginx/default.d/*.conf;

  error_page 404 /404.html;
  location = /404.html {
  }

  error_page 500 502 503 504 /50x.html;
  location = /50x.html {
  }
}
```

Validate and reload nginx
```
sudo nginx -t
sudo systemctl reload nginx
```

After configuring the nginx load balancer by following above steps, now lets click StaticApp and check. Its working as expected.

#### Learning from the task.
 - Nginx load balancing: Understand how to configure Nginx to act as a reverse proxy and load balancer, distributing client requests to a backend pool of servers.
 - High availability and scalability: Learn how load balancing increases availability by ensuring that if one application server fails, others can continue to handle requests.
 - Performance improvement: See how load balancing helps improve application performance by distributing the workload across multiple servers, preventing any single server from becoming a bottleneck.
 - How to inspect active ports on remote servers using ss
