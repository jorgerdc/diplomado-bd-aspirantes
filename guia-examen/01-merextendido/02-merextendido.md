# 1.4 Modelo entidad relación extendido

Para aumentar el poder de expresión del modelo Entidad Relación se han introducido
ciertas extensiones al modelo entidad relación que incorporan conceptos para facilitar
la representación de ciertas estructuras del mundo real y son:

## 1.4.1 Generalización

Permite abstraer un tipo de entidad superior a partir de varios tipos de entidades
llamadas subtipos; en estos casos los atributos comunes en los subtipos se asignan a la
entidad supertipo. Se pueden generalizar los tipos de profesores, por ejemplo; de tiempo
completo, de asignatura, etc.

<p align="center"\><img src=img/generalizacion-no-excluyente.png "hosts" alt="hosts"\>

En el ejemplo anterior un empleado es cajero u oficial o puede tener ambos roles, pero
debe tener un rol.

Cuando un empleado solo tiene un rol, entonces decimos que es una generalización
excluyente y se representa de la siguiente forma.

<p align="center"\><img src=img/generalizacion-excluyente.png "hosts" alt="hosts"\>

## 1.4.2 Especialización

La especialización es la operación inversa a la generalización, en ella un supertipo se
descompone en uno o varios subtipos, los cuales heredan todos los atributos y relaciones
del supertipo, además de tener los suyos propios. Un ejemplo es el caso del tipo empleado,
del que se pueden obtener los subtipos secretaria, técnico e ingeniero.

<p align="center"\><img src=img/especializacion-noexcluyente.png "hosts" alt="hosts"\>

En el ejemplo anterior cada persona puede ser empleado, cliente o ambas o ninguna de
ellas.

En el siguiente ejemplo, una persona puede ser empleado o cliente o ninguna de las dos
cosas, pero nunca ambas. Se  trata de una especialización excluyente.

<p align="center"\><img src=img/especializacion-excluyente.png "hosts" alt="hosts"\>

La existencia de supertipos y subtipos, en uno o varios niveles, da lugar a una jerarquía,
que permitirá representar una restricción del mundo real.

## 1.4.3 Agregación

La agregación, consiste en construir un nuevo tipo de entidad como composición de otras
dos y su relación y así poder manejarlo en un nivel de abstracción mayor. Por ejemplo, se
tienen los tipos de entidad empresa y solicitante de empleo relacionados mediante el tipo
de relación entrevista; pero es necesario que cada entrevista se corresponda con una
determinada oferta de empleo. Como no se permite la relación entre relaciones, se puede
crear un tipo de entidad compuesto por empresa, entrevista y solicitante de empleo y
relacionarla con el tipo de entidad oferta de empleo.

<p align="center"\><img src=img/agregacion.png "hosts" alt="hosts"\>
