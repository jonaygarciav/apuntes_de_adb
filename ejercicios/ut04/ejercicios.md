# Sentencias DDL Ejercicios

## Ejercicio 1: Usuarios y Direcciones (Relación Uno a Uno 1:1).

Cada empleado tiene una sola tarjeta de identificación.

1. Crea una base de datos llamada usuarios_db con utf8mb4_unicode_ci.
2. Modifica la base de datos usuarios_db para cambiar su collation a utf8mb4_general_ci.
3. Crea una tabla usuarios con los siguientes campos:

    * id: UNSIGNED INT, auto incremental, clave primaria.
    * nombre: VARCHAR(100), no nulo.

4.  Crea una tabla direcciones donde cada usuario tiene una única dirección, con los campos:

    * id: UNSIGNED INT, auto incremental, clave primaria.
    * usuario_id: UNSIGNED INT, clave foránea a usuarios(id), con restricción UNIQUE.
    * direccion: VARCHAR(255), no nulo.

5. Modifica la tabla direcciones para cambiar la clave primaria y hacer que usuario_id sea clave primaria y clave foránea a la vez.
6. Cambia el tamaño del campo nombre en la tabla usuarios a 150 caracteres.
7. Agrega una nueva columna telefono de tipo VARCHAR(15) después del campo nombre en usuarios.
8. Cambia el tipo de dato de telefono en usuarios para que sea BIGINT.
9. Elimina la columna telefono de la tabla usuarios.
10. Inserta un usuario llamado "Juan Pérez".
11. Inserta una dirección "Calle Mayor 123" para el usuario "Juan Pérez".
12. Inserta dos usuarios adicionales ("Ana Gómez" y "Carlos Ruiz").
13. Añade direcciones para los nuevos usuarios.
14. Consulta todas las direcciones junto con el nombre del usuario.
15. Muestra todos los usuarios que no tienen dirección registrada.
16. Actualiza la dirección de "Juan Pérez" a "Avenida Central 456".
17. Elimina la dirección de "Carlos Ruiz".
18. Consulta la estructura de la tabla direcciones.
19. Elimina las tablas direcciones y usuarios.
20. Elimina la base de datos usuarios_db.

## Ejemplo 2: Pacientes e Historia Clínica (Relación Uno a Uno - 1:1)

Cada paciente tiene una única historia clínica.

1. Crea una base de datos llamada hospital con utf8mb4_unicode_ci.
2. Modifica la base de datos hospital para cambiar su collation a utf8mb4_general_ci.
3. Crea una tabla pacientes con los siguientes campos:

    * id: UNSIGNED INT, auto incremental, clave primaria.
    * nombre: VARCHAR(100), no nulo.

4. Crea una tabla historias_clinicas donde cada paciente tiene una única historia clínica, con los campos:

    * paciente_id: UNSIGNED INT, clave primaria y clave foránea a pacientes(id).
    * diagnostico: TEXT, no nulo.
    * fecha_registro: DATETIME, DEFAULT CURRENT_TIMESTAMP.
    
5. Modifica la tabla historias_clinicas agregando una columna tratamiento de tipo TEXT.
6. Cambia el tamaño del campo nombre en la tabla pacientes a 150 caracteres.
7. Agrega una nueva columna telefono de tipo VARCHAR(15) después del campo nombre en pacientes.
8. Cambia el tipo de dato de telefono en pacientes para que sea BIGINT.
9. Elimina la columna telefono de la tabla pacientes.
10. Inserta un paciente llamado "Juan Pérez".
11. Inserta una historia clínica con diagnóstico "Hipertensión" para el paciente "Juan Pérez".
12. Inserta dos pacientes adicionales ("Ana Gómez" y "Carlos Ruiz").
13. Añade historias clínicas para los nuevos pacientes.
14. Consulta todas las historias clínicas junto con el nombre del paciente.
15. Muestra todos los pacientes que no tienen historia clínica registrada.
16. Actualiza el diagnóstico de "Juan Pérez" a "Hipertensión crónica".
17. Elimina la historia clínica de "Carlos Ruiz".
18. Consulta la estructura de la tabla historias_clinicas.
19. Elimina las tablas historias_clinicas y pacientes.
20. Elimina la base de datos hospital.

## Ejemplo 3: Biblioteca y Libros (Relación Uno a Muchos 1:N)

Un autor puede escribir muchos libros, pero cada libro pertenece a un solo autor.


1. Crea una base de datos llamada biblioteca con utf8mb4_unicode_ci.
2. Modifica la base de datos biblioteca para cambiar su collation a utf8mb4_general_ci.
3. Crea una tabla bibliotecas con los siguientes campos:

    * id: UNSIGNED INT, auto incremental, clave primaria.
    * nombre: VARCHAR(100), no nulo.

4. Crea una tabla libros con los siguientes campos:

    * id: AUTO_INCREMENT, clave primaria.
    * biblioteca_id: UNSIGNED INT, clave foránea a bibliotecas(id).
    * titulo: VARCHAR(255), no nulo.
    * autor: VARCHAR(100), no nulo.
    * anio_publicacion: YEAR, no nulo.

5. Modifica la tabla libros agregando una columna genero (VARCHAR(50)).
6. Cambia el tamaño de nombre en bibliotecas a 150 caracteres.
7. Elimina la columna genero de libros.
8. Añade una nueva columna isbn de tipo VARCHAR(20) después de titulo en libros.
9. Cambia el tipo de dato de isbn en libros para que sea CHAR(13).
10. Inserta una biblioteca llamada "Biblioteca Central".
11. Añade un libro "El Quijote" de "Miguel de Cervantes" en la Biblioteca Central.
12. Registra dos libros adicionales en la Biblioteca Central.
13. Consulta todos los libros con su biblioteca.
14. Muestra todas las bibliotecas sin libros registrados.
15. Actualiza el año de publicación de "1984" a 1950.
16. Elimina un libro con id = 1.
17. Elimina la Biblioteca Central y todos sus libros.
18. Consulta la estructura de la tabla libros.
19. Elimina la tabla libros y bibliotecas.
20. Elimina la base de datos biblioteca.

## Ejercicio 4: Departamento con empleados (1:N)

Un departamento puede tener muchos empleados, pero un empleado pertenece a un solo departamento.

1. Crea una base de datos llamada universidad con utf8mb4_unicode_ci.
2. Modifica la base de datos universidad para cambiar su collation a utf8mb4_general_ci.
3. Crea una tabla alumnos con los siguientes campos:
* id: UNSIGNED INT, auto incremental, clave primaria.
* nombre: VARCHAR(100), no nulo.
4. Crea una tabla asignaturas con los siguientes campos:
* id: AUTO_INCREMENT, clave primaria.
* nombre: VARCHAR(100), no nulo.
5. Crea la tabla intermedia matriculas para gestionar la relación muchos a muchos entre alumnos y asignaturas, con los campos:
* id: AUTO_INCREMENT, clave primaria.
* alumno_id: UNSIGNED INT, clave foránea a alumnos(id).
* asignatura_id: UNSIGNED INT, clave foránea a asignaturas(id).
* fecha_matricula: DATE, no nulo.
6. Modifica la tabla matriculas para agregar una columna nota de tipo DECIMAL(4,2).
7. Cambia el tamaño del campo nombre en la tabla asignaturas a 150 caracteres.
8. Elimina la columna nota de la tabla matriculas.
9. Añade un índice a la columna nombre en asignaturas para mejorar la búsqueda.
10. Inserta un alumno llamado "Luis Gómez".
11. Añade una asignatura llamada "Matemáticas".
12. Matricula al alumno en Matemáticas con fecha de matrícula de hoy.
13. Inserta dos alumnos adicionales ("María Fernández" y "Carlos Ruiz").
14. Añade tres asignaturas adicionales ("Física", "Historia", "Química").
15. Matricula a los alumnos en distintas asignaturas.
16. Consulta todas las asignaturas en las que está inscrito el alumno "Luis Gómez".
17. Consulta todos los alumnos que están inscritos en la asignatura "Matemáticas".
18. Elimina la inscripción de un alumno en una asignatura específica.
19. Elimina un alumno y sus matrículas asociadas.
20. Elimina la base de datos universidad.

## Ejercicio 5: Actores y Películas (Relación N:M)

Un estudiante puede inscribirse en varios cursos, y un curso puede tener varios estudiantes.

1. Crea una base de datos llamada cine con utf8mb4_unicode_ci.
2. Modifica la base de datos cine para cambiar su collation a utf8mb4_general_ci.
3. Crea una tabla actores con los siguientes campos:
* id: UNSIGNED INT, auto incremental, clave primaria.
* nombre: VARCHAR(100), no nulo.
4. Crea una tabla peliculas con los siguientes campos:
* id: AUTO_INCREMENT, clave primaria.
* titulo: VARCHAR(150), no nulo.
* anio_estreno: YEAR, no nulo.
5. Crea la tabla intermedia actores_peliculas para gestionar la relación muchos a muchos entre actores y peliculas, con los campos:
* id: AUTO_INCREMENT, clave primaria.
* actor_id: UNSIGNED INT, clave foránea a actores(id).
* pelicula_id: UNSIGNED INT, clave foránea a peliculas(id).
* personaje: VARCHAR(100), no nulo.
6. Modifica la tabla actores_peliculas para agregar una columna salario de tipo DECIMAL(10,2).
7. Cambia el tamaño del campo nombre en la tabla actores a 150 caracteres.
8. Elimina la columna salario de la tabla actores_peliculas.
9. Añade un índice a la columna titulo en peliculas para mejorar la búsqueda.
10. Inserta un actor llamado "Leonardo DiCaprio".
11. Añade una película llamada "Titanic" con año de estreno 1997.
12. Registra la participación de "Leonardo DiCaprio" en "Titanic" como el personaje "Jack Dawson".
13. Inserta dos actores adicionales ("Kate Winslet" y "Tom Hanks").
14. Añade tres películas adicionales ("Forrest Gump", "Avatar", "Inception").
15. Registra la participación de actores en distintas películas.
16. Consulta todas las películas en las que ha trabajado "Leonardo DiCaprio".
17. Consulta todos los actores que han participado en la película "Titanic".
18. Elimina la participación de un actor en una película específica.
19. Elimina un actor y sus registros de películas.
20. Elimina la base de datos cine.
