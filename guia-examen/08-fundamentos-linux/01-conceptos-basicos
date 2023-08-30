# 8. Fundamentos de Linux

## 8.1 ¿Qué es Unix, Linux, GNU?

Unix es uno de los sistemas operativos más populares debido a su extenso soporte
y distribución. Es un sistema  operativo que nace a principios de los 70s creado
principalmente por  Dennis Ritchie y Ken Thompson.

Entre 1971 y 1973, Dennis Ritchie crea C, un lenguaje de alto nivel para poder llevar Unix
a otras arquitecturas sin tener que reescribirlo. En 1973 se lanza la primera versión de
Unix escrita en C y portable.

Originalmente fue desarrollado como sistema multi tarea de tiempo compartido para
mini-computadoras y mainframes a mediados de los 70 en los laboratorios de AT&T, y desde
entonces se ha convertido en uno de los sistemas más utilizados.

Existen numerosas versiones de Unix para muchos sistemas, desde computadoras personales
hasta super computadoras como la Cray Y-MP. La mayoría de las versiones de Unix son muy
costosas.

Sus características principales son:

* Portabilidad, capacidad multi-usuario y multi-tarea, su eficiencia
* Alta seguridad, eficiencia en tareas que implican acceso a redes.

La filosofía de Unix esta basada en los principios de  minimalismo y modularidad: hacer
muchos programas que hagan una sola cosa  bien hecha y que, al comunicarse entre sí,
ejecuten tareas más complejas.

La forma de comunicarse es a través del concepto de **pipeline**.

<p align="center"><img src="img/01.png"></p>

Otra característica de Unix es la posibilidad de ofrecer un entorno de programación
amigable para que otros programadores puedan escribir programas que sean ejecutados
en el propio sistema operativo sin tener que escribir código en ensamblador, es
decir, a través de la **programación en Shell**

### 8.1.1 Estructura de un sistema UNIX

Unix se compone de 3 capas:

* **El kernel**.  Representa el núcleo del sistema, se comunica con el hardware,
  ejecuta los programas  y controla el acceso a los recursos de la máquina.
* **El shell**. Es una interfaz a través de la cual se comunica el usuario  con
  la máquina (computadora) a través del uso de comandos, es decir, el shell es
  un intérprete de comandos, traduce las instrucciones que los usuarios escriben
  en la terminal.
* **Herramientas**. Conjunto de programas escritos para ejecutar tareas específicas.
  Como se mencionó anteriormente, estos programas tienen la capacidad de trabajar
  en conjunto con otros programas a través del concepto de pipeline.
  Comandos comunes `ls`, `grep`, etc., son ejemplos de estos programas.

### 8.1.2 Sistema de archivos

El sistema de archivos representa un componente del sistema operativo responsable de
la administración de los datos almacenados en archivos en los diferentes dispositivos
de almacenamiento: discos, cintas, memorias, etc.

Este componente debe proporcionar los mecanismos necesarios para realizar un almacenamiento
y acceso a estos archivos de forma eficiente y segura.

La estructura de un sistema de archivos se organiza a través de **directorios**. Un
directorio se puede considerar como un archivo especial que contiene información empleada
para localizar otros archivos dentro de un dispositivo de almacenamiento. Los
directorios pueden contener otros directorios llamados **subdirectorios**.

<p align="center"><img src="img/02.png"></p>

## 8.2 GNU/Linux

A principios de los 90s, Linus Torvalds comenzo con la escritura de un sistema operativo
que pudiera ejecutarse en una computadora personal, que cualquier usuario pudiera utilizar.

Al mismo tiempo, ya se desarrollaba otro proyecto con la intención de crear un sistema
operativo tipo Unix pero **gratuito**, es decir, el proyecto **GNU** GNU's Not Unix
(GNU no es Unix). Este proyecto ya contaba con diversas herramientas pero le faltaba el
núcleo, lo que posteriormente se integró dando lugar a lo que hoy conocemos como
GNU/Linux, o simplemente Linux:  Un sistema operativo libre de la familia Unix.

Linux fue y es desarrollado con la ayuda de muchos programadores y expertos de todo el
mundo, comunicados a través de Internet. Cualquiera puede acceder a Linux y desarrollar
nuevos módulos o cambiarlo. El kernel Linux no utiliza ni una sola línea del código
original del Unix de AT&T o de cualquier otro software privativo, y se distribuye bajo la
licencia GNU GPL.

Básicamente, esta licencia establece que el software en cuestión debe ser distribuido
incluyendo todo el código fuente y la documentación. Establece además que cualquier
persona puede modificar el software de acuerdo a sus necesidades e inclusive puede
redistribuirlo, siempre y cuando lo haga bajo la misma licencia.

<p align="center"><img src="img/03.png"></p>

## 8.3  Introducción a la terminal de Linux

La terminal de Linux representa el principal mecanismo para escribir y ejecutar
comandos.

### 8.3.1 Emulador de una terminal

Un emulador de terminal es un programa que permite el uso de una terminal en un
entorno gráfico. El uso de este emulador es muy común ya que la mayoría de los
usuarios hacen uso del sistema operativo bajo un entorno gráfico. Algunos ejemplos
de emuladores de terminal:

* Mac OS X: Terminal (default), iTerm 2
* Windows: ConEmu, Windows Terminal, PuTTy
* Linux: Gnome Terminal, Konsole, XTerm

## 8.3.2 El Shell

En un sistema Linux, el shell representa una interfaz que permite la escritura de
comandos (command-line) así como scripts para ser interpretados y procesados por
el servidor Linux. Existen varios tipos de Shells ampliamente utilizados. Algunos
ejemplos:

* Bourne-Again shell (bash)
* C Shell
* Z shell (zsh)
* Fish Shell
* Ksh Shell
* Tcsh Shell
* Dash Shell
* Ash Shell
* Elvish Shell
* Ion Shell
* PowerShell

[Referencia](https://www.tutorialspoint.com/8-types-of-linux-shells)

El shell que se empleará en estas notas es Bash, el cual representa el shell por
default en la mayoría de las distribuciones Linux: Ubuntu, Fedora, RHEL.

### 8.3.2 Command prompt

Al entrar a sesión en Linux (Hacer login), generalmente se muestra el mensaje
del día (MOTD: Message Of The Day) que incluye información diversa, por ejemplo,
la versión de la distribución de Linux, etc.  Posterior a este mensaje, el
sistema presenta el **command prompt**, llamado también **shell prompt**. A partir
de este prompt se puede comenzar a escribir comandos. La información que muestra
el prompt puede ser personalizada. Ejemplo:

```bash
admin@lap-red-mint:~$
```

* `admin` es el username o nombre de usuario en sesión.
* `lap-red-mint` es el hostname (nombre de host) o nombre de la máquina.
* `~` Indica el directorio actual, es decir, el directorio en el que el usuario
  admin se encuentra.  En bash, el símbolo `~` representa al directorio _home_
  del usuario. En este caso representa al directorio `/home/admin`
* `$` representa el símbolo del prompt e indica el final del command prompt..
  posterior a este carácter, aparecerán los comandos que el usuario escriba

  Ejemplo:

```bash
#cambiarse al directorio home
admin@lap-red-mint:~$ cd ~
admin@lap-red-mint:~$ pwd
/home/admin
#Al cambiarse al directorio /var/log, el command prompt incluye la ruta /var/log
admin@lap-red-mint:~$ cd /var/log
admin@lap-red-mint:/var/log$ 
```

### 8.3.3 Ejecución de comandos

Los comandos se ejecutan en el command prompt especificando el nombre de un
archivo ejecutable (archivo o programa binario) o un script.

Cuando un comando se ejecuta, se crea una instancia llamada **proceso**. Por
default los comandos se ejecutan de forma síncrona (en primer plano - foreground)
por lo que el usuario debe esperar a que  el proceso termine antes de liberar
el command prompt.

Es importante mencionar que prácticamente todo lo que se escribe el Linux es
sensible a minúsculas y mayúsculas: comandos, directorios, etc. Ejemplo

```bash
#comando LS no es válido, debe ser ls
admin@lap-red-mint:~$ LS
LS: command not found

#carpeta ADMIN incorrecta, debe ser admin
admin@lap-red-mint:~$ cd /home/ADMIN
bash: cd: /home/ADMIN: No such file or directory

admin@lap-red-mint:~$ cd /home/admin
admin@lap-red-mint:~$ 
```

#### 8.3.3.1 Ejecución de comandos con opciones y parámetros

Se especifican posterior al nombre del comando seguido de un espacio

```bash
ls -la /home
```

* En el ejemplo anterior `-la` son opciones del comando. Estas opciones generalmente se especifican con `-` o con `--`. Las opciones se pueden
  combinar. Por ejemplo, `ls -la` es equivalente a `ls -l -a`. Las opciones se
  emplean para modificar el comportamiento del parámetro.  En este caso:
  * `-l` significa _long listing_  (mostrar detalle de la lista)
  * `-a` muestra todos los archivos incluyendo archivos ocultos.
* La cadena `/home` representa un parámetro del comando.

### 8.3.4 Variables de entorno

Cuando un usuario interactúa con el sistema operativo a través de una sesión shell,
existen diversos elementos, datos, variables y configuraciones que el shell utiliza
para que el usuario pueda interactuar con el sistema y acceder a sus recursos.

El shell realiza una administración de estos elementos, datos, variables y
configuraciones en una área denominada **entorno**. Esta área se crea cada vez
que el usuario inicia sesión. Entro otras cosas, este entorno contiene los valores
de ciertas variables que definen las propiedades del sistema llamadas
**variables de entorno**.

Las variables de entorno definen valores que se usan para cambiar la forma
en la que un comando es procesado y ejecutado. Cuando un usuario entra a sesión
en el sistema, se establece el valor de estas variables. Su valor se configura en
archivos que se leen justo durante el inicio de sesión. Para mostrar los nombres
de las variables de entorno y sus valores asignados se puede emplear el comando
`env`. Ejemplo:

```bash
admin@lap-red-mint:~$ env
SHELL=/bin/bash
SESSION_MANAGER=local/lap-red-mint:@/tmp/.ICE-unix/1890,unix/lap-red-mint:/tmp/.ICE-unix/1890
WINDOWID=111149062
QT_ACCESSIBILITY=1
COLORTERM=truecolor
XDG_CONFIG_DIRS=/etc/xdg/xdg-mate:/etc/xdg
XDG_SESSION_PATH=/org/freedesktop/DisplayManager/Session0
GTK_IM_MODULE=ibus
CLUTTER_BACKEND=x11
LANGUAGE=en_US
MANDATORY_PATH=/usr/share/gconf/mate.mandatory.path
...
```

#### 8.3.4.1 Variables de entorno frecuentes

* `PATH`: Contiene una lista de directorios separados por `:` donde se encuentran los archivos ejecutables (comandos), o los scripts. Al proporcionar un comando en el command prompt, el shell hará una búsqueda del comando capturado en los directorios configurados para poder localizarlo y ejecutarlo.
* `SHELL`: Describe el interprete shell que se empleará para procesar comandos.
   En la mayoría de los casos, será `bash`.
* `TERM`: Especifica el tipo de terminal a emular cuando se ejecuta el shell.
* `USER`: El usuario que inició sesión actualmente.
* `PWD`: El directorio actual de trabajo.
* `OLDPWD`: El directorio anterior de trabajo.
* `LANG`: Las configuraciones actuales de idioma y localización, incluida la
   codificación de caracteres. Por ejemplo: `en_US.UTF-8`.
* `HOME`: El directorio principal o directorio _home_ del usuario actual.

Para mostrar el valor de una variable se emplea el comando `echo`.

```bash
admin@lap-red-mint:~$ echo $PATH
/opt/jdk-17/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
admin@lap-red-mint:~$ 
```

#### 8.3.4.2 Cambiando valores de una variable de entorno

* Se emplea la sintaxis `export VAR=valor`. Para que la variable se considere
  como de entorno, se debe emplear el comando `export`.
* Para distinguir a las variables de entorno de otras variables, su nombre se
  escribe en mayúsculas.
* `export` permite que el valor de la variable esté disponible o sea heredada
  por todos los sub-procesos que se generen a partir del proceso actual en el
  que se ejecuta la instrucción `export`
* Lo anterior significa que si en una terminal se ejecuta la instrucción `export`,
  todos los subprocesos que se generan al escribir un comando en dicha terminal
  podrán heredar el valor de la variable.
* Es importante mencionar que si el usuario inicia una segunda sesión shell,
  es decir, abre una nueva terminal, las variables de entorno inicializadas
  en la primera sesión no estarán disponibles. Si se desea que estas variables
  estén disponibles en todas las sesiones shell de un usuario se deben considerar
  los conceptos de la siguiente sesión.

#### 8.3.4.3 Sesiones shell con y sin autenticación

Una sesión shell se puede crear de 2 formas:

* Se crea una sesión con autenticación cuando el usuario autentica en
  el sistema operativo, es decir, proporciona su password, por ejemplo,
  para iniciar una sesión gráfica, o cuando crea una nueva sesión con
  un usuario diferente al ejecutar el comando `su -l`
* Se crea una sesión sin autenticación.  Por ejemplo, cuando el usuario
  solo abre una nueva terminal. Se crea una nueva sesión shell, pero sin
  autenticar, es decir, con el mismo usuario.

Si se desea que ciertas variables de entorno estén disponibles cuando un usuario
crea una nueva sesión shell, dichas variables se pueden definir en ciertos archivos.
Los archivos que se leen dependen del tipo de inicio de sesión: con o sin autenticación.

* Se crea una sesión con autenticación (bash)
  1. Se lee el archivo `/etc/profile`
  2. Se leen archivos de configuración particulares al usuario. El archivo
     depende del tipo de intérprete. Por ejemplo, para bash se lee el primer
     archivo encontrado de los siguientes 3: `~/.bash_profile`, `~/.bash_login`
     y `~/.profile`

* Se crea una sesión sin autenticación (bash)
  1. Se lee el archivo `/etc/bash.bashrc`
  2. Se lee el archivo `~/.bashrc`
