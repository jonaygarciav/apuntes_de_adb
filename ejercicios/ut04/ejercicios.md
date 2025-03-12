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

## Ejemplo 2: Gestión de Clientes y Pedidos (Relación Uno a Muchos - 1:N)

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
