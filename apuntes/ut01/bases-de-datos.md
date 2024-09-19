# Sistemas de Almacenamiento de la Información

## Bases de Datos

Una base de datos es una colección organizada de datos que están estructurados para facilitar su acceso, gestión y actualización. Las bases de datos permiten almacenar grandes cantidades de información de manera que sea fácilmente recuperable, manipulable y protegida. Los elementos principale sde una base de datos son:

* __Tablas__: la unidad básica en bases de datos relacionales. Cada tabla contiene registros (filas) y campos (columnas).
* __Registros__: una fila en una tabla que representa una entrada completa de datos.
* __Campos__: las columnas de una tabla que especifican el tipo de datos que se almacenan, como nombres, fechas, números, etc.
* __Índices__: estructuras que mejoran la velocidad de las operaciones de búsqueda y ordenamiento.

Usos de las Bases de Datos:

* __Gestión de Información Empresarial__: almacenan y gestionan datos críticos como información de clientes, transacciones, inventarios y empleados.
* __Aplicaciones Web y Móviles__: Mantienen datos de usuarios, contenido dinámico, y permiten funcionalidades complejas como la personalización de contenidos y el seguimiento de interacciones.
* __Sistemas de Información__: Utilizados en organizaciones como hospitales, escuelas, bibliotecas y gobiernos para gestionar grandes volúmenes de datos relacionados con operaciones diarias.
* __Análisis de Datos y Big Data__: En análisis de grandes volúmenes de datos para obtener insights valiosos en tiempo real o casi real.

Tipos de Bases de Datos Según el Modelo de Datos

__Bases de Datos Relacionales (RDBMS)__

Organizan los datos en tablas relacionadas mediante claves primarias y ajenas. Utilizan el lenguaje SQL (Structured Query Language) para la gestión y manipulación de datos.

Características:
* Datos estructurados en filas y columnas.
* Integridad de datos mediante restricciones y reglas (p. ej., claves únicas, restricciones de integridad referencial).
* Soporte para transacciones: Atomicidad, Consistencia, Aislamiento y Durabilidad (ACID).

Ventajas:
* Alta consistencia y precisión de los datos.
* Eficiencia en consultas complejas y uniones de tablas.
* Bien soportadas y documentadas, con muchas herramientas de desarrollo disponibles.

Ejemplos: MySQL, MariaDB, PostgreSQL, Oracle Database, Microsoft SQL Server.

A continuación, se muestra un ejemplo de sentencias SQL en MySQL para crear la tabla e índice, e insertar los datos en la tabla:

```SQL
-- Creación de la tabla con la clave primaria y un índice en la columna correo
CREATE TABLE clientes (
    id INT PRIMARY KEY,
    nombre VARCHAR(50),
    correo VARCHAR(50),
    fecha_registro DATE
);

-- Creación del índice en la columna correo para optimizar las búsquedas por correo
CREATE INDEX idx_correo ON clientes(correo);

-- Inserción de los 5 registros
INSERT INTO clientes (id, nombre, correo, fecha_registro) VALUES
(1, 'Juan Pérez', 'juan.perez@mail.com', '2024-09-15'),
(2, 'María García', 'maria.garcia@mail.com', '2024-09-16'),
(3, 'Carlos Sánchez', 'carlos.sanchez@mail.com', '2024-09-17'),
(4, 'Ana López', 'ana.lopez@mail.com', '2024-09-18'),
(5, 'Luis Fernández', 'luis.fernandez@mail.com', '2024-09-19');
```

Descripción de los comandos:
* CREATE TABLE clientes (...): Crea una tabla llamada clientes con las siguientes columnas:
 * id INT PRIMARY KEY: Define el campo id como un entero y clave primaria de la tabla, lo que garantiza que cada registro sea único.
 * nombre VARCHAR(50): Almacena los nombres con un máximo de 50 caracteres.
 * correo VARCHAR(50): Almacena las direcciones de correo electrónico con un máximo de 50 caracteres.
 * fecha_registro DATE: Almacena las fechas en formato YYYY-MM-DD.
* CREATE INDEX idx_correo ON clientes(correo);: Crea un índice llamado idx_correo en la columna correo para mejorar el rendimiento de las búsquedas y consultas basadas en el correo electrónico.
* INSERT INTO clientes (...) VALUES (...): Inserta los 5 registros especificados con sus respectivos datos de ID, nombre, correo y fecha de registro.

A continuación, se muestra un ejemplo de sentencias SQL en MySQL para buscar un registro dentro de la tabla:

```SQL
-- Consulta SQL para buscar el registro con id = 4
SELECT * FROM clientes WHERE id = 4;
```

Para buscar el registro con id = 4 en MySQL y ver cuánto tarda la consulta, puedes usar el comando SELECT con la cláusula WHERE para filtrar por el id.

__Bases de Datos NoSQL__

Diseñadas para datos no estructurados o semiestructurados y para aplicaciones que requieren escalabilidad horizontal y flexibilidad. Los distintos tipos son:

* __Documentales__: Almacenan datos en documentos (JSON, BSON). Ej: MongoDB, CouchDB.
* __Clave-Valor__: Almacenan datos como pares clave-valor, muy rápidos y simples. Ej: Redis, DynamoDB.
* __Columnas__: Organizan datos por columnas, optimizadas para grandes volúmenes de datos analíticos. Ej: Apache Cassandra, HBase.
* __Grafos__: Almacenan datos en nodos y aristas, ideales para gestionar relaciones complejas. Ej: Neo4j.

Características:
* Mayor flexibilidad y capacidad de escalar horizontalmente.
* Diseñadas para manejar grandes volúmenes de datos distribuidos.

Ventajas:
* Escalabilidad masiva y flexibilidad en el diseño de esquemas.
* Mejor rendimiento en aplicaciones con datos no estructurados o semi-estructurados.

Desventajas:
* Menor consistencia y soporte limitado para transacciones complejas.
* Curva de aprendizaje mayor para administrar modelos de datos no convencionales.

Ejemplo JSON para MongoDB

```JSON
[
  {
    "_id": 1,
    "nombre": "Juan Pérez",
    "correo": "juan.perez@mail.com",
    "fechaRegistro": "2024-09-15"
  },
  {
    "_id": 2,
    "nombre": "María García",
    "correo": "maria.garcia@mail.com",
    "fechaRegistro": "2024-09-16"
  },
  {
    "_id": 3,
    "nombre": "Carlos Sánchez",
    "correo": "carlos.sanchez@mail.com",
    "fechaRegistro": "2024-09-17"
  },
  {
    "_id": 4,
    "nombre": "Ana López",
    "correo": "ana.lopez@mail.com",
    "fechaRegistro": "2024-09-18"
  },
  {
    "_id": 5,
    "nombre": "Luis Fernández",
    "correo": "luis.fernandez@mail.com",
    "fechaRegistro": "2024-09-19"
  }
]
```
Explicación del JSON:

* ___id__: este campo es el identificador único de cada documento en MongoDB. Aquí se usa como una clave primaria similar al ID en las bases de datos relacionales.
* __nombre__: almacena el nombre del cliente.
* __correo__: guarda la dirección de correo electrónico.
* __fechaRegistro__: almacena la fecha de registro en formato YYYY-MM-DD.

Ejemplo de simulación en la consola de mongoDB en una con

```
> use miBaseDeDatos
switched to db miBaseDeDatos

> db.clientes.find().pretty()
{
  "_id": 1,
  "nombre": "Juan Pérez",
  "correo": "juan.perez@mail.com",
  "fechaRegistro": "2024-09-15"
}
{
  "_id": 2,
  "nombre": "María García",
  "correo": "maria.garcia@mail.com",
  "fechaRegistro": "2024-09-16"
}
{
  "_id": 3,
  "nombre": "Carlos Sánchez",
  "correo": "carlos.sanchez@mail.com",
  "fechaRegistro": "2024-09-17"
}
{
  "_id": 4,
  "nombre": "Ana López",
  "correo": "ana.lopez@mail.com",
  "fechaRegistro": "2024-09-18"
}
{
  "_id": 5,
  "nombre": "Luis Fernández",
  "correo": "luis.fernandez@mail.com",
  "fechaRegistro": "2024-09-19"
}
```

* __db.clientes.find().pretty()__: Este comando en la consola de MongoDB muestra todos los documentos de la colección clientes de una manera legible (formato bonito).
* Cada documento representa un registro de cliente con un identificador único (_id), un nombre, un correo y la fecha de registro.

__Bases de Datos Orientadas a Objetos__

Integran conceptos de la programación orientada a objetos, permitiendo que los datos se almacenen como objetos con atributos y métodos. Los objetos se almacenan en una estructura que refleja las clases y herencias de los programas. Permiten almacenar datos complejos que incluyen relaciones y métodos.

Ventajas:
* Soportan almacenamiento de objetos complejos sin necesidad de descomponerlos en tablas.
* Ideal para aplicaciones con modelos de datos complejos y con requisitos de manipulación avanzada.

Ejemplos: ObjectDB, db4o.

__Bases de Datos Jerárquicas y de Red__

Las Bases de Datos Jerárquicas organizan los datos en una estructura jerárquica de árbol. Cada nodo tiene uno o varios nodos hijos pero un solo nodo padre. Común en sistemas antiguos como IMS (Information Management System) de IBM.

Desventajas:
* Estructura rígida que no permite relaciones complejas entre nodos.

Las Bases de Datos de Red son similares a la jerárquica, pero permite relaciones múltiples (nodos pueden tener múltiples padres). Se emplea empleada en sistemas complejos de modelado de datos previos a las bases de datos relacionales.

Ejemplos: IDMS (Integrated Database Management System).

## Tipos de Bases de Datos Según la Ubicación de la Información

En las bases de datos centralizadas Bases de Datos Centralizadas toda la información reside en un único servidor o centro de datos.

Ventajas:
* Sencillez en la gestión y el mantenimiento.
* Mejor control de seguridad y de acceso a los datos.

Desventajas:
* Punto único de fallo, lo que puede provocar problemas de disponibilidad y pérdida de datos si ocurre un fallo.
* Limitaciones en el escalado para soportar grandes volúmenes de usuarios.

En las bases de datos distribuidasd los datos se almacenan en múltiples ubicaciones físicas, pero se gestionan como una única base de datos lógica.

Ventajas:
* Mejor rendimiento y disponibilidad al distribuir la carga entre varios servidores.
* Redundancia y tolerancia a fallos mejorada.

Desventajas:
* Complejidad en la sincronización de datos y la gestión de la consistencia entre nodos.
* Mayor dificultad en la administración y en la implementación de seguridad.
* Funciones Clave de las Bases de Datos
* Gestión de Datos: Creación, actualización, eliminación y recuperación de datos.
* Control de Acceso: Definición de permisos para usuarios, roles y autenticación.
* Integridad y Consistencia: Mantenimiento de la validez de los datos mediante restricciones, como claves primarias y foráneas.
* Copias de Seguridad y Recuperación: Proporcionan herramientas para hacer copias de seguridad y restaurar datos en caso de fallos.
* Optimización de Consultas: Herramientas para analizar y mejorar el rendimiento de las consultas y de las operaciones de la base de datos.

## Conclusión

Las bases de datos son esenciales para la gestión de la información en aplicaciones modernas, proporcionando una estructura que permite a las empresas y organizaciones almacenar, acceder y analizar datos de manera segura y eficiente. La elección del tipo de base de datos depende de factores como la naturaleza de los datos, las necesidades de rendimiento, la escalabilidad y la complejidad de las relaciones entre los datos.