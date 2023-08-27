# 4. Lenguaje de Manipulación de Datos (SQL-DML)

El lenguaje de manipulación de datos (en inglés Data Manipulation Language, o DML).
Permite a los usuarios introducir datos para posteriormente realizar tareas de consultas o
modificación de los datos que contienen las Bases de Datos.

Los elementos que se utilizan para manipular los datos, son los siguientes:

    `select`, esta sentencia se utiliza para realizar
    consultas sobre los datos. (Se contempla en parte
    6 en Data Query Languaje, o DQL)

    `insert`, con esta instrucción podemos insertar los valores en una base de datos.

    `update`, sirve para modificar los valores de uno o varios renglones.

    `delete`, se utiliza para eliminar las filas de una tabla.

## 4.1 Sentencia `insert`

Este comando crea un/os renglón/es dentro de una tabla de la base de datos.

### 4.1.1 Ejemplos Sentencia `insert`

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

     ```sql

delete clientes
where cliente_id = 1;

commit;

delete clientes;

rollback;
  
    ```