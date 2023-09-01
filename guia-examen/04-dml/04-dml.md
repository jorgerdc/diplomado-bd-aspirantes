# 4. Lenguaje de Manipulación de Datos (SQL-DML)

El lenguaje de manipulación de datos (en inglés Data Manipulation Language, o DML),
permite a los usuarios, introducir, modificar o eliminar  datos.

Los elementos que se utilizan para manipular los datos, son los siguientes:

`insert`, Esta sentencia permite incorporar nuevos registros a una tabla existente en la base de datos.

`update`, sirve para modificar los valores de uno o varios registros.

`delete`, se utiliza para eliminar las filas de una tabla.

## 4.1 Sentencia `insert`

Esta sentencia permite incorporar nuevos registros a una tabla existente en la base de datos.

### 4.1.1 Ejemplos Sentencia `insert`

Sentencias para ingresar registros de formas variadas, como por ejemplo con el orden de creación de columnas, omitiendo el nombre de columnas, incluye una sentencia insert con select.

    ```sql
insert into clientes
( nombre,
  cliente_id,
  ap_paterno,
  genero,
  estado_civil,
  fecha_nacimiento
)
values
('Ivan',1,'Morales','M','SO','20-mar-04');

insert into clientes
values
(2,'Maria','Gonzalez','F','CA',to_date('20-07-2005',
'dd-mm-yyyy') );

insert into clientes
select 3,
       nombre,
       ap_paterno,
       genero,
       estado_civil,
       fecha_nacimiento
from clientes
where cliente_id = 1;

commit;
  
    ```

## 4.2 Sentencia `update`

Esta sentencia modifica un renglón dentro de una tabla de la base de datos.

### 4.2.1 Ejemplos sentencia `update`

Las siguientes sentencias actualizan un  registro particular y varios que cumplen con la igualdad de genero Femenino.

     ```sql

update clientes
set nombre = 'Maribel',
    ap_paterno = 'Garcia'
where cliente_id = 2;

update clientes
set genero = 'f'
where genero = 'F';

commit;
  
     ```

## 4.3 Sentencia `delete`

Este comando elimina un/os renglón/es dentro de una tabla de la base de datos.

### 4.2.1 Ejemplos Sentencia `delete`

Las sentencias a continuación eliminan un registro en particular, confirmando la transacción permanente con commit y se eliminan a todos los clientes, pero esa transacción no se lleva a cabo, por el comando rollback.

     ```sql

delete clientes
where cliente_id = 1;

commit;

delete clientes;

rollback;
  
     ```