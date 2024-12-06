# Instalar MySQL 8.0 en Fedora Server 40

* Instalar servidor y cliente MySQL
* Instalar cliente MySQL

## Instalar servidor y cliente MySQL 8.0

### Preparar la instalación de MySQL

```bash
$ ls -la
total 29552
drwx------. 2 alumno alumno     4096 dic  6 12:31 .
drwxr-xr-x. 3 root   root         20 dic  6 12:07 ..
-rw-r--r--. 1 alumno alumno       18 feb  9  2024 .bash_logout
-rw-r--r--. 1 alumno alumno      144 feb  9  2024 .bash_profile
-rw-r--r--. 1 alumno alumno      522 feb  9  2024 .bashrc
-rw-r--r--. 1 alumno alumno  3516681 dic  6 12:27 mysql-community-client-8.0.40-10.fc40.x86_64.rpm
-rw-r--r--. 1 alumno alumno  1311599 dic  6 12:30 mysql-community-client-plugins-8.0.40-10.fc40.x86_64.rpm
-rw-r--r--. 1 alumno alumno   569678 dic  6 12:27 mysql-community-common-8.0.40-10.fc40.x86_64.rpm
-rw-r--r--. 1 alumno alumno  2378846 dic  6 12:31 mysql-community-icu-data-files-8.0.40-10.fc40.x86_64.rpm
-rw-r--r--. 1 alumno alumno  1475148 dic  6 12:27 mysql-community-libs-8.0.40-10.fc40.x86_64.rpm
-rw-r--r--. 1 alumno alumno 20978064 dic  6 12:27 mysql-community-server-8.0.40-10.fc40.x86_64.rpm
```

### Instalar el servidor de MySQL

```bash
$ sudo dnf localinstall mysql-community-client-8.0.40-10.fc40.x86_64.rpm mysql-community-client-plugins-8.0.40-10.fc40.x86_64.rpm mysql-community-common-8.0.40-10.fc40.x86_64.rpm mysql-community-icu-data-files-8.0.40-10.fc40.x86_64.rpm mysql-community-libs-8.0.40-10.fc40.x86_64.rpm mysql-community-server-8.0.40-10.fc40.x86_64.rpm
```

```bash
$ sudo systemctl start mysqld.service
$ sudo systemctl enable mysqld.service
```

```bash
$ systemctl status mysqld.service
● mysqld.service - MySQL Server
     Loaded: loaded (/usr/lib/systemd/system/mysqld.service; enabled; preset: disabled)
    Drop-In: /usr/lib/systemd/system/service.d
             └─10-timeout-abort.conf
     Active: active (running) since Fri 2024-12-06 12:34:59 WET; 8s ago
       Docs: man:mysqld(8)
             http://dev.mysql.com/doc/refman/en/using-systemd.html
   Main PID: 1642 (mysqld)
     Status: "Server is operational"
      Tasks: 38 (limit: 4643)
     Memory: 472.3M (peak: 486.4M)
        CPU: 3.901s
     CGroup: /system.slice/mysqld.service
             └─1642 /usr/sbin/mysqld

dic 06 12:34:42 localhost.localdomain systemd[1]: Starting mysqld.service - MySQL Server...
dic 06 12:34:57 localhost.localdomain (mysqld)[1642]: mysqld.service: Referenced but unset environment variable evaluates to an empty string: MYSQLD_OPTS
dic 06 12:34:59 localhost.localdomain systemd[1]: Started mysqld.service - MySQL Server.
```

```bash
$ mysql --version
mysql  Ver 8.0.40 for Linux on x86_64 (MySQL Community Server - GPL)
```

```bash
$ sudo  grep 'temporary password' /var/log/mysqld.log
2024-12-06T08:46:10.503925Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: hDRh.Hrq>1Ab
```

```bash
$ sudo mysql_secure_installation

Securing the MySQL server deployment.

Enter password for user root:

The existing password for the user account root has expired. Please set a new password.

New password:

Re-enter new password:
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
Your MySQL connection id is 12
Server version: 8.0.40 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

### Permitir peticiones entrantes al puerto 3306 en Fedora

Por defecto el firewall de Fedora viene activado, así que tendremos que permitir peticiones entrantes al servicio MySQL a través del puerto 3306:

```bash
$ sudo firewall-cmd --permanent --add-port=3306/tcp
success
```

```bash
$ sudo firewall-cmd --reload
success
```

```bash
$ sudo firewall-cmd --list-ports
3306/tcp
```

## Instalar cliente MySQL 8.0

### Preparar la instalación de MySQL

#TODO
