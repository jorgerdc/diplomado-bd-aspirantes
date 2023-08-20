# 7 Fundamentos - Programación PL/SQL

## 7.7 Procedimientos almacenados

En secciones anteriores se revisó que los bloques anónimos que se compilan cada vez que
son ejecutados y no se almacenan en la base de datos. Si se desea que estos bloques sean
guardados en la base de datos, se requiere hacer uso de un procedimiento almacenado
(stored procedure). 

Un procedimiento almacenado es un programa PL/SQL que es compilado y almacenado en el
servidor. Una vez realizado esto, no se requiere volver a escribir todas las instrucciones
sino únicamente hacer referencia al procedimiento. Esto mejora el rendimiento del
servidor, ya que el programa se compila una sola vez y se ejecuta N veces.  

A diferencia de los bloques anónimos, un procedimiento requiere de un nombre.  Una función
puede regresar un valor, un procedimiento no regresa valores.  Tanto las funciones como
los procedimientos almacenados pueden ser invocados por el usuario.

Sintaxis:

```sql
create [or replace] procedure [schema.]<procedure_name>
   [
     (argument [{ in | out | in out }][nocopy] datatype [default expr]
     [,argument [{ in | out | in out }][nocopy] datatype [default expr]
     ]...
    )
   ] 
   [ invoker_rights_clause ]
   { is | as }
   { pl/sql_subprogram_body | call_spec } ;

```

* El usuario que desee crear un procedimiento deberá contar con el privilegio
 `create procedure`.

### Ejemplo - Crear nuevas asignaturas

Considerando el siguiente modelo relacional, crear un procedimiento almacenado llamado
`creaAsignatura` que será empleado para registrar una nueva asignatura. Las especificaciones
del procedimiento son:

* Recibirá como valores de entrada: nombre de la asignatura, créditos, clave del plan de
  estudios, nombre de la asignatura requerida en caso que la materia esté seriada con
  otra.
* Adicional a los parámetros anteriores, el procedimiento recibirá un parámetro de salida.
  El procedimiento deberá inicializar este parámetro con el identificador de la asignatura
  asignado empleando la secuencia.
* Notar que el procedimiento recibe la clave del plan de estudios, por lo que deberá
  obtener el identificador correspondiente para ser asignado en el campo `plan_estudios_id`.
* De forma similar, el procedimiento recibe de forma opcional el nombre de la asignatura
  requerida. El procedimiento deberá obtener el identificador correspondiente.

```sql
create or replace procedure creaAsignatura (
  p_asignatura_id out number ,p_nombre in varchar2,
  p_creditos in number,p_clave_plan in varchar2,
  p_asignatura_req in varchar2 default null) is 

  --declaración de variables
  v_asignatura_req_id asignatura.asignatura_requerida_id%type;
  v_plan_id plan_estudios.plan_estudios_id%type;

begin
 
 --generando el siguiente id de asignatura
 select asignatura_seq.nextval into p_asignatura_id
 from dual;

 --obtiene el id del plan
 select plan_estudios_id into v_plan_id
 from plan_estudios
 where clave =p_clave_plan;

 --en caso de haber asignatura requerida, obtiene el id
 if p_asignatura_req is not null then
  select asignatura_id into v_asignatura_req_id
  from asignatura 
  where lower(nombre) = lower(p_asignatura_req);
 else
  v_asignatura_req_id := null;
 end if;
 --insertando  a la nueva asignatura
 insert into asignatura(asignatura_id,nombre,creditos, plan_estudios_id,
  asignatura_requerida_id) 
 values(p_asignatura_id,p_nombre,p_creditos,v_plan_id,v_asignatura_req_id); 
end;
/
show errors
```

* En este ejemplo la principal finalidad de construir el procedimiento es ocultar al
  usuario los detalles de las consultas SQL requeridas para crear una asignatura. El
  usuario final únicamente proporciona los datos y el procedimiento se encarga de aplicar
  las sentencias SQL necesarias para registrar una nueva asignatura.
* En general, un procedimiento permite implementar y ocultar cierta lógica de código que
  puede ser reutilizable.
* Observar que el procedimiento recibe 5 parámetros. Para cada uno de ellos se especifica
  su tipo:
  * `IN`: Es un parámetro de entrada. Se emplea únicamente para leer su valor dentro del
    cuerpo del procedimiento.
  * `OUT`: Es un parámetro de salida. Este tipo de parámetro permite implementar una
     especie de valor o valores de retorno.  El procedimiento podrá escribir o modificar
     el valor de este tipo de parámetros para que puedan ser leídos fuera del
     procedimiento, posterior a su ejecución. Este tipo de parámetros funcionan similar a
     la estrategia de paso de valores por referencia.
  * `IN OUT`:  Es un parámetro que combina los 2 tipos anteriores. Puede ser tanto de
     entrada como de salida.
* Observar que en la declaración de la lista de parámetros no se especifica la precisión o
  el tamaño del tipo de dato. Solo se especifica su tipo.
* Observar la palabra `default` empleada en el parámetro `p_asignatura_req`. Este
  parámetro es considerado opcional ya que, si el usuario no lo específica, se empleará el
  valor por defecto, que en este caso es `null`.
* Observar la declaración de 2 variables adicionales para almacenar los identificadores
  del plan de estudios y de la asignatura requerida. En un procedimiento almacenado no se
  requiere especificar el bloque `declare`.
* Finalmente, observar la lógica del procedimiento para obtener los valores requeridos
  para crear la nueva asignatura.

### 7.7.1 Ejecución de procedimientos almacenados

Un procedimiento se puede invocar desde otro programa PL/SQL: trigger, procedimiento o un
bloque anónimo. El siguiente código muestra un bloque anónimo que hace uso del
procedimiento anterior.

```sql
set serveroutput on
declare
  v_id number;

begin
  
  creaAsignatura(v_id,'Electronica',12,'PL-2OO9');
  dbms_output.put_line('La asignatura Electronica creada con id: '||v_id);
  
  creaAsignatura(v_id,'Electronica Digital',12,'PL-2OO9','Electronica');
  dbms_output.put_line(
    'La asignatura Electronica Digital creada con id: '||v_id);
end;
/

```

* `exec` se omite si el procedimiento se invoca desde un programa PL/SQL
* Observar que en la primera llamada no se especifica el parámetro opcional que
  corresponde con el nombre de la materia antecedente o requerida.
* Existe una observación más al código anterior.  El código no es transaccional.  Las
  operaciones `insert` que generó el programa al invocar 2 veces al procedimiento nunca
  fueron confirmadas.  Lo correcto es escribir la instrucción `commit` al final de la
  ejecución del bloque anónimo. Como buena práctica, instrucciones como `commit`,
  `rollback`, `savepoint` no deben incluirse en el cuerpo del procedimiento. El control
  transaccional se debe controlar de forma externa:

```sql
declare
  v_id number;
begin
  creaAsignatura(v_id,'Electronica',12,'PL-2OO9');
  dbms_output.put_line('La asignatura Electronica creada con id: '||v_id);
  creaAsignatura(v_id,'Electronica Digital',12,'PL-2OO9','Electronica');
  dbms_output.put_line(
    'La asignatura Electronica Digital creada con id: '||v_id);
  commit;

  exception
    when others then
      dbms_output.put_line('Error al crear asignaturas');
      rollback;
      raise;
end;
/

```

* Observar que al final del bloque anónimo se hace `commit` para confirmar la inserción de
  las 2 nuevas asignaturas.
* El bloque `exception` permite manejar cualquier error que ocurra al intentar ejecutar el
  procedimiento. De ocurrir, se hace `rollback` para garantizar el estado consistente de la
  base de datos y se re-lanza la excepción.  Este es el comportamiento correcto y adecuado
  desde el punto de vista transaccional. Notar que no se especifica `end` para terminar el
  bloque de excepción ya que este siempre debe aparecer al final del bloque `begin`.

## 7.8 Funciones

* La principal diferencia de una función con respecto a un procedimiento es que una
  función si puede regresar un valor.  
* Lo anterior implica que una función puede ser invocada desde una sentencia SQL mientras
  que un procedimiento almacenado no.

```sql
select functionName(<param1>,<param2>,...,<paramN>) from dual
```

Las funciones también pueden ser empleadas como operando derecho en una expresión.

```sql
v_valor = functionName(<param1>,<param2>,...,<paramN>)
```

Sintaxis:

```sql
create [or replace] function [schema.]<fnction_name>
   [
     (argument [{ in | out | in out }][nocopy] datatype [default expr]
     [,argument [{ in | out | in out }][nocopy] datatype [default expr]
     ]...
    )
   ]
   return {datatype} 
   [ authid [definer | current_user]]
   [ deterministic | parallel_enabled ]
   [ pipelined ]
   [ result cache [relies on <table_name>]]
   is
   { pl/sql_subprogram_body | call_spec } ;
```

* El usuario que desee crear una función deberá contar con el privilegio
  `create procedure` (el mismo empleado para los procedimientos).

### Ejemplo - concatenar cadenas

Crear una función que realice la unión de hasta 5 cadenas empleando un carácter de unión.
Por ejemplo, para las cadenas “A”, “B”, “C,” “D”, “E”, generar una cadena empleando el
carácter `#` como carácter de unión. La función deberá regresar la cadena `A#B#C#D#E`.
Como mínimo la función deberá recibir las primeras 2 cadenas y el carácter de unión.  El
código es el siguiente:

```sql
create or replace function joinStrings(
  join_string varchar2,
  str_1 varchar2,
  str_2 varchar2,
  str_3 varchar2 default null,
  str_4 varchar2 default null,
  str_5 varchar2 default null
) return varchar2 is

  v_str varchar2(4000);
  begin
    v_str :=  str_1||join_string||str_2;
    if str_3 is not null then
      v_str := v_str||join_string||str_3;
    end if;
    if str_4 is not null then
      v_str := v_str||join_string||str_4;
    end if;
    if str_5 is not null then
      v_str := v_str||join_string||str_5;
    end if;
    return v_str;
  end;
/
show errors
```

Observar el primer parámetro corresponde con el carácter de unión. A partir del tercer
parámetro se agrega la opción `default` ya que como mínimo solo se requieren 2 cadenas.

### 7.8.1 Ejecución de funciones

Existen 2 principales técnicas para ejecutar una función.

* Empleando parámetros con notación posicional. Esto significa que los parámetros se deben
  proporcionar en el orden en el que los solicita la función. Si existen parámetros
  opcionales, se debe especificar un valor por default, o `null`.

```sql
select joinStrings('#','A','B',null,null,'E') as "join_string"
from dual;

```

Observar que se hace uso de la instrucción `select` para poder invocar a la función. De
forma similar a otras funciones existentes. En este ejemplo se requiere indicar que la
tercer y cuarta cadena no tienen valor para poder especificar el quinto parámetro. Como
resultado se obtiene:

```sql
join_string
-------------
A#B#E
```

* Empleando parámetros con notación por nombre. Esto significa que los parámetros pueden
  ser especificados en un orden diferente, pero para ser asignados correctamente, se debe
  especificar el nombre del parámetro al momento de invocar.  En Oracle se emplea el
  operador ` =>`  para asociar  el nombre del parámetro con su valor.

```sql
select joinStrings(
 str_1 => 'A',
 str_5 => 'E',
 str_2 => 'B',
 join_string => '#') as "join_string"
from dual;
```

Observar que los parámetros se especifican en orden diferente. Para los casos en donde
existen parámetros opcionales, está técnica suele ser más adecuada ya que no se requiere
especificarlos como lo fue el caso anterior. Esta notación también puede ser aplicada para
invocar procedimientos.

Finalmente, de este ejemplo se pueden mencionar algunas observaciones:

* La función tiene un número finito de parámetros.  ¿Qué sucede si de desea unir más de 5
  cadenas? Una manera de solucionarlo es mediante el uso de colecciones.
* Observar que la cadena resultante se ha declarado como una cadena con longitud máxima de
  4000 caracteres.  ¿Qué sucede si al aplicar la unión se excede este valor? Una manera de
  resolver es emplear un objeto LOB (Large Object), por ejemplo, un tipo de dato `CLOB`.

## 7.9. Conclusiones

El material mostrado en estos documentos incluyen una breve introducción a la programación
PL/SQL considerados como antecedentes mínimos requeridos para el presente diplomado. Para
mayores detalles y otros temas asociados con la programación PL/SQL, se anexan algunas
referencias:

* <https://docs.oracle.com/en/database/oracle/oracle-database/19/lnpls/database-pl-sql-language-reference.pdf>

* <https://learn.oracle.com/ols/course/oracle-database-19c-plsql-fundamentals/88387/90085>
