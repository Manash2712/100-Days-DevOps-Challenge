### Solution

For this task login to each of the app sever and check for the status of apache httpd service using below command.
```
sudo systemctl status httpd
```

After checking above we can determine httpd service is not running on app server 1.

Let's try to start the httpd service on app server 1.
```
systemctl start httpd
```

By running this got the below error.

```
[root@stapp01 ~]# systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since Wed 2025-11-12 17:15:46 UTC; 1min 21s ago
     Docs: man:httpd(8)
           man:apachectl(8)
  Process: 660 ExecStop=/bin/kill -WINCH ${MAINPID} (code=exited, status=1/FAILURE)
  Process: 659 ExecStart=/usr/sbin/httpd $OPTIONS -DFOREGROUND (code=exited, status=1/FAILURE)
 Main PID: 659 (code=exited, status=1/FAILURE)

Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com systemd[1]: Starting The Apache HTTP S...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com httpd[659]: (98)Address already in use...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com httpd[659]: no listening sockets avail...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com httpd[659]: AH00015: Unable to open logs
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: main proces...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com kill[660]: kill: cannot find process ""
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service: control pro...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com systemd[1]: Failed to start The Apache...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com systemd[1]: Unit httpd.service entered...
Nov 12 17:15:46 stapp01.stratos.xfusioncorp.com systemd[1]: httpd.service failed.
Hint: Some lines were ellipsized, use -l to show in full.
[root@stapp01 ~]#
```

From the above error, we can see the port for which httpd is configured is already in use. 
To identify the process which is using the port use below command.
```
sudo netstat -tulnp | grep 8082
```

Now kill the process with process id which we got from above command, in this case it is 634.
```
sudo kill 634
```

Now lets try to start the httpd service.
```
systemctl start httpd
```

Lets check the status of httpd
```
systemctl status httpd
```

Now the httpd service is running on the server.

