### Solution

Tomcat is an open-source Java container that runs Java applications, specifically those using Java Servlets and JavaServer Pages (JSP). 
It functions as a web server and servlet container, processing dynamic content for websites and providing the environment for Java-based web applications to run.

SSH to the server using below command.
```
ssh steve@stapp02
```

Lets do this task step by step, to install tomcat use below command.
```
yum install -y tomcat
```

Verify the tomcat service using below command.
```
systemctl status tomcat
```

Now to configure tomcat to run on port 5004 , we will need to edit the configuration file ```/usr/share/tomcat/conf/server.xml```.

Open the configuration file.
```
sudo vi /usr/share/tomcat/conf/server.xml
```

Edit the default connector port from:
```
xml

<Connector port=”8080" protocol=”HTTP/1.1" … />
```
To:
```
xml

<Connector port=”5004" protocol=”HTTP/1.1"

connectionTimeout=”20000"

redirectPort=”8443" />
```
Save the changes with “:wq”

Restart the tomcat service
```
sudo systemctl restart tomcat
```

To deploy the ROOT.war file follow below steps.

Copy the ROOT.war file from jumphost to appserver2
```
scp /tmp/ROOT.war steve@stapp02:/tmp/
```

Move the .WAR file to the webapps/ directory where Tomcat automatically looks for WAR files to deploy
```
mv /tmp/ROOT.war /usr/share/tomcat/webapps/ROOT.war
```

Give the correct ownership of tomcat to ROOT.war file ensuring it has permission to read and deploy the file.
```
chown tomcat:tomcat /usr/share/tomcat/webapps/ROOT.war
```

Restart tomcat service to deploy the new ROOT.war automatically.
```
sudo systemctl restart tomcat
```

Verify the deployment using below command.
```
curl http://stapp02:5004
```

And it worked! The Java application was successfully deployed and accessible via the base URL on the configured port.

Lesson learnt:
This task provides practical experience in web server management, application deployment, file transfer, and permissions management, which are key skills for a DevOps engineer. 
