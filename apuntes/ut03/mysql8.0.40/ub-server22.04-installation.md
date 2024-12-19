# Instalar MySQL 8.0 en Ubuntu Server 22.04

* Instalar servidor y cliente MySQL
* Instalar cliente MySQL

## Instalar servidor y cliente MySQL 8.0

### Preparar la instalación de MySQL

Descargar el paquete de configuración de MySQL APT:

```bash
$ wget https://dev.mysql.com/get/mysql-apt-config_0.8.33-1_all.deb
```

Este comando descarga el paquete de configuración de MySQL APT desde el sitio oficial de MySQL. Este archivo permite gestionar las versiones de MySQL que queremos instalar y facilita la instalación de MySQL a través del sistema de paquetes apt.

Verificar el archivo descargado:

```bash
$ ls -l *.deb
total 60
drwxr-x--- 4 alumno alumno  4096 oct 27 22:12 .
drwxr-xr-x 3 root   root    4096 oct  4 07:22 ..
-rw-rw-r-- 1 alumno alumno 18072 sep 27 08:45 mysql-apt-config_0.8.33-1_all.deb
```

Este comando lista el archivo .deb descargado para confirmar su presencia en el directorio. La salida muestra información detallada del archivo, como el tamaño y la fecha de modificación.

Instalar el paquete de configuración de MySQL APT:

```bash
$ sudo dpkg -i mysql-apt-config_0.8.33-1_all.deb
```

![][01]

![][02]

![][03]

![][04]

![][05]

Con este comando, utilizamos dpkg para instalar el archivo .deb descargado. Esto configura el sistema de paquetes APT para que pueda gestionar las versiones de MySQL y sus componentes.

Actualizar los repositorios de APT:

```bash
$ sudo apt update
```

Este comando actualiza la lista de paquetes disponibles y versiones, incluyendo los de MySQL, que se han añadido a los repositorios mediante la instalación del paquete _.deb_ anterior.

### Instalar el servidor de MySQL

Instalar MySQL Server y MySQL Client:

```bash
$ sudo apt install -f mysql-client=8.0* mysql-community-server=8.0* mysql-server=8.0*
```

![][06]

![][07]

![][08]

![][09]

Instalamos MySQL Server y el cliente de MySQL, especificando la versión 8.0. Esto garantiza que se instalen las versiones deseadas del servidor y cliente MySQL.

Verificar el estado del servicio MySQL:

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
alumno@ubuntu-server2204:~$
```

Una vez terminado, se puede salir de la consola de MySQL escribiendo exit y presionando `Enter`.

Referencia(s):
* [https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/](https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/)

## Instalar cliente MySQL 8.0

### Preparar la instalación de MySQL

Descargar el paquete de configuración de MySQL APT:

```bash
$ wget https://dev.mysql.com/get/mysql-apt-config_0.8.33-1_all.deb
```

Este comando descarga el paquete de configuración de MySQL APT desde el sitio oficial de MySQL. Este archivo permite gestionar las versiones de MySQL que queremos instalar y facilita la instalación de MySQL a través del sistema de paquetes apt.

Verificar el archivo descargado:

```bash
$ ls -l *.deb
total 60
drwxr-x--- 4 alumno alumno  4096 oct 27 22:12 .
drwxr-xr-x 3 root   root    4096 oct  4 07:22 ..
-rw-rw-r-- 1 alumno alumno 18072 sep 27 08:45 mysql-apt-config_0.8.33-1_all.deb
```

Este comando lista el archivo .deb descargado para confirmar su presencia en el directorio. La salida muestra información detallada del archivo, como el tamaño y la fecha de modificación.

Instalar el paquete de configuración de MySQL APT:

```bash
$ sudo dpkg -i mysql-apt-config_0.8.33-1_all.deb
```

![][01]

![][02]

![][03]

![][04]

![][05]

Con este comando, utilizamos dpkg para instalar el archivo .deb descargado. Esto configura el sistema de paquetes APT para que pueda gestionar las versiones de MySQL y sus componentes.

Actualizar los repositorios de APT:

```bash
$ sudo apt update
```

Este comando actualiza la lista de paquetes disponibles y versiones, incluyendo los de MySQL, que se han añadido a los repositorios mediante la instalación del paquete _.deb_ anterior.

### Instalar el cliente de MySQL

Instalar cliente de MySQL:

```bash
$ sudo apt install -f mysql-client=8.0*
```

Instalamos el cliente de MySQL, especificando la versión 8.0. Esto garantiza que se instale la versión deseada del cliente MySQL.

Comprobar la versión de MySQL instalada:

```bash
$ mysql -V
mysql  Ver 8.0.40 for Linux on x86_64 (MySQL Community Server - GPL)
```

Este comando muestra la versión de MySQL instalada en el sistema, confirmando que se ha instalado correctamente.

[01]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/configurar-apt01.png "01"
[02]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/configurar-apt02.png "02"
[03]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/configurar-apt03.png "03"
[04]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/configurar-apt04.png "04"
[05]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/configurar-apt05.png "05"
[06]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql01.png "06"
[07]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql02.png "07"
[08]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql03.png "08"
[09]: ../../img/ut03/instalar-mysql-8.0-ubuntu-server-22.04/instalar-mysql04.png "09"
