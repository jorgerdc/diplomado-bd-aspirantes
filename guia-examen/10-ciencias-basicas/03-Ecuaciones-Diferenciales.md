# Diplomado administración, clusterización y analítica de Bases de Datos

## Guía de conceptos básicos de ciencia de datos

## 3. Ecuaciones Diferenciales

### 3.1 Ecuaciones Diferenciales separables.

Teniendo una ecuación el la que se presentan  _x, y, y', y'',...,y^(n)_, donde _y_ es
una función de _x_ y _y^(n)_ es la enécima derivada de _y_ con respecto a _x_, es una
ecuación diferencial ordinaria de orden n, por ejemplo:


<p align ="center"><img src="imagenes/ED/ord_ed.png"></p>

Sea la función _f(° f(x))_ una solución de una ecuación difrencial si al sustituir _y_
por _f(x)_, obtenemos una identidad para todo _x_ en un intervalo.

Ejemplo:

<p align ="center"><img src="imagenes/ED/ejem_ed.png"></p>

tiene como solución

<p align ="center"><img src="imagenes/ED/ejem2_ed.png"></p>

Donde para todo númerop real _C_.

Lo anterior sucede porque al sustituir _y_ por _f(x)_ se llega a la identidad 
_6x^2 - 5 = 6x^2 - 5_. Por lo tanto decimos que _f(x) =  2x^3 - 5x + C_ es una
solución general de y' = 6x^2 -5.

Para obtener una solución particular se asignan valores específicos a _C_.
En ciertos casos se dispone de condiciones iniciales para determinar una solución
particular.

### 3.2 Ecuaciones Diferenciales Lineales de primer y segundo orden.

#### 3.2.1 Ecuaciones diferenciales lineales de primer orden

Una ecuación diferencial lineal de primer orden es una ecuación de la siguiente
forma:

<p align ="center"><img src="imagenes/ED/ecpo_ed.png"></p>

Donde _P_ y _Q_ son funciones continuas.

Laecuación diferencial lineal de primer orden _y' + P(x)y = Q(x)_ se puede transformar
en una ecuación diferencial separable multiplicando ambos lados de la ecuación por el
factor de integración:

<p align ="center"><img src="imagenes/ED/facint_ed.png"></p>

##### 3.2.2 Ecuaciones Diferenciales lineales de segundo orden

Una ecuación diferencial lineal de orden _n_ es una ecuación de forma:

<p align ="center"><img src="imagenes/ED/so_ed.png"></p>

donde _f1, f2, ..., fn_ y _k_ son funciones de una variable que tienen el mismo dominio.
Si _k(x) =  0_ para todo x, se dice que la ecuación es homogenea. Si _k(x) != 0 para
algún x, se dice que la ecuación es no homogenea.

Para la ecuación _y'' + by' + cy = 0_ se tiene uan ecuación auxiliar la cual es
_m^2 + bm + c = 0_.

La ecuación auxiliar tiene dos raíces distintas _m1_ y _m2_, una raíz real doble m, o dos
raíces complejas conjugadas si _b^2 - 4c_ es positivo, cero o negativo.

Por lo tanto, si las raíces _m1_ y _m2_ de la ecuación auxiliar son reales y distintas,
entonces la solución general de  _y'' + by' + cy = 0_ es:

<p align ="center"><img src="imagenes/ED/aux_ed.png"></p>

Si la ecuación auxiliar tiene una raíz doble _m_, entonces la solución general de
_y'' + by' + cy = 0_ es:

<p align ="center"><img src="imagenes/ED/aux2_ed.png"></p>

### 3.3 Ecuaciones Diferenciales Lineales no homogeneas.

Si _y = f(x)_ y _f''_ existe, entonces el operador diferencial lineal
_L = D^2 + bD + c se define por

<p align ="center"><img src="imagenes/ED/nh_ed.png"></p>

Recordar que es conveniente usar los simbolos _D_ y  _D^2_ para los operadores diferenciales
tales que si _y = f(x)_, entonces

<p align ="center"><img src="imagenes/ED/op_ed.png"></p>

y 

<p align ="center"><img src="imagenes/ED/op2_ed.png"></p>

[Bibliografía](bibliografía.md)