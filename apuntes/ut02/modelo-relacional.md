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

[01]: ../img/ut02/modelo-relacional01.png "01"