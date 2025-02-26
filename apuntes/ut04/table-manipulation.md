# Manipulación de Tablas con Data Definition Language (DDL)

* Introducción
* Crear una Tabla
    * Restricciones sobre las columnas de una tabla
    * Otras opciones a tener en cuenta en la creación de las tablas
* Eliminar una Tabla
* Modificar una Tabla
* Otros Comandos

## Introducción

Las __tablas__ son la estructura central en la organización de datos dentro de una base de datos relacional. Representan conjuntos de información organizada en filas y columnas, permitiendo el almacenamiento y recuperación eficiente de datos. En sistemas de gestión de bases de datos como MySQL, PostgreSQL, SQL Server u Oracle, las tablas son los elementos fundamentales donde se almacenan los registros que forman parte de una aplicación o sistema.

Dentro del __Lenguaje de Definición de Datos__ (DDL - Data Definition Language), el comando `CREATE TABLE` es esencial, ya que nos permite definir la estructura de una tabla, especificando:

* Los nombres de las columnas.
* Los tipos de datos asociados a cada columna.
* Restricciones de integridad como claves primarias, claves foráneas y restricciones únicas.
* Opciones adicionales como el motor de almacenamiento o el conjunto de caracteres.

El diseño correcto de una tabla es crucial para garantizar la integridad, eficiencia y escalabilidad de una base de datos. Al definir correctamente las tablas, establecemos la base sobre la cual se realizarán las consultas y modificaciones de datos en el futuro.

## Crear una Tabla

En MySQL, la sentencia `CREATE TABLE` se usa para crear nuevas tablas dentro de una base de datos. Las tablas deben crearse con una estructura clara y definida, indicando los tipos de datos y restricciones necesarias para cada columna. La sintaxis del comando es:

Para ver la definición completa del comando `CREATE TABLE`consultar la documentación oficial 
[https://dev.mysql.com/doc/refman/8.0/en/create-table.html](https://dev.mysql.com/doc/refman/8.0/en/create-table.html)

```sql
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    (create_definition,...)
    [table_options]

create_definition:
    col_name column_definition
  | [CONSTRAINT [symbol]] PRIMARY KEY (index_col_name,...)
  | [CONSTRAINT [symbol]] FOREIGN KEY (index_col_name,...) reference_definition
  | CHECK (expr)

column_definition:
    data_type [NOT NULL | NULL] [DEFAULT default_value]
      [AUTO_INCREMENT] [UNIQUE [KEY] | [PRIMARY] KEY]

reference_definition:
    REFERENCES tbl_name (index_col_name,...)
      [ON DELETE reference_option]
      [ON UPDATE reference_option]

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT

table_options:
    table_option [[,] table_option] ...

table_option:
    AUTO_INCREMENT [=] value
  | [DEFAULT] CHARACTER SET [=] charset_name
  | [DEFAULT] COLLATE [=] collation_name
  | ENGINE [=] engine_name
```

### Restricciones sobre las columnas de una tabla

Las restricciones en las columnas permiten controlar la integridad de los datos:

* `NOT NULL`: no permite valores nulos en la columna.
* `DEFAULT value`: asigna un valor por defecto si no se especifica otro.
* `AUTO_INCREMENT`: incrementa automáticamente valores numéricos.
* `UNIQUE`: garantiza que los valores sean únicos en la columna.
* `PRIMARY KEY`: define la clave primaria de la tabla.
* `CHECK`: restringe valores basados en una expresión. (Disponible desde MySQL 8.0).

__Ejemplo 1__: creación de una base de datos de _proveedores_ y las tablas _categoria_ y _pieza_:

```sql
DROP DATABASE IF EXISTS proveedores;
CREATE DATABASE proveedores CHARSET utf8mb4;
USE proveedores;

CREATE TABLE categoria (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

CREATE TABLE pieza (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  color VARCHAR(50) NOT NULL,
  precio DECIMAL(7,2) NOT NULL CHECK (precio > 0),  
  id_categoria INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_categoria) REFERENCES categoria(id)
);
```

__Ejemplo 2__: creación de un bases de datos _agencia_ y las tablas _turista_, _hotel_ y _reserva_:

```sql
DROP DATABASE IF EXISTS agencia;
CREATE DATABASE agencia CHARSET utf8mb4;
USE agencia;

CREATE TABLE turista (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(50) NOT NULL,
  apellidos VARCHAR(100) NOT NULL,
  direccion VARCHAR(100) NOT NULL,
  telefono VARCHAR(9) NOT NULL
);

CREATE TABLE hotel (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(50) NOT NULL,
  direccion VARCHAR(100) NOT NULL,
  ciudad VARCHAR(25) NOT NULL,
  plazas INTEGER NOT NULL,
  telefono VARCHAR(9) NOT NULL
);

CREATE TABLE reserva (
  id_turista INT UNSIGNED NOT NULL,
  id_hotel INT UNSIGNED NOT NULL,
  fecha_entrada DATETIME NOT NULL,
  fecha_salida DATETIME NOT NULL,
  regimen ENUM('MP', 'PC'),
  PRIMARY KEY (id_turista,id_hotel),
  FOREIGN KEY (id_turista) REFERENCES turista(id),
  FOREIGN KEY (id_hotel) REFERENCES hotel(id)
);
```

### Restricciones de Integridad Referencial (Foreign Key)

Las relaciones existentes entre distintas tablas de una base de datos MySQL que utilizan el motor de almacenamiento InnoDB pueden estar especificadas en forma de restricciones de clave externa (“Foreign Key Constraints”), de manera que la propia base de datos impida que se realicen operaciones que provocarían inconsistencias.

El comportamiento por defecto de una restricción de clave externa es impedir un cambio en la base de datos como consecuencia de una sentencia DELETE o UPDATE, si esta trajese como consecuencia un fallo de la integridad referencial.

Veremos primero en resumen las diferentes restricciones de integridad referencial, haciendo uso de algunas imágenes para el caso de ON DELETE.

Las imágenes consideran dos tablas personas y ciudades relacionadas mediante la columna ciudad_id:

![][01]

__RESTRICT__ es el comportamiento por defecto, que impide realizar modificaciones que atentan contra la integridad referencial.

En la imagen vemos el resultado de esta consulta:

```sql
DELETE FROM ciudades WHERE ciudad_id=4;
```

![][02]

Vemos que el registro se puede borrar porque no existe registro relacionado en la tabla personas.

En cambio esta consulta:

```sql
DELETE FROM ciudades WHERE ciudad_id=1;
```

Arrojaría un mensaje de error:

```
Cannot delete or update a parent row: a foreign key constraint fails (db.personas, CONSTRAINT personas_ibfk_1 FOREIGN KEY (ciudad_id) REFERENCES ciudades (ciudad_id))
```

Porque el DELETE viola la restricción. Si la fila 1 de ciudades se borrase, las filas 1 y 4 de personas quedarían huérfanas, o sea, sin relación en la tabla ciudades.

__CASCADE__ borra los registros de la tabla dependiente cuando se borra el registro de la tabla principal (en una sentencia DELETE), o actualiza el valor de la clave secundaria cuando se actualiza el valor de la clave referenciada (en una sentencia UPDATE).

En la imagen vemos el resultado de esta consulta:

```sql
DELETE FROM ciudades WHERE ciudad_id=1;
```

Aquí se borrarán en cascada CASCADE todos los registros de personas que tengan ciudad_id igual a 1, y como es evidente, se borrará en ciudades la ciudad con id 1.

![][03]

__SET NULL__ establece a NULL el valor de la clave secundaria cuando se elimina el registro en la tabla principal o se modifica el valor del campo referenciado.

Lo que vemos en la imagen es el resultado de esta consulta:

```sql
DELETE FROM ciudades WHERE ciudad_id=1;
```

Aquí la columna ciudad_id de la tabla personas establecerá los valores a NULL, en todas las filas cuyo ciudad_id sea igual a 1. Y como es evidente, se borrará en ciudades la ciudad con id 1.

![][04]

Ejemplo 1:

```sql
DROP DATABASE IF EXISTS proveedores;
CREATE DATABASE proveedores CHARSET utf8mb4;
USE proveedores;

CREATE TABLE categoria (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

CREATE TABLE pieza (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  color VARCHAR(50) NOT NULL,
  precio DECIMAL(7,2) NOT NULL,  
  id_categoria INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_categoria) REFERENCES categoria(id)
  ON DELETE RESTRICT
  ON UPDATE RESTRICT
);

INSERT INTO categoria VALUES (1, 'Categoria A');
INSERT INTO categoria VALUES (2, 'Categoria B');
INSERT INTO categoria VALUES (3, 'Categoria C');

INSERT INTO pieza VALUES (1, 'Pieza 1', 'Blanco', 25.90, 1);
INSERT INTO pieza VALUES (2, 'Pieza 2', 'Verde', 32.75, 1);
INSERT INTO pieza VALUES (3, 'Pieza 3', 'Rojo', 12.00, 2);
INSERT INTO pieza VALUES (4, 'Pieza 4', 'Azul', 24.50, 2);
```

* ¿Podríamos borrar la Categoría A de la tabla categoria?
* ¿Y la Categoría C?
* ¿Podríamos actualizar la Categoría A de la tabla categoria?

Ejemplo 2:

```sql
DROP DATABASE IF EXISTS proveedores;
CREATE DATABASE proveedores CHARSET utf8mb4;
USE proveedores;

CREATE TABLE categoria (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

CREATE TABLE pieza (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  color VARCHAR(50) NOT NULL,
  precio DECIMAL(7,2) NOT NULL,  
  id_categoria INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_categoria) REFERENCES categoria(id)
  ON DELETE CASCADE
  ON UPDATE CASCADE
);

INSERT INTO categoria VALUES (1, 'Categoria A');
INSERT INTO categoria VALUES (2, 'Categoria B');
INSERT INTO categoria VALUES (3, 'Categoria C');

INSERT INTO pieza VALUES (1, 'Pieza 1', 'Blanco', 25.90, 1);
INSERT INTO pieza VALUES (2, 'Pieza 2', 'Verde', 32.75, 1);
INSERT INTO pieza VALUES (3, 'Pieza 3', 'Rojo', 12.00, 2);
INSERT INTO pieza VALUES (4, 'Pieza 4', 'Azul', 24.50, 2);
```

* ¿Podríamos borrar la Categoría A de la tabla categoria?
* ¿Qué le ocurre a las piezas que pertenecen la Categoría A después de borrarla?
* ¿Podríamos actualizar la Categoría A de la tabla categoria?
* ¿Qué le ocurre a las piezas que pertenecen la Categoría A después de actualizarla?

Ejemplo 3:

```sql
DROP DATABASE IF EXISTS proveedores;
CREATE DATABASE proveedores CHARSET utf8mb4;
USE proveedores;

CREATE TABLE categoria (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

CREATE TABLE pieza (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  color VARCHAR(50) NOT NULL,
  precio DECIMAL(7,2) NOT NULL,  
  id_categoria INT UNSIGNED,
  FOREIGN KEY (id_categoria) REFERENCES categoria(id)
  ON DELETE SET NULL
  ON UPDATE SET NULL
);

INSERT INTO categoria VALUES (1, 'Categoria A');
INSERT INTO categoria VALUES (2, 'Categoria B');
INSERT INTO categoria VALUES (3, 'Categoria C');

INSERT INTO pieza VALUES (1, 'Pieza 1', 'Blanco', 25.90, 1);
INSERT INTO pieza VALUES (2, 'Pieza 2', 'Verde', 32.75, 1);
INSERT INTO pieza VALUES (3, 'Pieza 3', 'Rojo', 12.00, 2);
INSERT INTO pieza VALUES (4, 'Pieza 4', 'Azul', 24.50, 2);
```

* ¿Podríamos borrar la Categoría A de la tabla categoria?
* ¿Qué le ocurre a las piezas que pertenecen la Categoría A después de borrarla?
* ¿Podríamos actualizar la Categoría A de la tabla categoria?
* ¿Qué le ocurre a las piezas que pertenecen la Categoría A después de actualizarla?

Conclusión:

* `RESTRICT` bloquea la eliminación y actualización si hay dependencias.
* `CASCADE` propaga los cambios y eliminaciones automáticamente.
* `SET NULL` evita la eliminación forzada, pero deja registros huérfanos en pieza.

### Otras opciones a tener en cuenta en la creación de las tablas

Al crear tablas en MySQL, podemos definir varias opciones que influyen en su funcionamiento y estructura. Algunas de las más importantes son:

* `AUTO_INCREMENT`: permite establecer un valor inicial para un campo con auto-incremento.
* `CHARACTER SET`: define el conjunto de caracteres que se utilizará en la tabla.
* `COLLATE`: determina el tipo de cotejamiento que se aplicará en la tabla.
* `ENGINE`: especifica el motor de almacenamiento que se usará. Los más comunes en MySQL son InnoDB y MyISAM, siendo InnoDB el predeterminado.

Ejemplo:

```sql
DROP DATABASE IF EXISTS proveedores;
CREATE DATABASE proveedores CHARSET utf8mb4;
USE proveedores;

CREATE TABLE categoria (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
)  ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1000;

CREATE TABLE pieza (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  color VARCHAR(50) NOT NULL,
  precio DECIMAL(7,2) NOT NULL,  
  id_categoria INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_categoria) REFERENCES categoria(id)
)  ENGINE=InnoDB DEFAULT CHARSET=utf8 AUTO_INCREMENT=1000;
```

En este ejemplo se ha seleccionado para cada una de las tablas las siguientes opciones de configuración:
* `InnoDB` como motor de base de datos
* `utf8mb4` como _CHARACTER SET_
* `1000` como valor inicial para las columnas de tipo _AUTO_INCREMENT_. Así, el primer registro insertado en la tabla su 'id' tendrá un valor de 1000.

## Eliminar una Tabla

En MySQL, podemos eliminar una tabla de la base de datos utilizando la sentencia `DROP TABLE`. Esta acción es irreversible y elimina completamente la estructura y los datos de la tabla especificada.

La sintaxis básica es la siguiente:

```sql
DROP [TEMPORARY] TABLE [IF EXISTS] nombre_tabla [, nombre_tabla];
```

Opciones:

`DROP TABLE nombre_tabla;`: elimina la tabla especificada. Si la tabla no existe, MySQL mostrará un error.
`DROP TABLE IF EXISTS nombre_tabla;`: elimina la tabla solo si existe. Si la tabla no existe, no se genera un error, lo que evita interrupciones en scripts de automatización.
`DROP TABLE nombre_tabla_1, nombre_tabla_2;`: permite eliminar múltiples tablas en una sola instrucción.

Ejemplos de uso:

```sql
DROP TABLE clientes;
```

Este comando eliminará la tabla clientes de la base de datos actual. Si la tabla no existe, MySQL generará un error.

```sql
DROP TABLE IF EXISTS pedidos;
```

Aquí, la tabla pedidos se eliminará si existe. Si no existe, no se generará error.

```sql
DROP TABLE empleados, departamentos;
```

Este ejemplo eliminará las tablas empleados y departamentos al mismo tiempo.


Consideraciones importantes:
* __Irreversibilidad__: al ejecutar DROP TABLE, la tabla y todos sus datos se eliminan definitivamente. Si necesitas conservar los datos, es recomendable realizar una copia de seguridad antes de eliminarla.
* __Efectos en claves foráneas__: si la tabla que se elimina tiene claves foráneas referenciadas por otras tablas, MySQL impedirá su eliminación a menos que se eliminen primero las referencias o se deshabilite la verificación de claves foráneas (SET FOREIGN_KEY_CHECKS=0;).
* __Diferencia entre DROP TABLE y TRUNCATE TABLE__:
    * `DROP TABLE` elimina la tabla junto con su estructura y todos sus datos.
    * `TRUNCATE TABLE` borra solo los datos de la tabla pero mantiene la estructura para futuras inserciones.

> __Nota__: recomendación: Usa DROP TABLE con precaución, especialmente en entornos de producción, ya que una eliminación accidental puede causar pérdida permanente de datos.

## Modificar una Tabla

#TODO

[01]: ../img/ut04/table-manipulation/01.png "01"
[02]: ../img/ut04/table-manipulation/02.png "02"
[03]: ../img/ut04/table-manipulation/03.png "03"
[04]: ../img/ut04/table-manipulation/04.png "04"