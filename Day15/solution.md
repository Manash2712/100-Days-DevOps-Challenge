### Solution

Here is the approach you can try for this task.

First ssh to the app server 3.
```
ssh banner@stapp03
```

Install nginx on the server.
```
sudo yum install nginx
```

Create a directory to store the certificates.
```
mkdir -p /etc/nginx/pki/ssl
```

Copy the certificates from /tmp to the above directory
```
cp /tmp/nautilus.* /etc/nginx/pki/ssl/
```

Update the index.html, remove the content of the file and put Welcome! text in it then save and exit.
```
sudo vi /usr/share/nginx/html/index.html
```

Now edit the conf file for nginx and uncomment the code for TLS request and update the location of certificates as per the above certificates location. Then save and exit.
```
vi /etc/nginx/nginx.conf
```

Test the nginx configuration for syntax errors.
```
sudo nginx -t
```

Restart nginx service.
```
sudo systemctl restart nginx
```

Test the connection from jumphost for https connection.
```
curl -Ik https://<App_Server_2_IP>/
```
_Note: The -k flag ignores SSL certificate verification (since it’s self-signed)._

Output: HTTP 200 OK — Secured content successfully served! 

#### Key Learning Objectives from Day 15
 - Nginx Installation and Configuration: Learn to install Nginx and configure it to serve web content.
 - SSL Certificate Deployment: Practice deploying a self-signed SSL certificate and private key to secure a web server, a crucial step for HTTPS.
 - Basic HTML and Document Root: Create a simple HTML file and place it in the correct directory for Nginx to serve as the homepage.
 - Testing Secure Access: Use the curl command to verify that the Nginx server is accessible via HTTPS, using the correct hostname or IP address.
 - Integration with Previous Tasks: This task is part of a progression that includes previous work on application deployment and security, solidifying practical skills in managing and securing web servers. 
