# Diplomado administración, clusterización y analítica de Bases de Datos

## Guía de conceptos básicos de ciencia de datos

## 1. Algebra

### 1.1 Operaciones con matrices

#### **1.1.1 Multiplicación por un escalar**

Sea *A = (a)* una matriz de orden _m x n_ y _b_ un número real, entonces _bA=(ba)_ es decir:

<p align ="center"><img src="imagenes/Algebra/m_esc.png"></p>

A la matriz resultante también se le conoce como matriz escalar.

#### **1.1.2 Suma de matrices**

Sea _A = (a)_ y _B = (b)_ dos matrices de orden _m x n_ la suma de _A_ y _B_ está determinada por:

<p align ="center"><img src="imagenes/Algebra/sum_m.png"></p>

Donde _A + B_ es la matriz de orden _m x n_ que resulta de sumar los elementos correspondientes.

### 1.2 Inverso Aditivo

El inverso aditivo de _A_ de orden _m x n_ es _-A_.

El inverso aditivo de una matriz se obtiene multiplicando cada elemento por el escalar -1, por
lo tanto el inverso aditivo de una matriz _A_ es otra matriz _-A_, tal que _A + (- A) = **0**_.
Donde **0** es la matriz nula.

### 1.3 Resta de matrices

La resta de dos matrices _m x n_, se define:

<p align ="center"><img src="imagenes/Algebra/res_m.png"></p>

Donde _-B_ es el inverso aditivo de _B_

### 1.4 Multiplicación de matrices

Sea _A = (a)_ una matriz de orden _m x n_, y _B = (b)_ una matriz de orden _m x p_, la
multiplicación  _**AB**_ da como resultado la matriz _C = (c)_ de orden _m x p_, tal que:

<p align ="center"><img src="imagenes/Algebra/mul_m.png"></p>

Para: 

_i = 1, 2, 3,..., m;_

_j = 1, 2, 3,..., n_

Por lo tanto, el número de columnas de la matriz _A_, es igual al número de renglones de
la matriz _B_.

Ejemplo:

Matriz _A_  | Matriz _B_  |  Matriz _AB_
------------| ----------- | -------------
    2 x 3   | 3 x 4   |  2 x 4
    5 x 4   | 4 x 2   |  5 x 2

#### 1.5 Determinantes

El determinante de una matriz _A_ de orden _n_, es el número escalar que se relaciona
con la matriz, mediante una regla de operación. Denotado por _det**A** = |A|_

Sea la matriz de orden 2

<p align ="center"><img src="imagenes/Algebra/det2_m.png"></p>

El determinante de _A_ está dado por:

<p align ="center"><img src="imagenes/Algebra/det_m.png"></p>

### 1.6 Matriz Inversa

Dada una matriz cuadrada _P_ de orden _n_, si existe una matriz _Q_ tal que:

<p align ="center"><img src="imagenes/Algebra/mi_m.png"></p>

Entonces la matriz _Q_ es la matriz inversa de _P_ y se denota P^-1, de tal forma que:

Donde:

<p align ="center"><img src="imagenes/Algebra/mip_m.png"></p>

_**I**_: Es la matriz identidad de orden _n_.

Para que exista la inversa de la matriz _P_ es necesario que la matriz sea cuadrada y el _detP_ sea diferente de cero.

[Bibliografía](bibliografia.md)