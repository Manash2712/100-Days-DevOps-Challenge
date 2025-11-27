### Solution

For this task forst lets login to the app server 2.
```
ssh steve@stapp02
```

Now lets install apache httpd on the app server.
```
yum install httpd -y
```

Now start and enable httpd service.
```
systemctl enable httpd
```
```
systemctl restart httpd
```

Now lets configure the httpd to listen on port 6200. Open the httpd conf file in vi editor.
```
vi /etc/httpd/conf/httpd.conf
```

Search for Listen 80 and change it to Listen 6200.
```
Listen 6200
```

Now copy the contents from jumphost to app server 2.
```
scp -r /home/thor/beta/ steve@stapp02:/tmp
```
```
scp -r /home/thor/demo/ steve@stapp02:/tmp
```

Copy the /beta and /demo from demo to /var/www/html directory.
```
cp -r beta/ /var/www/html/
```
```
cp -r demo/ /var/www/html/
```

Now in the httpd conf file at the end of file add below code.
```
<VirtualHost *:6200>
    DocumentRoot /var/www/html
    <Directory "/var/www/html">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

Restart httpd service.
```
systemctl restart httpd
```

Verify the result.
```
curl http://localhost:6200/beta/
```
```
curl http://localhost:6200/demo/
```
