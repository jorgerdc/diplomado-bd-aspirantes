# 8. Fundamentos de Linux

## 8.5 Otros comandos

### 8.5.1 find

El comando find busca archivos que concuerden con un determinado criterio. La sintaxis de
la línea de órdenes es la siguiente:

```bash
find  [directorio...]  [criterio...] [acción...]
```

* `directorio` es el punto de partida de la búsqueda
* `criterio` es la condición que deben cumplir los archivos que estamos buscando
* `acción` es lo que se hará con los archivos encontrados.
Si no se especifica ningún directorio se asume el directorio actual. Si
no se proporciona ningún criterio todos los archivos son aceptados por find. Si no se
especifica ninguna acción se muestran por la salida estándar los archivos encontrados.
Ejemplos:

* Mostrar recursivamente todos los archivos del directorio actual

```bash
~$ find
.
./d
./d/cp.man
./rm.man
./ls.man.gz
```

Las siguientes opciones son las más comunes. Para mayores detalles, se puede
consultar  el manual del comando empleando la instricción `man find`

* Mostrar los archivos que terminen con `.man`

```bash
$ tree .
.
├── d
│   └── cp.man
├── ls.man.gz
└── rm.man

1 directory, 3 files

#ejecutar find
$ find . -name '*.man'
./d/cp.man
./rm.man

#ejecutar find
$ find -name '*.man'
./d/cp.man
./rm.man
```

Encontrar todos los archivos que sean de un tipo determinado:

* `f` archivo
* `d` directorio
* `b` dispositivo de bloques
* `c` dispositivo de caracteres
* `l` enlace simbólico

Encontrar todos los directorios a partir del directorio actual `.`

```bash
$ find . -type d
.
./d
```

* Opción `-exec`

Ejecuta el comando que queramos sobre los archivos seleccionados. El nombre del archivo
dentro del comando se referencia con `'{}'`, y el comando debe acabar en `\;`
Ejemplo: Encontrar los archivos txt y mostrar su contenido empleando el comando `cat`

```bash
find . -name '*.txt' -exec cat '{}' \;
```

### 8.5.2 comando wc

`wc` cuenta el número de caracteres, palabras y líneas de uno o más archivos. Se considera
que una palabra es una secuencia de caracteres delimitada por blancos (espacios,
tabuladores, saltos de línea y de página).

Sintaxis:

```bash
wc  [-lwcL]  [fichero...]

```

Por omisión `wc` muestra tres contadores: caracteres, palabras y líneas; si queremos que
solo muestre uno de ellos, podemos usar las opciones `-c` (caracteres), `-w` (palabras)
o `-l` (líneas). La opción `-L` muestra la longitud de la línea mas larga del fichero.
Estas opciones también pueden combinarse entre sí.

```bash
$ wc ls.man rm.man 
  341  2801 20981 ls.man
   80   549  4061 rm.man
  421  3350 25042 total

```

¿cuántas líneas tiene el manual del comando ls ?

```bash
$ man ls | wc -l
341
```

### 8.5.3 grep

El comando `grep` selecciona las lineas de texto que contengan un patrón que podemos definir
con expresiones regulares. Se puede usar para filtrar las lineas de un archivo de disco o
el texto que coja de la entrada estándar mediante el uso del concepto de pipeline

Opciones más útiles de grep

* `-v`: Muestra las que NO coinciden con el patrón
* `-l`: Sólo indica el nombre del fichero donde ha encontrado alguna coincidencia
* `-w`: El patrón tiene que ser una palabra independiente
* `-n`: Indica el número de linea donde ha encontrado el patrón
* `-i`: No distingue entre mayúscula y minúscula
* `-c`: Muestra la cantidad de lineas que cumplen con el patrón
* `-r`: Busca en los archivos de forma recursiva

Ejemplos de uso del comando grep

```bash
grep alumno /etc/passwd

```

busca el usuario alumno dentro del fichero passwd

```bash
grep -v deb-src /etc/apt/sources.list

```

selecciona del fichero sources.list las lineas que NO tienen el texto deb-src

```bash
history | grep ssh
```

busca las lineas que contengan la palabra ssh dentro del historial de comandos.

El siguiente documento muestra una lista de otros comandos comúnmente empleados.
[Lista de comandos](https://www.freecodecamp.org/espanol/news/comandos-de-linux/)
