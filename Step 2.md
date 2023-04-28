# STEP 2 — INSTALLING MYSQL

Now that I have a web server up and running, I need to install a Database Management System (DBMS) to be able to store and manage data for my site in a relational database. MySQL is a popular relational database management system used within PHP environments, so I will use it in our project.

```
$ sudo apt install mysql-server
```
When prompted, confirm installation by typing Y, and then ENTER.

When the installation is finished, log in to the MySQL console by typing:
```
$ sudo mysql
```
This will connect to the MySQL server as the administrative database user root, which is inferred by the use of sudo when running this command. We should see output like this:
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.22-0ubuntu0.20.04.3 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```
It’s recommended that we run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to my database system. Before running the script I will set a password for the root user, using mysql_native_password as default authentication method. I'm defining this user’s password as PassWord.1.
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
```
Exit the MySQL shell with:
```
mysql> exit
```
Start the interactive script by running:
```
$ sudo mysql_secure_installation
```
This will ask if I want to configure the VALIDATE PASSWORD PLUGIN.

Note: Enabling this feature is something of a judgment call. If enabled, passwords which don’t match the specified criteria will be rejected by MySQL with an error. It is safe to leave validation disabled, but we should always use strong, unique passwords for database credentials.

Answer Y for yes, or anything else to continue without enabling.
```
VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:
```
If we answer “yes”, we'll be asked to select a level of password validation. If I enter 2 for the strongest level, I will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words e.g PassWord.1.
There are three levels of password validation policy:
```
LOW    Length >= 8
MEDIUM Length >= 8, numeric, mixed case, and special characters
STRONG Length >= 8, numeric, mixed case, special characters and dictionary              file

Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1
```
Regardless of whether I chose to set up the VALIDATE PASSWORD PLUGIN, my server will next ask you to select and confirm a password for the MySQL root user. This is not to be confused with the system root. The database root user is an administrative user with full privileges over the database system. Even though the default authentication method for the MySQL root user dispenses the use of a password, even when one is set, I will  define a strong password here as an additional safety measure. 

If you enabled password validation, you’ll be shown the password strength for the root password you just entered and your server will ask if you want to continue with that password. If you are happy with your current password, enter Y for “yes” at the prompt:
```
Estimated strength of the password: 100 
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
```
For the rest of the questions, press Y and hit the ENTER key at each prompt. This will prompt me to change the root password, remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes I have made.

I will test if I'm able to log in to the MySQL console by typing:
```
$ sudo mysql -p
```
Notice the -p flag in this command, which will prompt you for the password used after changing the root user password.

To exit the MySQL console, type:
```
mysql> exit
```
Notice that you need to provide a password to connect as the root user.

For increased security, it’s best to have dedicated user accounts with less expansive privileges set up for every database, especially if you plan on having multiple databases hosted on your server.
```
Note: At the time of this writing, the native MySQL PHP library mysqlnd doesn’t support caching_sha2_authentication, the default
authentication method for MySQL 8. For that reason, when creating database users for PHP applications on MySQL 8, you’ll need to
make sure they’re configured to use mysql_native_password instead. We’ll demonstrate how to do that in Step 6.
```
Your MySQL server is now installed and secured. Next, we will install PHP, the final component in the LEMP stack.
