# 2. Diseño lógico de Bases de datos

En el diseño lógico se genera un modelo relacional, el cual es obtenido a partir del
modelo Entidad-Relación generado en el diseño conceptual. Este modelo fue propuesto por
Edgar Frank Codd en 1970, se basa en  estructuras de almacenamiento llamadas  tablas cada
una de las cuales tiene un nombre único y se relacionan entre ellas. A cada fila de una
tabla se le llama tupla y al conjunto de columnas de la tabla atributos.

Existen varias notaciones utilizadas para representar el modelo relacional, pero la más
utilizadas es la Crow's foot, la cual veremos a continuación.

## 2.1 Transformación del modelo Entidad-Relación al Modelo Relacional

Para transformar un modelo entidad-relación a modelo relacional seguiremos las siguientes
reglas:

### 2.1.1 Entidad fuerte

En el modelo relacional se utiliza el elemento tabla, se representa con un rectángulo
como se muestra a continuación:

<p align="center">
  <img src="img/tabla.png" >
</p>

En la parte superior del rectángulo, primera parte, se coloca la llave primaria de la
tabla (clave principal del MER) y en la parte inferior el resto de los atributos:

a) En claves candidatas se establece restricción de unicidad (unique)

b) Atributos compuestos se colocan en forma individual

c) Atributos multivalorados; se crea una nueva tabla pasando la clave primaria de la
tabla como clave foránea a la nueva tabla.

d) Atributo opcional se establece como atributo con valores nulos NULL.

e) Los atributos derivados se establecen como atributos calculados, o como columnas
virtuales en el caso de Oracle.

e) Se establecen restricciones sobre atributos.

Ejemplo:

La siguiente imagen representa a la entidad profesor

<p align="center">
  <img src="img/entidad-mer.jpg" >
</p>

Su representación en modelo relacional es:

<p align="center">
  <img src="img/entidad-relacional.jpg" >
</p>

### 2.2.2 Relaciones

* Relación uno a muchos 1:M

Se conoce como relación no identificativa y se representan con una línea discontinua.
La llave primaria (pk) de la tabla padre se pasa como un atributo en la tabla hija y se
denomina llave foránea (fk)

Ejemplo:

<p align="center">
  <img src="img/relacion-uno-muchos.png" >
</p>

Su representanción en el modelo relacional es:

<p align="center">
  <img src="img/uno-muchos.jpg" >
</p>

* Relación uno a uno 1:1

La llave primaria de una de las entidades se propaga a la otra entidad como llave foránea
y esta última se establece como llave candidata para conservar la unicidad. Si una entidad
tiene cardinalidad mínima cero, esta entidad recibe la llave primaria como llave foránea,
si la cardinalidad mínima es la misma en ambas entidades dependerá el contexto.

Ejemplo:

<p align="center">
  <img src="img/relacion-uno-uno.png" >
</p>

Su representación en el modelo relacional es:

<p align="center">
  <img src="img/uno-uno.jpg" >
</p>

* Relación muchos a muchos M:M

Las relaciones muchos a muchos generan una nueva tabla, esta nueva tabla tendrá una llave
primaria compuesta formada por las llaves primarias de las entidades de la relación. Si la
relación tiene atributos, éstos son colocados en la nueva tabla.

Ejemplo:

<p align="center">
  <img src="img/relacion-muchos-muchos.png" >
</p>

Su representación en el modelo relacional es:

<p align="center">
  <img src="img/muchos-muchos.jpg" >
</p>

* Relaciones recursivas

La llave primaria pasa a la misma tabla como llave foránea.

Ejemplo:

<p align="center">
  <img src="img/relacion-recursiva.png" >
</p>

Su representación en el modelo relacional es:

<p align="center">
  <img src="img/recursiva.jpg" >
</p>

### 2.2.3 Entidad débil

Se crea una tabla con sus atributos y se pasa la llave primaria de la entidad fuerte de
la que depende como llave foránea. La llave primaria de la nueva tabla es una llave
compuesta la cual se formará por la llave primaria de la entidad fuerte y el
discriminante de la entidad débil.

Ejemplo:

<p align="center">
  <img src="img/entidad-debil.png" >
</p>

Su representación en el modelo relacional es:

<p align="center">
  <img src="img/relacion-debil.jpg" >
</p>