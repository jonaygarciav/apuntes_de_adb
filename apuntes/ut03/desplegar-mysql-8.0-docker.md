# Desplegar un contenedor de MySQL 8.0 en Docker

* Introducción
* Contenedor sin persistencia
* Contenedor con persistencia
* Compartir una carpeta entre el Host y el contenedor
* Acceso externo al servicio del contenero

## Introducción

Imagen oficial de MySQL para Docker:
* [https://hub.docker.com/_/mysql](https://hub.docker.com/_/mysql)

## Descargar imagen de Mysql 8.0 para Docker

Descargar una Imagen de MySQL:

```
$ docker pull mysql/mysql-server:8.0
8.0: Pulling from mysql/mysql-server
6a4a3ef82cdc: Pull complete
5518b09b1089: Pull complete
b6b576315b62: Pull complete
349b52643cc3: Pull complete
abe8d2406c31: Pull complete
c7668948e14a: Pull complete
c7e93886e496: Pull complete
Digest: sha256:d6c8301b7834c5b9c2b733b10b7e630f441af7bc917c74dba379f24eeeb6a313
Status: Downloaded newer image for mysql/mysql-server:8.0
docker.io/mysql/mysql-server:8.0
```

* `docker pull`: descarga una imagen de Docker desde el Docker Hub o de otro registro de Docker configurado.
* `mysql/mysql-server:8.0`: especifica la imagen mysql/mysql-server con la etiqueta 8.0. La etiqueta indica la versión específica de MySQL que se descargará.

Docker verifica si la imagen ya está almacenada localmente. Si no lo está, comienza a descargar cada capa de la imagen, lo que se indica con la palabra Pull complete cuando se completa cada capa.

Ver las imágenes disponibles en el sistema local:

```
$ docker images
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
hello-world          latest    d2c94e258dcb   18 months ago   13.3kB
mysql/mysql-server   8.0       1d9c2219ff69   21 months ago   496MB
```
Este comando muestra todas las imágenes de Docker que se han descargado o creado localmente. Muestra la siguiente información:

* REPOSITORY: Nombre del repositorio de la imagen (por ejemplo, mysql/mysql-server).
* TAG: Etiqueta de la imagen, que suele representar la versión (por ejemplo, 8.0).
* IMAGE ID: Identificador único de la imagen.
* CREATED: Fecha en la que se creó la imagen.
* SIZE: Tamaño de la imagen en disco.

En este caso, aparece la imagen `mysql/mysql-server` con la versión `8.0` en la lista de imágenes.

Eliminar una imagen de docker:

```
alumno@ubuntu-server2204:~$ docker rmi mysql/mysql-server:8.0
Untagged: mysql/mysql-server:8.0
Untagged: mysql/mysql-server@sha256:d6c8301b7834c5b9c2b733b10b7e630f441af7bc917c74dba379f24eeeb6a313
Deleted: sha256:1d9c2219ff69238d2f8e576dba546bcd16baaef710babbb1f89e67bbd3530267
Deleted: sha256:1436737b7e3c6e28ae669afc75f6222d137e331c9eee916666b8b0f04c9d453b
Deleted: sha256:904fb564042e80400a99f3f57b88d449865acd94303f7f5a7529b56290b10756
Deleted: sha256:023437eb0e6c05200a573703111fee17cbbf90f0e36b1edc9e94e9de1db9fdc0
Deleted: sha256:fcc58f7739aa572e8f7d949b8df604abe48b9d74aeeea75bdd3ca2bed24eefc4
Deleted: sha256:b95d8286e5565760c5248f29ef6c4908d8b460e2085b800d08303fce5ce8bd70
Deleted: sha256:aac1f7e6d4e5d9eb5c90ab3560ee346285dd24732e8224eafb935ada3ea4f978
Deleted: sha256:e3235af76f171c0ce79ba56cacc80695504a0db3d087a9934c296e565a83ae40
```

* `docker rmi`: elimina una imagen de Docker del sistema local.
* `mysql/mysql-server:8.0`: especifica la imagen y la versión que se desea eliminar.

> __Nota__: si la imagen está en uso por un contenedor en ejecución o detenido, no se podrá eliminar. En ese caso, debes detener o eliminar el contenedor primero antes de eliminar la imagen.

## Contenedor sin persistencia

Crear y ejecutar un contenedor de MySQL con Docker:

```bash
$ docker run -d --name mysql-8.0-srv1 -e MYSQL_ROOT_PASSWORD=mysql8 mysql/mysql-server:8.0
Unable to find image 'mysql/mysql-server:8.0' locally
8.0: Pulling from mysql/mysql-server
6a4a3ef82cdc: Pull complete
5518b09b1089: Pull complete
b6b576315b62: Pull complete
349b52643cc3: Pull complete
abe8d2406c31: Pull complete
c7668948e14a: Pull complete
c7e93886e496: Pull complete
Digest: sha256:d6c8301b7834c5b9c2b733b10b7e630f441af7bc917c74dba379f24eeeb6a313
Status: Downloaded newer image for mysql/mysql-server:8.0
87f99c3cb1e53369dc064fd7d31afe7f7e7142983ac6743dc3c2bfe84b14bbf5
```

* `docker run -d`: crea y ejecuta el contenedor en segundo plano (modo detached).
* `--name mysql-8.0-srv1`: asigna el nombre mysql-8.0-srv1 al contenedor, para facilitar su administración.
* `-e MYSQL_ROOT_PASSWORD=mysql8`: configura la contraseña del usuario root de MySQL en el contenedor como mysql8.
* `mysql/mysql-server:8.0`: especifica la imagen de MySQL que Docker utilizará, en este caso, la versión 8.0.

Si la imagen no está disponible localmente, Docker la descargará y luego ejecutará el contenedor, mostrando su ID.

Verificar las imágenes de Docker disponibles:

```bash
$ docker images
REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
mysql/mysql-server   8.0       1d9c2219ff69   21 months ago   496MB
```

Este comando lista todas las imágenes de Docker almacenadas en el sistema local. Cada imagen muestra:

* __REPOSITORY__: nombre del repositorio de la imagen.
* __TAG__: versión de la imagen.
* __IMAGE ID__: identificador único de la imagen.
* __CREATED__: cuándo fue creada la imagen.
* __SIZE__: tamaño de la imagen.

Debe aparecer la imagen `mysql/mysql-server` con la versión `8.0`.

Verificar los contenedores en ejecución:

```bash
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS                    PORTS                       NAMES
87f99c3cb1e5   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   35 seconds ago   Up 34 seconds (healthy)   3306/tcp, 33060-33061/tcp   mysql-8.0-srv1
```

Este comando muestra todos los contenedores en ejecución y su estado. Muestra información como:

* __CONTAINER ID__: identificador del contenedor.
* __IMAGE__: imagen de la cual fue creado el contenedor.
* __COMMAND__: comando principal que el contenedor está ejecutando.
* __STATUS__: estado actual del contenedor.
* __PORTS__: puertos expuestos por el contenedor.
* __NAMES__: nombre asignado al contenedor.

El contenedor `mysql-8.0-srv1` debe estar en ejecución y en estado Up.

Acceder a la consola MySQL dentro del contenedor:

```bash
$ docker exec -it mysql-8.0-srv1 mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> exit
Bye
```

* `docker exec -it`: ejecuta un comando dentro del contenedor en modo interactivo.
* `mysql-8.0-srv1`: nombre del contenedor en el cual se ejecutará el comando.
* `mysql -u root -p`: inicia la consola de MySQL como usuario root, solicitando la contraseña configurada (mysql8 en este caso).

Esto nos permite acceder a la consola de MySQL para ejecutar comandos SQL.

Acceder al sistema operativo del contenedor:

```bash
$ docker exec -it mysql-8.0-srv1 bash
bash-4.4# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 14
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> exit
Bye

bash-4.4# exit
exit
```

Este comando abre una sesión de terminal (bash) dentro del contenedor, lo que permite ejecutar comandos directamente en el sistema operativo del contenedor, es decir, muestra un prompt bash dentro del contenedor con el que podemos interactuar con el sistema, ejecutar comandos de administración de MySQL o explorar el sistema de archivos del contenedor.

Detener el contenedor de MySQL:

```bash
$ docker stop mysql-8.0-srv1
mysql-8.0-srv1
```

Este comando detiene el contenedor `mysql-8.0-srv1` sin eliminarlo. Esto es útil cuando quieres detener temporalmente el servicio sin eliminar el contenedor.

Eliminar el contenedor de MySQL:

```bash
alumno@ubuntu-server2204:~$ docker rm mysql-8.0-srv1
mysql-8.0-srv1
```

Este comando elimina el contenedor `mysql-8.0-srv1` del sistema. El contenedor debe estar detenido antes de poder eliminarlo.

Verificar los contenedores activos:

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
Este comando muestra nuevamente la lista de contenedores activos. Después de eliminar el contenedor mysql-8.0-srv1, éste último no debería de estar en la lista.

## Contenedor con persistencia

```bash
$ docker volume create mysql-8.0-srv1-data
mysql-8.0-data-srv1
```

```bash
$ docker volume ls
DRIVER    VOLUME NAME
local     mysql-8.0-srv1-data
```

```bash
$ docker volume inspect mysql-8.0-srv1-data
[
    {
        "CreatedAt": "2024-10-30T06:59:56Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/mysql-8.0-srv1-data/_data",
        "Name": "mysql-8.0-srv1-data",
        "Options": null,
        "Scope": "local"
    }
]
```

```bash
$ docker run -d --name mysql-8.0-srv1 -v mysql-8.0-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mysql8  mysql/mysql-server:8.0
622c21a3e55f1eac0056c808e2b9280299b7b00377e46b3f974cd108cfec4fc5
```

```bash
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS                    PORTS                                                            NAMES
622c21a3e55f   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   45 seconds ago   Up 44 seconds (healthy)   3306/tcp, 33060-33061/tcp   mysql-8.0-srv1
```

```bash
$ docker  inspect mysql-8.0-srv1 |grep mounts -i -A10
        "Mounts": [
            {
                "Type": "volume",
                "Name": "mysql-8.0-data",
                "Source": "/var/lib/docker/volumes/mysql-8.0-data/_data",
                "Destination": "/var/lib/mysql",
                "Driver": "local",
                "Mode": "z",
                "RW": true,
                "Propagation": ""
            }
```

```bash
$ docker exec -it mysql-8.0-srv1 mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 12
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> exit
Bye
```

```bash
$ docker exec -it mysql-8.0-srv1 bash
bash-4.4# mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 15
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> exit
Bye

bash-4.4# exit
exit
```

```bash
$ docker exec -it mysql-8.0-srv1 mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 21
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE pruebas;
Query OK, 1 row affected (0.03 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pruebas            |
| sys                |
+--------------------+
5 rows in set (0.00 sec)

mysql> exit
Bye
```

```bash
alumno@ubuntu-server2204:~$ docker stop mysql-8.0-srv1
mysql-8.0-srv1
```

```bash
alumno@ubuntu-server2204:~$ docker rm mysql-8.0-srv1
mysql-8.0-srv1
```

```bash
alumno@ubuntu-server2204:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

```bash
alumno@ubuntu-server2204:~$ docker run -d --name mysql-8.0-srv1 -v mysql-8.0-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=mysql8  mysql/mysql-server:8.0
28a24a02cfdd9d3cb287234b2fcd74ce7da7e83caca07f1a709571d9d422aa9c
```

```bash
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS                    PORTS                                                            NAMES
28a24a02cfdd   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   59 seconds ago   Up 58 seconds (healthy)   3306/tcp, 33060-33061/tcp   mysql-8.0-srv1
```

```bash
$ docker exec -it mysql-8.0-srv1 mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| pruebas            |
| sys                |
+--------------------+
5 rows in set (0.00 sec)

mysql>
```

## Compartir una carpeta entre el Host y el contenedor

```bash
$ pwd
/home/alumno
```

```bash
$ mkdir scripts
```

```bash
$ ls -l
total 24
drwxrwxr-x 2 alumno alumno  4096 oct 30 07:14 scripts
```

```bash
$ docker run -d --name mysql-8.0-srv1 -v ./scripts:/scripts -p33306:3306 -e MYSQL_ROOT_PASSWORD=mysql8 mysql/mysql-server:8.0
18a841a174512de7b640cf313cd2da096430a7ca9c60f0b530c37bf122e657cf
```

```bash
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED         STATUS                   PORTS                                                            NAMES
18a841a17451   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   2 minutes ago   Up 2 minutes (healthy)   33060-33061/tcp, 0.0.0.0:33306->3306/tcp, [::]:33306->3306/tcp   mysql-8.0-srv1
```

```bash
$ docker  inspect mysql-8.0-srv1 | grep mounts -i -A10
        "Mounts": [
            {
                "Type": "bind",
                "Source": "/home/alumno/scripts",
                "Destination": "/scripts",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],
        "Config": {
```

```bash
$ docker exec mysql-8.0-srv1 ls -l /
total 80
lrwxrwxrwx   1 root root    7 Oct  9  2021 bin -> usr/bin
dr-xr-xr-x   2 root root 4096 Oct  9  2021 boot
drwxr-xr-x   5 root root  340 Oct 30 07:15 dev
drwxr-xr-x   2 root root 4096 Jan 18  2023 docker-entrypoint-initdb.d
-rwxr-xr-x   1 root root 8544 Jan 18  2023 entrypoint.sh
drwxr-xr-x   1 root root 4096 Oct 30 07:15 etc
-rwxr-xr-x   1 root root 1098 Jan 18  2023 healthcheck.sh
drwxr-xr-x   2 root root 4096 Oct  9  2021 home
lrwxrwxrwx   1 root root    7 Oct  9  2021 lib -> usr/lib
lrwxrwxrwx   1 root root    9 Oct  9  2021 lib64 -> usr/lib64
drwxr-xr-x   2 root root 4096 Oct  9  2021 media
drwxr-xr-x   2 root root 4096 Oct  9  2021 mnt
drwxr-xr-x   2 root root 4096 Oct  9  2021 opt
dr-xr-xr-x 191 root root    0 Oct 30 07:15 proc
dr-xr-x---   2 root root 4096 Oct  9  2021 root
drwxr-xr-x   1 root root 4096 Jan 18  2023 run
lrwxrwxrwx   1 root root    8 Oct  9  2021 sbin -> usr/sbin
drwxrwxr-x   2 1000 1000 4096 Oct 30 07:14 scripts
drwxr-xr-x   2 root root 4096 Oct  9  2021 srv
dr-xr-xr-x  13 root root    0 Oct 30 07:15 sys
drwxrwxrwt   1 root root 4096 Oct 30 07:15 tmp
drwxr-xr-x   1 root root 4096 Jan 16  2023 usr
drwxr-xr-x   1 root root 4096 Jan 16  2023 var
```

```bash
$ docker stop mysql-8.0-srv1
mysql-8.0-srv1
```

```bash
$ docker rm mysql-8.0-srv1
mysql-8.0-srv1

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Acceso externo al servicio del contenedor

```bash
$ docker run -d --name mysql-8.0-srv1 -p33306:3306 -e MYSQL_ROOT_PASSWORD=mysql8 mysql/mysql-server:8.0
39a5d23773d23bcafbdd360bece4cff5a00d9e58d87c64a2cc5069650c494caa
```

```bash
$ docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS                    PORTS                                                            NAMES
39a5d23773d2   mysql/mysql-server:8.0   "/entrypoint.sh mysq…"   53 seconds ago   Up 52 seconds (healthy)   33060-33061/tcp, 0.0.0.0:33306->3306/tcp, [::]:33306->3306/tcp   mysql-8.0-srv1
```

```bash
alumno@ubuntu-server2204:~$ docker exec -it mysql-8.0-srv1 mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 10
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2023, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)

mysql> use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+------------------------------------------------------+
| Tables_in_mysql                                      |
+------------------------------------------------------+
| columns_priv                                         |
| component                                            |
| db                                                   |
| default_roles                                        |
| engine_cost                                          |
| func                                                 |
| general_log                                          |
| global_grants                                        |
| gtid_executed                                        |
| help_category                                        |
| help_keyword                                         |
| help_relation                                        |
| help_topic                                           |
| innodb_index_stats                                   |
| innodb_table_stats                                   |
| ndb_binlog_index                                     |
| password_history                                     |
| plugin                                               |
| procs_priv                                           |
| proxies_priv                                         |
| replication_asynchronous_connection_failover         |
| replication_asynchronous_connection_failover_managed |
| replication_group_configuration_version              |
| replication_group_member_actions                     |
| role_edges                                           |
| server_cost                                          |
| servers                                              |
| slave_master_info                                    |
| slave_relay_log_info                                 |
| slave_worker_info                                    |
| slow_log                                             |
| tables_priv                                          |
| time_zone                                            |
| time_zone_leap_second                                |
| time_zone_name                                       |
| time_zone_transition                                 |
| time_zone_transition_type                            |
| user                                                 |
+------------------------------------------------------+
38 rows in set (0.01 sec)

mysql> select host,user from user;
+-----------+------------------+
| host      | user             |
+-----------+------------------+
| localhost | healthchecker    |
| localhost | mysql.infoschema |
| localhost | mysql.session    |
| localhost | mysql.sys        |
| localhost | root             |
+-----------+------------------+
5 rows in set (0.00 sec)

mysql> CREATE USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'mysql8';
Query OK, 0 rows affected (0.03 sec)

mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
Query OK, 0 rows affected (0.03 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.02 sec)

mysql> select host,user from user;
+-----------+------------------+
| host      | user             |
+-----------+------------------+
| %         | root             |
| localhost | healthchecker    |
| localhost | mysql.infoschema |
| localhost | mysql.session    |
| localhost | mysql.sys        |
| localhost | root             |
+-----------+------------------+
6 rows in set (0.00 sec)

mysql> exit
Bye
```

```bash
$ mysql -h 127.0.0.1 -P 33306 -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 17
Server version: 8.0.32 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

```bash
$ docker stop mysql-8.0-srv1
mysql-8.0-srv1
```

```bash
$ docker rm mysql-8.0-srv1
mysql-8.0-srv1
```

```bash
$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
