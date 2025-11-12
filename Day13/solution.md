### Solution

iptables is a command-line utility in Linux that configures the kernel's packet filtering firewall by creating and managing rules. 
It allows administrators to control network traffic by defining how incoming and outgoing packets are handled, enabling them to block or allow specific connections, 
manage network address translation (NAT), and perform other networking functions. 

Basic Syntax of iptables command:
 - sudo iptables: This executes the iptables command with superuser privileges.
 - \-A INPUT: Appends a new rule to the INPUT chain. The INPUT chain handles incoming traffic destined for the local system.
 - \-p tcp: Specifies the protocol as TCP. You can also use -p udp for UDP ports.
 - \--dport 80: Matches packets destined for destination port 80.
 - \-j DROP: Specifies the target action for matching packets as DROP. This silently discards the packets, making the port appear unreachable. An alternative is -j REJECT, which sends an error message back to the sender (e.g., "Connection refused").
 - \-j ACCEPT: Specifies the action to take, which is to accept the connection.

Built-in chains
 - INPUT: This chain handles packets that are destined for the local machine itself.
 - OUTPUT: This chain handles packets that are created by the local machine and are leaving its network interface.
 - FORWARD: This chain handles packets that are being routed through the machine to another destination, rather than being consumed by the local machine itself. This is common on routers or gateways.
 - PREROUTING: This chain applies rules to incoming packets before any routing decisions are made. It's often used for altering the destination IP or port of a packet.
 - POSTROUTING: This chain applies rules after a routing decision has been made and the packet is about to leave the network interface. It's commonly used for Source Network Address Translation (SNAT) or to modify the source IP or port of outgoing packets. 

For this task login to each server via ssh and follow the below steps on every app server.

Step 1: Install iptable on the server.
```
yum install iptables-services -y
```

Verify the installation using below:
```
iptables --version
```

Step 2: Now add rule to block all incoming traffic using the below command.
```
sudo iptables -A INPUT -p tcp --dport 6200 -j DROP
```

Step 3: Add rule to allow incoming traffic from LBR.
```
sudo iptables -I INPUT -s 172.16.238.14 -p tcp --dport 6200 -j ACCEPT
```

Ste 4: Verify the rules using below command.
```
sudo iptables -L
```

Start the iptable services.
```
sudo systemctl start iptables
```

Step 5: Save the iptable rules so they are automatically applied after reboot.
```
sudo service iptables save
```
or
```
sudo iptables-save > /etc/sysconfig/iptables
```

Step 6: Enable the iptables service to start on boot, using the command.
```
sudo systemctl enable iptables
```

Now check the connection from LBR server.
```
curl http://stapp01:6200
```

