# Tipos de Datos

* Números Enteros
* Números en Punto Flotante (Valores Aproximados)
* Números en Punto Fijo (Valores Exactos)
* Fechas y Tiempo
* JSON (Formato de Datos Estructurados)

## Introducción

En MySQL, los datos se almacenan en diferentes formatos dependiendo de su tipo. A continuación, se detallan los principales tipos de datos disponibles.

## Números Enteros

Los números enteros almacenan valores sin decimales y pueden ser SIGNED (con signo) o UNSIGNED (sin signo).

| **Tipo**             | **Bytes** | **Mínimo**                  | **Máximo**                  |
|----------------------|----------|-----------------------------|-----------------------------|
| `TINYINT`           | 1        | -128                         | 127                         |
| `TINYINT UNSIGNED`  | 1        | 0                            | 255                         |
| `SMALLINT`          | 2        | -32,768                      | 32,767                      |
| `SMALLINT UNSIGNED` | 2        | 0                            | 65,535                      |
| `MEDIUMINT`         | 3        | -8,388,608                   | 8,388,607                   |
| `MEDIUMINT UNSIGNED`| 3        | 0                            | 16,777,215                  |
| `INT` o `INTEGER`   | 4        | -2,147,483,648               | 2,147,483,647               |
| `INT UNSIGNED`      | 4        | 0                            | 4,294,967,295               |
| `BIGINT`            | 8        | -9,223,372,036,854,775,808   | 9,223,372,036,854,775,807   |
| `BIGINT UNSIGNED`   | 8        | 0                            | 18,446,744,073,709,551,615  |

Ejemplo de uso en SQL:

```sql
CREATE TABLE empleados (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  edad TINYINT NOT NULL,
  salario MEDIUMINT
);
```

```sql
INSERT INTO empleados (edad, salario) VALUES (25, 35000);
INSERT INTO empleados (edad, salario) VALUES (30, 45000);
```

## Números en Punto Flotante (Valores Aproximados)

Se utilizan para almacenar valores decimales con precisión aproximada.

| **Tipo**              | **Bytes** | **Mínimo**                      | **Máximo**                      |
|----------------------|----------|---------------------------------|---------------------------------|
| `FLOAT`             | 4        | ±1.175494351E-38                | ±3.402823466E+38               |
| `FLOAT UNSIGNED`    | 4        | 1.175494351E-38                 | 3.402823466E+38                |
| `DOUBLE`            | 8        | ±1.7976931348623157E+308        | ±2.2250738585072014E-308       |
| `DOUBLE UNSIGNED`   | 8        | 1.7976931348623157E+308         | 2.2250738585072014E-308        |

Ejemplo de uso en SQL:

```sql
CREATE TABLE productos (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  precio FLOAT(7,2) NOT NULL
);
```

```sql
INSERT INTO productos (precio) VALUES (99.99);
INSERT INTO productos (precio) VALUES (49.95);
```

## Números en Punto Fijo (Valores Exactos)

Los tipos DECIMAL y NUMERIC almacenan valores exactos, sin pérdida de precisión.

| **Tipo**              | **Bytes**               | **Precisión**                 |
|----------------------|-----------------------|------------------------------|
| `DECIMAL(M,D)`      | `M + 2` bytes si `D > 0` | `M`: Número total de dígitos, `D`: Número de decimales |
| `NUMERIC(M,D)`      | Igual a `DECIMAL`       | Igual a `DECIMAL` |


Ejemplo de uso en SQL:

```sql
CREATE TABLE cuentas (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  saldo DECIMAL(10,2) NOT NULL
);
```

```sql
INSERT INTO cuentas (saldo) VALUES (1500.75);
INSERT INTO cuentas (saldo) VALUES (4200.00);
```

## Fechas y Tiempo

Los tipos de datos de fecha y hora permiten almacenar información temporal.

| **Tipo**       | **Bytes** | **Formato**              | **Rango**                     |
|---------------|----------|------------------------|------------------------------|
| `DATE`       | 3        | `YYYY-MM-DD`           | 1000-01-01 a 9999-12-31     |
| `DATETIME`   | 8        | `YYYY-MM-DD HH:MM:SS`  | 1000-01-01 00:00:00 a 9999-12-31 23:59:59 |
| `TIMESTAMP`  | 4        | `YYYY-MM-DD HH:MM:SS`  | 1970-01-01 00:00:00 a 2038-01-19 03:14:07 |


```sql
CREATE TABLE eventos (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  fecha_evento DATE NOT NULL,
  hora_inicio TIME NOT NULL
);
```

```sql
INSERT INTO eventos (fecha_evento, hora_inicio) VALUES ('2025-12-25', '18:30:00');
INSERT INTO eventos (fecha_evento, hora_inicio) VALUES ('2025-06-15', '14:00:00');
```

## JSON (Formato de Datos Estructurados)

Permite almacenar datos en formato JSON en MySQL.

```sql
CREATE TABLE datos (
  id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  info JSON NOT NULL
);
```

```sql
INSERT INTO datos (info) VALUES ('{"nombre": "Carlos", "edad": 30}');
INSERT INTO datos (info) VALUES ('{"producto": "Laptop", "precio": 1200.99}');
```
