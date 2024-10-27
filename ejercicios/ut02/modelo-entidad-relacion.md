# Modelo Entidad/Relación (Ejercicios)

__Ejercicio 1__

A partir del siguiente enunciado se desea realizar el modelo entidad-relación.

Una empresa vende productos a varios clientes. Se necesita conocer los datos personales de los clientes (nombre, apellidos, dni, dirección y fecha de nacimiento). La dirección del cliente debe contemplar el tipo de vía, el nombre, el número y el código postal. Cada producto tiene un nombre y un código, así como un precio unitario. Un cliente puede comprar varios productos a la empresa, y un mismo producto puede ser comprado por varios clientes.

Se debe tener en cuenta que un producto solo puede ser suministrado por un proveedor, y que un proveedor puede suministrar diferentes productos. De cada proveedor se desea conocer el NIF, nombre y dirección.

__Ejercicio 2__

A partir del siguiente enunciado diseñar el modelo entidad-relación.

Se desea diseñar la base de datos de un Instituto. En la base de datos se desea guardar los datos de los profesores del Instituto (DNI, nombre, dirección y teléfono). Los profesores imparten módulos, y cada módulo tiene un código y un nombre. Cada alumno está matriculado en uno o varios módulos. De cada alumno se desea guardar el nº de expediente, nombre, apellidos y fecha de nacimiento. Los profesores pueden impartir varios módulos, pero un módulo sólo puede ser impartido por un profesor. Cada curso tiene un grupo de alumnos, uno de los cuales es el delegado del grupo.

__Ejercicio 3__

A partir del siguiente enunciado diseñar el modelo entidad-relación.

Se desea diseñar una BD de una entidad bancaria que contenga información sobre los clientes, las cuentas, las sucursales y las transacciones producidas. Construir el Modelo E/R teniendo en cuenta las siguientes restricciones:

* Una transacción viene determinada por un número de transacción (único para cada cuenta), la fecha y la cantidad.
* Un cliente puede tener muchas cuentas.
* Una cuenta puede ser de muchos clientes.
* Una cuenta sólo puede estar en una sucursal.

__Ejercicio 4__

A partir del siguiente enunciado diseñar el modelo entidad-relación.

Se desea informatizar la gestión de una tienda informática. La tienda dispone de una serie de productos que se pueden vender a los clientes.

De cada producto informático se desea guardar el código, descripción, precio y número de existencias. De cada cliente se desea guardar el código, nombre, apellidos, dirección y número de teléfono.

Un cliente puede comprar varios productos en la tienda y un mismo producto puede ser comprado por varios clientes. Cada vez que se compre un artículo quedará registrada la compra en la base de datos junto con la fecha en la que se ha comprado el artículo. La tienda tiene contactos con varios proveedores que son los que suministran los productos. Un mismo producto puede ser suministrado por varios proveedores. De cada proveedor se desea guardar el código, nombre, apellidos, dirección, provincia y número de teléfono"

__Ejercicio 5__

A partir del siguiente enunciado diseñar el modelo entidad-relación.

Una clínica necesita llevar un control informatizado de su gestión de pacientes y médicos.

De cada paciente se desea guardar el código, nombre, apellidos, dirección, población, provincia, código postal, teléfono y fecha de nacimiento.

De cada médico se desea guardar el código, nombre, apellidos, teléfono y especialidad.

Se desea llevar el control de cada uno de los ingresos que el paciente hace en el hospital. Cada ingreso que realiza el paciente queda registrado en la base de datos. De cada ingreso se guarda el código de ingreso (que se incrementará automáticamente cada vez que el paciente realice un ingreso), el número de habitación y cama en la que el paciente realiza el ingreso y la fecha de ingreso.

Un médico puede atender varios ingresos, pero un ingreso solamente puede ser atendido por un único médico. Un paciente puede realizar varios ingresos en el hospital.
