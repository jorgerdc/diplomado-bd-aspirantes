# 6.0 Lenguaje de Consulta de Datos (DQL)

## 6.3 SQL Joins (inner, outer, natural, self, cross)

El operador Join se utiliza para recuperar datos de varias tablas. Se realiza un JOIN
cada vez que se unen dos o más tablas en una instrucción SQL.

Hay diferentes tipos de joins:

* `INNER JOIN` (o`JOIN`)
* `LEFT OUTER JOIN` (o `LEFT JOIN`)
* `RIGHT OUTER JOIN` (o `RIGHT JOIN`)
* `FULL OUTER JOIN` (o `FULL JOIN`)
* `NATURAL JOIN`
* `SELF JOIN`
* `CROSS JOIN`

### 6.3.1 `INNER JOIN`

Es el tipo de join más común. `INNER JOIN` devuelve todos los registros de varias tablas
donde se cumple la condición de combinación.

La sintaxis para `inner join` es:

```sql
select columnas
from tabla1 
inner join tabla2
on tabla1.columna = tabla2.columna;
```

<p align="center"\><img src=img/fig_1.png width="200"\>

* `INNER JOIN` devuelve el área sombreada. Devolverá los registros donde se cruzan tabla1
 y tabla2.

Ejemplo:

```sql
select po.producto_id, pe.proveedor_id
from producto po
inner join proveedor pe
on po.producto_id=pe.producto_id;
```

En este ejemplo se mostrarán todas los registro de los atributos `producto_id` y
`proveedor_id` de las tablas de `proveedor` y `producto` donde haya un valor de
`producto_id` coincidente en las tablas de `proveedor` y `producto`.

### 6.3.2 `LEFT OUTER JOIN`

Este tipo de Join incluye todos los registros que se obtendrían al realizar un
`inner join`, y de forma adicional, todos los registros de la tabla que aparece a la
izquierda de la cláusula `join` que cumplan con las condiciones de la cláusula `where`
sin importar si cumplen o no con la condición de la cláusula `on`. Dicho de otra forma,
obtiene todos los registros de la tabla izquierda sin importar si tienen correspondencia
con los registros de la tabla derecha.

La sintaxis para `left outer join` es:

```sql
select columnas
from tabla1
left [outer] join tabla2
on tabla1.columna = tabla2.columna;
```

La palabra clave `left outer join` se puede reemplazar por `left join`.

<p align="center"\><img src=img/fig_2.png width="200"\></p>

* `LEFT OUTER JOIN` devuelve el área sombreada. Devolverá todos los registros de tabla1 y
solo aquellos registros de tabla2 que se cruzan con tabla1.

Ejemplo:

```sql
select e.empleado_id, p.proyecto_nombre
from empleado e
left outer join proyecto p
on e.empleado_id=p.empleado_id;
```

En este ejemplo se mostrarán todas los registros del atributo empleado_id de la tabla de
empleado y solo aquellos registros de la tabla de proyecto donde el atributo empleado_id
es igual.

Si un valor de empleado_id en la tabla empleado no existe en la tabla de proyecto, el
atributo proyecto_nombre de la tabla de proyecto se mostrarán como null en el conjunto de
resultados.

### 6.3.3 `RIGHT OUTER JOIN`

 Este tipo de Join incluye todos los registros que se obtendrían al realizar un
 `inner join`, y de forma adicional, todos los registros de la tabla que aparece a la
 derecha de la cláusula `join` que cumplan con las condiciones de la cláusula `where` sin
 importar si cumplen o no con la condición de la cláusula `on`. Dicho de otra forma,
 obtiene todos los registros de la tabla derecha sin importar si tienen correspondencia
 con los registros de la tabla izquierda.

La sintaxis para `right outer join` es:

```sql
select columnas
from tabla1
right [outer] join tabla2
on tabla1.columna = tabla2.columna;
```

La palabra clave `right outer join` se puede reemplazar por `right join`.

<p align="center"\><img src=img/fig_3.png width="200"\></p>

`RIGHT OUTER JOIN` devuelve el área sombreada. Devolverá todos los registros de la tabla2
y solo aquellos registros de tabla1 que se cruzan con tabla2.

Ejemplo:

```sql
select pe.pedido_id, pe.pedido_fecha, pv.proveedor_nombre
from proveedor pv
right outer join pedido pe
on pv.proveedor_id = pe.proveedor_id;
```

En este ejemplo se mostrarán todas los registros de la tabla de `pedido` y solo aquellos
registros de la tabla de `proveedor` donde el atributo `proveedor_id` es igual.

Si un valor de `pedido_id` en la tabla de `pedido` no existe en la tabla de `proveedor`, el
atributo `proveedor_nombre` de la tabla `proveedor` se mostrará como null en el conjunto de
resultados.

### 6.3.4 `FULL OUTER JOIN`

Este tipo de join devuelve todas los registros de la tabla de la izquierda y la tabla de
la derecha con valores nulos donde no se cumple la condición de unión.

La sintaxis para `full outer join` es:

```sql
select columnas
from tabla1
full [outer] join tabla2
on tabla1.columna = tabla2.columna;
```

La palabra clave `full outer join` se puede reemplazar por `full join`.

<p align="center"\><img src=img/fig_4.png width="200"\></p>

`FULL OUTER JOIN` devuelve el área sombreada. Devolverá todos los registros de tabla1 y
tabla2.

Ejemplo:

```sql
select pv.proveedor_id, pv.proveedor_nombre, pe.pedido_fecha
from proveedor pv
full outer join pedido pe
on pv.proveedor_id = pe.proveedor_id;
```

En este ejemplo se mostrarán todas los registros de la tabla de `proveedor` y todas los
registros de la tabla de `pedido` y dónde no se cumpla la condición de unión, se mostrarán
nulls en esos registros en el conjunto de resultados.

Si un valor de `proveedor_id` en la tabla de `proveedor` no existe en la tabla de `pedido`,
todos los registros del atributo `pedido_fecha` de la tabla de `pedido` se mostrarán como
null en el conjunto de resultados. Si un valor de `proveedor_id` en la tabla de `pedido`
no existe en la tabla de `proveedor`, todos los registros de los atributos de la tabla de
`proveedor` se mostrarán como null en el conjunto de resultados.

### 6.3.5 `NATURAL JOIN`

Este tipo de join crea una cláusula de unión implícita basada en las columnas comunes de
las dos tablas que se unen. Las columnas comunes son columnas que tienen el mismo nombre
en ambas tablas.

`NATURAL JOIN` puede ser `INNER JOIN`, `LEFT OUTER JOIN` o `RIGHT OUTER JOIN`. El valor
predeterminado es `INNER JOIN`.

La sintaxis para `natural join` es:

```sql
select columnas
from tabla1 natural [ { left | right } [ outer ] | inner ] 
join tabla2;
```

Ejemplo:

```sql
select producto_nombre, pedido_id
from producto
natural join pedido;
```

En este ejemplo existe en ambas tablas el atributo `producto_id`, por lo que
se mostrarán los registros del atributo `producto_nombre` y `pedido_id` de aquellos
productos que coinciden en ambas tablas.

### 6.3.6 `SELF JOIN`

Es un `join` de una tabla consigo misma. Esta tabla aparece dos veces en la cláusula `from`
y va seguida del alias de la tabla que califican los nombres de las columnas en la
condición de combinación. Para realizar un `self join`, se combinan y devuelve las filas
de la tabla que cumplen la condición de unión.

`SELF JOIN` puede ser `INNER JOIN`, `LEFT OUTER JOIN` o `RIGHT OUTER JOIN`. El valor
predeterminado es `INNER JOIN`.

La sintaxis para `SELF JOIN` es:

```sql
select t1.columna, t2.columna
from tabla1 t1 [ { left | right } [ outer ] | inner ]
join tabla1 t2
on t1.columna=t2.columna;
```

Observemos que no existe una cláusula `self join` dentro de la sintaxis, este tipo de
`join` es solo conceptual.

Ejemplo:

```sql
select e1.empleado_id, e2.empleado_sup
from empleado e1
inner join empleado e2
on e1.empleado_id=e2.empleado_sup;
```

En este ejemplo se mostrará a todos los empleados y su empleado supervisor, considerando
que dicha información se encuentra en la misma tabla `empleado`.

### 6.3.7 CROSS JOIN

Es una operación `join` que genera el producto cartesiano de dos tablas. A diferencia de
otros operadores `join`, no le permite especificar una cláusula de unión. `cross join` no
lleva la cláusula `on`, sin embargo, puede especificar una cláusula `where` en la
instrucción `select`.

La sintaxis para CROSS JOIN es:

```sql
select columnas
from tabla1 cross join tabla2;
```

Ejemplo:

```sql
select producto_id, talla_id
from inventario
cross join talla;
```

En este ejemplo se mostrará para cada uno de los productos del inventario cada una de las
tallas que se tienen registradas.
