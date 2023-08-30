# Normalización

La normalización es un proceso que tiene por objetivo reducir los probemas de redundancia
y actualización en las tablas mediante una serie de reglas llamadas formas normales
propuestas por Edgar F. Cood con la aportaciónn de otros investigadores.

## Primera forma normal (1FN)

Una realación está en primera forma normal 1FN si y solo si:

* Todos sus atributos son atómicos, es decir, si toda tupla contiene exactamente un solo valor para cada atributo.
* No hay grupos de repetición
* La tabla tiene una llave primaria

## Segunda forma normal (2FN)

Una tabla está en segunda foma normal 2FN si y solo si:

* Está en 1FN
* Tdosos los atributos que no sean parte de la llave primaria depende de toda la llave
primaria en vez de solo una parte de ella, es decir, ninguno de los atributos no clave son funcionalmente dependientes de una parte de la llave primaria de la tabla.

## Tercera Forma Nomal (3FN)

Una tabla está tercera forma normal 3FN si y solo si:

* La tabla está en 2FN
* Ningun atributo no llave es dependiente de otro atributo no llave. Es decir no hay
dependencias transitivas.

## Dependencias funcionales

Sea R una relación y sean X y Y subconjuntos cualesquiera del conjunto de atributos de R,
entonces podemos decir que Y es dependiente funcionalmente de X, si y sólo si en todo
valor válido posible de R, cada valor X está asociado  con un valor de Y.

<p align="center">
  <img src="img/dependencia-funcional2.png" >
</p>

La parte izquierda de una dependencia funcional DF se denomina determinante y la derecha
dependiente.

### Dependencia parcial

* Puede existir solamente en tablas con llave primaria compuesta.
* Existe dependencia parcial cuando un atributo que es parte de la llave primaria es
determinante de uno o más atributos no clave.

### Dependencia transitiva

* Si un atribto no clave es determiannte de cualquier atributo o atrubtos no clave hay
dependencia transitiva.

## Cuarta forma normal (4FN)

Una tabla está en cuarta forma normal 4FN si:

* Está en su tercera forma normal 3FN
* No hay dependencias multivalor

### Dependencia multivalor

Si la llave primaria determina multiples valores de 2 o más campos y no hay relación
entre ellos, se dice que hay dependencias multivalor.
