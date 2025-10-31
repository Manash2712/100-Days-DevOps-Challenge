### Solution

To establish password-less SSH authentication from the thor user on the jump host to all application servers, we will need to generate SSH key pair on the jumphost 
and then copy the public keys to the respective application servers inside ~/.ssh/authorized_keys file.

Follow the below steps for performing this task.

 - Step 1: Generate the keys on the jump server, use below command to generate the keys. Press enter to escape the questions.
```
ssh-keygen -t rsa -b 4096
```
 - Step 2: Login to the application server
```
ssh steve@stapp02
```
 - Step 3: Create ssh directory if does not exist
```
mkdir ~/.ssh
```
 - Step 4: Create authorized_keys file inside the ssh directory and copy the public key file contents to it and save the file.
```
vi ~/.ssh/authorized_keys
```
 - Step 5: Modify the authorized_keys file permission to 600
```
chmod 600 ~/.ssh/authorized_keys
```
 - Step 6: Verfiify the changes, by trying to login to the app server again by using ssh, this time password will not be required.
```
ssh steve@stapp02
```
