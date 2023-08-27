# 3. Lenguaje de Definición de Datos (SQL-DDL)

El lenguaje de definición de datos (en inglés Data Definition Language, o DDL),
es el que se encarga de la modificación de la  estructura de los objetos de la
base de datos. Incluye órdenes para modificar, borrar o definir las tablas en
las que se almacenan las base de datos.
Existen tres operaciones básicas: `create`, `alter` y `drop`.

## 3.1 Sentencia `create`

Esta sentencia crea un objeto dentro de la base de datos. Puede ser un tablespace,
una tabla, un índice, una secuencia (objeto de base de datos que permite la generación
automática de valores), una vista materializada, una tabla de índice organizado,
un usuario, un cluster, una función, un procedimiento, un trigger, un sinónimo (alias para
los objetos de bases de datos de otro servidor, base de datos, esquema).

### 3.1.1 Ejemplos sentencia `create`

```sql
create table clientes
( cliente_id number(5) primary key,
  nombre varchar2(30) not null,
  ap_paterno varchar2(30) not null,
  genero char(1) not null,
  estado_civil char(2) not null,
  fecha_nacimiento date not null
);

  create table productos  
( producto_id number(6) primary key,  
  nombre varchar2(50) not null,
  precio number(6,2) not null
);

  create table ventas
(
  folio_id number(6) not null,
  cliente_id number(5) not null,  
  fecha_id date not null
);

  create table desglose_ventas
(
   folio_id number(6) not null,
   producto_id number(6),
   cantidad number(10,2)
);

 create sequence idfolio
 increment by 1 start with 1;

 create view vista_productos as
 select nombre,
        precio
 from productos
 where precio between 25 and 50;

 create synonym precios_originales
 for fabrica.productos;

 create index indx_nom_prod
 on productos (nombre);


```

### 3.1.2 Algunas vistas del diccionario de datos que almacenan metadatos de los objetos

* dictionary
* user_objects
* all_objects
* dba_objects
* user_tables
* user_tab_columns
* user_constraints
* user_cons_columns
* user_indexes
* user_views
* user_sequences
* user_synonyms
* user_source
* dba_data_files
* dba_profiles
* dba_sys_privs
* dba_roles
* dba_tablespaces
* dba_users
* ....

## 3.2 sentencia `alter`

Esta sentencia permite modificar la estructura de un objeto. Se pueden agregar o
quitar campos (columnas) a una tabla, modificar el tipo de dato de un campo,
modificar un trigger, agregar constraints a una tabla, etc.

### 3.2.1 Ejemplos sentencia `alter`

```sql
alter table ventas add constraint pk_ventas
primary key (folio_id);

alter table desglose_ventas add constraint
pk_desglose_ventas
primary key (folio_id, producto_id);

alter table ventas add constraint fk_ven_cli
foreign key (cliente_id)
reference Clientes (cliente_id);

alter table clientes
add direccion varchar(100) null;

alter table clientes
rename column direccion to direccion_completa;

alter table clientes
modify direccion varchar(150) null;

alter table ventas
disable validate
constraint fk_ven_cli;

alter table ventas
enable validate
constraint fk_ven_cli;

alter table ventas
drop constraint fk_ven_cli;

alter table clientes
drop column direccion;
```

## 3.3 Sentencia `drop`

Esta sentencia elimina un objeto de la base de datos. Puede ser una tabla, vista,
índice, trigger, función, procedimiento o cualquier otro objeto.

### 3.3.1 Ejemplos Sentencia `drop`

```sql
drop table desglose_ventas;

drop index indx_nom_prod;

drop sequence idfolio;

drop synonym precios_originales;

```
