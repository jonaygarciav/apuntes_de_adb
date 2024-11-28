# Acciones posteriores a la instalación

* Crear un usuario administrador remoto
* Crear una base de datos y un usuario
* Cargar un archivo SQL en una base de datos

## Crear un usuario administrador remoto

```sql
-- Crear usuario admin con password admin
mysql> CREATE USER 'admin'@'%' IDENTIFIED WITH mysql_native_password BY 'admin';
Query OK, 0 rows affected (0.03 sec)

-- Dar todos los permisos al usuario admin sobre todas las bases de datos
mysql> GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
Query OK, 0 rows affected (0.03 sec)

-- Recargar permisos
mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0,02 sec)
```

Por defecto, MySQL está configurado para aceptar peticiones únicamente desde local (localhost) por motivos de seguridad, lo que restringe las conexiones solamente a aquellas provenientes de la misma máquina. Para permitir conexiones desde cualquier equipo, es necesario configurar el valor `bind-address` a `0.0.0.0`, permitiendo que MySQL acepte conexiones desde cualquier dirección IP externa, lo cual es necesario si deseas que usuarios o aplicaciones remotas accedan a la base de datos. 

```bash
$ sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf

[mysqld]
...
bind-address = 0.0.0.0
```

```bash
$ sudo systemctl restart mysql.service
```

Ahora realizamos la conexión desde la máquina remota al servidor MySQL (en este caso el servidor MySQL tiene la IP 192.168.150.12):

```bash
$ mysql -h 192.168.150.12 -u admin -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9
Server version: 8.0.40 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

## Crear un base de datos y un usuario

```sql
-- Crear base de datos testdb
CREATE DATABASE testdb;
Query OK, 1 row affected (0,03 sec)

-- Crear usuario test con password test
CREATE USER 'test'@'%' IDENTIFIED WITH 'mysql_native_password' BY 'test';
Query OK, 1 row affected (0,03 sec)

-- Dar todos los permisos al usuario test sobre la base de datos testdb
GRANT ALL PRIVILEGES ON testdb.* TO 'test'@'%';
Query OK, 0 rows affected (0,02 sec)

-- Recargar permisos
FLUSH PRIVILEGES;
Query OK, 0 rows affected (0,02 sec)

--Verificar si la base de datos testdb está creada
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| testdb             |
+--------------------+
5 rows in set (0,00 sec)

-- Verificar permisos
SHOW GRANTS FOR 'test'@'%';
+--------------------------------------------------+
| Grants for test@%                                |
+--------------------------------------------------+
| GRANT USAGE ON *.* TO `test`@`%`                 |
| GRANT ALL PRIVILEGES ON `testdb`.* TO `test`@`%` |
+--------------------------------------------------+
2 rows in set (0,01 sec)
```

# Cargar un archivo SQL en una base de datos

```bash
$ cat seed.sql
CREATE DATABASE IF NOT EXISTS testdb;
USE testdb;

CREATE TABLE IF NOT EXISTS alumnos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    apellidos VARCHAR(50),
    email VARCHAR(100),
    telefono VARCHAR(15)
);

INSERT INTO alumnos (nombre, apellidos, email, telefono) VALUES
    ('Juan', 'Perez Dominguez', 'juan.perez@gmail.com', '1234567890'),
    ('Maria', 'Lopez Cano', 'maria.lopez@gmail.com', '2345678901'),
    ('Carlos', 'Ramirez Nuñez', 'carlos.ramirez@gmail.com', '3456789012'),
    ('Ana', 'Morales Rios', 'ana.morales@gmail.com', '4567890123'),
    ('Pedro', 'Rodriguez Marin', 'pedro.rodriguez@gmail.com', '5678901234'),
    ('Sofia', 'Mendez Santos', 'sofia.mendez@gmail.com', '6789012345'),
    ('Luis', 'Fernandez Ruiz', 'luis.fernandez@gmail.com', '7890123456'),
    ('Laura', 'Castillo Fuentes', 'laura.castillo@gmail.com', '8901234567'),
    ('David', 'Torres Molina', 'david.torres@gmail.com', '9012345678'),
    ('Marta', 'Ramos Pardo', 'marta.ramos@gmail.com', '0123456789');

$ ls -l
total 24
-rw-rw-r-- 1 alumno alumno  1020 nov 28 09:36 seed.sql
```

Realizar la carga del archivo SQL:

```bash
$ mysql -u test -p testdb < seed.sql
```

Método alternativo para realizar la carga del archivo SQL:

```bash
$ mysql -u test -p
Enter password:
çWelcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 18
Server version: 8.0.40 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> use testdb;
Database changed

mysql> source seed.sql
Query OK, 1 row affected, 1 warning (0,01 sec)

Database changed
Query OK, 0 rows affected (0,09 sec)

Query OK, 10 rows affected (0,02 sec)
Records: 10  Duplicates: 0  Warnings: 0

mysql>
```

Nos conectamos como usuario root:

```bash
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 13
Server version: 8.0.40 MySQL Community Server - GPL

Copyright (c) 2000, 2024, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

```sql
mysql> SHOW databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| testdb             |
+--------------------+
5 rows in set (0,01 sec)

mysql> USE testdb;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW tables;
+------------------+
| Tables_in_testdb |
+------------------+
| alumnos          |
+------------------+
1 row in set (0,00 sec)

mysql> DESCRIBE alumnos;
+-----------+--------------+------+-----+---------+----------------+
| Field     | Type         | Null | Key | Default | Extra          |
+-----------+--------------+------+-----+---------+----------------+
| id        | int          | NO   | PRI | NULL    | auto_increment |
| nombre    | varchar(50)  | YES  |     | NULL    |                |
| apellidos | varchar(50)  | YES  |     | NULL    |                |
| email     | varchar(100) | YES  |     | NULL    |                |
| telefono  | varchar(15)  | YES  |     | NULL    |                |
+-----------+--------------+------+-----+---------+----------------+
5 rows in set (0,00 sec)

mysql> SELECT * FROM alumnos;
+----+--------+------------------+---------------------------+------------+
| id | nombre | apellidos        | email                     | telefono   |
+----+--------+------------------+---------------------------+------------+
|  1 | Juan   | Perez Dominguez  | juan.perez@gmail.com      | 1234567890 |
|  2 | Maria  | Lopez Cano       | maria.lopez@gmail.com     | 2345678901 |
|  3 | Carlos | Ramirez Nuñez    | carlos.ramirez@gmail.com  | 3456789012 |
|  4 | Ana    | Morales Rios     | ana.morales@gmail.com     | 4567890123 |
|  5 | Pedro  | Rodriguez Marin  | pedro.rodriguez@gmail.com | 5678901234 |
|  6 | Sofia  | Mendez Santos    | sofia.mendez@gmail.com    | 6789012345 |
|  7 | Luis   | Fernandez Ruiz   | luis.fernandez@gmail.com  | 7890123456 |
|  8 | Laura  | Castillo Fuentes | laura.castillo@gmail.com  | 8901234567 |
|  9 | David  | Torres Molina    | david.torres@gmail.com    | 9012345678 |
| 10 | Marta  | Ramos Pardo      | marta.ramos@gmail.com     | 0123456789 |
+----+--------+------------------+---------------------------+------------+
10 rows in set (0,00 sec)
```
