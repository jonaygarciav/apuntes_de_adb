# Sistemas Gestores de Base de Datos

## Introducción

Los Sistemas Gestores de Bases de Datos (SGBD) son software diseñados para facilitar la creación, manipulación y administración de bases de datos. Estos sistemas permiten a los usuarios almacenar, recuperar, actualizar y eliminar datos de manera eficiente, garantizando la integridad, seguridad y consistencia de la información. Los SGBD son esenciales en cualquier aplicación que requiera gestión de datos estructurados, desde pequeños programas de escritorio hasta complejos sistemas empresariales y aplicaciones web.

A continuación, se muestra una imagen donde se muestran los Sistemas Gestores de Bases de Datos más utilizados según DB-Engines:

![][01]


## Sistemas Gestores de Bases de Datos Relacionales

### MySQL

![][02]

MySQL es un Sistema Gestor de Bases de datos de código abierto más popular del mercado. Según DB-Engines, MySQL se clasifica como la segunda base de datos más popular, detrás de Oracle Database. MySQL está detrás de aplicaciones como como Facebook, Twitter, Netflix, Uber, Airbnb, Shopify y Booking.com. Dado que MySQL es de código abierto, incluye numerosas funciones desarrolladas en estrecha colaboración con los usuarios durante más de 25 años. Por lo tanto, la gran mayoría de lenguajes de programación favorito sea compatible con MySQL Database.

El logotipo MySQL es un delfín llamado Sakila. El nombre se eligió de entre una larga lista sugerida por los usuarios durante el concurso "Ponle nombre al delfín". El nombre ganador fue enviado por Ambrose Twebaze, un desarrollador de software de código abierto de Eswatini (antigua Swazilandia), África.

MySQL es de código abierto, lo que significa que que cualquier usuario puede utilizar y modificar el software. Cualquier persona puede descargar el software MySQL de Internet y utilizarlo sin pagar por ello. También puedes modificar su código fuente para adaptarlo a tus necesidades. El software MySQL utiliza la GNU General Public License (GPL) para definir lo que puede y no puede hacer con el software en diferentes situaciones.

MySQL se sitúa sistemáticamente como la base de datos más popular entre los desarrolladores, según encuestas de Stack Overflow y JetBrains debido a su alto rendimiento, confiabilidad y facilidad de uso.

MySQL es compatible con algunos lengaujes de desaroollo como  PHP, Python, Java, Node.js, Perl, Ruby, Rust, C, C++, ...

MySQL también se ha convertido en el Sistema Gestor de Bases de Datos elegido por muchas de las aplicaciones de código abierto de mayor éxito, como WordPress, Drupal, Joomla y Magento. MySQL es la "M" en la popular pila de código abierto LAMP (Linux, Apache, MySQL, Perl/Python/PHP) para desarrollar aplicaciones web.

Las principales ventajas de MySQL incluyen:
* __Facilidad de uso__: los desarrolladores pueden instalar MySQL en minutos y la base de datos es fácil de gestionar.
* __Confiabilidad__: MySQL es una de las bases de datos más maduras y utilizadas. Lleva más de 25 años probándose en una amplia variedad de casos, incluso en muchas de las mayores empresas del mundo. Las organizaciones utilizan MySQL para ejecutar aplicaciones clave para el negocio debido a su confiabilidad.
* __Escalabilidad__: MySQL se amplía para satisfacer las demandas de las aplicaciones más accesibles. La arquitectura de replicación nativa de MySQL permite a organizaciones como Facebook escalar aplicaciones para admitir miles de millones de usuarios.
* __Alta disponibilidad__: MySQL ofrece un conjunto completo de tecnologías de replicación nativas y totalmente integradas para una alta disponibilidad y recuperación ante desastres.
* __Flexibilidad__: el almacén de documentos MySQL proporciona a los usuarios la máxima flexibilidad para desarrollar aplicaciones de base de datos SQL tradicionales y sin esquema NoSQL. Los desarrolladores pueden combinar datos relacionales y documentos JSON en la misma base de datos y aplicación.

Casos de uso de MySQL:
* __Comercio electrónico__: muchas de las aplicaciones de comercio electrónico más grandes del mundo (por ejemplo, Shopify, Uber y Booking.com) ejecutan sus sistemas transaccionales en MySQL. Es una opción popular para gestionar perfiles de usuario, credenciales, contenido de usuario, datos financieros, incluidos pagos y detección de fraudes.
* __Plataformas sociales__: Facebook, Twitter y LinkedIn se encuentran entre las redes sociales más grandes del mundo que utilizan MySQL.
* __Gestión de contenido__: a diferencia de las bases de datos de documentos de un solo propósito, MySQL activa SQL y NoSQL con una sola base de datos. El almacén de documentos MySQL permite operaciones CRUD y la potencia de SQL para consultar datos de documentos JSON para informes y análisis.

MySQL se ofrece en dos versiones principales: Community Edition y Enterprise Edition. Cada versión está diseñada para diferentes tipos de usuarios y casos de uso, con diferencias clave en términos de características, soporte y licenciamiento.

__MySQL Community Edition__

_MySQL Community Edition_ es la versión gratuita y de código abierto de MySQL, disponible bajo la Licencia Pública General de GNU (GPL). Es la versión más utilizada de MySQL y es mantenida y actualizada por Oracle, así como por una comunidad activa de desarrolladores.

Características:
* __Código abierto__: disponible de forma gratuita y su código fuente está abierto para modificaciones y redistribución bajo la licencia GPL.
* __Características completas de SQL__: soporta transacciones ACID, procedimientos almacenados, triggers, vistas, y muchas de las funcionalidades estándar de SQL.
* __Motores de almacenamiento__: Incluye InnoDB para transacciones y MyISAM para rendimiento de lectura rápida, entre otros motores de almacenamiento.
* __Actualizaciones y parches de seguridad__: recibe actualizaciones regulares y parches de seguridad de la comunidad y de Oracle.
* __Soporte comunitario__: el soporte es proporcionado por la comunidad de usuarios a través de foros, documentación en línea y recursos de la comunidad.

Uso Común:
* Ideal para pequeñas y medianas empresas, desarrolladores, aplicaciones web, y cualquier proyecto que busque una solución de base de datos potente sin costo asociado.

A continuación, se muestra un ejemplo de sentencias SQL en un SGBD MySQL para crear una tabla y un índice, e insertar registros en la tabla:

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
* __CREATE TABLE clientes (...)__: crea una tabla llamada clientes con las siguientes columnas:
 * __id INT PRIMARY KEY__: define el campo id como un entero y clave primaria de la tabla, lo que garantiza que cada registro sea único.
 * __nombre VARCHAR(50)__: almacena los nombres con un máximo de 50 caracteres.
 * __correo VARCHAR(50)__: almacena las direcciones de correo electrónico con un máximo de 50 caracteres.
 * __fecha_registro DATE__: almacena las fechas en formato YYYY-MM-DD.
* __CREATE INDEX idx_correo ON clientes(correo);__: crea un índice llamado idx_correo en la columna correo para mejorar el rendimiento de las búsquedas y consultas basadas en el correo electrónico.
* __INSERT INTO clientes (...) VALUES (...)__: inserta los 5 registros especificados con sus respectivos datos de ID, nombre, correo y fecha de registro.

Para buscar el registro con id = 4, puedes usar el comando _SELECT_ con la cláusula _WHERE_ para filtrar por el _id_:

```SQL
-- Consulta SQL para buscar el registro con id = 4
SELECT * FROM clientes WHERE id = 4;
```

__MySQL Enterprise Edition__

 Es la versión comercial y de pago de MySQL, diseñada para aplicaciones empresariales que requieren un alto nivel de soporte, seguridad y características adicionales que no están disponibles en la Community Edition.

Características Adicionales:
* Soporte técnico profesional: soporte 24/7 proporcionado por Oracle con opciones de asistencia telefónica y por correo electrónico.
* Monitoreo y administración: incluye MySQL Enterprise Monitor para la supervisión en tiempo real del rendimiento y la seguridad.
* Seguridad avanzada: características de seguridad adicionales como el cifrado de datos en reposo, autenticación avanzada y auditoría.
* Alta disponibilidad: herramientas avanzadas de replicación y alta disponibilidad, incluyendo MySQL InnoDB Cluster y MySQL Router para configuraciones de alta disponibilidad.
* Backup y recuperación Avanzada: MySQL Enterprise Backup proporciona copias de seguridad sin interrupciones y recuperación rápida, incluso para grandes volúmenes de datos.
* MySQL enterprise audit: herramientas de auditoría para el cumplimiento de normativas y la supervisión de la actividad de la base de datos.
* Licencia: requiere una suscripción de pago, que incluye el derecho de uso de las herramientas adicionales y acceso a parches de seguridad exclusivos antes de su publicación en Community Edition.

Uso Común:
* Utilizada por grandes corporaciones, bancos, gobiernos y cualquier entidad que necesite características avanzadas de seguridad, soporte y alta disponibilidad.

Resumen:
* __MySQL Community Edition__: ideal para desarrolladores, proyectos de código abierto y pequeñas empresas que necesitan una solución robusta sin costo.
* __MySQL Enterprise Edition__: dirigida a entornos empresariales donde la seguridad, soporte, y alta disponibilidad son esenciales y justifican el costo adicional de la licencia.

> __Nota__: ambas versiones son muy potentes, pero la elección dependerá de las necesidades específicas del proyecto y los recursos disponibles para su mantenimiento y soporte.

MySQL utiliza una versión personalizada del lenguaje SQL basada en los estándares SQL, como SQL-92, SQL:1999, SQL:2003, SQL:2008, SQL:2011 y SQL:2016, pero incluye extensiones y características específicas que no siempre cumplen al 100% con estos estándares.

MySQL sigue principalmente los estándares de _SQL-92_ y ha ido incorporando características de versiones más recientes del estándar SQL, como _SQL:1999_, _SQL:2003_, _SQL:2008_, y _SQL:2011_. Sin embargo, MySQL no implementa completamente todos los aspectos de estos estándares y a menudo tiene su propia manera de manejar ciertas funcionalidades. MySQL ha añadido muchas extensiones y características propias que no están necesariamente alineadas con los estándares oficiales. Estas extensiones incluyen funciones específicas, tipos de datos adicionales, y características de optimización. Por ejemplo, MySQL tiene su propia manera de manejar funciones de agregación, variables de usuario, y procedimientos almacenados, que pueden diferir de las implementaciones estrictamente estandarizadas.

Compatibilidad con otros Sistemas Gestores de Bases de Datos:
* MySQL puede tener pequeñas diferencias en la implementación de algunos comandos SQL en comparación con otros sistemas de bases de datos que siguen estrictamente los estándares, como PostgreSQL o SQL Server.

Versiones de MySQL:

| **Versión de MySQL** | **Año de Lanzamiento** |
|-----------------------|------------------------|
| MySQL 1.0             | 1995                   |
| MySQL 3.11            | 1996                   |
| MySQL 3.20            | 1997                   |
| MySQL 3.21            | 1998                   |
| MySQL 3.22            | 1998                   |
| MySQL 3.23            | 2000                   |
| MySQL 4.0             | 2003                   |
| MySQL 4.1             | 2004                   |
| MySQL 5.0             | 2005                   |
| MySQL 5.1             | 2008                   |
| MySQL 5.5             | 2010                   |
| MySQL 5.6             | 2013                   |
| MySQL 5.7             | 2015                   |
| MySQL 8.0             | 2018                   |

Las versiones de MySQL no siguen una numeración continua. Por ejemplo, después de MySQL 5.7 se pasó directamente a MySQL 8.0, omitiendo las versiones 6.x y 7.x por diversas razones internas de desarrollo.
MySQL 8.0 es la versión más actual (a partir de 2024) y ha introducido importantes mejoras en rendimiento, seguridad, y compatibilidad con los estándares SQL más recientes.

### MariaDB

![][03]

MariaDB es un sistema de bases de datos relacional desarrollado como un fork de MySQL por los creadores originales de MySQL. Se diseñó como una alternativa gratuita y abierta tras la adquisición de MySQL por Oracle, manteniendo compatibilidad con las versiones de MySQL pero añadiendo mejoras de rendimiento y nuevas características:
* Totalmente compatible con MySQL en términos de comandos, bibliotecas y API.
* Mejoras en rendimiento y seguridad en comparación con MySQL, con características como motores de almacenamiento avanzados (Aria, XtraDB).
* Soporte mejorado para transacciones, particionamiento y replicación.
* Ciclos de desarrollo más rápidos y transparentes con nuevas funcionalidades y optimizaciones.

Es la opción preferida para los desarrolladores que buscan una alternativa más libre y abierta a MySQL, con adopción creciente en proyectos de código abierto.

Versiones de MariaDB y su compatibilidad con MySQL:

| **Versión de MariaDB** | **Año de Lanzamiento** | **Compatibilidad con MySQL**          |
|-------------------------|------------------------|---------------------------------------|
| MariaDB 5.1             | 2009                   | Compatible con MySQL 5.1             |
| MariaDB 5.2             | 2010                   | Compatible con MySQL 5.1             |
| MariaDB 5.3             | 2011                   | Compatible con MySQL 5.1             |
| MariaDB 5.5             | 2012                   | Compatible con MySQL 5.5             |
| MariaDB 10.0            | 2014                   | Compatible con MySQL 5.6             |
| MariaDB 10.1            | 2015                   | Compatible con MySQL 5.6             |
| MariaDB 10.2            | 2017                   | Compatible con MySQL 5.7             |
| MariaDB 10.3            | 2018                   | Compatible con MySQL 5.7             |
| MariaDB 10.4            | 2019                   | Parcialmente compatible con MySQL 5.7|
| MariaDB 10.5            | 2020                   | Parcialmente compatible con MySQL 8.0|
| MariaDB 10.6            | 2021                   | Parcialmente compatible con MySQL 8.0|
| MariaDB 10.7            | 2021                   | Parcialmente compatible con MySQL 8.0|
| MariaDB 10.8            | 2022                   | Parcialmente compatible con MySQL 8.0|
| MariaDB 10.9            | 2022                   | Parcialmente compatible con MySQL 8.0|
| MariaDB 10.10           | 2022                   | Parcialmente compatible con MySQL 8.0|
| MariaDB 10.11           | 2023                   | Parcialmente compatible con MySQL 8.0|

Notas sobre compatibilidad:
* __Versiones iniciales (5.1 - 5.5)__: las primeras versiones de MariaDB fueron desarrolladas como reemplazos directos de MySQL y mantienen una alta compatibilidad en cuanto a comandos SQL, estructuras de datos y funciones básicas.
* __Versiones 10.x__: A partir de MariaDB 10.0, se empezaron a añadir características que no están presentes en MySQL y se mejoraron algunas funciones, lo que ocasionó algunas diferencias y limitaciones en la compatibilidad bidireccional.
* __Compatibilidad con MySQL 8.0__: MariaDB no es completamente compatible con MySQL 8.0 debido a diferencias en la implementación de algunos comandos, tipos de datos, y funciones específicas.

> __Nota__: MariaDB sigue siendo en gran parte compatible con MySQL, especialmente en sus primeras versiones, pero a medida que ha evolucionado, ha introducido características propias que pueden causar diferencias en ciertos casos de uso.

MariaDB utiliza una versión propia del lenguaje SQL basada en los estándares SQL, similar a MySQL, pero con sus propias extensiones y mejoras que la diferencian. MariaDB sigue principalmente los estándares SQL-92, SQL:1999, SQL:2003, SQL:2008, SQL:2011, y SQL:2016. Sin embargo, al igual que MySQL, MariaDB no implementa completamente todos los aspectos de estos estándares y tiene algunas variaciones y extensiones propias. La versión SQL implementada en MariaDB incluye soporte para transacciones ACID, subconsultas, funciones de ventana, y otros elementos avanzados de los estándares SQL modernos.

Aunque MariaDB sigue una línea de compatibilidad con MySQL, las versiones más recientes (a partir de MariaDB 10.4) han empezado a incluir características que no están presentes en MySQL, lo que puede llevar a comportamientos ligeramente diferentes o a la falta de compatibilidad bidireccional en ciertos casos.

MariaDB utiliza una versión personalizada del lenguaje SQL basada en los estándares SQL reconocidos, con extensiones propias para mejorar el rendimiento, la flexibilidad, y la funcionalidad. La compatibilidad con MySQL es alta, especialmente en versiones anteriores, pero MariaDB sigue evolucionando con características únicas que lo distinguen en el ecosistema de bases de datos.

### Oracle Database

![][04]

Oracle Database es uno de los Sistemas Gestores de Bases de Datos más robustos y completos del mercado, desarrollado por Oracle Corporation. Es ampliamente utilizado en grandes corporaciones y entornos empresariales por su capacidad para manejar enormes volúmenes de datos y alta disponibilidad.

Características:
* Soporta características avanzadas como transacciones distribuidas, alta disponibilidad, y recuperación ante desastres (Oracle RAC, Data Guard).
* Optimización de rendimiento con particionamiento avanzado y paralelismo.
* Seguridad avanzada con opciones de cifrado, autenticación y auditoría.
* Soporte para procedimientos almacenados y extensiones propias (PL/SQL).

Utilizado en grandes empresas, bancos, telecomunicaciones, y cualquier entorno que requiera alta fiabilidad, escalabilidad y seguridad.

A continuación, se muestra una tabla con las versiones principales de Oracle Database y sus respectivos años de lanzamiento:

| **Versión de Oracle** | **Año de Lanzamiento** |
|------------------------|------------------------|
| Oracle V2              | 1979                   |
| Oracle 3               | 1983                   |
| Oracle 4               | 1984                   |
| Oracle 5               | 1985                   |
| Oracle 6               | 1988                   |
| Oracle 7               | 1992                   |
| Oracle 8               | 1997                   |
| Oracle 8i              | 1999                   |
| Oracle 9i              | 2001                   |
| Oracle 10g             | 2003                   |
| Oracle 11g             | 2007                   |
| Oracle 12c             | 2013                   |
| Oracle 18c             | 2018                   |
| Oracle 19c             | 2019                   |
| Oracle 21c             | 2021                   |
| Oracle 23c (beta)      | 2023                   |

Notas:
* Oracle V2 fue la primera versión comercializada de Oracle (no hubo versión 1).
* Las versiones 8i, 9i, y 10g introdujeron características importantes como la integración con Internet (i) y computación grid (g).
* Oracle 12c introdujo la arquitectura multitenant, que permite la gestión de múltiples bases de datos como contenedores.
* Oracle 18c y 19c forman parte de la estrategia de versiones anuales, con el año de lanzamiento reflejado en el número de la versión.
* Oracle 23c es la versión más reciente anunciada, actualmente en fase beta.

### PostgreSQL

![][05]

Descripción: PostgreSQL es un sistema de bases de datos relacional de código abierto, conocido por su robustez, extensibilidad y cumplimiento de estándares SQL. A menudo es referido como la base de datos de código abierto más avanzada del mundo.
Características:
Soporte avanzado para transacciones ACID, integridad referencial y concurrencia sin bloqueos.
Ampliamente extensible, permitiendo añadir funciones personalizadas, tipos de datos y operadores.
Soporte para JSON y JSONB, permitiendo trabajar con datos semi-estructurados como en bases de datos NoSQL.
Amplias capacidades de replicación y opciones de alta disponibilidad.
Uso Común: Preferido por desarrolladores para aplicaciones web, análisis de datos, sistemas GIS, y aplicaciones que requieren complejas consultas y alta integridad de datos.

Aquí tienes una tabla en formato Markdown con las versiones principales de PostgreSQL y sus respectivos años de lanzamiento:

| **Versión de PostgreSQL** | **Año de Lanzamiento** |
|---------------------------|------------------------|
| PostgreSQL 6.0            | 1997                   |
| PostgreSQL 6.1            | 1997                   |
| PostgreSQL 6.2            | 1997                   |
| PostgreSQL 6.3            | 1998                   |
| PostgreSQL 6.4            | 1998                   |
| PostgreSQL 6.5            | 1999                   |
| PostgreSQL 7.0            | 2000                   |
| PostgreSQL 7.1            | 2001                   |
| PostgreSQL 7.2            | 2002                   |
| PostgreSQL 7.3            | 2002                   |
| PostgreSQL 7.4            | 2003                   |
| PostgreSQL 8.0            | 2005                   |
| PostgreSQL 8.1            | 2005                   |
| PostgreSQL 8.2            | 2006                   |
| PostgreSQL 8.3            | 2008                   |
| PostgreSQL 8.4            | 2009                   |
| PostgreSQL 9.0            | 2010                   |
| PostgreSQL 9.1            | 2011                   |
| PostgreSQL 9.2            | 2012                   |
| PostgreSQL 9.3            | 2013                   |
| PostgreSQL 9.4            | 2014                   |
| PostgreSQL 9.5            | 2016                   |
| PostgreSQL 9.6            | 2016                   |
| PostgreSQL 10             | 2017                   |
| PostgreSQL 11             | 2018                   |
| PostgreSQL 12             | 2019                   |
| PostgreSQL 13             | 2020                   |
| PostgreSQL 14             | 2021                   |
| PostgreSQL 15             | 2022                   |

Notas:
* PostgreSQL comenzó a numerarse con la versión 6.0 tras su separación del proyecto original de Ingres y el inicio del desarrollo independiente.
* Las versiones más recientes han adoptado un esquema de numeración más simple (10, 11, etc.) en lugar del formato anterior (9.x).
* Cada versión de PostgreSQL suele introducir mejoras en rendimiento, nuevas características SQL, y mayor soporte para tipos de datos avanzados y estándares de integridad.
* Esta tabla refleja la evolución de PostgreSQL a lo largo de los años, destacando su desarrollo continuo y su adopción como una de las bases de datos relacionales más avanzadas y confiables.

PostgreSQL utiliza una versión del lenguaje SQL que se adhiere de cerca a los estándares internacionales, incluyendo características de las especificaciones más recientes de SQL, como SQL:2011, SQL:2016, y SQL:2019. PostgreSQL es conocido por su cumplimiento con los estándares SQL y por su capacidad de incorporar funcionalidades avanzadas y extensiones propias.

PostgreSQL, a lo largo de sus versiones, ha ido incorporando cada vez más características de los estándares SQL, desde SQL-92 hasta los más recientes, como SQL:2016 y SQL:2019. A continuación, te detallo cómo cada versión principal de PostgreSQL ha ido adoptando y extendiendo estos estándares.

La siguiente tabla muestra las versiones de PostgreSQL y los estándares SQL que implementa cada una:

| **Versión de PostgreSQL** | **Estándar SQL Implementado**        | **Notas**                                                                                       |
|---------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------|
| PostgreSQL 6.x            | SQL-92                               | Introducción de características básicas del estándar SQL-92.                                  |
| PostgreSQL 7.x            | SQL-92 y SQL:1999                    | Soporte mejorado para subconsultas y funciones agregadas.                                     |
| PostgreSQL 8.0            | SQL:1999                             | Introducción de transacciones avanzadas, y mejoras en subconsultas y procedimientos.          |
| PostgreSQL 8.4            | SQL:2003                             | Incorporación de funciones de ventana y CTEs (Common Table Expressions).                      |
| PostgreSQL 9.0            | SQL:2003 y SQL:2008                  | Soporte para replicación y gestión de datos XML.                                              |
| PostgreSQL 9.1            | SQL:2008                             | Implementación de funciones de ventana y soporte para estándares avanzados de transacciones.  |
| PostgreSQL 9.3            | SQL:2011                             | Mejoras en manejo de JSON y funciones avanzadas en las consultas.                             |
| PostgreSQL 9.4            | SQL:2011 y SQL:2016                  | Introducción de JSONB, un formato binario de JSON más rápido y eficiente.                     |
| PostgreSQL 9.6            | SQL:2016                             | Mejoras en paralelismo de consultas y soporte de funciones avanzadas de manejo de datos.      |
| PostgreSQL 10             | SQL:2016                             | Soporte para declarative table partitioning y mejoras en el paralelismo y en funciones JSON.  |
| PostgreSQL 11             | SQL:2016                             | Introducción de mejoras en el manejo de índices y más funciones de ventana.                   |
| PostgreSQL 12             | SQL:2016 y parciales de SQL:2019     | Optimización en consultas con particionamiento y mejoras en la gestión de JSON y funciones.   |
| PostgreSQL 13             | SQL:2016 y características de SQL:2019| Mejoras en índices y funciones avanzadas, con soporte parcial para funcionalidades SQL:2019.  |
| PostgreSQL 14             | SQL:2016 y características de SQL:2019| Nuevas funciones de ventana y mejoras en el rendimiento del sistema de transacciones.         |
| PostgreSQL 15             | SQL:2016 y algunas de SQL:2019       | Incorporación de nuevas funciones SQL avanzadas y soporte de tipos de datos adicionales.      |

Esta tabla refleja cómo PostgreSQL ha ido incorporando y mejorando las características de los estándares SQL a lo largo de sus versiones, destacando su enfoque en la compatibilidad y la innovación en la funcionalidad de bases de datos.

A continuación, se muestra un ejemplo de sentencias SQL en un SGBD PostgreSQL para crear una tabla y un índice, e insertar registros en la tabla:

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

Para buscar el registro con id = 4, puedes usar el comando _SELECT_ con la cláusula _WHERE_ para filtrar por el _id_:

```SQL
-- Consulta SQL para buscar el registro con id = 4
SELECT * FROM clientes WHERE id = 4;
```

Descripción de los comandos:
* __CREATE TABLE clientes (...)__: crea una tabla llamada clientes con las siguientes columnas:
  * __id INT PRIMARY KEY__: define el campo id como un entero y clave primaria de la tabla, garantizando que cada registro sea único.
  * __nombre VARCHAR(50)__: almacena los nombres con un máximo de 50 caracteres.
  * __correo VARCHAR(50)__: almacena las direcciones de correo electrónico con un máximo de 50 caracteres.
  * __fecha_registro DATE__: almacena las fechas en formato YYYY-MM-DD.
* __CREATE INDEX idx_correo ON clientes(correo);__: crea un índice llamado idx_correo en la columna correo para mejorar el rendimiento de las búsquedas y consultas basadas en el correo electrónico.
* __INSERT INTO clientes (...) VALUES (...)__: inserta los 5 registros especificados con sus respectivos datos de id, nombre, correo y fecha de registro.

### SQLite

![][06]

SQLite es un motor de bases de datos embebido, ligero y de código abierto que no requiere una configuración de servidor separado.

Algunas de sus características son:
* Extremadamente ligero y fácil de integrar en aplicaciones.
* No requiere configuración de servidor ni administración de usuarios.
* Ideal para aplicaciones pequeñas y medianas con necesidades de almacenamiento local.
* Soporta transacciones ACID, lo que garantiza la integridad de los datos.

Utilizado en aplicaciones móviles (iOS y Android), navegadores web, software de escritorio, y pequeños dispositivos embebidos.


### SQL Server (Microsoft SQL Server)

![][07]

Descripción: SQL Server es un sistema de gestión de bases de datos relacional desarrollado por Microsoft. Es conocido por su integración con el ecosistema de productos de Microsoft y su capacidad para manejar datos a gran escala.
Características:
Soporte para transacciones ACID, procedimientos almacenados, y funcionalidades avanzadas de seguridad.
Integración estrecha con otros productos de Microsoft como Azure, .NET, y Visual Studio.
Capacidades de Business Intelligence con herramientas como SQL Server Reporting Services (SSRS) y SQL Server Integration Services (SSIS).
Alta disponibilidad con características como AlwaysOn Availability Groups.
Uso Común: Utilizado ampliamente en entornos empresariales, aplicaciones comerciales, sistemas de gestión, y como backend para aplicaciones .NET.
Conclusión
Cada sistema de bases de datos tiene sus fortalezas y aplicaciones específicas, desde la ligereza de SQLite hasta la robustez de Oracle y SQL Server. La elección del sistema adecuado depende de factores como el tamaño de los datos, la complejidad de las consultas, la necesidad de escalabilidad, y el entorno en el que se va a desplegar la aplicación. En la actualidad, las bases de datos relacionales siguen siendo esenciales para la mayoría de las aplicaciones empresariales, sitios web, y servicios en la nube debido a su capacidad para gestionar datos de forma estructurada y fiable.

## Sistemas Gestores de Bases de Datos NoSQL

MongoDB

![][08]

Redis

![][09]

## Ofertas de Empleo 1

oferta empleo 1

oferta empleo 2

oferta empleo 3

[01]: ../img/ut01/db-engines.png "01"
[02]: ../img/ut01/mysql-logo.png "02"
[03]: ../img/ut01/mariadb-logo.png "03"
[04]: ../img/ut01/oracle-logo.png "04"
[05]: ../img/ut01/postgresql-logo.png "05"
[06]: ../img/ut01/sqlite3-logo.png "06"
[07]: ../img/ut01/sqlsersqlite3-logo.png "07"
[08]: ../img/ut01/sqlserver-logo.png "08"
[09]: ../img/ut01/mongodb-logo.png "09"
[10]: ../img/ut01/redis-logo.png "10"
