# Diplomado administración, clusterización y analítica de Bases de Datos

## Guía de conceptos básicos de ciencia de datos

## 2. Cálculo Diferencial

### 2.1 Definición de derivada

Sea _f_ una función definida en un intervalo abierto que contiene a _a_. La derivada 
de _f_ en _a_, denotada por _f´(a), está dada por:

<p align ="center"><img src="imagenes/Calculo_dif/def_deri.png"></p>

Definición alternativa

<p align ="center"><img src="imagenes/Calculo_dif/def2_deri.png"></p>

y se representa por:

<p align ="center"><img src="imagenes/Calculo_dif/rep_deri.png"></p>

#### 2.1.1 Regla de los 4 pasos

Sea una función _y = f(x)_, entonces:

<p align ="center"><img src="imagenes/Calculo_dif/reg4_deri.png"></p>

#### 2.1.2 Derivada de una función compuesta (Regla de la cadena)

Sea _y = g(u), u = f(x)_, entonces la derivada de _y = (g ° f)(x) = g(f(x)) se define:

<p align ="center"><img src="imagenes/Calculo_dif/cade_deri.png"></p>

### 2.2 Derivadas de funciones implícitas

Una función implícita se expresa en términos de _x_ y _y_

Ejemplo:

* _sen x = cos(x-y)_
* e^(x+y) = x

Para proceder a derivar una función implícita, se deriva término a término los elementos
de la igualdad con respecto a la variable que se indica, y se despeja la derivada.

### 2.3 Derivadas de orden superior

Sea _y = f(x)_ una función de orden superior, se derivará tantas veces como lo indique
el orden requerido.

La derivada de primer orden está representada por: 

<p align ="center"><img src="imagenes/Calculo_dif/prim_deri.png"></p>

La segunda derivada, es la derivada de la derivada de primer orden, y se denota por:

<p align ="center"><img src="imagenes/Calculo_dif/seg_deri.png"></p>

Al proceso de hallar derivadas, una tras otra, se le denomina derivación sucesiva.

Para calcular la enésima derivada de una función se denota por:

<p align ="center"><img src="imagenes/Calculo_dif/ene_deri.png"></p>

[Bibliografía](bibliografia.md)