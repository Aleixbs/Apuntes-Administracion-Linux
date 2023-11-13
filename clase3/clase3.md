# CLASE 3 DE LINUX

#### HOY VEREMOS LOS COMANDOS BÁSICOS Y Gestion de usuarios.

-HEAD
-TAIL
-TEE
-SED

Si no hay dns pues los hosts se guardan en etc(hosts)

Hoy vamos a ver algunos comandos un poco más avanzados.

Y gestión de usuarios.

(Página 137/160)

En todo Linux el tema de usuarios són en los mismos ficheros.

## Gestión de usuarios

En etc/passwd tenemos la lista de usuarios

cat /etc/passwd

el usuario 0 es el root

!! El usuario root es el necesrio para modificar el archivo /etc/passwd

Antes la contraseña se encontraba en el fichero /etc/passwd pero ahora se encuentra en /etc/shadow. Y en su lugar en el ficher /etc/passwd se encuentra una x.

El terminal de usuario y cuando se hace un login se pone en home/usuario. Puedes cambiar la ubicación en el archivo para cambiar la carpeta en que se inicia el usuario. Luego cuándo este usuario se loggee va a entrear en el campo de carpeta.

Si quiere que el usuario no inicie sesión meter

:/sbin/nologin

```bash
usuario:x:1000:1000:usuario:/home/usuario:/bin/bash
```

Cambiar el directorio de inicio de sesión de un usuario

- Entrar en modo edición de texto en el archivo /etc/passwd y cambiar la carepta /home/usuario por la carpeta destino deseada.

```bash
usuario:x:1000:1000:usuario:/home/usuario2:/bin/bash
```

Hacer que el usuario no inicie sesión:

Cambiar el método /bin/bash por /sbin/nologin

```bash
usuario:x:1000:1000:usuario:/home/usuario:/sbin/nologin
```

El método su permite iniciar sesión como otro usuario.

```bash
su usuario
```

Al usar este comando se te pedirá la contraseña del usuario al que quieres acceder.

Podemos instalar una aplicación para manejar los terminales.

En este caso vamos a instalar terminator:

```bash
[usuario@formacion ~]$ su -
Password:
[root@formacion ~]# yum install terminator
```

/etc/group

Grupos del usuario.

```bash
cat /etc/group
```

```bash
usuario:x:1000:
```

#### Grupo wheel

El usuario que es del grupo wheel puede hacer sudo.

```bash
[root@formacion ~]# cat /etc/group | grep wheel
wheel:x:10:root,usuario
```

Y tiene permisos casi de administración total.

Puede incluso cambiar la contraseña del root.

Lo más recomendado es usar una cuenta en el grupo wheel y usar sudos para hacer las tareas de administración de un entorno Linux. E intentar usar el root lo menos posible y usar usuarios sin privilegios

Para ello debemos meter el usuario en el grupo wheel.

```bash
[root@formacion ~]# usermod -aG wheel usuario
```

o cómo nos muestran en el curso:

```bash
[root@formacion ~]# vi /etc/group
```

```bash
wheel:x:10:usuario
```

### Almacenaje de constraseñas de usuarios

/etc/shadow

```bash
cat /etc/shadow
```

En el archivo /etc/shadow se almacenan las contraseñas de los usuarios.

Allí es dónde se pueden administrar las contraseñas de estos.

El algoritmo de encriptación de las contraseñas es el MD5. Y normalmente se usa un seed y dentro del archivo se guarda el seed y la contraseña encriptada.

Ek MD5 no es muy seguro ya que por fuerza bruta ses puede conseguir el psswd

El que normalmente se usa es el SHA-512 identificado por $6$

### /etc/login.defs

Hay distintos modos cómo UMASK, HOME_MODE, etc.

En este archivo es donde hay los comandos para configurar los usuarios.

Estos comandos se pueden cambiar para que se apliquen a todos los usuarios.

### /etc/skel

En la carpeta skel hay varios archivos.

Estos archivos son los que se copian en la carpeta de un usuario cuando se crea.

Por ejemplo el .bashrc
lo lee siempre al crear una nueva sesión

```bash
[root@formacion ~]# cd /etc/skel
[root@formacion skel]# ls -lah
total 24K
drwxr-xr-x.   3 root root   78 Mar 13  2022 .
drwxr-xr-x. 145 root root 8.0K Nov 13 15:48 ..
-rw-r--r--.   1 root root   18 Jul 27  2021 .bash_logout
-rw-r--r--.   1 root root  141 Jul 27  2021 .bash_profile
-rw-r--r--.   1 root root  376 Jul 27  2021 .bashrc
drwxr-xr-x.   4 root root   39 Mar 13  2022 .mozilla
```

Podemos modificar estos archivos para que se apliquen a todos los usuarios cuándo se creen o se modifiquen.

También en el skel se puede crear un archivo de bienvenida.

Por ejemplo:

Crear un nuevo archvo:

```bash
[root@formacion skel]# vi .bash_welcome
```

```bash
[root@formacion skel]# echo "Bienvenido a la formación de Linux" > .bash_welcome
```

```bash
[root@formacion skel]# cat .bash_welcome
```

/// Esta muy bien explicado en el libro:::

### /etc/defaults/

### Crear un nuevo usuario

```bash
[root@formacion skel]# useradd usuario2
```

en /etc/group

```bash
u1:x:5000:
```

Aparece con el cambio de grupos que hemos hecho en el login.defs

```bash
[root@formacion ~]# cat /etc/login.defs
#
# Please note that the parameters in this configuration file control the
# behavior of the tools from the shadow-utils component. None of these
# tools uses the PAM mechanism, and the utilities that use PAM (such as the
# passwd command) should therefore be configured elsewhere. Refer to
# /etc/pam.d/system-auth for more information.
#

# *REQUIRED*
#   Directory where mailboxes reside, _or_ name of file, relative to the
#   home directory.  If you _do_ define both, MAIL_DIR takes precedence.
#   QMAIL_DIR is for Qmail
#
#QMAIL_DIR	Maildir
MAIL_DIR	/var/spool/mail
#MAIL_FILE	.mail

# Default initial "umask" value used by login(1) on non-PAM enabled systems.
# Default "umask" value for pam_umask(8) on PAM enabled systems.
# UMASK is also used by useradd(8) and newusers(8) to set the mode for new
# home directories if HOME_MODE is not set.
# 022 is the default value, but 027, or even 077, could be considered
# for increased privacy. There is no One True Answer here: each sysadmin
# must make up their mind.
UMASK		022

# HOME_MODE is used by useradd(8) and newusers(8) to set the mode for new
# home directories.
# If HOME_MODE is not set, the value of UMASK is used to create the mode.
HOME_MODE	0700

# Password aging controls:
#
#	PASS_MAX_DAYS	Maximum number of days a password may be used.
#	PASS_MIN_DAYS	Minimum number of days allowed between password changes.
#	PASS_MIN_LEN	Minimum acceptable password length.
#	PASS_WARN_AGE	Number of days warning given before a password expires.
#
PASS_MAX_DAYS	99999
PASS_MIN_DAYS	0
PASS_MIN_LEN	5
PASS_WARN_AGE	7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN                  5000
UID_MAX                 60000
# System accounts
SYS_UID_MIN               201
SYS_UID_MAX               999

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN                  5000
GID_MAX                 60000
# System accounts
SYS_GID_MIN               201
SYS_GID_MAX               999

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD	/usr/sbin/userdel_local

#
# If useradd should create home directories for users by default
# On RH systems, we do. This option is overridden with the -m flag on
# useradd command line.
#
CREATE_HOME	yes

# This enables userdel to remove user groups if no members exist.
#
USERGROUPS_ENAB yes

# Use SHA512 to encrypt password.
ENCRYPT_METHOD SHA512
```

en /etc/shadow
el usuario no tiene contraseña

```bash
u1:!!:19674:0:99999:7:::
```

#### Cómo le damos una contraseña al usuario?

```bash
[root@formacion ~]# passwd usuario2
Changing password for user usuario2.
New password:
BAD PASSWORD: The password fails the dictionary check - it is based on a dictionary word
Retype new password:
passwd: all authentication tokens updated successfully.
```

Podemos ver cómo en el usuario : u1 también se le ha creado un home con todos los archivos del skel.:

```bash
[root@formacion home]# ll
total 4
drwx------.  3 u1      u1        78 Nov 13 16:02 u1
drwx------. 15 usuario usuario 4096 Nov 13 15:39 usuario
```

```bash
[root@formacion home]# cd u1
[root@formacion u1]# ls -lah
total 12K
drwx------. 3 u1   u1    78 Nov 13 16:02 .
drwxr-xr-x. 4 root root  31 Nov 13 16:02 ..
-rw-r--r--. 1 u1   u1    18 Jul 27  2021 .bash_logout
-rw-r--r--. 1 u1   u1   141 Jul 27  2021 .bash_profile
-rw-r--r--. 1 u1   u1   376 Jul 27  2021 .bashrc
drwxr-xr-x. 4 u1   u1    39 Mar 13  2022 .mozilla
```

Sin contraseña no se puede autenticar el usuario. Por lo que no se puede loggear.

El siguiente paso es crear la constraseña:

```bash
[root@formacion u1]# passwd u1
Changing password for user u1.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
[root@formacion u1]#
```

En este caso las directivas són saltadas sólo si el root lo desea. Pero los otros usuarios deben seguir las directivas

En el archivo .bashrc se puede establecer variables de entorno.

```bash
[root@formacion u1]# cat .bashrc
# .bashrc
export PS1="\u@\h:\w\$ "
```

Luego al leer la variable de entorno se puede ver el usuario y el host.

```bash
[root@formacion u1]# echo $PS1
\u@\h:\w\$
```

## Let’s check the new user with the id command we learned before:

[root@rhel-instance ~]# id user01
uid=1001(user01) gid=1001(user01) groups=1001(user01)
After the steps taken in this section, we now have the user in the system and ready to be used. The
main options we could have used to customize the user creation with useradd are the following:
• -u or --uid: Assign a specific UID to the user.
• -g or --gid: Assign a main group to the user. It can be specified by number (GID) or by
name. The group needs to be created first.
• -G or --groups: Make the user part of other groups by providing a comma-separated list
of them.
• -c or --comment: Provide a description for the user, specified between quotes if you want
to use spaces.
• -d or --home-dir: Define the home directory for the user.
• -s or --shell: Assign a custom shell to the user.
• -p or --password: A way to provide a password to the user. The password should be already
encrypted to use this method. It is not recommended to use this option, as there are ways to
capture the encrypted password. Please use passwd instead.
• -r or --system: To create a system account instead of a user account.

## What if we need to change any of the user’s properties, such as, for example, the description?

The tool for that is usermod.

Let’s modify the description to user01:
[root@rhel-instance ~]# usermod -c "User 01" user01
[root@rhel-instance ~]# grep user01 /etc/passwd
user01:x:1001:1001:User 01:/home/user01:/bin/bash
The usermod command uses the same options as useradd. It will be easy to customize your
current users now

Let’s create user02 as an example of how to use the options:

[root@rhel-instance ~]# useradd --uid 1002 --groups wheel \
--comment "User 02" --home-dir /home/user02 \
--shell /bin/bash user02
[root@rhel-instance ~]# grep user02 /etc/passwd
user02:x:1002:1002:User 02:/home/user02:/bin/bash
[root@rhel-instance ~]# id user02
uid=1002(user02) gid=1002(user02) groups=1002(user02),10(wheel)

ver números de UID y GID en el ls\_

ls -lanh

![Alt text](image.png)
