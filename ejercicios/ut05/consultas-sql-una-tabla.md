# Ejercicios Consultas SQL una Tabla

## Ejercicio 1. Tienda de informática

Modelo Entidad/Relación:

![][01]

Creación de la Base de Datos:

```sql
DROP DATABASE IF EXISTS tienda;
CREATE DATABASE tienda CHARACTER SET utf8mb4;
USE tienda;

CREATE TABLE fabricante (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL
);

CREATE TABLE producto (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  precio DOUBLE NOT NULL,
  id_fabricante INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_fabricante) REFERENCES fabricante(id)
);

INSERT INTO fabricante VALUES(1, 'Asus');
INSERT INTO fabricante VALUES(2, 'Lenovo');
INSERT INTO fabricante VALUES(3, 'Hewlett-Packard');
INSERT INTO fabricante VALUES(4, 'Samsung');
INSERT INTO fabricante VALUES(5, 'Seagate');
INSERT INTO fabricante VALUES(6, 'Crucial');
INSERT INTO fabricante VALUES(7, 'Gigabyte');
INSERT INTO fabricante VALUES(8, 'Huawei');
INSERT INTO fabricante VALUES(9, 'Xiaomi');

INSERT INTO producto VALUES(1, 'Disco duro SATA3 1TB', 86.99, 5);
INSERT INTO producto VALUES(2, 'Memoria RAM DDR4 8GB', 120, 6);
INSERT INTO producto VALUES(3, 'Disco SSD 1 TB', 150.99, 4);
INSERT INTO producto VALUES(4, 'GeForce GTX 1050Ti', 185, 7);
INSERT INTO producto VALUES(5, 'GeForce GTX 1080 Xtreme', 755, 6);
INSERT INTO producto VALUES(6, 'Monitor 24 LED Full HD', 202, 1);
INSERT INTO producto VALUES(7, 'Monitor 27 LED Full HD', 245.99, 1);
INSERT INTO producto VALUES(8, 'Portátil Yoga 520', 559, 2);
INSERT INTO producto VALUES(9, 'Portátil Ideapd 320', 444, 2);
INSERT INTO producto VALUES(10, 'Impresora HP Deskjet 3720', 59.99, 3);
INSERT INTO producto VALUES(11, 'Impresora HP Laserjet Pro M26nw', 180, 3);
```

1. Lista el nombre de todos los productos que hay en la tabla producto.
2. Lista los nombres y los precios de todos los productos de la tabla producto.
3. Lista todas las columnas de la tabla producto.
4. Lista el nombre de los productos, el precio en euros (EUR) y el precio en dólares estadounidenses (USD) si el cambio está a 1 EUR = 1.14 USD.
5. Lista el nombre de los productos, el precio en euros (EUR) y el precio en dólares estadounidenses (USD) si el cambio está a 1 EUR = 1.14 USD. Utiliza los siguientes alias para las columnas: nombre de producto, euros, dólares.
6. Lista los nombres y los precios de todos los productos de la tabla producto, convirtiendo los nombres a mayúscula.
7. Lista los nombres y los precios de todos los productos de la tabla producto, convirtiendo los nombres a minúscula.
8. Lista el nombre de todos los fabricantes en una columna, y en otra columna obtenga en mayúsculas los dos primeros caracteres del nombre del fabricante.
9. Lista los nombres y los precios de todos los productos de la tabla producto, redondeando el valor del precio.
10. Lista los nombres y los precios de todos los productos de la tabla producto, truncando el valor del precio para mostrarlo sin ninguna cifra decimal.
11. Lista el identificador de los fabricantes que tienen productos en la tabla producto.
12. Lista el identificador de los fabricantes que tienen productos en la tabla producto, eliminando los identificadores que aparecen repetidos.
13. Lista los nombres de los fabricantes ordenados de forma ascendente.
14. Lista los nombres de los fabricantes ordenados de forma descendente.
15. Lista los nombres de los productos ordenados en primer lugar por el nombre de forma ascendente y en segundo lugar por el precio de forma descendente.
16. Devuelve una lista con las 5 primeras filas de la tabla fabricante.
17. Devuelve una lista con 2 filas a partir de la cuarta fila de la tabla fabricante. La cuarta fila también se debe incluir en la respuesta.
18. Lista el nombre y el precio del producto más barato. (Utilice solamente las cláusulas ORDER BY y LIMIT)
19. Lista el nombre y el precio del producto más caro. (Utilice solamente las cláusulas ORDER BY y LIMIT)
20. Lista el nombre de todos los productos del fabricante cuyo identificador de fabricante es igual a 2.
21. Lista el nombre de los productos que tienen un precio menor o igual a 120€.
22. Lista el nombre de los productos que tienen un precio mayor o igual a 400€.
23. Lista el nombre de los productos que no tienen un precio mayor o igual a 400€.
24. Lista todos los productos que tengan un precio entre 80€ y 300€. Sin utilizar el operador BETWEEN.
25. Lista todos los productos que tengan un precio entre 60€ y 200€. Utilizando el operador BETWEEN.
26. Lista todos los productos que tengan un precio mayor que 200€ y que el identificador de fabricante sea igual a 6.
27. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5. Sin utilizar el operador IN.
28. Lista todos los productos donde el identificador de fabricante sea 1, 3 o 5. Utilizando el operador IN.
29. Lista el nombre y el precio de los productos en céntimos (Habrá que multiplicar por 100 el valor del precio). Cree un alias para la columna que contiene el precio que se llame céntimos.
30. Lista los nombres de los fabricantes cuyo nombre empiece por la letra S.
31. Lista los nombres de los fabricantes cuyo nombre termine por la vocal e.
32. Lista los nombres de los fabricantes cuyo nombre contenga el carácter w.
33. Lista los nombres de los fabricantes cuyo nombre sea de 4 caracteres.
34. Devuelve una lista con el nombre de todos los productos que contienen la cadena Portátil en el nombre.
35. Devuelve una lista con el nombre de todos los productos que contienen la cadena Monitor en el nombre y tienen un precio inferior a 215 €.
36. Lista el nombre y el precio de todos los productos que tengan un precio mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente).

[01]: ./01.png "01"

## Ejercicio 2. Gestión de empleados

Modelo Entidad/Relación:

![][02]

Creación de la Base de Datos:

```sql
DROP DATABASE IF EXISTS empleados;
CREATE DATABASE empleados CHARACTER SET utf8mb4;
USE empleados;

CREATE TABLE departamento (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  presupuesto DOUBLE UNSIGNED NOT NULL,
  gastos DOUBLE UNSIGNED NOT NULL
);

CREATE TABLE empleado (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nif VARCHAR(9) NOT NULL UNIQUE,
  nombre VARCHAR(100) NOT NULL,
  apellido1 VARCHAR(100) NOT NULL,
  apellido2 VARCHAR(100),
  id_departamento INT UNSIGNED,
  FOREIGN KEY (id_departamento) REFERENCES departamento(id)
);

INSERT INTO departamento VALUES(1, 'Desarrollo', 120000, 6000);
INSERT INTO departamento VALUES(2, 'Sistemas', 150000, 21000);
INSERT INTO departamento VALUES(3, 'Recursos Humanos', 280000, 25000);
INSERT INTO departamento VALUES(4, 'Contabilidad', 110000, 3000);
INSERT INTO departamento VALUES(5, 'I+D', 375000, 380000);
INSERT INTO departamento VALUES(6, 'Proyectos', 0, 0);
INSERT INTO departamento VALUES(7, 'Publicidad', 0, 1000);

INSERT INTO empleado VALUES(1, '32481596F', 'Aarón', 'Rivero', 'Gómez', 1);
INSERT INTO empleado VALUES(2, 'Y5575632D', 'Adela', 'Salas', 'Díaz', 2);
INSERT INTO empleado VALUES(3, 'R6970642B', 'Adolfo', 'Rubio', 'Flores', 3);
INSERT INTO empleado VALUES(4, '77705545E', 'Adrián', 'Suárez', NULL, 4);
INSERT INTO empleado VALUES(5, '17087203C', 'Marcos', 'Loyola', 'Méndez', 5);
INSERT INTO empleado VALUES(6, '38382980M', 'María', 'Santana', 'Moreno', 1);
INSERT INTO empleado VALUES(7, '80576669X', 'Pilar', 'Ruiz', NULL, 2);
INSERT INTO empleado VALUES(8, '71651431Z', 'Pepe', 'Ruiz', 'Santana', 3);
INSERT INTO empleado VALUES(9, '56399183D', 'Juan', 'Gómez', 'López', 2);
INSERT INTO empleado VALUES(10, '46384486H', 'Diego','Flores', 'Salas', 5);
INSERT INTO empleado VALUES(11, '67389283A', 'Marta','Herrera', 'Gil', 1);
INSERT INTO empleado VALUES(12, '41234836R', 'Irene','Salas', 'Flores', NULL);
INSERT INTO empleado VALUES(13, '82635162B', 'Juan Antonio','Sáez', 'Guerrero', NULL);
```

1. Lista el primer apellido de todos los empleados.

2. Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

3. Lista todas las columnas de la tabla empleado.

4. Lista el nombre y los apellidos de todos los empleados.

5. Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado.

6. Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado, eliminando los identificadores que aparecen repetidos.

7. Lista el nombre y apellidos de los empleados en una única columna.

8. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula.

9. Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.

10. Lista el identificador de los empleados junto al nif, pero el nif deberá aparecer en dos columnas, una mostrará únicamente los dígitos del nif y la otra la letra.

11. Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.

12. Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

13. Lista el nombre de todos los departamentos ordenados de forma ascendente.

14. Lista el nombre de todos los departamentos ordenados de forma descendente.

15. Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.

16. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

17. Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

18. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

19. Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

20. Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla empleado.

21. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

23. Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

24. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

25. Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

26. Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

27. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.

28. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.

29. Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.

30. Lista todos los datos de los empleados cuyo segundo apellido sea NULL.

31. Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.

32. Lista todos los datos de los empleados cuyo segundo apellido sea López.

33. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Sin utilizar el operador IN.

34. Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Utilizando el operador IN.

35. Lista los nombres, apellidos y nif de los empleados que trabajan en el departamento 3.

36. Lista los nombres, apellidos y nif de los empleados que trabajan en los departamentos 2, 4 o 5.

## Ejercicio 3. Gestión de ventas

Modelo Entidad/Relación:

![][03]

Creación de la Base de Datos:

```sql
DROP DATABASE IF EXISTS ventas;
CREATE DATABASE ventas CHARACTER SET utf8mb4;
USE ventas;

CREATE TABLE cliente (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  apellido1 VARCHAR(100) NOT NULL,
  apellido2 VARCHAR(100),
  ciudad VARCHAR(100),
  categoria INT UNSIGNED
);

CREATE TABLE comercial (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(100) NOT NULL,
  apellido1 VARCHAR(100) NOT NULL,
  apellido2 VARCHAR(100),
  comision FLOAT
);

CREATE TABLE pedido (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  total DOUBLE NOT NULL,
  fecha DATE,
  id_cliente INT UNSIGNED NOT NULL,
  id_comercial INT UNSIGNED NOT NULL,
  FOREIGN KEY (id_cliente) REFERENCES cliente(id),
  FOREIGN KEY (id_comercial) REFERENCES comercial(id)
);

INSERT INTO cliente VALUES(1, 'Aarón', 'Rivero', 'Gómez', 'Almería', 100);
INSERT INTO cliente VALUES(2, 'Adela', 'Salas', 'Díaz', 'Granada', 200);
INSERT INTO cliente VALUES(3, 'Adolfo', 'Rubio', 'Flores', 'Sevilla', NULL);
INSERT INTO cliente VALUES(4, 'Adrián', 'Suárez', NULL, 'Jaén', 300);
INSERT INTO cliente VALUES(5, 'Marcos', 'Loyola', 'Méndez', 'Almería', 200);
INSERT INTO cliente VALUES(6, 'María', 'Santana', 'Moreno', 'Cádiz', 100);
INSERT INTO cliente VALUES(7, 'Pilar', 'Ruiz', NULL, 'Sevilla', 300);
INSERT INTO cliente VALUES(8, 'Pepe', 'Ruiz', 'Santana', 'Huelva', 200);
INSERT INTO cliente VALUES(9, 'Guillermo', 'López', 'Gómez', 'Granada', 225);
INSERT INTO cliente VALUES(10, 'Daniel', 'Santana', 'Loyola', 'Sevilla', 125);

INSERT INTO comercial VALUES(1, 'Daniel', 'Sáez', 'Vega', 0.15);
INSERT INTO comercial VALUES(2, 'Juan', 'Gómez', 'López', 0.13);
INSERT INTO comercial VALUES(3, 'Diego','Flores', 'Salas', 0.11);
INSERT INTO comercial VALUES(4, 'Marta','Herrera', 'Gil', 0.14);
INSERT INTO comercial VALUES(5, 'Antonio','Carretero', 'Ortega', 0.12);
INSERT INTO comercial VALUES(6, 'Manuel','Domínguez', 'Hernández', 0.13);
INSERT INTO comercial VALUES(7, 'Antonio','Vega', 'Hernández', 0.11);
INSERT INTO comercial VALUES(8, 'Alfredo','Ruiz', 'Flores', 0.05);

INSERT INTO pedido VALUES(1, 150.5, '2017-10-05', 5, 2);
INSERT INTO pedido VALUES(2, 270.65, '2016-09-10', 1, 5);
INSERT INTO pedido VALUES(3, 65.26, '2017-10-05', 2, 1);
INSERT INTO pedido VALUES(4, 110.5, '2016-08-17', 8, 3);
INSERT INTO pedido VALUES(5, 948.5, '2017-09-10', 5, 2);
INSERT INTO pedido VALUES(6, 2400.6, '2016-07-27', 7, 1);
INSERT INTO pedido VALUES(7, 5760, '2015-09-10', 2, 1);
INSERT INTO pedido VALUES(8, 1983.43, '2017-10-10', 4, 6);
INSERT INTO pedido VALUES(9, 2480.4, '2016-10-10', 8, 3);
INSERT INTO pedido VALUES(10, 250.45, '2015-06-27', 8, 2);
INSERT INTO pedido VALUES(11, 75.29, '2016-08-17', 3, 7);
INSERT INTO pedido VALUES(12, 3045.6, '2017-04-25', 2, 1);
INSERT INTO pedido VALUES(13, 545.75, '2019-01-25', 6, 1);
INSERT INTO pedido VALUES(14, 145.82, '2017-02-02', 6, 1);
INSERT INTO pedido VALUES(15, 370.85, '2019-03-11', 1, 5);
INSERT INTO pedido VALUES(16, 2389.23, '2019-03-11', 1, 5);
```

1. Devuelve un listado con todos los pedidos que se han realizado. Los pedidos deben estar ordenados por la fecha de realización, mostrando en primer lugar los pedidos más recientes.

2. Devuelve todos los datos de los dos pedidos de mayor valor.

3. Devuelve un listado con los identificadores de los clientes que han realizado algún pedido. Tenga en cuenta que no debe mostrar identificadores que estén repetidos.

4. Devuelve un listado de todos los pedidos que se realizaron durante el año 2017, cuya cantidad total sea superior a 500€.

5. Devuelve un listado con el nombre y los apellidos de los comerciales que tienen una comisión entre 0.05 y 0.11.

6. Devuelve el valor de la comisión de mayor valor que existe en la tabla comercial.

7. Devuelve el identificador, nombre y primer apellido de aquellos clientes cuyo segundo apellido no es NULL. El listado deberá estar ordenado alfabéticamente por apellidos y nombre.

8. Devuelve un listado de los nombres de los clientes que empiezan por A y terminan por n y también los nombres que empiezan por P. El listado deberá estar ordenado alfabéticamente.

9. Devuelve un listado de los nombres de los clientes que no empiezan por A. El listado deberá estar ordenado alfabéticamente.

10. Devuelve un listado con los nombres de los comerciales que terminan por el o o. Tenga en cuenta que se deberán eliminar los nombres repetidos.

## Ejercicio 4. Jardinería

Modelo Entidad/Relación:

![][04]

Creación de la Base de Datos:

```sql
DROP DATABASE IF EXISTS jardineria;
CREATE DATABASE jardineria CHARACTER SET utf8mb4;
USE jardineria;

CREATE TABLE oficina (
  codigo_oficina VARCHAR(10) NOT NULL,
  ciudad VARCHAR(30) NOT NULL,
  pais VARCHAR(50) NOT NULL,
  region VARCHAR(50) DEFAULT NULL,
  codigo_postal VARCHAR(10) NOT NULL,
  telefono VARCHAR(20) NOT NULL,
  linea_direccion1 VARCHAR(50) NOT NULL,
  linea_direccion2 VARCHAR(50) DEFAULT NULL,
  PRIMARY KEY (codigo_oficina)
);

CREATE TABLE empleado (
  codigo_empleado INTEGER NOT NULL,
  nombre VARCHAR(50) NOT NULL,
  apellido1 VARCHAR(50) NOT NULL,
  apellido2 VARCHAR(50) DEFAULT NULL,
  extension VARCHAR(10) NOT NULL,
  email VARCHAR(100) NOT NULL,
  codigo_oficina VARCHAR(10) NOT NULL,
  codigo_jefe INTEGER DEFAULT NULL,
  puesto VARCHAR(50) DEFAULT NULL,
  PRIMARY KEY (codigo_empleado),
  FOREIGN KEY (codigo_oficina) REFERENCES oficina (codigo_oficina),
  FOREIGN KEY (codigo_jefe) REFERENCES empleado (codigo_empleado)
);

CREATE TABLE gama_producto (
  gama VARCHAR(50) NOT NULL,
  descripcion_texto TEXT,
  descripcion_html TEXT,
  imagen VARCHAR(256),
  PRIMARY KEY (gama)
);

CREATE TABLE cliente (
  codigo_cliente INTEGER NOT NULL,
  nombre_cliente VARCHAR(50) NOT NULL,
  nombre_contacto VARCHAR(30) DEFAULT NULL,
  apellido_contacto VARCHAR(30) DEFAULT NULL,
  telefono VARCHAR(15) NOT NULL,
  fax VARCHAR(15) NOT NULL,
  linea_direccion1 VARCHAR(50) NOT NULL,
  linea_direccion2 VARCHAR(50) DEFAULT NULL,
  ciudad VARCHAR(50) NOT NULL,
  region VARCHAR(50) DEFAULT NULL,
  pais VARCHAR(50) DEFAULT NULL,
  codigo_postal VARCHAR(10) DEFAULT NULL,
  codigo_empleado_rep_ventas INTEGER DEFAULT NULL,
  limite_credito NUMERIC(15,2) DEFAULT NULL,
  PRIMARY KEY (codigo_cliente),
  FOREIGN KEY (codigo_empleado_rep_ventas) REFERENCES empleado (codigo_empleado)
);

CREATE TABLE pedido (
  codigo_pedido INTEGER NOT NULL,
  fecha_pedido date NOT NULL,
  fecha_esperada date NOT NULL,
  fecha_entrega date DEFAULT NULL,
  estado VARCHAR(15) NOT NULL,
  comentarios TEXT,
  codigo_cliente INTEGER NOT NULL,
  PRIMARY KEY (codigo_pedido),
  FOREIGN KEY (codigo_cliente) REFERENCES cliente (codigo_cliente)
);

CREATE TABLE producto (
  codigo_producto VARCHAR(15) NOT NULL,
  nombre VARCHAR(70) NOT NULL,
  gama VARCHAR(50) NOT NULL,
  dimensiones VARCHAR(25) NULL,
  proveedor VARCHAR(50) DEFAULT NULL,
  descripcion text NULL,
  cantidad_en_stock SMALLINT NOT NULL,
  precio_venta NUMERIC(15,2) NOT NULL,
  precio_proveedor NUMERIC(15,2) DEFAULT NULL,
  PRIMARY KEY (codigo_producto),
  FOREIGN KEY (gama) REFERENCES gama_producto (gama)
);

CREATE TABLE detalle_pedido (
  codigo_pedido INTEGER NOT NULL,
  codigo_producto VARCHAR(15) NOT NULL,
  cantidad INTEGER NOT NULL,
  precio_unidad NUMERIC(15,2) NOT NULL,
  numero_linea SMALLINT NOT NULL,
  PRIMARY KEY (codigo_pedido, codigo_producto),
  FOREIGN KEY (codigo_pedido) REFERENCES pedido (codigo_pedido),
  FOREIGN KEY (codigo_producto) REFERENCES producto (codigo_producto)
);

CREATE TABLE pago (
  codigo_cliente INTEGER NOT NULL,
  forma_pago VARCHAR(40) NOT NULL,
  id_transaccion VARCHAR(50) NOT NULL,
  fecha_pago date NOT NULL,
  total NUMERIC(15,2) NOT NULL,
  PRIMARY KEY (codigo_cliente, id_transaccion),
  FOREIGN KEY (codigo_cliente) REFERENCES cliente (codigo_cliente)
);
```

1. Devuelve un listado con el código de oficina y la ciudad donde hay oficinas.

2. Devuelve un listado con la ciudad y el teléfono de las oficinas de España.

3. Devuelve un listado con el nombre, apellidos y email de los empleados cuyo jefe tiene un código de jefe igual a 7.

4. Devuelve el nombre del puesto, nombre, apellidos y email del jefe de la empresa.

5. Devuelve un listado con el nombre, apellidos y puesto de aquellos empleados que no sean representantes de ventas.

6. Devuelve un listado con el nombre de los todos los clientes españoles.

7. Devuelve un listado con los distintos estados por los que puede pasar un pedido.

8. Devuelve un listado con el código de cliente de aquellos clientes que realizaron algún pago en 2008. Tenga en cuenta que deberá eliminar aquellos códigos de cliente que aparezcan repetidos. Resuelva la consulta:

* Utilizando la función YEAR de MySQL.
* Utilizando la función DATE_FORMAT de MySQL.
* Sin utilizar ninguna de las funciones anteriores.

9. Devuelve un listado con el código de pedido, código de cliente, fecha esperada y fecha de entrega de los pedidos que no han sido entregados a tiempo.

10. Devuelve un listado con el código de pedido, código de cliente, fecha esperada y fecha de entrega de los pedidos cuya fecha de entrega ha sido al menos dos días antes de la fecha esperada.

* Utilizando la función ADDDATE de MySQL.
* Utilizando la función DATEDIFF de MySQL.

11. Devuelve un listado de todos los pedidos que fueron rechazados en 2009.

12. Devuelve un listado de todos los pedidos que han sido entregados en el mes de enero de cualquier año.

13. Devuelve un listado con todos los pagos que se realizaron en el año 2008 mediante Paypal. Ordene el resultado de mayor a menor.

14. Devuelve un listado con todas las formas de pago que aparecen en la tabla pago. Tenga en cuenta que no deben aparecer formas de pago repetidas.

15. Devuelve un listado con todos los productos que pertenecen a la gama Ornamentales y que tienen más de 100 unidades en stock. El listado deberá estar ordenado por su precio de venta, mostrando en primer lugar los de mayor precio.

16. Devuelve un listado con todos los clientes que sean de la ciudad de Madrid y cuyo representante de ventas tenga el código de empleado 11 o 30.

[01]: ./01.png "01"
[02]: ./02.png "02"
[03]: ./03.png "03"
[04]: ./04.png "04"
