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

* __Esquema__: [gestion-ventas-schema.sql](./gestion-ventas-schema.sql)
* __Datos__: [gestion-ventas-data.sql](./gestion-ventas-data.sql)

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

* __Esquema__: [jardineria-schema.sql](./jardineria-schema.sql)
* __Datos__: [jardineria-data.sql](./jardineria-data.sql)

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

## Ejercicio 5. Universidad

Modelo Entidad/Relación:

![][05]

Creación de la Base de Datos:

* __Esquema__: [universidad-schema.sql](./universidad-schema.sql)
* __Datos__: [universidad-data.sql](./universidad-data.sql)

1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de todos los alumnos. El listado deberá estar ordenado alfabéticamente de menor a mayor por el primer apellido, segundo apellido y nombre.

2. Averigua el nombre y los dos apellidos de los alumnos que no han dado de alta su número de teléfono en la base de datos.

3. Devuelve el listado de los alumnos que nacieron en 1999.

4. Devuelve el listado de profesores que no han dado de alta su número de teléfono en la base de datos y además su nif termina en K.

5. Devuelve el listado de las asignaturas que se imparten en el primer cuatrimestre, en el tercer curso del grado que tiene el identificador 7.

6. Lista los nombres de todos los alumnos.

7. Lista los alumnos que viven en “Madrid”.

8. Lista los alumnos cuya ciudad comience por “S”.

9. Lista los alumnos que no viven en “Madrid”.

10. Muestra cuántos alumnos hay en total.

11. Muestra cuántas ciudades diferentes hay entre los alumnos.

12. Muestra los nombres y ciudades de los alumnos ordenados alfabéticamente por ciudad.

13. Muestra el número de alumnos por ciudad.

14. Muestra los alumnos cuyo nombre contenga la letra “a”.

15. Muestra los alumnos cuya ciudad tenga exactamente 5 caracteres.

16. Lista el nombre de todos los profesores.

17. Muestra los profesores que pertenecen al departamento 10.

18. Muestra los profesores cuyo nombre empiece por “M”.

19. Muestra cuántos profesores hay por cada departamento.

20. Muestra el nombre del profesor que tiene el código más alto.

21. Muestra cuántos profesores hay en total.

22. Muestra los códigos de departamento distintos de los profesores.

23. Muestra el nombre de todas las asignaturas de 1er curso.

24. Muestra las asignaturas del primer cuatrimestre.

25. Muestra las asignaturas que tengan más de 6 créditos.

26. Muestra cuántas asignaturas hay por cada curso.

27. Muestra las asignaturas ordenadas por número de créditos (descendente).

28. Muestra los nombres de asignaturas que tengan la palabra "Programación".

29. Muestra cuántas asignaturas hay en total.

30. Muestra cuántas matrículas hay registradas.

## Ejercicio 6. Shakila (Español)

Modelo Entidad/Relación:

![][06]

Creación de la Base de Datos:

* __Esquema__: [shakila-es-schema.sql](./shakila-es-schema.sql)
* __Datos__: [shakila-es-data.sql](./shakila-es-data.sql)

1. ¿Cuál es el título de la película con el ID 10?

2. ¿Cuántas películas hay en total en la tabla film?

3. ¿Cuál es el ID de la película más cara?

4. ¿Cuántos actores están asociados con la película cuyo título es "ACADEMY DINOSAUR"?

5. ¿Cuáles son los primeros 5 títulos de películas con una clasificación de "PG"?

6. ¿Qué director tiene más películas en la base de datos?

7. ¿Cuántas películas tienen un alquiler con un costo superior a 3.50?

8. ¿Cuál es el título de la película con el ID más bajo?

9. ¿Cuántas películas en total están disponibles para alquilar en la tienda?

10. ¿Cuál es la duración promedio de las películas en la tabla film?

11. ¿Qué actor tiene más películas asociadas a él en la tabla film_actor?

12. ¿Cuáles son los 10 títulos de películas con la mayor duración?

13. ¿Cuál es la clasificación más común entre las películas?

14. ¿Qué idioma se utiliza con mayor frecuencia en las películas?

15. ¿Cuántas películas fueron estrenadas en el año 2005?

16. ¿Cuántas películas tienen una clasificación de "R" y un costo de alquiler superior a 4.00?

17. ¿Qué película tiene el precio de alquiler más bajo?

18. ¿Cuál es el actor con más películas en la tabla film_actor?

19. ¿Cuáles son los 3 títulos de películas que tienen la mayor cantidad de copias disponibles en inventario?

20. ¿Cuáles son los 5 actores más comunes en las películas de la categoría "Action"?

21. ¿Cuántas películas están catalogadas como "Drama" y tienen una duración superior a 120 minutos?

22. ¿Cuántas películas fueron estrenadas antes del 1 de enero de 2000?

23. ¿Cuál es el costo promedio de alquiler de todas las películas?

24. ¿Qué película tiene el mayor precio de compra?

25. ¿Cuántos actores participaron en la película con el título "CHAMPION"?

26. ¿Cuál es la película más reciente en la base de datos?

27. ¿Cuál es el precio promedio de las películas en la categoría "Action"?

28. ¿Cuáles son los 10 primeros títulos de películas cuyo título empieza con la letra "S"?

29. ¿Cuáles son las 5 películas que tienen la menor duración y están disponibles para alquilar?

30. ¿Cuál es la película con más copias en inventario?

[01]: ./01.png "01"
[02]: ./02.png "02"
[03]: ./03.png "03"
[04]: ./04.png "04"
[05]: ./05.png "05"
[06]: ./06.png "06"
