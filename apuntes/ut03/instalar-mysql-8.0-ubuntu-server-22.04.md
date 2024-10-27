# Instalar MySQL 8.0 en Ubuntu Server 22.04

```bash
$ wget https://dev.mysql.com/get/mysql-apt-config_0.8.33-1_all.deb
```

```bash
$ ls -l *.deb
total 60
drwxr-x--- 4 alumno alumno  4096 oct 27 22:12 .
drwxr-xr-x 3 root   root    4096 oct  4 07:22 ..
-rw-rw-r-- 1 alumno alumno 18072 sep 27 08:45 mysql-apt-config_0.8.33-1_all.deb
```

```bash
$ sudo apt install ./mysql-apt-config_0.8.33-1_all.deb
```

```bash
$ sudo apt update
```

```bash
$ sudo apt install -f mysql-client=8.0* mysql-community-server=8.0* mysql-server=8.0*
```

```bash
$ systemctl status mysql.service
● mysql.service - MySQL Community Server
     Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2024-10-27 22:31:15 UTC; 41s ago
       Docs: man:mysqld(8)
             http://dev.mysql.com/doc/refman/en/using-systemd.html
   Main PID: 5250 (mysqld)
     Status: "Server is operational"
      Tasks: 38 (limit: 2226)
     Memory: 360.5M
        CPU: 661ms
     CGroup: /system.slice/mysql.service
             └─5250 /usr/sbin/mysqld

oct 27 22:31:13 ubuntu-server2204 systemd[1]: Starting MySQL Community Server...
oct 27 22:31:15 ubuntu-server2204 systemd[1]: Started MySQL Community Server.
```

```bash
$ mysql -V
mysql  Ver 8.0.40 for Linux on x86_64 (MySQL Community Server - GPL)
```

```bash
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.40 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

Para salir de la terminal:

```bash
mysql> exit
Bye
alumno@ubuntu-server2204:~$
```
