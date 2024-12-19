# Instalar MySQL 8.0 en Ubuntu Server 22.04

* Instalar servidor y cliente MySQL
    * Acceso a MySQL Server
* Instalar cliente MySQL

## Instalar servidor y cliente MySQL 8.0

Descargar los paquetes necesarios de la URL [https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/):

* __Select Version__: 8.0.40
* __Select Operating System__: Ubuntu Linux
* __Select OS Version__: Ubuntu Linux 24.04 (x86, 64-bit)

```bash
$ ls -l
total 33140
-rw-rw-r-- 1 alumno alumno    58808 dic 13 05:47 mysql-client_8.0.40-1ubuntu22.04_amd64.deb
-rw-rw-r-- 1 alumno alumno    60094 dic 13 05:47 mysql-common_8.0.40-1ubuntu22.04_amd64.deb
-rw-rw-r-- 1 alumno alumno  2228606 dic 13 05:47 mysql-community-client_8.0.40-1ubuntu22.04_amd64.deb
-rw-rw-r-- 1 alumno alumno  2131742 dic 13 05:47 mysql-community-client-core_8.0.40-1ubuntu22.04_amd64.deb
-rw-rw-r-- 1 alumno alumno  1442522 dic 13 05:47 mysql-community-client-plugins_8.0.40-1ubuntu22.04_amd64.deb
-rw-rw-r-- 1 alumno alumno    70592 dic 13 05:47 mysql-community-server_8.0.40-1ubuntu22.04_amd64.deb
-rw-rw-r-- 1 alumno alumno 27924720 dic 13 05:47 mysql-community-server-core_8.0.40-1ubuntu22.04_amd64.deb
```

Realizar la instalación de todos los paquetes `.deb`:

```bash
$ sudo apt install ./*.deb
```

![][06]

![][07]

![][09]

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

Con este comando, verificamos si el servicio MySQL está activo y funcionando. La salida mostrará el mensaje `Active: active (running)` si el servicio está en ejecución, junto con detalles adicionales como el tiempo que ha estado activo y el ID del proceso.

Comprobar la versión de MySQL instalada:

```bash
$ mysql -V
mysql  Ver 8.0.40 for Linux on x86_64 (MySQL Community Server - GPL)
```

Este comando muestra la versión de MySQL instalada en el sistema, confirmando que se ha instalado correctamente.

### Acceso a MySQL Server

Utilizar el cliente MySQL para acceder al servidor MySQL:

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

El comando `mysql -u root -p` se utiliza para acceder a la consola de MySQL como un usuario específico (en este caso, root):

* __mysql__: es el cliente de MySQL. Cuando ejecutas este comando, intentas iniciar sesión en MySQL y abrir la interfaz de línea de comandos de MySQL.
* __-u root__: la opción -u especifica el usuario con el cual deseas acceder a MySQL. En este ejemplo, root es el nombre del usuario de MySQL que se está usando. Puedes reemplazar root con cualquier nombre de usuario válido en tu sistema MySQL.
* __-p__: este parámetro indica que se solicitará una contraseña al intentar iniciar sesión. Al usar _-p_, MySQL te pedirá que ingreses la contraseña correspondiente al usuario especificado (root en este caso) antes de concederte acceso.

Este comando abre el cliente MySQL con el usuario root, solicitando la contraseña. Una vez autenticado, accedes a la consola de MySQL para realizar consultas y configuraciones.

Para salir de la terminal:

```bash
mysql> exit
Bye
$
```

Una vez terminado, se puede salir de la consola de MySQL escribiendo exit y presionando `Enter`.

## Instalar cliente MySQL 8.0

Descargar los paquetes necesarios de la URL [https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/):

* __Select Version__: 8.0.40
* __Select Operating System__: Ubuntu Linux
* __Select OS Version__: Ubuntu Linux 24.04 (x86, 64-bit)

```bash
$ ls -l
total 5592
drwxr-xr-x  3 alumno alumno    4096 dic 19 09:35 .
drwxr-x--- 17 alumno alumno    4096 dic 13 05:56 ..
-rw-rw-r--  1 alumno alumno   57774 dic 19 09:34 mysql-client_8.0.40-1ubuntu24.04_amd64.deb
-rw-rw-r--  1 alumno alumno   59074 dic 19 09:34 mysql-common_8.0.40-1ubuntu24.04_amd64.deb
-rw-rw-r--  1 alumno alumno 2073356 dic 19 09:34 mysql-community-client_8.0.40-1ubuntu24.04_amd64.deb
-rw-rw-r--  1 alumno alumno 2131712 dic 19 09:35 mysql-community-client-core_8.0.40-1ubuntu24.04_amd64.deb
-rw-rw-r--  1 alumno alumno 1376574 dic 19 09:34 mysql-community-client-plugins_8.0.40-1ubuntu24.04_amd64.deb
```

Realizar la instalación de todos los paquetes `.deb`:

```bash
$ sudo apt install ./*.deb
```

Comprobar la versión del cliente:

```bash
$ mysql -V
mysql  Ver 8.0.40 for Linux on x86_64 (MySQL Community Server - GPL)
```

Este comando muestra la versión de MySQL instalada en el sistema, confirmando que se ha instalado correctamente.

[06]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql01.png "06"
[07]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql02.png "07"
[09]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql04.png "09"
