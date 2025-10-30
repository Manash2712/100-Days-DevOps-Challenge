### Solution
To change the file permissions in linux we can use chmod which stands for change mode.

Follow the below steps to change the permission of file.

**Step 1:** Login to the server 
```
ssh steve@stapp02
```

**Step 2:** Change the current working directory to /tmp, as the file is stored there.
```
cd /tmp/
```

**Step 3:** Change the file permissions. Here we can use 755 which means the user (current owner of file) will get read, write and execute permissions where as group and others will have read and execute permissions.
```
chmod 755 xfusioncorp.sh
```

**Step 4:** Verify the file permissions
```
ls -l xfusioncorp.sh
```
