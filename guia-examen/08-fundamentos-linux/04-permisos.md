# 8. Fundamentos de Linux

## 8.6 Permisos

UNIX es un sistema operativo multitarea y multiusuario. Esto posibilita que varios
usuarios ejecuten distintas tareas a la vez, y en consecuencia, se hace necesario
establecer algún mecanismo que proteja la información de cada uno.

La forma en la que el sistema identifica a cada usuario es mediante la asignación de
cuentas. Cada usuario dispone de un nombre de usuario que lo identifica (`login`,
`login_id`) y además puede pertenecer a uno o varios grupos. En un sistema GNU/Linux,  al
menos deben existir 2 cuentas:

* Una para `root` (superusuario), que debe utilizarse, por motivos de seguridad, solo durante el tiempo de efectuar una labor de administración
* Usuario normal para la realización del trabajo cotidiano. A este usuario se le
  puede otorgar permisos para ser administrador a través del uso del comando `sudo`.

La identidad del usuario junto con el grupo principal al que pertenece determinan los
derechos de acceso a los archivos y otros recursos del sistema.

Cuando un usuario inicia su sesión, teclea un nombre (login o login_id) y después confirma
que efectivamente es él escribiendo una contraseña (password). El sistema en realidad
reconoce al usuario por medio de un número llamado identificador del usuario (**UID**).
Además del UID, al usuario se le asigna un identificador de grupo principal (**GID**),
que lo coloca dentro de cierta clase de usuarios.

El sistema mantiene toda la información que necesita conocer sobre cada usuario en dos
archivos:

* `/etc/passwd`
* `/etc/group`

El archivo passwd contiene una línea por usuario con el siguiente formato:

```bash
login_id:clave_codificada:UID:GID:varios:directorio_de_entrada:shell
```

El primer campo contiene el nombre de login del usuario. El segundo está reservado para la
contraseña del usuario, aparece una `x`, el sistema almacena las contraseañas en
`/etc/shadow`. Cuando un usuario se identifica con su contraseña, esta se codifica y se
compara con la contraseña almacenada en `/etc/shadow`; si ambas coinciden, se le
permite al usuario iniciar la sesión.

Los campos tercero y cuarto contienen los identificadores numéricos de usuario (UID) y de
grupo principal (GID). El campo `varios` puede contener cualquier cosa, como el nombre
completo del usuario, la dirección, el número de teléfono, etc.

El sexto campo indica el directorio _home_ del usuario, y por último, el campo `shell`
le dice al sistema qué shell deberá ejecutar cuando el usuario inicie la sesión.

Un usuario puede pertenecer a más de un grupo. El grupo que aparece en el fichero
`/etc/passwd` se llama grupo principal y el resto de los grupos a los que pertenece son
sus grupos secundarios. El fichero `/etc/group` contiene la lista de los grupos que
existen en el sistema, donde cada línea representa a un grupo:

```bash
nombre_grupo:x:GID:lista_de_usuarios
```

La línea anterior contiene  la siguiente estructura:

* El nombre del grupo
* Una posible contraseña que podría tener (normalmente se mostrará una x)
* El GID (grupo principal) y la lista separada por comas de los usuarios que
  pertenecen al grupo como grupo secundario.

Cada fichero tiene un **propietario** (inicialmente el usuario que lo creó) y pertenece a
un **grupo** en particular (generalmente el grupo principal del propietario). Basado en
esta estructura, el sistema asigna permisos a tres niveles:

* a nivel del propietario dueño del archivo.
* a nivel del grupo del archivo (grupo al que pertenece el propietario).
* a nivel de todos los demás usuarios.

Para cada uno de estos tres niveles, asigna tres tipos de permisos básicos:

* `r` para la lectura.
* `w` para la escritura.
* `x` para la ejecución.

Esta información se guarda en el nodo-i del archivo y se puede ver con un
listado largo (ls -l)

```bash
~$ ls -l

drwxrwxr-x 2 jorge jorge 4096 Dec 31  2022  backups
drwxr-xr-x 3 jorge jorge 4096 Aug 20 15:29  Desktop
drwxr-xr-x 2 jorge jorge 4096 Dec 30  2022  Documents
drwxr-xr-x 2 jorge jorge 4096 Aug 28 18:32  Downloads
lrwxrwxrwx 1 jorge jorge   22 Jan 12  2023  git -> /media/jorge/PROYS/git
drwxr-xr-x 2 jorge jorge 4096 Dec 30  2022  Music
drwxrwxr-x 3 jorge jorge 4096 Feb 23  2023  oradiag_jorge
drwxr-xr-x 2 jorge jorge 4096 Dec 30  2022  Pictures
drwxr-xr-x 2 jorge jorge 4096 Dec 30  2022  Public
drwxr-xr-x 2 jorge jorge 4096 Dec 30  2022  Templates
drwxr-xr-x 2 jorge jorge 4096 Dec 30  2022  Videos
drwxrwxr-x 3 jorge jorge 4096 Feb 16  2023 'VirtualBox VMs'

```

Existen dos formas de escribir los permisos cuando los tenemos que especificar como
argumentos de algunos comandos:

* Modo simbólico
* Modo octal

### 8.6.1 Permisos en modo simbólico

El modo simbólico utiliza letras para especificar los permisos. En el ejemplo anterior
los permisos se muestran con la primera cadena del lado izquierdo, por ejemplo:
`drwxrwxr-x`.  Se tiene un total de 10 caracteres:

* Primer carácter indica el tipo de archivo:
  `d:` directorio
  `l:` liga simbólica
  `b:` Archivo especial de bloques
  `c:` Archivo especial de caracteres
  `p:` Archivo especial named pipe
  `s:` Archivo especial socket local.
* Los siguientes 3 caracteres `rwx`  definen los permisos para el dueño: `u`
* Los siguientes 3 caracteres `rwx`  definen los permisos para el grupo: `g`
* Los siguientes 3 caracteres `rwx`  definen los permisos para usuarios que no
  son dueños y pertenecen a otros grupos: `o`
* Se puede emplear el caracter `a` para hacer referencia a los 3 tipos de roles
  `u`, `g`, `o`
* El significado de los caracteres `rwx` es:
  * `r:` permisos de lectura
  * `w:` permisos de escritura
  * `x:` permisos de ejecución

Ejemplo

```bash
chmod ugo+rwx archivoDePrueba
```

* Se emplea el comando `chmod` para cambiar los permisos al archivo.
* `ugo` significa, asignar el permiso tanto a los 3 roles: dueño, grupo y a los
   demás usuarios
* El permiso a asignar a los 3 roles es `rwx`, es decir se otorgan todos los
  permisos a los 3 roles: lectura, escritura, ejecución.
* El símbolo `+`  significa añadir permisos. Existen otros 2 símbolos:
  * `-` quitar un permiso
  * `=` asignar permisos fijos

Ejemplo

Quitar permisos de lectura, escritura,  y ejecución a  los otros usuarios:

```bash
chmod o-rwx archivoDePrueba
```

### 8.6.1 Permisos en modo octal

El comando chmod también es compatible con otra nomenclatura basada en el sistema
octal.

Suponer que los permisos del propietario (r w x) están identificados por 0 y 1. Es decir,
si por ejemplo queremos dar permisos de lectura y escritura solamente (y no permisos de
ejecución) sería: 110. Si queremos solo el permiso de lectura sería: 100.

Por lo tanto, teniendo en cuenta todas las posibilidades existentes obtenemos los
siguientes valores:

```bash
0 0 0: 0
0 0 1: 1
0 1 0: 2
0 1 1: 3
1 0 0: 4
1 0 1: 5
1 1 0: 6
1 1 1: 7
```

Ejemplo

Otorgar permisos totales al propietario y dejar sin ningún permiso a los otros dos roles
(grupo y otros) es decir `rwx --- ---  => 700`

```bash
chmod 700 archivoDePrueba
```

Otorgar permisos de lectura y escritura a todos los roles  `rwx => 110 = 6`

```bash
chmod 666 archivoDePrueba
```

## 8.7 El comando chown

Los archivos o directorios de Linux tienen un propietario asignado, y para cambiar esto
está el comando `chown`. (change owner).

Si un usuario realiza cambios en un archivo, el usuario root podrá dar uso de `chown` para
cambiar estas propiedades. En todo caso, al realizar un cambio de usuario propietario, el
grupo no se cambiará con él. Incluso si el nuevo fichero pertenece a un grupo diferente,
el grupo propietario seguirá siendo el anterior.

Ejemplo
Cambiar el dueño a `usuario` para el archivo `archivoPrueba`

```bash
sudo chown usuario archivoPrueba
```

es posible que este cambio sea sobre un directorio, por lo cual si queremos que se aplique
en orden, y de forma recursiva para todos los archivos, esto nos garantiza que los
directorios y subdirectorios, tendrán el cambio de propietario correspondiente.

```bash
sudo chown -R usuario directorioPrueba
```

## 8.8 El comando chgrp

Este comando es similar a `chown`, pero nos permite realizar el cambio del grupo al que
pertenece un archivo o directorio. Esto también se puede realizar con `chown`, como
veremos más adelante. Al igual que ocurre con el anterior, si realizamos el cambio de
grupo de un archivo, el usuario propietario no cambiará. Esto se puede realizar de la
siguiente forma.

```bash
sudo chgrp grupo archivoPrueba
```

De forma similar, de forma recursiva:

```bash
sudo chgrp -R grupo archivoPrueba
```

El comando chown puede emplearse para cambiar tanto en dueño como el grupo
de un archivo o directorio en una sola instrucción:

```bash
sudo chown usuario:grupo ruta/archivo
```

Se emplean `:` para separar al nuevo dueño y al nuevo grupo.

Para mayores detalles, clic [aquí](https://www.fpgenred.es/GNU-Linux/permisos.html)

## 8.9 Conclusiones

Los documentos de esta sección representan solo una pequeña introducción a
conceptos y comandos básicos y fundamentales en Linux.  Definitivamente
existe una gran cantidad de conceptos y comandos por revisar para profundizar
y aumentar los conocimientos en general de los sistemas UNIX, GNU/Linux.
