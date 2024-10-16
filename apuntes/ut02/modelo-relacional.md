# Modelo Relacional

## Introducción

Los __Sistemas de Gestión de Bases de Datos__ (SGBD) se pueden clasificar según diferentes criterios, como el modelo lógico que soportan, el número de usuarios que pueden gestionar simultáneamente, el número de puestos de trabajo, o incluso el coste. Sin embargo, la clasificación más significativa de los SGBD está relacionada con el modelo lógico que utilizan. Los principales modelos que predominan en el mercado son:

* __Modelo Jerárquico__: este modelo organiza los datos en una estructura de árbol, donde cada nodo padre puede tener varios nodos hijo, pero cada nodo hijo tiene un solo nodo padre.
* __Modelo en Red__: similar al modelo jerárquico, pero más flexible, ya que permite que un nodo hijo tenga múltiples nodos padre, lo que facilita las relaciones más complejas entre datos.
* __Modelo Relacional__: este es el modelo más común y se basa en tablas bidimensionales que representan las entidades y sus relaciones. Este es el modelo en el que nos vamos a centrar.
* __Modelo Orientado a Objetos__: este modelo combina conceptos de bases de datos con los principios de la programación orientada a objetos, permitiendo almacenar objetos completos en la base de datos.

El modelo relacional ha dominado el mercado de los SGBD principalmente por dos razones:

* __Fundamentos sólidos__: el modelo relacional se basa en el álgebra relacional, que es un modelo matemático con principios bien establecidos, lo que le otorga una base teórica robusta y confiable. Esto garantiza un manejo de datos eficaz y coherente.
* __Simplicidad y eficacia__: el modelo relacional utiliza tablas (también llamadas relaciones) como estructura fundamental, lo que resulta en un sistema simple pero potente para representar y manipular los datos. Las tablas están formadas por filas y columnas, donde cada fila (o tupla) representa una instancia de una entidad, y cada columna (o atributo) representa una propiedad de dicha entidad.

Si en una base de datos queremos representar la entidad __PERSONA__, el modelo relacional la traducirá a una tabla llamada "_PERSONAS_". Los atributos de la entidad, como nombre, edad, y dirección, se convertirán en las columnas de la tabla. Cada fila de la tabla "_PERSONAS_" contendrá los datos específicos de una persona, es decir, cada fila será un registro o una instancia de la entidad _PERSONA_.

Este enfoque permite que las bases de datos relacionales sean fácilmente escalables y adaptables a una gran variedad de aplicaciones, lo que contribuye a su popularidad y uso extendido en muchos sistemas comerciales y de gestión de información.

### Estructura de datos relacional

| D.N.I.     | Nombre   | Apellido  | Nacimiento  | Sexo | Estado civil |
|------------|----------|-----------|-------------|------|--------------|
| 45.123.654 | Pedro    | Gómez     | 12/03/1980  | H    | Casado       |
| 23.456.789 | Ana      | Martínez  | 05/07/1975  | M    | Soltera      |
| 78.654.321 | Carlos   | Pérez     | 19/11/1990  | H    | Divorciado   |

En el modelo relacional, una relación se refiere únicamente a la definición estructural de una tabla. Esta definición incluye el nombre de la relación (o tabla) y la lista de atributos que componen dicha tabla. Es importante destacar que, en este contexto, la relación no implica aún los datos almacenados, sino que se enfoca exclusivamente en cómo está organizada la tabla.

Una manera de representar esta definición sería listando el nombre de la relación seguido de los nombres de los atributos que la conforman. Por ejemplo:

* __Relación__: PERSONAS
* __Atributos__: D.N.I., Nombre, Apellido, Fecha de Nacimiento, Sexo, Estado Civil

En este caso, se define la estructura de la tabla PERSONAS con sus correspondientes atributos o columnas, como el D.N.I., el Nombre, el Apellido, etc.

![][01]

Para identificar de manera única cada registro en una tabla del modelo relacional, se utiliza lo que se conoce como clave primaria o principal. Esta clave se compone de uno o varios atributos de la tabla, y su función es garantizar que no haya dos registros (filas) con el mismo valor en estos atributos.

En algunas tablas, puede haber más de una combinación de atributos que permita identificar de manera única una fila; estas combinaciones se conocen como claves candidatas. Sin embargo, entre todas las claves candidatas, se selecciona una que será utilizada como la clave primaria de la relación. Es importante destacar que los atributos que forman parte de la clave primaria no pueden contener valores nulos, ya que su función es asegurar la unicidad de los registros.

* __Clave primaria__: atributo o conjunto de atributos que identifican de manera única cada fila de una tabla. No pueden ser nulos.
* __Claves candidatas__: otras combinaciones posibles de atributos que también podrían identificar unívocamente las filas, pero de las cuales solo una se elige como clave primaria.

### Elementos y propiedades del modelo relacional

Una relación o tabla en el modelo relacional representa las entidades de las que se desea almacenar información en la base de datos (BD). Está compuesta por:

* __Filas__ (también llamadas _registros_ o _tuplas_): cada fila representa una ocurrencia específica de la entidad.
* __Columnas__ (también conocidas como _atributos_ o _campos_): cada columna corresponde a una propiedad de la entidad.

Propiedades de las relaciones:

* __Nombre único__: cada relación tiene un nombre distinto de todas las demás relaciones en la misma base de datos.
* __Nombres de atributos únicos__: no pueden existir dos atributos con el mismo nombre dentro de la misma relación.
* __El orden de los atributos no es importante__: no hay un orden fijo para las columnas o atributos.
* __Tuplas únicas__: cada tupla debe ser única; no se permiten tuplas duplicadas en una relación. Como mínimo, las tuplas deben diferenciarse en su clave primaria.
* __El orden de las tuplas no es importante__: no hay un orden predeterminado para los registros o filas en la tabla.

Conceptos clave:

* __Clave candidata__: es un atributo o conjunto de atributos que puede identificar de manera única una tupla en la relación. Existen varias claves candidatas, y cualquiera de ellas podría usarse como clave principal.
* __Clave principal__: es la clave candidata que se elige como identificador único de las tuplas. Sirve para asegurar que cada registro en la tabla sea único.
* __Clave alternativa__: todas las claves candidatas que no se seleccionan como clave principal se denominan claves alternativas.
* __Integridad de la entidad__: la clave principal no puede contener valores nulos. Esto garantiza que cada tupla esté identificada de manera única.
* __Dominio de un atributo__: el conjunto de valores permitidos que un atributo puede asumir.
* __Clave externa__ (_foránea_ o _ajena_): es un atributo o conjunto de atributos que actúa como clave principal en otra relación. Las claves externas son fundamentales para mantener la integridad referencial, ya que los valores presentes en la clave externa deben coincidir con valores existentes en la clave principal de la tabla relacionada.

Este conjunto de reglas asegura la coherencia y consistencia de los datos en una base de datos relacional, permitiendo una organización eficiente y evitando duplicidades o inconsistencias en la información.

### Transformación de un esquema E/R a un esquema relacional

Para traducir un Modelo Entidad/Relación (E/R) al modelo relacional, se deben seguir varias reglas o normas que guían el proceso de transformación de las entidades, relaciones y atributos del modelo conceptual a una estructura lógica basada en tablas.


[01]: ../img/ut02/modelo-relacional01.png "01"