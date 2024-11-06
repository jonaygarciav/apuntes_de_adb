# Normalización (Ejercicios)

## Ejercicio 1 (Resuelto)

La siguiente tabla representa una base de datos simplificada para una biblioteca:

| CodLibro | Titulo              | Autor                         | Editorial      | CodLector | NombreLector            | FechaDev     |
|----------|---------------------|-------------------------------|----------------|-----------|-------------------------|--------------|
| 1001     | Variable Compleja   | Murray Spiegel                | McGraw Hill    | 501       | Pérez Gómez, Juan       | 15/04/2014   |
| 1004     | Visual Basic 5      | E. Petroustsos                | Anaya          | 502       | Ríos Terán, Ana         | 17/04/2014   |
| 1005     | Estadística         | Murray Spiegel                | McGraw Hill    | 503       | Roca, René              | 16/04/2014   |
| 1006     | Oracle University   | Nancy Greenberg, Priya Nathan | Oracle Corp.   | 504       | García Roque, Luis      | 20/04/2014   |
| 1007     | Clipper 5.01        | Ramalho                       | McGraw Hill    | 501       | Pérez Gómez, Juan       | 18/04/2014   |
| 1004     | Visual Basic 5      | E. Petroustsos                | Anaya          | 505       | Padrón González, Alicia | 30/04/2014   |

### Primera Forma Normal (1NF)

La clave primaria sería compuesta por los campos _CodLibro_ y _CodLector_, ya que cada combinación única identifica un préstamo específico de un libro a un lector.

> __Nota__: al elegir como clave primaria _CodLibro_ y _CodLector_, significa que no permitimos que un mismo lector puede sacar el mismo libro más de una vez.

Para cumplir con la _1NF_, descomponemos el nombre del lector en sus componentes atómicos: _Apellido1_, _Apellido2_ y _Nombre_.

Tabla `Biblioteca` en 1NF:

| CodLibro | Titulo              | Autor                          | Editorial      | CodLector | Apellido1 |Apellido2 | Nombre | FechaDev   |
|----------|---------------------|--------------------------------|----------------|-----------|-----------|----------|--------|------------|
| 1001     | Variable Compleja   | Murray Spiegel                 | McGraw Hill    | 501       | Pérez     | Gómez    | Juan   | 15/04/2014 |
| 1004     | Visual Basic 5      | E. Petroustsos                 | Anaya          | 502       | Ríos      | Terán    | Ana    | 17/04/2014 |
| 1005     | Estadística         | Murray Spiegel                 | McGraw Hill    | 503       | Roca      |          | René   | 16/04/2014 |
| 1006     | Oracle University   | Nancy Greenberg, Priya Nathan  | Oracle Corp.   | 504       | García    | Roque    | Luis   | 20/04/2014 |
| 1007     | Clipper 5.01        | Ramalho                        | McGraw Hill    | 501       | Pérez     | Gómez    | Juan   | 18/04/2014 |
| 1004     | Visual Basic 5      | E. Petroustsos                 | Anaya          | 505       | Padrón    | González | Alicia | 30/04/2014 |

Además los valores del campo `Autor` no son atómicos, con lo que creamos distintos registros para crear cada uno de los autores:

| CodLibro | Titulo              | Autor           | Editorial      | CodLector | Apellido1 |Apellido2 | Nombre | FechaDev   |
|----------|---------------------|-----------------|----------------|-----------|-----------|----------|--------|------------|
| 1001     | Variable Compleja   | Murray Spiegel  | McGraw Hill    | 501       | Pérez     | Gómez    | Juan   | 15/04/2014 |
| 1004     | Visual Basic 5      | E. Petroustsos  | Anaya          | 502       | Ríos      | Terán    | Ana    | 17/04/2014 |
| 1005     | Estadística         | Murray Spiegel  | McGraw Hill    | 503       | Roca      |          | René   | 16/04/2014 |
| 1006     | Oracle University   | Nancy Greenberg | Oracle Corp.   | 504       | García    | Roque    | Luis   | 20/04/2014 |
| 1006     | Oracle University   | Priya Nathan    | Oracle Corp.   | 504       | García    | Roque    | Luis   | 20/04/2014 |
| 1007     | Clipper 5.01        | Ramalho         | McGraw Hill    | 501       | Pérez     | Gómez    | Juan   | 18/04/2014 |
| 1004     | Visual Basic 5      | E. Petroustsos  | Anaya          | 505       | Padrón    | González | Alicia | 30/04/2014 |

Este cambio genera una redundancia en la clave primaria, por lo que sigue sin cumplir la _1FN_ por lo que debemos crear una tabla para guardar los `autores`.

Tabla `Biblioteca`:

| CodLibro | Titulo              | Editorial      | CodLector | Apellido1 |Apellido2 | Nombre | FechaDev   |
|----------|---------------------|----------------|-----------|-----------|----------|--------|------------|
| 1001     | Variable Compleja   | McGraw Hill    | 501       | Pérez     | Gómez    | Juan   | 15/04/2014 |
| 1004     | Visual Basic 5      | Anaya          | 502       | Ríos      | Terán    | Ana    | 17/04/2014 |
| 1005     | Estadística         | McGraw Hill    | 503       | Roca      |          | René   | 16/04/2014 |
| 1006     | Oracle University   | Oracle Corp.   | 504       | García    | Roque    | Luis   | 20/04/2014 |
| 1007     | Clipper 5.01        | McGraw Hill    | 501       | Pérez     | Gómez    | Juan   | 18/04/2014 |
| 1004     | Visual Basic 5      | Anaya          | 505       | Padrón    | González | Alicia | 30/04/2014 |

Tabla `Autores`:

| CodLibro | Autor           |
|----------|-----------------|
| 1001     | Murray Spiegel  |
| 1004     | E. Petroustsos  |
| 1005     | Murray Spiegel  |
| 1006     | Nancy Greenberg |
| 1006     | Priya Nathan    |
| 1007     | Ramalho         |

De esta forma solucionamos la redundancia en la clave primaria y cumple la _1FN_.

Claves primarias:
* Tabla `Biblioteca` (_compuesta_): _CodLibro_ y _CodLector_.
* Tabla `Autores`: _CodLibro_.

### Segunda Forma Normal (2NF)

La 2NF elimina las dependencias funcionales.

Análisis de dependencias funcionales:
* _Titulo_ y _Editorial_ dependen solamente de _CodLibro_, ya que estas características pertenecen exclusivamente al libro y no dependen del lector. Esto indica una _dependencia funcional parcial_ con respecto a la clave primaria compuesta (_CodLibro_, _CodLector_).
* _Apellido1_, _Apellido2_ y _Nombre_ dependen solamente de _CodLector_, porque estos datos pertenecen únicamente al lector y no están relacionados directamente con el libro. Esto también es una _dependencia funcional parcial_ respecto a la clave primaria compuesta (_CodLibro_, _CodLector_).
* _FechaDev_ depende _CodLibro_ y _CodLector_, porque estos datos están relacionados con el lector y el libro. Esto _dependencia funcional completa_ respecto a la clave primaria compuesta.

Se crean tablas adicionales para los datos de los _libros_, _lectores_ y la _relación préstamo_.

Tabla `Libros`:

| CodLibro | Titulo              | Editorial    |
|----------|---------------------|--------------|
| 1001     | Variable Compleja   | McGraw Hill  |
| 1004     | Visual Basic 5      | Anaya        |
| 1005     | Estadística         | McGraw Hill  |
| 1006     | Oracle University   | Oracle Corp. |
| 1007     | Clipper 5.01        | McGraw Hill  |

Tabla `Lectores`:

| CodLector | Apellido1 | Apellido2 | Nombre |
|-----------|-----------|-----------|--------|
| 501       | Pérez     | Gómez     | Juan   |
| 502       | Ríos      | Terán     | Ana    |
| 503       | Roca      |           | René   |
| 504       | García    | Roque     | Luis   |
| 505       | Padrón    | González  | Alicia |

Tabla `Prestamos`:

| CodLibro | CodLector | FechaDev   |
|----------|-----------|------------|
| 1001     | 501       | 15/04/2014 |
| 1004     | 502       | 17/04/2014 |
| 1005     | 503       | 16/04/2014 |
| 1006     | 504       | 20/04/2014 |
| 1007     | 501       | 18/04/2014 |
| 1004     | 505       | 30/04/2014 |

Recuerda que, anteriormente, ya habíamos generado la tabla `Autores`:

| CodLibro | Autor           |
|----------|-----------------|
| 1001     | Murray Spiegel  |
| 1004     | E. Petroustsos  |
| 1005     | Murray Spiegel  |
| 1006     | Nancy Greenberg |
| 1006     | Priya Nathan    |
| 1007     | Ramalho         |

Ahora sí cumple la _2FN_.

### Tercera Forma Normal (3NF)

No existen  dependencias transitivas:

Tabla `Autores`:
* __Clave primaria__ (compuesta): _CodLibro_ y _Autor_.
* Análisis de dependencias transitivas:
    * `CodLibro → Autor`: _Autor_ depende directamente de _CodLibro_.

En esta tabla, no hay dependencias transitivas porque cada atributo _Autor_ depende únicamente de la clave primaria _CodLibro_ y no de ningún otro atributo intermedio.

Tabla `Libros`:
* __Clave primaria__: _CodLibro_.
* Análisis de dependencias transitivas:
    * `CodLibro → Titulo`: _Titulo_ depende directamente de _CodLibro_.
    * `CodLibro → Editorial`: _Editorial_ depende directamente de _CodLibro_.

En esta tabla, no hay dependencias transitivas porque cada atributo _Titulo_ y _Editorial_ depende únicamente de la clave primaria _CodLibro_ y no de ningún otro atributo intermedio.

Tabla `Lectores`:

* __Clave primaria__: _CodLector_
* Análisis de dependencias transitivas:
    * `CodLector → Apellido1, Apellido2, Nombre`: todos estos atributos dependen directamente de _CodLector_.

No existen dependencias transitivas en esta tabla, ya que cada atributo _Apellido1_, _Apellido2_ y _Nombre_ depende exclusivamente de la clave primaria _CodLector_ y no de ningún otro atributo intermedio.

Tabla `Prestamos`:

* __Clave primaria compuesta__: (_CodLibro_, _CodLector_)
* Análisis de dependencias transitivas:
    * `(CodLibro, CodLector) → FechaDev`: _FechaDev_ depende directamente de la clave primaria compuesta (_CodLibro_, _CodLector_).

En esta tabla, no existen dependencias transitivas porque _FechaDev_ depende completamente de la clave primaria compuesta (_CodLibro_, _CodLector_) y no de ningún otro atributo intermedio.

## Ejercicio 2 (Resuelto)

Partimos de una tabla sin normalizar que contiene información sobre órdenes de compra y artículos.

| IdOrden | Fecha     | IdCliente | NombreCliente | TelefonoCliente     | Municipio  | Provincia              | IdArticulo | NombreArticulo | Cantidad | Precio |
|---------|-----------|-----------|---------------|---------------------|------------|------------------------|------------|----------------|----------|--------|
| 2301    | 23/02/14  | 101       | Martin        | 922141423 657659873 | Candelaria | Santa Cruz de Tenerife | 3786       | Red            | 3        | 35,00  |
| 2301    | 23/02/14  | 101       | Martin        | 922141423 657659873 | Candelaria | Santa Cruz de Tenerife | 4011       | Raqueta        | 6        | 65,00  |
| 2301    | 23/02/14  | 101       | Martin        | 922141423 657659873 | Candelaria | Santa Cruz de Tenerife | 9132       | Paq-3          | 8        | 4,75   |
| 2302    | 25/02/14  | 107       | Herman        | 928339463 633987125 | Telde      | Las Palmas             | 5794       | Paq-6          | 4        | 5,00   |
| 2303    | 27/02/14  | 110       | Pedro         | 928388841 798456870 | Telde      | Las Palmas             | 4011       | Raqueta        | 2        | 65,00  |
| 2303    | 27/02/14  | 110       | Pedro         | 928388841 798456870 | Telde      | Las Palmas             | 3141       | Funda          | 2        | 10,00  |

Datos a tener en cuenta:
* el campo _Precio_ indica el valor unitario del producto.

### Primera Forma Normal (1FN)

Para cumplir con la _1NF_, el campo _TelefonoCliente_ no es atómico, así que creamos la tabla `Telefonos`.

Tabla `Ordenes`:

| IdOrden | Fecha     | IdCliente | NombreCliente | Municipio  | Provincia              | IdArticulo  | NombreArticulo  | Cantidad | Precio |
|---------|-----------|-----------|---------------|------------|------------------------|-------------|-----------------|----------|--------|
| 2301    | 23/02/14  | 101       | Martin        | Candelaria | Santa Cruz de Tenerife | 3786        | Red             | 3        | 35,00  |
| 2301    | 23/02/14  | 101       | Martin        | Candelaria | Santa Cruz de Tenerife | 4011        | Raqueta         | 6        | 65,00  |
| 2301    | 23/02/14  | 101       | Martin        | Candelaria | Santa Cruz de Tenerife | 9132        | Paq-3           | 8        | 4,75   |
| 2302    | 25/02/14  | 107       | Herman        | Telde      | Las Palmas             | 5794        | Paq-6           | 4        | 5,00   |
| 2303    | 27/02/14  | 110       | Pedro         | Telde      | Las Palmas             | 4011        | Raqueta         | 2        | 65,00  |
| 2303    | 27/02/14  | 110       | Pedro         | Telde      | Las Palmas             | 3141        | Funda           | 2        | 10,00  |

Tabla `Telefonos`:

| IdCliente | TelefonoCliente |
|-----------|-----------------|
| 101       | 922141423       |
| 101       | 657659873       |
| 107       | 928339463       |
| 107       | 633987125       |
| 110       | 928388841       |
| 110       | 798456870       |

Claves primarias:

* Tabla `Ordenes`: compuesta por los campos _IdOrden_ y _IdArticulo_, ya que cada combinación única de estos campos identifica una orden de compra.
* Tabla `Telefonos`: compuesta por los campos _IdCliente_ y _TelefonoCliente_.

Las tablas `Ordenes` y `Telefonos` cumplen con la _1FN_ ya que todos los valores son atómicos.

### Segunda Forma Normal (2FN)

Para cumplir con la _2FN_, eliminamos las dependencias funcionales:
* Tabla `Ordenes`:
    * _NombreArticulo_ y _Precio_ dependen exclusivamente de _IdArticulo_, no de _IdOrden_. Esto significa que _NombreArticulo_ y _Precio_ tienen una dependencia parcial respecto a la clave compuesta (_IdOrden_, _IdArticulo_).
    * _NombreCliente_, _Municipio_ y _Provincia_ dependen exclusivamente de _IdCliente_. Esto significa que _NombreCliente_, _Municipio_ y _Provincia_ tienen una dependencia parcial respecto a la clave compuesta (_IdOrden_, _IdArticulo_).
    * _Fecha_ depende de _IdOrden y de _IdCliente_. Esto significa que _Fecha_ tiene una dependencia completa respecto a la clave compuesta (_IdOrden_, _IdArticulo_).
    * _Cantidad_ depende de _IdOrden_ y _IdArticulo_. Esto significa que _Cantidad_ tiene una dependencia parcial respecto a la clave compuesta (_IdOrden_, _IdArticulo_).
* Tabla `Telefonos`:
    * _TelefonoCliente_ depende exclusivamente de _IdCliente_, tienen una dependencia funcional completa respecto a la clave primaria _IdCliente_).

Para eliminar las dependencias funcionales creamos las tablas `Articulos` y `Clientes`.

Tabla `Articulos`:

| IdArticulo  | NombreArticulo  | Precio |
|-------------|-----------------|--------|
| 3786        | Red             | 35,00  |
| 4011        | Raqueta         | 65,00  |
| 9132        | Paq-3           | 4,75   |
| 5794        | Paq-6           | 5,00   |
| 3141        | Funda           | 10,00  |

Clave primaria: _IdArticulo_.

Tabla `Clientes`:

| IdCliente | NombreCliente | Municipio  | Provincia              |
|-----------|---------------|------------|------------------------|
| 101       | Martin        | Candelaria | Santa Cruz de Tenerife |
| 107       | Herman        | Telde      | Las Palmas             |
| 110       | Pedro         | Telde      | Las Palmas             |

Clave primaria: _IdCliente_.

Tabla `Ordenes`:

| IdOrden | Fecha     | IdCliente |
|---------|-----------|-----------|
| 2301    | 23/02/14  | 101       |
| 2302    | 25/02/14  | 107       |
| 2303    | 27/02/14  | 110       |

Clave primaria: _IdOrden_.

> __Nota__: es necesario añadir el campo _IdCliente_ para poder relacionar la orden de compra con el cliente.

Tabla `DetalleOrdenes`:

| IdOrden | IdArticulo | Cantidad |
|---------|------------|----------|
| 2301    | 3786       | 3        |
| 2301    | 4011       | 6        |
| 2301    | 9132       | 8        |
| 2302    | 5794       | 4        |
| 2303    | 4011       | 2        |
| 2303    | 3141       | 2        |

Clave primaria: _IdOrden_ y _IdArticulo_.

Tabla `Telefonos`(Calculada en la 1FN):

| IdCliente | TelefonoCliente |
|-----------|-----------------|
| 101       | 922141423       |
| 101       | 657659873       |
| 107       | 928339463       |
| 107       | 633987125       |
| 110       | 928388841       |
| 110       | 798456870       |

Clave primaria: _IdCliente_ y _TelefonoCLiente_.

Ahora sí cumple la _2FN_.

### Tercera Forma Normal (3FN)

Análisis de dependencias transitivas:

* Tabla `Clientes`: en esta tabla, existe una dependencia transitiva entre `NombreCliente → Municipio → Provincia`, con lo que crearemos la Tabla `Provincias`.

Tabla `Clientes`:

| IdCliente | NombreCliente | Municipio  |
|-----------|---------------|------------|
| 101       | Martin        | Candelaria |
| 107       | Herman        | Telde      |
| 110       | Pedro         | Telde      |

Clave primaria: _IdCliente_.

Tabla `Provincias`:

| Municipio  | Provincia              |
|------------|------------------------|
| Candelaria | Santa Cruz de Tenerife |
| Telde      | Las Palmas             |

Clave primaria: _Municipio_.

Ahora sí cumple la _3FN_.

## Ejercicio 3

En una base de datos de una empresa de alquiler de vehículos, se tiene la siguiente tabla `Alquileres` que contiene información sobre los vehículos alquilados y sus conductores.

Normaliza la tabla `Alquileres` para que cumpla con 1FN, 2FN y 3FN. Identifica las dependencias funcionales y elimina las dependencias parciales y transitivas en cada paso.

| AlquilerID | FechaAlquiler | ClienteID | ClienteNombre | Vehiculos                  | PrecioVehiculos |
|------------|---------------|-----------|---------------|----------------------------|-----------------|
| 101        | 10/03/2023    | 201       | Carlos        | "Sedán, SUV"               | "50, 70"       |
| 102        | 12/03/2023    | 202       | Laura         | "Convertible, Pickup"      | "80, 65"       |
| 103        | 15/03/2023    | 203       | Pedro         | "SUV, Van, Sedán"          | "70, 60, 50"   |
| 104        | 18/03/2023    | 204       | Ana           | "Sedán"                    | "50"           |

## Ejercicio 4

Una tienda de suministros almacena los datos de sus pedidos en la siguiente tabla `Pedidos`.

Normaliza la tabla `Pedidos` para que cumpla con 1FN, 2FN y 3FN. Identifica las dependencias funcionales y elimina las dependencias parciales y transitivas en cada paso.

| PedidoID | FechaPedido | ClienteID | ClienteNombre | ProductoID | ProductoNombre | Cantidad | PrecioUnitario |
|----------|-------------|-----------|---------------|------------|----------------|----------|----------------|
| 301      | 05/04/2023  | 501       | Juan          | 1001       | Lápiz          | 10       | 0.5            |
| 301      | 05/04/2023  | 501       | Juan          | 1002       | Cuaderno       | 5        | 1.5            |
| 302      | 06/04/2023  | 502       | María         | 1003       | Bolígrafo      | 8        | 0.8            |
| 303      | 07/04/2023  | 503       | Luis          | 1001       | Lápiz          | 12       | 0.5            |
| 303      | 07/04/2023  | 503       | Luis          | 1004       | Borrador       | 4        | 0.3            |

## Ejercicio 5

En una universidad, se lleva un registro de cursos, estudiantes y sus calificaciones. Sin embargo, la tabla CursosEstudiantes no está completamente normalizada.

Normaliza la tabla `CursosEstudiantes` para que cumpla con 1FN, 2FN y 3FN. Identifica las dependencias funcionales y elimina las dependencias parciales y transitivas en cada paso.

| RegistroID | EstudianteID | NombreEstudiante | Cursos                   | Profesor        | Notas          | Departamento |
|------------|--------------|------------------|--------------------------|-----------------|----------------|--------------|
| 1          | 201          | Alicia           | "Matemáticas, Física"    | "Dr. Pérez"     | "85, 90"       | Ciencias     |
| 2          | 202          | Roberto          | "Matemáticas, Química"   | "Dr. Pérez"     | "78, 88"       | Ciencias     |
| 3          | 203          | Julia            | "Historia, Literatura"   | "Dr. Gómez"     | "92, 80"       | Humanidades  |
| 4          | 204          | Mario            | "Química"                | "Dr. Pérez"     | "75"           | Ciencias     |
