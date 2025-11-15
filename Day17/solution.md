### Solution

For this task lets login to the db server.
```
ssh peter@stdb01
```

Now let's access the PostgreSQL Command Line by Switching to the postgres user to manage the database using the command:
```
psql -U postgres
```

To create the user use below command.
```
CREATE USER kodekloud_top WITH ENCRYPTED PASSWORD 'YchZHRcLkL';
```

Now in psql command line. run below command to create a db with name _kodekloud_db07_
```
CREATE DATABASE kodekloud_db7;
```

For grating the _kodekloud_top_ user permissions on _kodekloud_db07_, run below command in psql command line.
```
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db7 TO kodekloud_top;
```

To verify if the user has been created successfully use below command.
``` 
\du
```

TO check if the database has been created successfully use below.
```
\l
```

To exit the psql command line use below:
```
\q
```

#### Learnings from this task:
 - How to use psql command line.
 - How to create a user with secure password in postgres database.
 - How to create a database in postgres.
 - How to grant full privileges to a user for a database in postgres.
