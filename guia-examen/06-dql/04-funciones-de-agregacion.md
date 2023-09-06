
# 6.0 Lenguaje de Consulta de Datos (DQL)

## 6.4 Funciones de agregación (min, max, sum, avg, count)

Las funciones de agregación nos permiten efectuar operaciones sobre un conjunto de
resultados, devolviendo un único valor. Los conjuntos de registros pueden ser agrupados
por diversos criterios.

* Permiten obtener un resultado basado en los valores contenidos en una columna de una
tabla.

Las funciones de agregación son las siguientes:

* `MIN`: devuelve el valor mínimo del campo que especifiquemos, se ignoran los valores
nulos. Su sintaxis:

```sql
    min([distinct | all] campo)
```

* `MAX`: devuelve el valor máximo del campo que especifiquemos, se ignoran los valores
nulos. Su sintaxis:

```sql
    max([distinct | all] campo)
```

* `SUM`: suma los valores del campo que especifiquemos. Sólo se puede utilizar en columnas
numéricas, se omiten los valores nulos. Su sintaxis:

```sql
    sum([distinct | all] campo)
```

* `AVG`: devuelve el valor promedio del campo que especifiquemos. Sólo se puede utilizar
en columnas numéricas. Omite los valores nulos. Su sintaxis:

```sql
    avg([distinct | all] campo)
```

* `COUNT`: devuelve el número total de filas seleccionadas por la consulta. Su sintaxis:

```sql
    count({ * | [distinct | all] campo})
```

Todas estas funciones se aplican a una sola columna, que especificaremos entre paréntesis,
excepto la función `count`, que se puede aplicar a una columna o indicar un '$\ast$'. La
diferencia entre poner el nombre de una columna o un '$\ast$', es que en el primer caso no
cuenta los valores nulos para dicha columna, y en el segundo si.

* `distinct` hace que la función considere únicamente valores no duplicados;
* `all` hace que considere todos los valores, incluidos los duplicados. El valor por
defecto es `all` por lo que no es necesario especificarlo.
* Los tipos de datos para las funciones pueden ser `char`, `varchar2`, `number` o `date`.

### 6.4.1 Cláusula `GROUP BY`

Con ésta cláusula se indica él o los campos por los cuales se desea agrupar un conjunto de
registros.

* Comúnmente esta agrupación va acompañada con una serie de funciones de agregación.
* El o los campos por el cual se agrupa debe de incluirse en el `select`

### 6.4.2 Cláusula `GROUP BY .. HAVING`

Se ocupa únicamente cuando se desea especificar una función de agregación en la condición

### Ejemplos

Se muestra la utilización de cada una de las funciones mencionadas utilizando las
siguientes tablas del esquema *human resource*:

<p align="center"\><img src=img/employees.png width="500"\>
<p align="center"\><img src=img/jobs.png width="500"\>

1. Cantidad de empleados que son Gerentes de ventas

   ```sql
   select count(employee_id) cantidad
   from employees
   join jobs using(job_id)
   where job_title='Sales Manager';

     CANTIDAD
   ----------
            5
   ```

2. Cantidad de empleados que reciben comisión

   ```sql
   select count(commission_pct)
   from employees;

   COUNT(COMMISSION_PCT)
   ---------------------
                      35
   ```

3. El salario máximo pagado a un empleado.

   ```sql
   select max(salary)
   from employees;

   MAX(SALARY)
   -----------
         24000
   ```

4. Clave del departamento y el monto total necesario para pagarle a los empleados de cada
departamento.

   ```sql
   select department_id, sum(salary)
   from employees
   group by department_id;

   DEPARTMENT_ID SUM(SALARY)
   ------------- -----------
             50      156400
             40        6500
            110       20308
             90       58000
             30       24900
             70       10000
                       7000
             10        4400
             20       19000
             60       28800
            100       51608
             80      304500
   ```

5. Sueldo promedio por cada departamento.

   ```sql
   select department_id, avg(salary)
   from employees
   group by department_id;

   DEPARTMENT_ID AVG(SALARY)
   ------------- -----------
           50  3475.55556
           40        6500
          110       10154
           90  19333.3333
           30        4150
           70       10000
                     7000
           10        4400
           20        9500
           60        5760
          100  8601.33333
           80  8955.88235
   ```

6. Salario mínimo pagado por puesto.

   ```sql
   select job_id, min(salary)
   from employees
   group by job_id;

   JOB_ID     MIN(SALARY)
   ---------- -----------
   AD_VP            17000
   FI_ACCOUNT        6900
   PU_CLERK          2500
   SH_CLERK          2500
   HR_REP            6500
   PU_MAN           11000
   AC_MGR           12008
   ST_CLERK          2100
   AD_ASST           4400
   IT_PROG           4200
   SA_MAN           10500
   AC_ACCOUNT        8300
   FI_MGR           12008
   ST_MAN            5800
   AD_PRES          24000
   MK_MAN           13000
   SA_REP            6100
   MK_REP            6000
   PR_REP           10000
   ```

7. Clave de departamento y sueldo promedio de sus empleados, de aquellos departamentos
cuyo salario promedio sea mayor de $5000.

   ```sql
   select department_id, avg(salary)
   from employees
   group by department_id
   having avg(salary)>5000;

   DEPARTMENT_ID AVG(SALARY)
   ------------- -----------
              40        6500
             110       10154
              90  19333.3333
              70       10000
                        7000
              20        9500
              60        5760
             100  8601.33333
              80  8955.88235
   ```
