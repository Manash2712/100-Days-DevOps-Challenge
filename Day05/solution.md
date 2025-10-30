### Solution

SELinux is a special security system built into Linux computers. The main purpose of the SELinux is to control what different programs and users are allowed to access on the computer.
With SELinux, each program and user is limited in what they can see and do. 

Follow the below steps to install and disable SELinux.

**Step 1:** Install SELinux.
```
sudo dnf install selinux-policy selinux-policy-targeted policycoreutils
```
**Step 2:** Edit the SELinux configuration file 

- Open the configuration file in a text editor like nano or vim.
```
sudo vi /etc/selinux/config
```
- Locate the line that starts with SELINUX= and change enforcing to disabled.
  
    - Change this:
   
    ```
    SELINUX=enforcing
    ```
   - To this:
  ```
  SELINUX=disabled
  ```
*Bonus tip: you can check the selinux status using the below command*
```
sestatus
```
