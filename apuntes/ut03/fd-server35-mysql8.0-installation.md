# Instalar MySQL 8.0 en Fedora Server 35

* Instalar servidor y cliente MySQL
* Instalar cliente MySQL

## Instalar servidor y cliente MySQL 8.0

### Preparar la instalación de MySQL

```bash
$ wget https://dev.mysql.com/get/mysql80-community-release-fc35-1.noarch.rpm
```

```bash
$ sudo dnf localinstall mysql80-community-release-fc35-1.noarch.rpm
```

```bash
$ dnf repolist enabled | grep "mysql.*-community.*"
mysql-connectors-community       MySQL Connectors Community
mysql-tools-community            MySQL Tools Community
mysql80-community                MySQL 8.0 Community Server
```

```bash
$ sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
```

### Instalar el servidor de MySQL

```bash
$ dnf install mysql-community-server
```

```bash
$ sudo service mysqld start
$ sudo systemctl enable mysqld.service
```

```bash
$ systemctl status mysqld.service
● mysqld.service - MySQL Server
     Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; vendor preset: disabled)
     Active: active (running) since Fri 2024-12-06 08:46:20 WET; 32s ago
       Docs: man:mysqld(8)
             http://dev.mysql.com/doc/refman/en/using-systemd.html
   Main PID: 30593 (mysqld)
     Status: "Server is operational"
      Tasks: 39 (limit: 4649)
     Memory: 471.0M
        CPU: 3.110s
     CGroup: /system.slice/mysqld.service
             └─ 30593 /usr/sbin/mysqld

dic 06 08:46:04 fedora systemd[1]: Starting MySQL Server...
dic 06 08:46:20 fedora systemd[1]: Started MySQL Server.
```

```bash
$ mysql --version
mysql  Ver 8.0.31 for Linux on x86_64 (MySQL Community Server - GPL)
```

```bash
$ sudo  grep 'temporary password' /var/log/mysqld.log
2024-12-06T08:46:10.503925Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: hDRh.Hrq>1Ab
```

```bash
$ sudo mysql_secure_installation

Securing the MySQL server deployment.

Enter password for user root:
The 'validate_password' component is installed on the server.
The subsequent steps will run with the existing configuration
of the component.
Using existing password for root.

Estimated strength of the password: 100
Change the password for root ? ((Press y|Y for Yes, any other key for No) : y

New password:

Re-enter new password:

Estimated strength of the password: 100
Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : y
By default, a MySQL installation has an anonymous user,
allowing anyone to log into MySQL without having to have
a user account created for them. This is intended only for
testing, and to make the installation go a bit smoother.
You should remove them before moving into a production
environment.

Remove anonymous users? (Press y|Y for Yes, any other key for No) : y
Success.


Normally, root should only be allowed to connect from
'localhost'. This ensures that someone cannot guess at
the root password from the network.

Disallow root login remotely? (Press y|Y for Yes, any other key for No) : y
Success.

By default, MySQL comes with a database named 'test' that
anyone can access. This is also intended only for testing,
and should be removed before moving into a production
environment.


Remove test database and access to it? (Press y|Y for Yes, any other key for No) : y
 - Dropping test database...
Success.

 - Removing privileges on test database...
Success.

Reloading the privilege tables will ensure that all changes
made so far will take effect immediately.

Reload privilege tables now? (Press y|Y for Yes, any other key for No) : y
Success.

All done!
```

```bash
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 16
Server version: 8.0.31 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

## Instalar cliente MySQL 8.0

### Preparar la instalación de MySQL

#TODO
