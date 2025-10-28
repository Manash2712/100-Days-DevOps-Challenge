### Solution:
To disable root login on all the app servers follow below steps for all the servers.

Step 1:
Access the server: Access the server by using ssh command, ssh user_name@server_name/ip.
```
ssh tony@stapp01
```
Step 2:
Edit ssh configuration file (/etc/ssh/sshd_config). You may use vi or nano editor based on your preference.
```
vi /etc/ssh/sshd_config
```
Step 3:
Modify Modify PermitRootLogin, find PermitRootLogin line in the config file and change its value to no from yes, if the line is commented uncomment it and put the value to no
```
PermitRootLogin no
```
Step 4:
Restart sshd service
```
sudo systemctl restart sshd
```
