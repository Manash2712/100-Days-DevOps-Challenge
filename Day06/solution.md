### Solution

Before creating a cron job first lets understand what is a cron job. A cron job is a scheduled task on a Unix-like operating system that runs commands or scripts automatically at specified intervals. It uses a time-based scheduler, known as the "cron daemon," and is configured using a crontab, which is a file listing the commands and their schedules.

How it works
 - Cron daemon: A background process that checks crontab files for jobs to run.
 - Crontab: A configuration file where you define the schedule and the command to be executed.
 - Cron expression: A format used to specify the timing of a job, including the minute, hour, day of the month, month, and day of the week. For example, * * * * * would mean "every minute". 

Here's the breakdown of the standard five-field cron expression:
 - Minute: (0-59)
 - Hour: (0-23, 24-hour format)
 - Day of Month: (1-31)
 - Month: (1-12 or JAN-DEC)
 - Day of Week: (0-6 or SUN-SAT, where 0 and 7 both represent Sunday)

Special Characters:
 - \* (Asterisk): Represents all possible values for that field. For example, * in the minute field means "every minute."
 - , (Comma): Used to specify a list of values. For example, 1,15 in the day of month field means "on the 1st and 15th."
 - \- (Hyphen): Used to specify a range of values. For example, MON-FRI in the day of week field means "Monday through Friday."
 - / (Slash): Used to specify step values. For example, */5 in the minute field means "every 5 minutes." 0/15 in the minute field means "at minute 0, 15, 30, and 45."
 - ? (Question Mark): Used in the Day of Month or Day of Week field to indicate "no specific value." This is useful when you want to specify a schedule based on one of these fields but not the other. You cannot use * in both Day of Month and Day of Week simultaneously.
 - L (Last): Used in the Day of Month field to represent the last day of the month, or in the Day of Week field to represent the last instance of a specific day of the week in the month (e.g., 6L for the last Friday).
 - W (Weekday): Used in the Day of Month field to specify the nearest weekday to a given day. For example, 15W means the nearest weekday to the 15th of the month.
 - \# (Nth day of week): Used in the Day of Week field to specify the "nth" occurrence of a specific day of the week in the month. For example, 6#3 means the third Friday of the month. 

Now follow the below steps to perform this task:

 - Step 1: ssh to the server:
```
ssh steve@stapp02
```
 - Ste 2 : Install cronie
```
sudo dnf install cronie
```
 - Step 3: Start crond daemon
```
systemctl start crond
```
 - Step 4: Edit the crontab for root user and make the entry of cronjob you want to run and save the file.
```
sudo crontab -u root -e
```
- Put the below text in the file and save the file.
```
*/5 * * * * echo hello > /tmp/cron_text
```
 - Step 5: Check if the entry is present in crontab
```
sudo crontab -u root -l
``` 
