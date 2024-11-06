# Normalización (Ejercicios)

## Ejercicio 1 (Resuelto)

La siguiente tabla representa una base de datos simplificada para una biblioteca:

| CodLibro | Titulo              | Autor                         | Editorial      | CodLector | NombreLector            | FechaDev     |
|----------|---------------------|-------------------------------|----------------|-----------|-------------------------|--------------|
| 1001     | Variable Compleja   | Murray Spiegel                | McGraw Hill    | 501       | Pérez Gómez, Juan       | 15/04/2014   |
| 1004     | Visual Basic        | E. Petroustsos                | Anaya          | 502       | Ríos Terán, Ana         | 17/04/2014   |
| 1005     | Estadística         | Murray Spiegel                | McGraw Hill    | 503       | Roca, René              | 16/04/2014   |
| 1006     | Oracle University   | Nancy Greenberg, Priya Nathan | Oracle Corp.   | 504       | García Roque, Luis      | 20/04/2014   |
| 1007     | Clipper 5.01        | Ramalho                       | McGraw Hill    | 501       | Pérez Gómez, Juan       | 18/04/2014   |

### Primera Forma Normal (1NF)

Para cumplir con la _1NF_, descomponemos el nombre del lector en sus componentes atómicos: _Apellido1_, _Apellido2_ y _Nombre_.

Tabla `Biblioteca` en 1NF:

| CodLibro | Titulo              | Autor             | Editorial      | CodLector | Apellido2 | Nombre  | FechaDev     |
|----------|---------------------|-------------------|----------------|-----------|-----------|---------|--------------|
| 1001     | Variable Compleja   | Murray Spiegel    | McGraw Hill    | 501       | Gómez     | Juan    | 15/04/2014   |
| 1004     | Visual Basic 5      | E. Petroustsos    | Anaya          | 502       | Terán     | Ana     | 17/04/2014   |
| 1005     | Estadística         | Murray Spiegel    | McGraw Hill    | 503       |           | René    | 16/04/2014   |
| 1006     | Oracle University   | Nancy Greenberg   | Oracle Corp.   | 504       | Roque     | Luis    | 20/04/2014   |
| 1007     | Clipper 5.01        | Ramalho           | McGraw Hill    | 501       | Gómez     | Juan    | 18/04/2014   |

### Segunda Forma Normal (2NF)

La 2NF elimina las dependencias parciales.

Análisis de dependencias parciales:
* __Clave Primaria__ (compuesta): en esta tabla, la clave primaria podría ser compuesta por _CodLibro_ y _CodLector_, ya que cada combinación única identifica un préstamo específico de un libro a un lector.
* __Dependencias Parciales__:
    * _Titulo_, _Autor_, y _Editorial_ dependen solamente de _CodLibro_, ya que estas características pertenecen exclusivamente al libro y no dependen del lector. Esto indica una dependencia parcial con respecto a la clave primaria compuesta (CodLibro, CodLector).
    * _Apellido2_, _Nombre_, y _FechaDev_ dependen solamente de _CodLector_, porque estos datos pertenecen únicamente al lector y no están relacionados directamente con el libro. Esto también es una dependencia parcial respecto a la clave primaria compuesta.

Se crean tablas adicionales para los datos de los _libros_, _lectores_ y la _relación préstamo_.

Tabla `Libros`:

| CodLibro | Titulo              | Autor             | Editorial    |
|----------|---------------------|-------------------|--------------|
| 1001     | Variable Compleja   | Murray Spiegel    | McGraw Hill  |
| 1004     | Visual Basic 5      | E. Petroustsos    | Anaya        |
| 1005     | Estadística         | Murray Spiegel    | McGraw Hill  |
| 1006     | Oracle University   | Nancy Greenberg   | Oracle Corp. |
| 1007     | Clipper 5.01        | Ramalho           | McGraw Hill  |

Tabla `Lectores`:

| CodLector | Apellido1 | Apellido2 | Nombre |
|-----------|-----------|-----------|--------|
| 501       | Pérez     | Gómez     | Juan   |
| 502       | Ríos      | Terán     | Ana    |
| 503       | Roca      |           | René   |
| 504       | García    | Roque     | Luis   |

Tabla `Prestamos`:

| CodLibro | CodLector | FechaDev   |
|----------|-----------|------------|
| 1001     | 501       | 15/04/2014 |
| 1004     | 502       | 17/04/2014 |
| 1005     | 503       | 16/04/2014 |
| 1006     | 504       | 20/04/2014 |
| 1007     | 501       | 18/04/2014 |

### Tercera Forma Normal (3NF)

No existen  dependencias transitivas:

Tabla `Libros`:
* __Clave primaria__: _CodLibro_
* Análisis de dependencias transitivas:
    * `CodLibro → Titulo`: _Titulo_ depende directamente de _CodLibro_.
    * `CodLibro → Autor`: _Autor_ depende directamente de _CodLibro_.
    * `CodLibro → Editorial`: _Editorial_ depende directamente de _CodLibro_.

En esta tabla, no hay dependencias transitivas porque cada atributo _Titulo_, _Autor_ y _Editorial_ depende únicamente de la clave primaria _CodLibro_.

Tabla `Lectores`:

* __Clave primaria__: _CodLector_
* Análisis de dependencias transitivas:
    * `CodLector → Apellido1, Apellido2, Nombre`: todos estos atributos dependen directamente de _CodLector_.

No existen dependencias transitivas en esta tabla, ya que cada atributo depende exclusivamente de la clave primaria _CodLector_.

Tabla `Prestamos`:

* __Clave primaria compuesta__: (_CodLibro_, _CodLector_)
* Análisis de dependencias transitivas:
    * `(CodLibro, CodLector) → FechaDev`: _FechaDev_ depende directamente de la clave primaria compuesta (_CodLibro_, _CodLector_).

En esta tabla, no existen dependencias transitivas porque FechaDev depende completamente de la clave primaria compuesta (_CodLibro_, _CodLector_) y no de ningún otro atributo intermedio.

## Ejercicio 2 (Resuelto)

Partimos de una tabla sin normalizar que contiene información sobre órdenes y artículos. Esta tabla contiene grupos repetidos para _Num\_art_, _Nom\_art_, _Cant_, y _Precio_, lo cual no cumple la Primera Forma Normal (1FN):

| Id_orden | Fecha     | Id_cliente | Nom_cliente | Provincia   | Num_art | Nom_art | Cant | Precio |
|----------|-----------|------------|-------------|-------------|---------|---------|------|--------|
| 2301     | 23/02/14  | 101        | Martin      | Cajamarca   | 3786    | Red     | 3    | 35,00  |
| 2301     | 23/02/14  | 101        | Martin      | Cajamarca   | 4011    | Raqueta | 6    | 65,00  |
| 2301     | 23/02/14  | 101        | Martin      | Cajamarca   | 9132    | Paq-3   | 8    | 4,75   |
| 2302     | 25/02/14  | 107        | Herman      | Lima        | 5794    | Paq-6   | 4    | 5,00   |
| 2303     | 27/02/14  | 110        | Pedro       | Piura       | 4011    | Raqueta | 2    | 65,00  |
| 2303     | 27/02/14  | 110        | Pedro       | Piura       | 3141    | Funda   | 2    | 10,00  |

### Primera Forma Normal (1FN)

Esta tabla cumple con la 1FN ya que todos los valores son atómicos

### Segunda Forma Normal (2FN)

Para cumplir con la 2FN, eliminamos las dependencias parciales.

* __Clave Primaria (Compuesta)__: en esta tabla, la clave primaria es la combinación de Id_orden y Num_art, ya que cada fila representa una línea específica de artículo en una orden.
* __Dependencias Parciales__: una dependencia parcial ocurre cuando un atributo depende solo de una parte de la clave primaria compuesta y no de la clave completa. En este caso:
     * _Nom\_art_ y _Precio_ dependen exclusivamente de _Num_art_, no de _Id_orden_. Esto significa que _Nom_art_ y _Precio_ tienen una dependencia parcial respecto a la clave compuesta (_Id_orden_, _Num_art_).

Creamos una nueva tabla `Articulos` que separa los datos que dependen solamente de _Num_art_.

Tabla `Articulos_ordenes`:

| Id_orden | Num_art | Cant |
|----------|---------|------|
| 2301     | 3786    | 3    |
| 2301     | 4011    | 6    |
| 2301     | 9132    | 8    |
| 2302     | 5794    | 4    |
| 2303     | 4011    | 2    |
| 2303     | 3141    | 2    |

Tabla `Articulos`:

| Num_art | Nom_art | Precio |
|---------|---------|--------|
| 3786    | Red     | 35,00  |
| 4011    | Raqueta | 65,00  |
| 9132    | Paq-3   | 4,75   |
| 5794    | Paq-6   | 5,00   |
| 3141    | Funda   | 10,00  |

### Tercera Forma Normal (3FN)

No existen  dependencias transitivas.

Análisis de Dependencias Transitivas:
* Tabla `Articulos_ordenes`: en esta tabla, cada atributo (Id_orden, Num_art, y Cant) depende directamente de la clave primaria compuesta (_Id\_orden_, _Num\_art_). No hay dependencias transitivas, ya que no hay atributos adicionales que dependan indirectamente de la clave.
* Tabla `Articulos`: en esta tabla, cada atributo (_Nom_art_ y _Precio_) depende directamente de la clave primaria _Num\_art_, y no hay otras dependencias transitivas.

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
