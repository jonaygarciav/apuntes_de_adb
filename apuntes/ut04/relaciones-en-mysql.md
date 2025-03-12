# Relaciones en MySQL

* Introducción
* Relaciones
    * Uno a Uno (1:1)
    * Uno a Muchos (1:M)
    * Muchos a Muchos (M:M)

## Introducción

En una base de datos relacional, una _relación_ es el vínculo que existe entre dos o más tablas a través de _claves primarias_ y _claves foráneas_. Estas relaciones permiten organizar la información de manera eficiente y evitar la redundancia de datos.

¿Por qué usar relaciones en MySQL?
* __Normalización__: evita la duplicación de datos y mantiene la integridad.
* __Eficiencia__: mejora el rendimiento al reducir la cantidad de datos repetidos.
* __Flexibilidad__: permite estructurar los datos de manera modular y escalable.
* __Integridad referencial__: asegura que las conexiones entre tablas sean válidas y consistentes.

## Relaciones

Las bases de datos relacionales utilizan claves primarias y claves foráneas para establecer relaciones entre tablas. Existen tres tipos principales de relaciones: _uno-a-uno_, _uno-a-mucho_ y _muchos-a-muchos_. 

### Relación Uno a Uno (1:1)

Esta relación ocurre cuando un registro en una tabla está asociado exclusivamente con un único registro en otra tabla. Se usa cuando queremos dividir información en varias tablas para mejorar la organización y normalización de los datos.

__Ejemplo 1__: Usando una clave foránea con UNIQUE.

Un usuario tiene una sola dirección.

```sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE direcciones (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario_id INT UNIQUE, -- Asegura que un usuario solo pueda tener una dirección
    direccion VARCHAR(255) NOT NULL,
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE
);
```

* `usuario_id` en direcciones es una clave foránea que referencia `id` en usuarios.
* Se aplica `UNIQUE` a `usuario_id` para garantizar que un usuario tenga máximo una dirección.

__Ejemplo 2__: usando la clave primaria como clave foránea.

Otra forma de implementar una relación 1:1 es haciendo que la clave primaria de una tabla sea también la clave foránea que referencia otra tabla.

Caso práctico: Un usuario tiene una única tarjeta de identificación.

```sql
CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE identificaciones (
    usuario_id INT PRIMARY KEY, -- Es clave primaria y foránea al mismo tiempo
    numero_identificacion VARCHAR(20) UNIQUE NOT NULL,
    fecha_emision DATE NOT NULL,
    FOREIGN KEY (usuario_id) REFERENCES usuarios(id) ON DELETE CASCADE
);
```

* En la tabla `identificaciones`, `usuario_id` es la clave primaria y también la clave foránea que referencia a `usuarios(id)`.
* Esto impide que haya varias identificaciones para el mismo usuario.
* Si un usuario es eliminado, su identificación también lo será por la opción `ON DELETE CASCADE`.

Diferencias entre ambas implementaciones:

| Método                      | Clave primaria independiente                        | Clave primaria es clave foránea                        |
|-----------------------------|----------------------------------------------------|------------------------------------------------------|
| `usuario_id UNIQUE`        | `id` en `direcciones` es una clave primaria independiente | `usuario_id` en `identificaciones` actúa como clave primaria y foránea |
| Uso de `AUTO_INCREMENT`     | Se usa `AUTO_INCREMENT` en la segunda tabla       | No se usa `AUTO_INCREMENT` en la segunda tabla     |

### Relación Uno a Muchos (1:N)

Se usa cuando una fila en la tabla A puede estar relacionada con muchas filas en la tabla B, pero una fila en la tabla B solo puede estar relacionada con una fila en la tabla A.

__Ejemplo__: un cliente puede tener varias órdenes.

```sql
CREATE TABLE clientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE ordenes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente_id INT,
    fecha DATE NOT NULL,
    total DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (cliente_id) REFERENCES clientes(id) ON DELETE CASCADE
);
```

* Un cliente puede tener muchas órdenes, pero cada orden pertenece a un solo cliente.

### Relación Muchos a Muchos (N:M)

Se usa cuando muchas filas en la tabla A pueden estar relacionadas con muchas filas en la tabla B.

__Ejemplo__: un estudiante puede estar inscrito en varios cursos, y un curso puede tener varios estudiantes. Para esto, se necesita una tabla intermedia (inscripciones):

```sql
CREATE TABLE estudiantes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE cursos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL
);

CREATE TABLE inscripciones (
    id INT AUTO_INCREMENT PRIMARY KEY,
    estudiante_id INT,
    curso_id INT,
    fecha_inscripcion DATE NOT NULL,
    FOREIGN KEY (estudiante_id) REFERENCES estudiantes(id) ON DELETE CASCADE,
    FOREIGN KEY (curso_id) REFERENCES cursos(id) ON DELETE CASCADE
);
```
