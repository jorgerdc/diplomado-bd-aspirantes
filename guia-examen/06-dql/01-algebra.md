# 6.0 Lenguaje de Consulta de Datos (DQL)

DQL es la abreviatura del Data Query Language (lenguaje de consulta de datos) de
SQL.
El comando que pertenece a este lenguaje es el comando SELECT, este comando SELECT nos va
a permitir fundamentalmente:

* Obtener datos de ciertas columnas de una tabla (proyección)
* Obtener registros (tuplas) de una tabla de acuerdo con ciertos criterios (selección)
* Mezclar datos de tablas diferentes (asociar, join)
* Realizar cálculos sobre los datos
* Agrupar datos

## 6.1 Álgebra Relacional

El álgebra relacional es un álgebra en la cual:

* Sus operandos son relaciones (instancias) o variables que representan relaciones.

* Sus operadores están diseñados para hacer las tareas más comunes que se necesitan para
manipular relaciones en una base de datos.

El álgebra relacional se puede utilizar como un lenguaje de consulta de datos, es un
lenguaje de bases de datos que nos permite manipular los datos, nos permite extraer
información de una base de datos.
Las operaciones de álgebra relacional manipulan relaciones. Es decir de una o más
relaciones existentes se genera otra relación. Se tiene dos tipos de operadores:

* Básicos o fundamentales: Selección, proyección, unión, diferencia y producto cartesiano.
* Derivados: Intersección, reunión natural o join y división.

### 6.1.1 Operadores básicos

* Selección ( $\sigma$ )

  Operador de selección $\sigma$, permite seleccionar un subconjunto de registros de una relación (R),
todas aquellas que satisfacen cierto predicado P, esto es:

  $$\sigma_P(R)$$

  Un predicado puede contener una combinación booleana, donde se pueden usar operadores
lógicos como: ∨,∧ combinándolos con operadores de comparación (>, <, =, <>, <= , >=)

* Proyección ( $\pi$ )

  Consiste en la obtención de una nueva relación formada por algunos atributos
  seleccionados de la relación existente

  El operador toma una relación como argumento y el resultado es una nueva relación.
  $$\pi A_1, A_2,…,A_n(R)$$
  Donde:
  $A_1, A_2,…,A_n$ son atributos de la relación R

* Unión ( $\cup$ )

  Esta operación es el resultado de la relación formada por la agregación de dos
  relaciones que ya existen.

  $$ R_1 \cup  R_2$$

  Ambas relaciones deben tener el mismo número de atributos

  El dominio del atributo i-ésimo de cada relación debe coincidir.

* Diferencia (–)

  Esta operación tiene como resultado la relación formada por los registros de una
  relación ya creada que no figura en otra relación también creada.
  $$R_1 – R_2$$

  Se deben cumplir las mismas restricciones que para la unión

* Producto cartesiano ( X )

  Representa al producto cartesiano usual de conjuntos.

  Combina tuplas de cualquieras dos (o más) relaciones, hace la combinación de todos con
todos.

  Si las relaciones a operar tienen N y M tuplas de n y m atributos respectivamente, la
relación resultante del producto cartesiano tiene N×M tuplas de n+m atributos.
  $$R_1 X R_2$$

### 6.1.2 Operadores derivados

* Intersección ( $\cap$ )

  Esta operación tiene como resultado la relación formada por las tuplas comunes a las
relaciones que ya existen.

  Las relaciones con las que se ha de operar deben tener el mismo grado y los mismos
dominios en sus atributos.
  $$R1 \cap  R_2 = R_1 -(R_1 - R_2)$$

* Reunión natural o join ( $\bowtie$ )

  Realiza un producto cartesiano y hace una selección forzando la igualdad de atributos
  que aparecen en ambas relaciones.

  Elimina repetidos (como toda operación de conjuntos).

* División ($\div$)

  Toma dos relaciones una unaria y una binaria que concuerden en el otro atributo de la
binaria con todos los valores de la relación unaria.

  Definición de la operación división con operadores básicos:

  * $R_1$={$A_1,A_2$}, $R_2$={$A_2$}
  * $R_1$ $\div$ $R_2$ =$\pi$ $A_1( R_1 )$- $(\pi$ $A_1$ $((\pi$ $A_1 (R_1 )X R_2)–R_1))$

## 6.1.3 Ejemplos

Considere los siguientes esquemas relacionales

cliente={cliente_id(pk),nombreCte,direccionCte,paisCte}
producto={producto_id(pk),descProd,precio}
venta= {venta_id(pk),cliente_id(fk),producto_id(fk),cantidad}

1. Nombre de los clientes del país México.

    $\pi_{nombreCte}$ ( $\sigma_{paisCte='México'}$ (cliente) )

2. Nombre de los clientes, descripción y cantidad de los productos comprados.

    $\pi_{nombreCte,descProd,cantidad}$ ($\sigma_{cliente.cliente\_id=venta.cliente\_id}$
     \^$_{venta.cliente\_id=producto.producto\_id}$ (cliente X venta X producto))

3. Clientes que no han comprado ningún producto

    $\pi_{nombreCte}$ ( cliente) - $\pi_{nombreCte}$ ( cliente $\bowtie$ venta )

4. Clientes que compraron todos los producto de la empresa

    $\pi_{nombreCte, producto\_id}$ ( cliente $\bowtie$ venta ) $\div$
     $\pi_{producto\_id}$ ( producto)

5. Descripción de los productos que no se han vendido en México

    $\pi_{descProd}$ ( venta $\bowtie$ producto ) - $\pi_{descProd}$
     ($\sigma_{paisCte='México'}$ ( cliente $\bowtie$ venta $\bowtie$ producto))

6. Descripción de los productos que fueron comprados por clientes mexicanos y españoles.

    $\pi_{descProd}$ ($\sigma_{paisCte='México'}$ ( cliente $\bowtie$ venta $\bowtie$
     producto)) $\cap$ $\pi_{descProd}$ ($\sigma_{paisCte='España'}$ ( cliente $\bowtie$
      venta $\bowtie$ producto))  
7. Descripción de los procuctos que fueron comprados por clientes mexicanos o españoles

    $\pi_{descProd}$ ($\sigma_{paisCte='México'}$ ( cliente $\bowtie$ venta $\bowtie$
     producto)) $\cup$ $\pi_{descProd}$ ($\sigma_{paisCte='España'}$ ( cliente $\bowtie$
      venta $\bowtie$ producto))
