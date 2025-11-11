### Solution

To begin with the solution lets first test the status of apache service running on app server 1.
```
systemctl status httpd
```

From the above commands output we cann see the status of service is in failed state. And we can see there is some port conflict, 
port 6100 is being used by some other process.

To find which process is using the port 6100 use below command.
```
sudo netstat -tulpn | grep 6100
```

By running above command we can see the process id associated with port 6100, here it is 502. To kill the process use below command, to free the port.
```
sudo kill 502
```

Now lets try starting the httpd process.
```
sudo systemctl start httpd
```

No error from above commands, lets checck the status of process.
```
systemctl status httpd
```

Even with Apache running, it remained unreachable from the jump host. This pointed to a firewall issue. 

Check the iptables rules using below command.
```
sudo iptables -L
```

A check of the iptables rules showed a global REJECT rule that was blocking all incoming traffic. 
The specific ACCEPT rule for port 6100 was missing, and it's essential to add it.

Now lets add the accept rule for port 6100, to add the rule use below command.
```
iptables -I INPUT -p tcp --dport 6100 -j ACCEPT
```

Now the rule has been added to accept traffic on port 6100, but this rule will be lost once the server gets rebooted.
To save it permanently use below.
```
iptables-save > /etc/sysconfig/iptables
```

Now lets try accessing the website using curl command.
```
curl http://stapp01:6100
```

Bingoo!! It worked.

#### Learning Outcome: 
This challenge typically focuses on troubleshooting and network configuration, specifically resolving issues like port binding conflicts, 
restarting services, and adjusting firewall rules to allow external access. 
This hands-on task reinforces practical skills in diagnosing and fixing common problems in a DevOps environment, such as a service not listening on a custom port.

 - Key Skills Reinforced:

    - Process Management: Killing processes that are occupying a required port.
    - Service Management: Restarting services and verifying they are listening on the correct port.
    - Network Configuration: Adjusting firewall rules (e.g., iptables) to allow specific ports to be accessible from outside the server.
    - Connectivity Testing: Using tools like curl to verify end-to-end connectivity after making changes.
