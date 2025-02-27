# Manipulación de Bases de Datos con Data Definition Language (DDL)

* Introducción
* Crear una Base de Datos
* Eliminar una Base de Datos
* Modificar una Base de Datos
* Otros Comandos

## Introducción

Las __bases de datos__ son un pilar fundamental en el almacenamiento, gestión y recuperación de información en el mundo actual. En entornos informáticos, trabajamos con _Sistemas de Gestión de bases de datos_ (_SGBD_) como _MySQL_, _PostgreSQL_, _SQL Server_ u _Oracle_, que permiten estructurar y manipular grandes volúmenes de datos de manera eficiente.

Dentro del _Lenguaje de Definición de Datos_ (DDL - Data Definition Language), el comando `CREATE` es esencial, ya que nos permite crear los diferentes objetos que conforman una base de datos, tales como:

* Bases de datos
* Tablas
* Índices
* Vistas
* Procedimientos almacenados
* Funciones y disparadores (triggers)

El uso correcto del comando `CREATE` es el primer paso para diseñar bases de datos eficientes y optimizadas para su posterior manipulación mediante consultas y modificaciones.

### Crear una Base de Datos

La creación de Bases de Datos en MySQL 8 se realiza mediante el comando `CREATE DATABASE`, que nos permite definir el nombre de la base de datos, el _character set_ y el _collation_. La sintaxis general es la siguiente:

```sql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] database_name;
```

* `DATABASE` y `SCHEMA` son sinónimos en MySQL.
* `IF NOT EXISTS` evita errores en caso de que la base de datos ya exista.

Ejemplos:

Si no especificamos _CHARACTER SET_, se usará el que esté configurado por defecto en nuestro servidor MySQL:

```sql
mysql> SELECT @@character_set_server;
+------------------------+
| @@character_set_server |
+------------------------+
| utf8mb4                |
+------------------------+
1 row in set (0,00 sec)
```

```sql
CREATE DATABASE test_db;
```

> __Nota__: en este caso la base de datos _test\_db_ utilizará el _CHARACTER SET_ _utf8mb4_ que es el que está definido por defecto en el servidor.

Si queremos asegurarnos de que la base de datos _test\_db_ utilice _UTF-8_:

```sql
CREATE DATABASE test_db CHARACTER SET utf8mb4; 
```

Al no especificar _COLLATION_, se usará el que esté configurado por defecto en nuestro servidor MySQL:

```sql
mysql> SELECT @@collation_server;
+--------------------+
| @@collation_server |
+--------------------+
| utf8mb4_0900_ai_ci |
+--------------------+
1 row in set (0,00 sec)
```

Si además deseamos especificar el _COLLATION_ (criterio de ordenación de cadenas de texto), la sintaxis sería la siguiente:

```sql
CREATE DATABASE test_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

> __Nota__: MySQL recomiendo el uso de `_` en vez de `-` para nombres de bases de datos.

Una vez creada la base de datos, podemos consultar el _CHARACTER SET_ y el _COLLATION_ que tiene asignado:

```sql
mysql> CREATE DATABASE test_db;
Query OK, 1 row affected (0,01 sec)

mysql> use test_db;
Database changed

mysql> SELECT @@character_set_database;
+--------------------------+
| @@character_set_database |
+--------------------------+
| utf8mb4                  |
+--------------------------+
1 row in set (0,00 sec)

mysql> SELECT @@collation_database;
+----------------------+
| @@collation_database |
+----------------------+
| utf8mb4_0900_ai_ci   |
+----------------------+
1 row in set (0,00 sec)

mysql> SELECT @@character_set_database, @@collation_database;
+--------------------------+----------------------+
| @@character_set_database | @@collation_database |
+--------------------------+----------------------+
| utf8mb4                  | utf8mb4_0900_ai_ci   |
+--------------------------+----------------------+
1 row in set (0,00 sec)
```

El _COLLATION_ puede ser:
* __case-sensitive (_cs)__: los caracteres a y A son diferentes (sensible a las mayúsculas).
* __case-insensitive (_ci)__: los caracteres a y A son iguales (no-sensible a las mayúsculas).
* __binary (_bin)__: dos caracteres son iguales si los valores de su representación numérica son iguales.

## Eliminar una Base de Datos

Para eliminar una base de datos utilizamos el comando `DROP DATABASE`. La sintaxis es la siguiente:

```sql
DROP {DATABASE | SCHEMA} [IF EXISTS] test_db;
```

* `DROP DATABASE` y `DROP SCHEMA`: ambos comandos son equivalentes en MySQL.
* `IF EXISTS`: evita errores si la base de datos no existe.

Ejemplos:

Eliminar una base de datos ya existente:

```sql
DROP DATABASE test_db;
```

Eliminar una base de datos evitando errores si no existe:

```sql
DROP DATABASE IF EXISTS test_db;
```

Si intentamos eliminar una base de datos que no existe sin `IF EXISTS`, MySQL devolverá un error:

```bash
ERROR 1008 (HY000): Can't drop database 'test_db'; database doesn't exist
```

Consideraciones importantes al eliminar Bases de Datos:

* Una vez eliminada la base de datos, no se puede recuperar, a menos que se tenga una copia de seguridad.
* Todos los objetos dentro de la base de datos como _tablas_ y _datos_ serán eliminados permanentemente, a menos que se tenga una copia de seguridad.
* Para eliminar una base de datos, el usuario debe tener el privilegio `DROP`.

Podemos verificar las bases de datos existentes antes de eliminar una ejecutando:

```sql
SHOW DATABASES;
```

Si queremos afinar más la búsqueda para comprobar si una base de datos existe antes de eliminarla, consultamos la tabla `information_shcema.SCHEMATA`:

```sql
SELECT SCHEMA_NAME FROM information_schema.SCHEMATA WHERE SCHEMA_NAME = 'test_db';
```

* La tabla `information_schema.SCHEMATA` contiene información sobre todas las bases de datos en un servidor de MySQL.

## Modificar una Base de Datos

El comando `ALTER DATABASE` se usa para modificar las propiedades de una base de datos existente, como su _CHARACTER SET_, _COLLATION_ y otras configuraciones. La sintaxis es la siguiente:

```sql
ALTER {DATABASE | SCHEMA} nombre_base_datos
  alter_specification [, alter_specification] ...;
```

Donde `alter_specification` puede incluir configuraciones como:
* __CHARACTER SET__: cambiar el conjunto de caracteres predeterminado.
* __COLLATION__: cambiar la intercalación predeterminada.

Cambiar el _CHARACTER SET_ de una base de datos:

```sql
ALTER DATABASE test_db CHARACTER SET utf8mb4;
```

🔹 Esto cambia el conjunto de caracteres de la base de datos a `utf8mb4`.

Cambiar _COLLATION_ de una base de datos:

```sql
ALTER DATABASE test_db COLLATE utf8mb4_unicode_ci;
```

🔹 Esto establece el _COLLATION_ de la base de datos a `utf8mb4_unicode_ci`, que es más precisa para ordenamiento de caracteres en múltiples idiomas.

Cambiar tanto el _CHARACTER SET_ como _COLLATION_:

```sql
ALTER DATABASE test_db CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

Consideraciones importantes:
* No cambia automáticamente las tablas existentes, es decir, si se cambia el _CHARACTER SET_, las tablas dentro de la base de datos seguirán con su configuración previa, a menos que se modifiquen individualmente con el comando `ALTER TABLE`, solamente las tablas que se creen con el comando `CREATE TABLE` a partir del cambio de _CHARACTER SET_ sí tendrán la nueva configuración.
* En MySQL, solo el usuario con privilegios `ALTER` sobre la base de datos puede ejecutar este comando.

## Otros Comandos Útiles

Consultar el listado de todas las bases de datos a las que el usuario actual tiene acceso:

```sql
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| test_db            |
+--------------------+
5 rows in set (0,01 sec)
```

> __Nota__: si el usuario tiene permisos limitados, es posible que no vea todas las bases de datos del servidor. Bases de datos como `information_schema`, `mysql` y `performance_schema` son internas de MySQL.

Seleccionar una base de datos con la que queremos trabajar en la sesión actual:

```sql
USE test_db;
```

Si el cambio es exitoso, MySQL responderá con:

```sql
Database changed
```

* Después de ejecutar `USE`, todas las consultas afectarán a la base de datos seleccionada sin necesidad de especificarla en cada comando.

Si la base de datos no existe, dará un error:

```
ERROR 1049 (42000): Unknown database 'test_db'
```

Mostrar la sentencia SQL de creación de una base de datos:

```sql
SHOW CREATE DATABASE nombre_base_de_datos;
```

* Muestra la sentencia SQL que se usó para crear la base de datos, incluyendo su _CHARACTER SET_ y _COLLATION_.

```sql
mysql> SHOW CREATE DATABASE test_db;
+----------+-----------------------------------------------------------------------------------------------------------------------------------+
| Database | Create Database                                                                                                                   |
+----------+-----------------------------------------------------------------------------------------------------------------------------------+
| test_db  | CREATE DATABASE `test_db` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci */ /*!80016 DEFAULT ENCRYPTION='N' */ |
+----------+-----------------------------------------------------------------------------------------------------------------------------------+
1 row in set (0,00 sec)
```

* Verifica el comando utilizado para la creación de la base de datos.
* Reutiliza la sentencia para crear una base de datos similar en otro servidor.
