# 6.0 Lenguaje de Consulta de Datos (DQL)

DQL es la abreviatura del Data Query Language (lenguaje de consulta de datos) de SQL.
El comando que pertenece a este lenguaje es el comando `select`, este comando nos va a
permitir fundamentalmente:

* Obtener datos de ciertas columnas de una tabla (proyección)
* Obtener registros (tuplas) de una tabla de acuerdo con ciertos criterios (selección)
* Mezclar datos de tablas diferentes (asociar, join)
* Realizar cálculos sobre los datos
* Agrupar datos

## 6.1 Álgebra Relacional

El álgebra relacional es un conjunto de operaciones básicas sobre tablas relacionales, a
partir de las cuales se definen operaciones más complejas.

* Sus operandos son relaciones (tablas) o variables que representan a un conjunto de
datos.

* Sus operadores estan diseñados para realizar el acceso a datos como parte del
procesamiento de una consulta compleja.

* Las operaciones de álgebra relacional actuán sobre relaciones generando como resultado
una nueva relación. Es decir de una o más relaciones existentes se genera otra relación.
Se tiene los siguientes tipos de operadores:

  * Básicos y derivados
  * Propios de Bases de Datos y de conjuntos.

### 6.1.1 Operadores básicos

Dentro de los operadores básicos o fundamentales tenemos:

* Operadores unarios, es decir, actúan sobre una sola relación
  * Selección
  * Proyección
* Operadores binarios, es decir, actúan sobre dos relaciones. Son operacionalmente
completos, permiten expresar cualquier consulta sobre una Base de Datos
  * Unión
  * Diferencia
  * Producto cartesiano.

#### Selección ( $\sigma$ )

  Permite seleccionar un subconjunto de registros de una relación (R), todas aquellas que
  satisfacen cierto predicado P, donde P está representado por una expresión booleana,
  hace uso de operadores lógicos como: ∨,∧ combinándolos con operadores de comparación
  (>, <, =, <>, <= , >=), esto es:
  $$\sigma_P(R)$$

<p align ="center"\><img src=img/seleccion.png width="400"></p>

#### Proyección ( $\pi$ )

  Consiste en la obtención de una nueva relación formada por algunos atributos
  seleccionados de la relación existente.

  El operador toma una relación como argumento y el resultado es una nueva relación.
  $$\pi A_1, A_2,…,A_n(R)$$
  Donde:
  $A_1, A_2,…,A_n$ son atributos de la relación R

  <p align="center"\><img src=img/proyeccion.png width="400"></p>

#### Unión ( $\cup$ )

  Esta operación es el resultado de la relación formada por la agregación o adición
  vertical de dos relaciones que ya existen.
  $$R_1 \cup R_2$$

  <p align="center"\><img src=img/union.png width="150"></p>

#### Diferencia (–)

  Esta operación tiene como resultado la relación formada por los registros de la relación
  $R_1$ que no se encuentran en la relación $R_2$.
  $$R_1 – R_2$$

  <p align="center"\><img src=img/diferencia.png width="150"></p>

  En las operaciones de unión y diferencia ambas relaciones deben tener el mismo número
  de atributos y el dominio del atributo i-ésimo de cada relación debe coincidir.

#### Producto cartesiano ( X )

  El producto cartesiano realiza combinaciones de las tuplas de una relación R1 con cada
  una de las tuplas de otra relación R2. Esta combinación permite realizar uniones
  horizontales de cualquer par de relaciones. Son uniones horizontales porque a partir de
  dos relaciones se obtiene una sola, cuyas columnas es la unión de las columnas de las
  relaciones originales.

  Combina tuplas de cualquieras dos (o más) relaciones, hace la combinación de todos con
  todos.

  Si las relaciones a operar tienen N y M tuplas de n y m atributos respectivamente, la
  relación resultante del producto cartesiano tiene N×M tuplas de n+m atributos.
  $$R_1 X R_2$$

  <p align="center"\><img src=img/producto1.png width="250"></p>
  <p align="center"\><img src=img/producto2.png width="250"></p>

### 6.1.2 Operadores derivados

Dentro de los operadores derivados, llamados así porque son obtenidos a partir de
operadores básicos, tenemos:

* Reunión natural (join natural)
* Intersección
* División

Estos operadores fueron creados para simplificar la construcción de consultas.

### Reunión natural o join ( $\bowtie$ )

  Realiza un producto cartesiano y hace una selección forzando la igualdad de atributos
  que aparecen en ambas relaciones. Permite combinar tuplas de dos relaciones a través de
  una condición sobre los atributos.

  <p align="center"\><img src=img/reunion_natural.png width="450"></p>

### Intersección ( $\cap$ )

  Esta operación tiene como resultado la relación formada por las tuplas comunes a las
  relaciones que ya existen.

  Las relaciones con las que se ha de operar deben tener el mismo grado y los mismos
  dominios en sus atributos.
  $$R_1 \cap  R_2 = R_1 -(R_1 - R_2)$$

  <p align="center"\><img src=img/interseccion1.png width="120"></p>
  
### División ($\div$)

  Toma dos relaciones una binaria R1={A1,A2} (relación que tiene dos atributos) y una
  unaria R2={A2} (relación que tiene un único atributo) dónde el atributo "A2" es el mismo
  en ambas relaciones, la división de "R1 ÷ R2" dará como resultado los valores de "A1"
  tales que para todo valor "A2" en R2 existe una tupla en R1.
  
  <p align="center"\><img src=img/division.png width="350"></p>

  Definición de la operación división con operadores básicos:

  <p align="center"\><img src=img/definicion_division.png width="450"></p>

  Todas las operaciones de conjuntos eliminan tuplas repetidas.

## 6.1.3 Ejemplos

Considere los siguientes esquemas relacionales

```sql
cliente={cliente_id(pk), nombreCte, direccionCte, paisCte}
  
producto={producto_id(pk), descProd, precio}

venta= {cliente_id(fk), producto_id(fk), cantidad}
```

1. Nombre de los clientes del país México.

   ![select|50](img/ejemplo_1.png)

   En este ejemplo observamos el uso de los operadores unarios

2. Nombre de los clientes, descripción y cantidad de los productos comprados.

   ![select|50](img/ejemplo_2.png)

   En este ejemplo observamos la utilización del producto cartesiano, con la
   condición de igualdad de atributos.

3. Clientes que no han comprado ningún producto

   ![select|50](img/ejemplo_3.png)

   En este ejemplo se observa el uso del operador diferencia

4. Clientes que compraron todos los producto de la empresa

   ![select|50](img/ejemplo_4.png)

   En este ejemplo se muestra el uso del operador división, en el que tenemos una relación
   binaria y una unaria, dando como resultado el nombre de todos aquellos clientes que
   compraron todos los productos que se encuentran en la relación producto.

5. Descripción de los productos que no se han vendido en México

   ![select|50](img/ejemplo_5.png)

   En este ejemplo se observa el uso del join y el operador diferencia.

6. Descripción de los productos que fueron comprados por clientes mexicanos y españoles.

   ![select|50](img/ejemplo_6.png)

   En este ejemplo se observa el uso del operador intersección, se mostrará como resultado
   la descripción de todos aquellas productos que coincidan en ambas consultas.

7. Descripción de los productos que fueron comprados por clientes mexicanos o clientes
españoles

   ![select|50](img/ejemplo_7.png)

   En este ejemplo se muestra el uso del operador unión, se mostrará como resultado la
   unión vertical de la descripción de los productos se tienen en ambas relaciones.
