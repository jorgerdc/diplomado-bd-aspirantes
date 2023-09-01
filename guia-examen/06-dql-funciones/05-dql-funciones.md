# 6.0 Lenguaje de Consulta de Datos (DQL)

## 6.5 Funciones para manejo de fechas, números y cadenas

### 6.5.1 Funciones para manejo de fechas

Existe un variedad de funciones para manejo de fechas, algunas de las más utilizadas son:

`SYSDATE`. Es una función de fecha que devuelve la fecha y hora actual del servidor de
bases de datos.

Ejemplo: Para mostrar la fecha actual

```sql
select sysdate
from dual;

SYSDATE
--------
20/08/23
```

`ADD_MONTHS`. Aumenta o resta la cantidad de meses de una fecha

Ejemplo:

```sql
select add_months(sysdate,4) 
from dual;

ADD_MONT
--------
20/12/23
```

`EXTRACT`. Extrae el tipo de dato (año, mes, día, hora, minuto, segundo) de una fecha
seleccionada. Utiliza year, month, day, minute y second.

Ejemplo:

```sql
select extract(day from to_date('25/12/2022')) dia
from dual;

       DIA
----------
        25
```

`ROUND`. Esta función generalmente es utilizada en números también aplica a fechas, lo que
hará es redondear a la fecha más próxima

Ejemplo:

```sql
select round(to_date( '25/12/2023'),'MONTH') fecha
from dual;

FECHA
--------
01/01/24
```

`TRUNC`. Esta función truncará el resultado devolviendo a la fecha original.

```sql
select trunc(to_date('25/12/2022'),'MONTH') fecha
from dual;

FECHA
--------
01/12/22
```

`MONTHS_BETWEEN`. Esta función obtiene la cantidad de meses entre 2 fechas.

```sql
select months_between(sysdate,to_date('30/05/2023')) meses
from dual;

     MESES
----------
2.89594161
```

`LAST_DAY`. Devuelve el último día del mes que contiene la fecha proporcionada.

```sql
select last_day(to_date('30/05/2023')) 
from dual;

LAST_DAY
--------
31/05/23
```

`CURRENT_DATE`. Devuelve la fecha y hora actual según la zona horaria configurada en la
sesión.

```sql
select current_date 
from dual; 

CURRENT_DATE
------------
    20/08/23
```

### 6.5.1.1 Operaciones Aritméticas con Fechas

Dado que la base de datos almacena fechas como números, se pueden realizar cálculos
mediante operadores aritméticos como la suma o la resta. Puede sumar y restar constantes
numéricas además de fechas.

Ejemplo:

```sql
SELECT last_name,
       (SYSDATE-hire_date)/7,
       SYSDATE+3,
       SYSDATE-3,
       SYSDATE-(SYSDATE+6)     
FROM employees
WHERE  department_id = 60;


LAST_NAME                 (SYSDATE-HIRE_DATE)/7 SYSDATE- SYSDATE+ SYSDATE-(SYSDATE+6)
------------------------- --------------------- -------- -------- -------------------
Hunold                               920.695299 17/08/23 23/08/23                  -6
Ernst                                848.838156 17/08/23 23/08/23                  -6
Austin                               948.123871 17/08/23 23/08/23                  -6
Pataballa                            915.981014 17/08/23 23/08/23                  -6
Lorentz                              863.552442 17/08/23 23/08/23                  -6
```

### 6.5.2 Funciones para manejo de números

Las funciones numéricas aceptan parámetros de entrada de tipo numérico y retornan valores
numéricos. Algunas de ellas son:

`ROUND`. La función `ROUND (m, n)` acepta como entrada un número y devuelve como salida
otro número redondeado a un número específico de decimales que se indica en el segundo
parámetro de la función. Si no se especifica el número de decimales a mostrar, la función
devolverá el número redondeado al entero más próximo. Si el número de decimales a
redondear es negativo, entonces el redondeo se realiza avanzando hacia la izquierda del
separador decimal, en lugar de hacia la derecha.

Ejemplo:

```sql
select (round (20.35)), 
       (round (20.35, 1)),
       (round (20.33, 1)),
       (round (20.35, 2)),
       (round (20.35, -2)),
       (round (225, -2))
from dual;

(ROUND(20.35)) (ROUND(20.35,1)) (ROUND(20.33,1)) (ROUND(20.35,2)) (ROUND(20.35,-2)) (ROUND(225,-2))
-------------- ---------------- ---------------- ---------------- ----------------- ---------------
            20             20.4             20.3            20.35                 0             200
```

`TRUNC`. La función TRUNC (m, n) permite indicar el número de decimales a truncar a la
derecha o izquierda del separador decimal. La función TRUNC simplemente elimina o trunca
los dígitos, es decir, no realiza un redondeo.

Ejemplo:

```sql
select (trunc (20.35)), 
       (trunc (20.35, 1)),
       (trunc (20.33, 1)),
       (trunc (20.35, 2)),
       (trunc (20.35, -2)),
       (trunc (225, -2))
from dual;

(TRUNC(20.35)) (TRUNC(20.35,1)) (TRUNC(20.33,1)) (TRUNC(20.35,2)) (TRUNC(20.35,-2)) (TRUNC(225,-2))
-------------- ---------------- ---------------- ---------------- ----------------- ---------------
            20             20.3             20.3            20.35                 0             200
```

`FLOOR`. La función FLOOR (m) redondea una expresión numérica no entera al siguiente
entero inferior.

Ejemplo:

```sql
select (floor (3.5))
from dual;

(FLOOR(3.5))
------------
           3
```

`MOD`. La función `MOD (m, n)` obtiene el residuo del resultado de dividir m entre n.

Ejemplo:

```sql
select (mod (25, 6)), (mod (25, 9))
from dual;

(MOD(25,6)) (MOD(25,9))
----------- -----------
          1           7
```

`CEIL`. Esta función devuelve el menor entero mayor o igual que el número especificado
como parámetro.

Ejemplo:

```sql
select ceil(4.5)
from dual;

 CEIL(4.5)
----------
         5
```

### 6.5.3 Funciones para manejo de cadenas

Algunas de las funciones exclusivas para el manejo de cadenas son las siguientes

`ASCII`. La función `ASCII` devuelve el código numérico que representa el carácter pasado
por parámetro. Si se ingresa más de un carácter como parámetro a la función esta solo
devolverá el valor `ascii` para el primer carácter de la cadena e ignorará todos los demás
caracteres después del primero.

Ejemplo:

```sql
select ascii('t'), ascii('T'), ascii('T2') 
from dual;

ASCII('T') ASCII('T') ASCII('T2')
---------- ---------- -----------
       116         84          84
```

`CHR`. Esta función devuelve un caracter basada en el código numérico pasado por parámetro.

Ejemplo:

```sql
select chr(116), chr(84) 
from dual; 

C C
- -
t T
```

`CONCAT`. Pemite concatenar dos cadenas y juntarlas en una sola.

Ejemplo:

```sql
select concat('Este es', 'un ejemplo'), concat('A', 'b')
from dual;

CONCAT('ESTEES',' CO
----------------- --
Este esun ejemplo Ab
```

`LENGTH`. Devuelve la longitud de la cadena enviada por parámetro. Si el parámetro es un
valor nulo la función devolverá por resultado NULL.

Ejemplo:

```sql
select length(null), 
       length(''),
       length('Este es un ejemplo'),
       length('Este es unejemplo ')
from dual;    


LENGTH(NULL) LENGTH('') LENGTH('ESTEESUNEJEMPLO') LENGTH('ESTEESUNEJEMPLO')
------------ ---------- ------------------------- -------------------------
                                               18                        19
```

`LOWER`. Convierte todas las letras a minúsculas de la cadena pasada por parámetro. Si en
la cadena existen caracteres que no son letras, ellos no se ven afectados por esta función.

```sql
select lower('Este es un ejemplo'),
       lower('ESTE ES UN EJEMPLO')
from dual;

LOWER('ESTEESUNEJE LOWER('ESTEESUNEJE
------------------ ------------------
este es un ejemplo este es un ejemplo

```

`LPAD`. Completa una cadena agregando una cadena o caracter especifico a la izquierda
hasta completar la longitud deseada (Sólo cuando la cadena pasada por parámetro no es un
valor nulo). La cadena será formateada con n caracteres a la izquierda. Si  la longitud
es más pequeña que la cadena original, la funcion LPAD truncará el tamaño de la cadena a
el tamaño de la longitud izquierda. Si el parámetro es omitido la función `LPAD`
completará la cadena resultante con espacion en blanco al lado izquierdo.

Ejemplo:

```sql
select lpad('00001',7),
       lpad('0001',2),
       lpad('00001',8,'0'),
       lpad('00001',8,'z'),
       lpad('00001',5,'0')
from dual; 

LPAD('0 LP LPAD('00 LPAD('00 LPAD(
------- -- -------- -------- -----
  00001 00 00000001 zzz00001 00001
```

`LTRIM`. Remueve todos los caracteres especificados al lado izquierdo de la cadena. Si el
parámetro es omitido, la funcion `LTRIM` removerá todos los espacios en blanco al lado
izquierdo de CADENA.

```sql
select ltrim('   Hola'),
       ltrim('   Hola',' '),
       ltrim('0000Prueba','0'),
       ltrim('123123Total', 'Total'),
       ltrim('123123Total123','123'),
       ltrim('yxzyyyTotal','xyz'),
       ltrim('6372Total','1234567890')
from dual;


LTRI LTRI LTRIM( LTRIM('1231 LTRIM('1 LTRIM LTRIM
---- ---- ------ ----------- -------- ----- -----
Hola Hola Prueba 123123Total Total123 Total Total
```

`SUBSTR`. Permite extraer una parte de una cadena o subcadena de una cadena. La sintaxis
es la siguiente:

```sql
   SUBSTR(CADENA, POSICION_INICIAL, [LONGITUD])
```

CADENA es la cadena fuente pasada por parametro a la funcion.
POSICION_INICIAL es la posicion inicial en la CADENA a partir de la cual iniciará la
extraccion de la subcadena. La posición inicial de CADENA es 1.

LONGITUD es opcional. Indica el número de caracteres a extraer. Si este parámetro es
omitido, la función `SUBSTR` retornara la cantidad de caracteres restantes de CADENA a
partir de la POSICION_INICIAL.

* Si POSICION_INICIAL es 0, la función SUBSTR fijará a 1 la POSICION_INICIAL.

* Si POSICION_INICIAL es un número positivo, la función empezará a contrar desde el inicio
de la cadena y hacia adelante, el número de posiciones indicadas en POSICION_INICIAL

* Si POSICION_INICIAL es un número negativo, la función empezará a contar desde el final
de la cadena y hacia atrás, el número de posiciones indicadas en POSICION_INICIAL

* Si LONGITUD es un valor negativo, la función devulvera NULL.

Ejemplos:

```sql
SQL> select substr('Esta es una prueba',6,2) from dual;

SU
--
es

SQL> select substr('Esta es una prueba',6) from dual;

SUBSTR('ESTAE
-------------
es una prueba

SQL> select substr('Esta es una prueba',1,4) from dual;

SUBS
----
Esta

SQL> select substr('Esta es una prueba',-3,3) from dual;

SUB
---
eba

SQL> select substr('Esta es una prueba',-6,3) from dual;

SUB
---
pru

SQL> select substr('Esta es una prueba',-8,2) from dual;

SU
--
a
````

Para mayor información consulte en:

* <https://docs.oracle.com/applications/help/es/enterprise-performance-management/11.2/HFMAM/date_and_time_functions.htm>

* <https://docs.oracle.com/cd/E11882_01/server.112/e41084/functions002.htm#SQLRF51183>
