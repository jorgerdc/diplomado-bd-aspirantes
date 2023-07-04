# 3. Lenguaje de Definición de Datos (SQL-DDL)

El lenguaje de definición de datos (en inglés Data Definition Language, o DDL), es el que
se encarga de la modificación de la  estructura de los objetos de la base de datos. Incluye
órdenes para modificar, borrar o definir las tablas en las que se almacenan las base de datos.
Existen cuatro operaciones básicas: CREATE, ALTER, DROP y TRUNCATE.

## CREATE

Este comando crea un objeto dentro de la base de datos. Puede ser un tablespace, una tabla,
un índice, una vista, una tabla de índice organizado, un usuario, un cluster,  una función,
un procedimiento, un trigger.

### Ejemplo

```sql
Create Table ventas  
( producto_id NUMBER(6),  
  cliente_id NUMBER(5),  
  fecha_id DATE,  
  canal_id CHAR(1),  
  promocion_id NUMBER(6), 
  numero_vendido NUMBER(3),  
  cantidad_vendida NUMBER(10,2)
)

PARTITION BY RANGE (fecha_id)
( PARTITION ventas_q1_2022 VALUES LESS THAN (TO_DATE(’01-APR-2022′,’dd-MON-yyyy’))  
TABLESPACE tsa,
PARTITION ventas_q2_2022 VALUES LESS THAN (TO_DATE(’01-JUL-2022′,’dd-MON-yyyy’))  
TABLESPACE tsb,
PARTITION ventas_q3_2022 VALUES LESS THAN (TO_DATE(’01-OCT-2022′,’dd-MON-yyyy’))  
TABLESPACE tsc,
PARTITION ventas_q4_2022 VALUES LESS THAN (TO_DATE(’01-JAN-2022′,’dd-MON-yyyy’))  
TABLESPACE tsd
);  
```

## ALTER

Este comando permite modificar la estructura de un objeto. Se pueden agregar/quitar campos
a una tabla, modificar el tipo de un campo, modificar un trigger, etc.

## DROP

Este comando elimina un objeto de la base de datos. Puede ser una tabla, vista, índice,
trigger, función, procedimiento o cualquier otro objeto.
