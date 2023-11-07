# CLASE 2

En esta clase vamos a seguir el libro que nos facilitaron. Desde dónde lo dejamos en la clase1

### Que es un pid??

Es un proces identifiere, las apps tienen uso de tiempo de ejecución para procesos

### SYS

Partes del kernel, podemos encontrar información o modificar comportamientos del sistema ejemplo ver información/manipular la información de cache.

### /USR

Contiene los programas y archivos que no son necesarios para el sistema, pero si para los usuarios. Es practicamente todo el sistema

## Enlaces simbólicos

Muy importante saber los enlaces simbólicos

```bash
lrwxrwxrwx.   1 root root    7 Oct 11  2021 lib -> usr/lib
lrwxrwxrwx.   1 root root    9 Oct 11  2021 lib64 -> usr/lib64
```

### Comando DU (Disk Usage)

nos indica el espacio que ocupa cada una de las carpetas

```bash
[root@formacion /]# du -csh ./* 2</dev/null
0	./bin
245M	./boot
0	./dev
32M	./etc
90M	./home
0	./lib
0	./lib64
0	./media
512	./mnt
19M	./opt
0	./proc
52K	./root
60M	./run
0	./sbin
0	./srv
0	./sys
12K	./tmp
4.6G	./usr
1.6G	./var
6.6G	total
```

### /BIN

En bin se suele encontrar los binarios de los programas que se pueden ejecutar por cualquier usuario.

```bash
[root@formacion bin]# ls -l
total 352516
-rwxr-xr-x. 1 root root       54992 Oct 21  2021 '['
-rwxr-xr-x. 1 root root       30472 Apr 12  2021  ac
-rwxr-xr-x. 1 root root       25008 Oct 11  2021  aconnect
-rwxr-xr-x. 1 root root       34176 Nov 10  2021  addr2line
-rwxr-xr-x. 1 root root          29 Oct  9  2021  alias
-rwxr-xr-x. 1 root root       84112 Oct 11  2021  alsaloop
-rwxr-xr-x. 1 root root       81600 Oct 11  2021  alsamixer
-rwxr-xr-x. 1 root root         123 Jun 16  2021  alsaunmute
-rwxr-xr-x. 1 root root       25000 Oct 11  2021  amidi
-rwxr-xr-x. 1 root root       62520 Oct 11  2021  amixer
-rwxr-xr-x. 1 root root        2668 Apr 12  2021  amuFormat.sh
-rwxr-xr-x. 1 root root        2756 Sep 24  2021  anaconda-cleanup
-rwxr-xr-x. 1 root root         102 Nov  8  2018  anaconda-disable-nm-ibft-plugin
-rwxr-xr-x. 1 root root        8111 May 27  2020  analog
-rwxr-xr-x. 1 root root       82784 Oct 11  2021  aplay
-rwxr-xr-x. 1 root root       25032 Oct 11  2021  aplaymidi
.
.
.
```

### /LIB

### /usr/lib

### /usr/local/

### /usr/bin

Esta carpeta se suele montar en otro disco. Por si falla el sistema principal se podria arrancar desde aqui en cierta forma.

### usr/sbin

Sbin serían los binarios mínimos para inciar el sistema.

### /var

#### /var/log

Donde suelen estar todas las herramientas que delegan o guardan logs en el sistema. No es un requisito que los archivos de log esten en esta carpeta, pero es lo mas habitual.

--- Por ejemplo sql deja mucha info en /var/lib/mysql ---

### Comando df (disk free)

Nos muestra el espacio libre en disco

```bash
[root@formacion bin]# df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        1.9G     0  1.9G   0% /dev
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           2.0G  9.2M  2.0G   1% /run
tmpfs           2.0G     0  2.0G   0% /sys/fs/cgroup
/dev/sda1        32G  6.9G   26G  22% /
tmpfs           393M   32K  393M   1% /run/user/1000
/dev/sr0         51M   51M     0 100% /run/media/usuario/VBox_GAs_7.0.12
apuntes         477G  337G  141G  71% /mnt
[root@formacion bin]# df
Filesystem     1K-blocks      Used Available Use% Mounted on
devtmpfs         1983916         0   1983916   0% /dev
tmpfs            2011312         0   2011312   0% /dev/shm
tmpfs            2011312      9420   2001892   1% /run
tmpfs            2011312         0   2011312   0% /sys/fs/cgroup
/dev/sda1       33537028   7218772  26318256  22% /    #Parecido a C: en windows pero en UNIX todo pende de la raíz= /
tmpfs             402260        32    402228   1% /run/user/1000
/dev/sr0           52196     52196         0 100% /run/media/usuario/VBox_GAs_7.0.12
apuntes        499429892 352336760 147093132  71% /mnt
```

el df nos mostrario el espacio usado en binario

el df -h seria en formato humano

Lo que nos muestra df en principio con /dev o /run o /sys que son tmps... suelen serarchivos que no existen.

La raíz de /dev/sda1 es el disco duro que usamos real

La raíz del /mnt nos muestra los archivos compartidos.... (en este caso es un disco duro virtual) pero también nos mostraría los archivos compartidos de una red por ejemplo.

Del mensaje anterior de bash podemos ver la carpeta en el ordenador principal que se llama apuntes y que esta montada en /mnt dentro de la máquina virtual.

### Comando mount

Nos muestra los archivos montados

```bash
[root@formacion bin]# mount
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime,seclabel)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,seclabel,size=1983916k,nr_inodes=495979,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,seclabel)
.
.
.
```

El comando mount nos muestra los archivos montados en el sistema, dónde se encuentran montados, de qué tipo son y que opciones y valores tienen asignados.

### cifs

Es el controlador a través del cuál linux puede acceder a archivos compartidos de windows.

También podría utilizarse Samba para compartir archivos de linux a windows.

-- cifs-utils --

es el cliente para acceder a archivos compartidos de windows

### fat/fat32/xfat/ntsf

Son los sistemas de archivos de windows y linux puede acceder a ellos.

Buscar más información en:

https://learn.microsoft.com/es-es/troubleshoot/windows-client/backup-and-storage/file-systems

Por ejemplo con una raspberry pi normalmente el sistema de archivos es fat32

## CÓMO FUNCIONAN LOS EDITORES

Con el comando pwd me dice dónde estoy

y en etc hay muchos archivos de configuración de texto plano. por ejemplo passwd contiene los usuarios del sistema operativo.

Con el comando cat podemos visualizar el contenido de un archivo de texto plano.

Pero hay editores de texto que se pueden usar para modificar archivos de texto plano.

--- _gedit_ (editor de texto de gnome) _--no recomendado para editar archivos de configuración_
consume mas recursos porqué tiene una interfaz gráfica, alguna vez no puedes usarlo porqué no tienes interfaz gráfica. Además a veces utiliza archivos adicionales al editar un config y puede ocasionar problemas.
--- _nano_ (editor de texto de consola)
facilita el movimiento en los ficheros. Es bueno para editar archivos de configuración. Te puedes mover con las flechitas y podemso ver a bajo algunas opciones de teclado rápido.

```bash
^G Get Help     ^O Write Out    ^W Where Is     ^K Cut Text     ^J Justify	^C Cur Pos	M-U Undo
^X Exit         ^R Read File    ^\ Replace	^U Uncut Text   ^T To Spell     ^_ Go To Line   M-E Redo
```

El ^ es el control

--- vi/vim (editor de texto de consola) -- es un infierno normalmente pero es el editor por excelencia en cualquier linux.

Es muy potente y muy configurable. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente. Es el que más se usa en servidores porqué no consume recursos y es muy potente.

```bash
[root@formacion etc]# vi passwd
```

JUEGO PARA APRENDER VIM
https://vim-adventures.com/

(mínimo 2-3 días dedicados a ver vi para obtener soltura)

### Comando cp

```bash
cp /etc/passwd /etc/passwd.bak
```

(cp) (etc/passwd) (etc/passwd.bak)
comando carpeta origen carpeta destino

Sirve para copiar archivos

```bash
cp -r /etc /etc.bak # copia recursiva
```

## Usar vi/vim cómo editor de archivos

vi realmente es un alias de vim. y la ruta del ejecutable es /usr/bin/vim

```bash
[root@formacion etc]# which vi
alias vi='vim'
        /usr/bin/vim
```

para salir de vi hay que **pulsar ESC\_** y **luego _:q_**

TECLAS DE MOVIMIENTO:

**TRADICIONALES** : **HJKL** --- en este caso las flechas se usan cómo teclas de control y no de movimiento

TECLA H --- para moverse a la izquierda
TECLA J --- para moverse hacia abajo
TECLA K --- para moverse hacia arriba
TECLA L --- para moverse a la derecha

**NUEVOS**: **FLECHAS** --- en este caso también podríamos usar **HJKL**

TECLA I --- para insertar texto
TECLA O --- para insertar texto en la siguiente línea
TECLA A --- para insertar texto al final de la línea
TECLA U --- para deshacer
TECLA CTRL+R --- para rehacer
TECLA D --- para borrar
TECLA DD --- para borrar la línea entera
TECLA ZZ --- para guardar y salir
TECLA ESC --- para salir del modo de edición
TECLA $ --- para ir al final de la línea
TECLA 0 --- para ir al principio de la línea
TECLA G --- para ir al final del archivo
TECLA 1G --- para ir al principio del archivo
TECLA / --- para buscar
TECLA N --- para buscar la siguiente coincidencia
TECLA Y --- para copiar
TECLA P --- para pegar
TECLA V --- para seleccionar texto
TECLA W --- para moverse a la siguiente palabra
TECLA B --- para moverse a la palabra anterior
TECLA M --- para moverse a la mitad de la pantalla
TECLA % --- para moverse al paréntesis correspondiente
TECLA C --- para borrar y entrar en modo de edición

COMANDOS

COMANDO :wq --- para guardar y salir
COMANDO :q! --- para salir sin guardar
COMANDO :q --- para salir
COMANDO :w --- para guardar
COMANDO :

Si ecribo números antes de las teclas de movimiento, se moverá tantas veces cómo indique el número. Si no se indica número se moverá una vez.
Esto es muy útil para moverse por el archivo de forma rápida. También pasa con los comandos de borrar. Si no se indica número se borrará una vez. Si se indica número se borrará tantas veces cómo indique el número.

## NANO (editor de texto de consola)

control + W : Buscar
control + O : Guardar
Control + V : Siguiente página
control + X : Salir (si no se ha guardado, propone guardar cambios)

Control + K : Cortar línea y almacenar en buffer
Control + U : Pega el buffer cortado en el punto del cursor

## SALIDAS DE COMANDOS // REDIRECCIONES

STODUT (standard output) --- salida estándar
STDERR (standard error) --- salida de error
STDIN (standard input) --- entrada estándar

Página 77/100 del libro

Con cat la salida estándar del comando es el terminal. Coge el contenido del archivo y lo muestra en el terminal.

#### >

La salida estandar se puede redirigir a un archivo con el comando > (mayor que)
Este seria en forma de **sobreescribir** el archivo

```bash
cat /etc/passwd > /etc/passwd.bak
```

resultado:

```bash

```

#### >>

Para añadir contenido a un archivo se usa el comando >> (doble mayor que)
Este seria en forma de añadir al final del archivo **(append)**

```bash
cat /etc/passwd >> /etc/passwd.bak
```

resultado:

```bash
    [root@formacion etc]# cat /etc/passwd.bak
    root:x:0:0:root:/root:/bin/bash
    bin:x:1:1:bin:/bin:/sbin/nologin
    daemon:x:2:2:daemon:/sbin:/sbin/nologin
    adm:x:3:4:adm:/var/adm:/sbin/nologin
    lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

##### NOTAS PROFE

-- REDIRECCIONES

[usuario@formacion ~]$ echo "texto"
texto
[usuario@formacion ~]$ echo "Texto" > salidaecho
[usuario@formacion ~]$
[usuario@formacion ~]$ ls
curso Documents file1 file3 Music Pictures salidacat Templates
Desktop Downloads file2 file4 passwd Public salidaecho Videos
[usuario@formacion ~]$ cat salidaecho
Texto
[usuario@formacion ~]$ echo "Otro texto" > salidaecho
[usuario@formacion ~]$
[usuario@formacion ~]$ cat salidaecho
Otro texto
[usuario@formacion ~]$
[usuario@formacion ~]$
[usuario@formacion ~]$ echo "Otro texto mas" >> salidaecho
[usuario@formacion ~]$ cat salidaecho
Otro texto
Otro texto mas
[usuario@formacion ~]$

#### |

El comando | (pipe) sirve para redirigir la salida estándar de un comando a la entrada estándar de otro comando.

Esto sería para concatenar la salida de un comando con la entrada de otro comando.

```bash
cat /etc/passwd | grep root
```

grep es un comando que busca coincidencias en un archivo de texto plano.

```bash
[root@formacion etc]# cat /etc/passwd | grep root
root:x:0:0:root:/root:/bin/bash
```

en el caso anterior grep busca la palabra root en el archivo de texto plano /etc/passwd y sólo muestra las líneas que contienen la palabra root.

```bash
[root@formacion etc]# cat /etc/passwd | grep root | grep bash
root:x:0:0:root:/root:/bin/bash
```

en este caso grep busca la palabra root en el archivo de texto plano /etc/passwd y sólo muestra las líneas que contienen la palabra root y además busca la palabra bash en el resultado anterior y sólo muestra las líneas que contienen la palabra bash.

awk es un comando que permite filtrar la salida de un comando.

```bash
[root@formacion etc]# cat /etc/passwd | awk -F: '{print $1}'
root
bin
daemon
adm
.
.
.
```

---- ALERTA ----

No todos los programas aceptan la entrada estándar. La mayoría de programas básicos de administración si lo aceptan pero no todos. Hay en algunos casos que tienes que ponerle un modificador. -s , -i, etc. ....

Puedes concatenar y puedes crear una línea de comando para hacer cosas muy potentes.

Por ejemplo filtrar las entradas de log.

#### <

El comando < (menor que) sirve para redirigir la entrada estándar de un comando a un archivo. Se llama reverse redirect

```bash
cat < /etc/passwd
```

Muy útil con el sistema mysql

#### Comando FIND

El comando find sirve para buscar archivos en el sistema.

```bash
find / -name passwd
```

Le estamos diciendo:

busca desde la barra un fichero con el nombre passwd

-- BUSCAR FICHEROS

```bash
find / -name file4
```

-- Salen errores y ficheros encontrados no obstante estamos redirigiendo la salida estándar a un archivo que se va a crear en usuario y se va a llamar resultadobusqueda

```bash
find / -name file4 > /home/usuario/resultadobusqueda
```

-- Salen errores
-- El fichero encontrado está escrito en el fichero /home/usuario/resultadobusqueda

```bash
find / -name file4 2> /home/usuario/salidaerrores
```

-- No salen errores porqué se encuentran redirigidos mediante el comando 2> a un archivo que se va a crear en usuario y se va a llamar salidaerrores

-- Los ficheros encontrados salen por pantalla || la salida estándar

```bash
find / -name file4 > salidacorrecta 2> salidaerror
```

-- Errores al fichero
-- Los ficheros encontrados al fichero

En este caso vas capturando la información de la salida estándar y la salida de error en archivos diferentes.

##### Programas en el os que generan datos aleatorios

--- RANDOM

```bash
[root@formacion etc]# echo $RANDOM
```

--- NULL o /dev/null

```bash
[root@formacion etc]# echo "hola" > /dev/null
```

Este comando no muestra nada porqué la salida estándar se redirige a /dev/null que es un archivo que no existe y por lo tanto no muestra nada. Y a la vez destruye esta información.

```bash
[root@formacion etc]# echo "hola" > salidacorrecta 2> /dev/null
```

En el caso de las salidas de error podemos enviarlo a dev/null si no queremos generar el log de errores en el sistema. Por eso los redirigimos a dev/null para eliminarlos.

```bash
[root@formacion etc]# echo "hola" > salidacorrecta 2> /dev/null
```

##### Búsqueda de archivos con expresiones

La línea de comanndos de linux suele usar expresiones regulares de Perl.

https://www.perl.org/

**\*** --- significa cualquier cosa similar a un wildcard

```bash
find / -name "file*" #expression regular que busca cualquier archivo que empiece por file
```

**?** --- significa cualquier caracter

```bash
find / -name "file?" #expression regular que busca cualquier archivo que empiece por file y tenga un caracter más
```

**[ ]** --- significa cualquier caracter dentro de los corchetes

```bash
find / -name "file[123]"
```

Y después de generar la expressión podemos redirigir errores o salidas correctas a archivos

```bash
find / -name "file*" > salidacorrecta 2> /dev/null
```

o

```bash
find / -name "file?" 2> salidaerror
```

## MAN PAGES

The most common resource used to obtain documentation is manual pages, also referred to by the
command used to invocate them: man.

```bash
[root@rhel-instance ~]# man tar
TAR(1)                                    GNU TAR
Manual                                   TAR(1)
NAME
       tar - an archiving utility
SYNOPSIS
   Traditional usage
       tar {A|c|d|r|t|u|x}[GnSkUWOmpsMBiajJzZhPlRvwo] [ARG...]
   UNIX-style usage
       tar -A [OPTIONS] ARCHIVE ARCHIVE
       tar -c [-f ARCHIVE] [OPTIONS] [FILE...]
       tar -d [-f ARCHIVE] [OPTIONS] [FILE...]
```

#### MAN BASHBUILTINS

Si usamos man cd (por ejemplo) podemos ver los BASHBUILTINS

--- eso es debido a que cd es una función de bash y no un comando del sistema operativo por eso aparece el manual de builtins de bash ---

```bash
[usuario@formacion /]$ man cd

BASH_BUILTINS(1)                                     General Commands Manual                                    BASH_BUILTINS(1)

NAME
       bash, :, ., [, alias, bg, bind, break, builtin, caller, cd, command, compgen, complete, compopt, continue, declare, dirs,
       disown, echo, enable, eval, exec, exit, export, false, fc, fg, getopts, hash, help,  history,  jobs,  kill,  let,  local,
       logout, mapfile, popd, printf, pushd, pwd, read, readonly, return, set, shift, shopt, source, suspend, test, times, trap,
       true, type, typeset, ulimit, umask, unalias, unset, wait - bash built-in commands, see bash(1)

BASH BUILTIN COMMANDS
...
.
.
```

Hay que saber interpretar las páginas de número del manual, por ejemplo en los números del manua indican secciones:

(1) --- COMANDOS
(2) --- LLAMADAS AL SISTEMA
(3) --- LLAMADAS A LA BIBLIOTECA
(4) --- ARCHIVOS ESPECIALES
(5) --- FICHEROS DE CONFIGURACIÓN
(6) --- JUEGOS
(7) --- PAQUETES VARIOS
(8) --- COMANDOS DE ADMINISTRACIÓN

Si un elemento se encuentra en una sección del manual te muestra sólo esa sección. En cambio si el elemento se encuentra en varias secciones te muestra todas las secciones. empezando por la más cercana

```bash
       The table below shows the section numbers of the manual followed by the types of pages they contain.

       1   Executable programs or shell commands
       2   System calls (functions provided by the kernel)
       3   Library calls (functions within program libraries)
       4   Special files (usually found in /dev)
       5   File formats and conventions eg /etc/passwd
       6   Games
       7   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7)
       8   System administration commands (usually only for root)
       9   Kernel routines [Non standard]

```

## INFO PAGES

Las páginas de info són excesivamente detalladas pero igualmente pueden servir para obtener información de procesos de bash.

```bash
[usuario@formacion /]$ info cd
```

## GREP

Es un comando que se usa para buscar coincidencias en archivos de texto plano.

```bash
[root@formacion etc]# grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

En el caso anterior grep busca la palabra root en el archivo de texto plano /etc/passwd y sólo muestra las líneas que contienen la palabra root.

Pero el funcionamiento de grep va más allá.

Se puede usar grep de forma recursiva para buscar en todos los archivos de un directorio y sus subdirectorios. Coincidencia de palabras que busco.

```bash
[root@formacion etc]# grep -r root /etc
```

En el anterior caso grep busca la palabra root en el directorio /etc de forma recursiva y en todos sus subdirectorios y muestra las líneas que contienen la palabra root.

También se puede usar archivos de texto.

-- BUSCAR TEXTO EN FICHEROS

```bash
[usuario@formacion ~]$ grep -r ./* -e "Texto que busco"
./file2:Texto que busco
./file4:Texto que busco
```

En este caso anterior grep busca la palabra "Texto que busco" en todos los archivos de texto plano del directorio actual y muestra las líneas que contienen la palabra "Texto que busco".

```bash
grep -r /var/log -e "192.168.1.100" 2> /dev/null
```

```bash
[usuario@formacion ~]$ grep -r ./* -e "Texto que busco" -n > busqueda_grep
[usuario@formacion ~]$ ls
busqueda_grep  Downloads  file4     resultadobusqueda  salidaerrores
curso          file1      Music     salidacat          Templates
datos          file11     passwd    salidacorrecta     Videos
Desktop        file2      Pictures  salidaecho
Documents      file3      Public    salidaerror
[usuario@formacion ~]$ cat busqueda_grep
./datos/file2:2:Texto que busco
./datos/file2:6:Texto que busco
./datos/file2:9:Texto que busco
./file2:2:Texto que busco
./file4:3:Texto que busco
[usuario@formacion ~]$
```

En el caso anterior grep busca la palabra "Texto que busco" en todos los archivos de texto plano del directorio actual y muestra las líneas que contienen la palabra "Texto que busco" y además muestra el número de línea en el que se encuentra la coincidencia. Después redirige la salida estándar a un archivo que se va a crear en el directorio actual y se va a llamar busqueda_grep.

En la siguiente línea se busca el nuevo archivo creado y se muestra su contenido. con el cat

```bash
[usuario@formacion ~]$ grep -r ./* -e "Texto que busco" -c
./busqueda_grep:5
./datos/file2:3
./Documents/RED_HAT_ENTERPRISE_LINUX_9_ADMINISTRATION.pdf:0
./file1:0
./file11:0
./file2:1
./file3:0
./file4:1
./passwd:0
./resultadobusqueda:0
./salidacat:0
./salidacorrecta:0
./salidaecho:0
./salidaerror:0
./salidaerrores:0
```

El -c nos muestra el número de coincidencias que ha encontrado grep en cada archivo.

## MORE / LESS

-- Facilitan el cat para textos grandes y verlo de forma interactiva

```bash
man grep > texto_grep
```

```bash
cat texto_grep | more
```

```bash
more texto_grep
```

```bash
cat texto_grep | less
```

```bash
less texto_grep
```

**More** es una forma de moverse en los textos grandes cómo por ejemplo en los manuales en txt.

**Less** es una forma de moverse en los textos grandes cómo por ejemplo en los manuales en txt. (Suele tener más funcionalidades que more)

Otra forma sería con comando:

**/texto a buscar**

**:n ---** para ir a la siguiente coincidencia

## HEAD

Nos muestra las primeras líneas de un archivo de texto plano.
El head serían las 10 primeras líneas.

```bash
[root@formacion etc]# head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
.
.
```

Para mostrar las primeras 5 líneas

```bash
[root@formacion etc]# head -n 5 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

## TAIL

Nos muestra las últimas líneas de un archivo de texto plano.
El tail serían las 10 últimas líneas.

```bash
[root@formacion etc]# tail /etc/passwd
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
.
.
.
```

Para mostrar las últimas 3 líneas

```bash
[root@formacion etc]# tail -n 3 /etc/passwd
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
```

**TIENE MUCHA UTILIDAD PARA VER LOGS**

```bash
[usuario@formacion ~]$ tail -f file5
texto1
texto2
texto3
texto4



[root@formacion ~]# tail -f /var/log/secure
```

## TEE

man tee

Tee es un comando que nos permite redirigir la salida estándar a un archivo y a la vez mostrarla por pantalla.

```bash
[root@formacion etc]# cat /etc/passwd | tee /etc/passwd.bak
```

## Comando SED

El comando sed sirve para modificar archivos de texto plano.

```bash
[root@formacion etc]# sed -i 's/root/usuario/g' /etc/passwd
```

En el caso anterior sed busca la palabra root en el archivo de texto plano /etc/passwd y la sustituye por la palabra usuario. La g al final indica que se sustituirán todas las coincidencias de la palabra root por la palabra usuario.

Esto es muy útil para modificar archivos de configuración o usando junto al comando find o comando grep.

```bash
[root@formacion etc]# find / -name passwd | xargs sed -i 's/root/usuario/g'
```

En el caso anterior se busca el archivo passwd en todo el sistema y se usa el comando sed para sustituir la palabra root por la palabra usuario en todos los archivos passwd del sistema.

## Comando AWK O GAWK

El comando awk sirve para filtrar la salida de un comando.

```bash
[root@formacion etc]# cat /etc/passwd | awk -F: '{print $1}'
```

En el caso anterior lee el archivo de texto plano /etc/passwd y muestra la primera columna de cada línea. La primera columna es el nombre de usuario. mediante el comando awk y el separador : (dos puntos) y la opción -F luego se dice que se muestra la primera columna de cada línea a través del comando print y la opción $1.

$1 --- primera columna
$2 --- segunda columna
$3 --- tercera columna
$4 --- cuarta columna

Es un comando muy potente y muy utilizado en administración de sistemas. Se puede usar para filtrar la salida de un comando y mostrar sólo la información que nos interesa.

El awk es un lengüaje de programación que se puede usar para filtrar la salida de un comando.

## TAR

El comando tar sirve para comprimir y descomprimir archivos.

También nos permite crear archivos de backup.

```bash

```

#### CONTINUAR MANUAL DESDE PÁGINA:

80/103
