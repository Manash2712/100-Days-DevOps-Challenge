### Solution

For this task first we will need to set up password less authentication from appserver3 to backup server, follow the below steps to set this up.

Step 1: Login to appserver 3
```
ssh banner@stapp03
```

Step 2: Create ssh key.
```
ssh-keygen -t rsa
```

Step 3: Login to the backup server
```
ssh clint@stbkp01
```

Step 4: Create a directory names .ssh
```
mkdir .ssh
```

Step 5: Copy the contents of id_rsa.pub file from app server and paste it in the new file named authorized_keys on backup server under .ssh directory and save it.
```
vi authorized_keys
```

Step 6: Change permissions of above file
```
chmod 600 authorized_keys
```

Step 7: Verify the passwordless authentication from app server, this should not ask for password.
```
ssh clint@stbkp01
```

Now password less authentication is set create the below script in /scripts/ directory of app server, with the name backup.sh

```

#!/bin/bash

# Script will create the backup of website stored in /var/www/html/official
# Then copy the backup to  Nautilus Backup Server
# Please keep in mind to have passwordless access setup for backup server.

# Create backup of website

zip -r /backup/xfusioncorp_official.zip /var/www/html/official

# copy the created archive to backup server
scp /backup/xfusioncorp_official.zip clint@stbkp01:/backup

```

Change the permission of above file to make it executable by other users.
```
chmod 755 backup.sh
```
