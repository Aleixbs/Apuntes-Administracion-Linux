# Clase 6

(perdí los primeros 53 min por presentación + comunicación equipo)

--- Recuperar tema desde el libro.

(200página) --- bastante bien explicado.

El verdadero comando es dnf-3 (yum y otros comandos de instalación son alias de dnf-3)

YUM -
DNF -

```bash
# Rocky-BaseOS.repo
#
# The mirrorlist system uses the connecting IP address of the client and the
# update status of each mirror to pick current mirrors that are geographically
# close to the client.  You should use this for Rocky updates unless you are
# manually picking other mirrors.
#
# If the mirrorlist does not work for you, you can try the commented out
# baseurl line instead.

[baseos]
name=Rocky Linux $releasever - BaseOS
mirrorlist=https://mirrors.rockylinux.org/mirrorlist?arch=$basearch&repo=BaseOS-$releasever
#baseurl=http://dl.rockylinux.org/$contentdir/$releasever/BaseOS/$basearch/os/
gpgcheck=1
enabled=1
countme=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-rockyofficial

```

````bash


```bash
[root@formacion yum.repos.d]# nano Rocky-BaseOS.repo
[root@formacion yum.repos.d]# dnf-3 repolist --all
repo id                        repo name                                                            status
appstream                      Rocky Linux 8 - AppStream                                            enabled
appstream-debug                Rocky Linux 8 - AppStream - Source                                   disabled
appstream-source               Rocky Linux 8 - AppStream - Source                                   disabled
baseos                         Rocky Linux 8 - BaseOS                                               enabled
baseos-debug                   Rocky Linux 8 - BaseOS - Source                                      disabled
baseos-source                  Rocky Linux 8 - BaseOS - Source                                      disabled
devel                          Rocky Linux 8 - Devel WARNING! FOR BUILDROOT AND KOJI USE            disabled
epel                           Extra Packages for Enterprise Linux 8 - x86_64                       enabled
epel-debuginfo                 Extra Packages for Enterprise Linux 8 - x86_64 - Debug               disabled
epel-modular                   Extra Packages for Enterprise Linux Modular 8 - x86_64               enabled
epel-modular-debuginfo         Extra Packages for Enterprise Linux Modular 8 - x86_64 - Debug       disabled
epel-modular-source            Extra Packages for Enterprise Linux Modular 8 - x86_64 - Source      disabled
epel-playground                Extra Packages for Enterprise Linux 8 - Playground - x86_64          disabled
epel-playground-debuginfo      Extra Packages for Enterprise Linux 8 - Playground - x86_64 - Debug  disabled
epel-playground-source         Extra Packages for Enterprise Linux 8 - Playground - x86_64 - Source disabled
epel-source                    Extra Packages for Enterprise Linux 8 - x86_64 - Source              disabled
epel-testing                   Extra Packages for Enterprise Linux 8 - Testing - x86_64             disabled
epel-testing-debuginfo         Extra Packages for Enterprise Linux 8 - Testing - x86_64 - Debug     disabled
epel-testing-modular           Extra Packages for Enterprise Linux Modular 8 - Testing - x86_64     disabled
epel-testing-modular-debuginfo Extra Packages for Enterprise Linux Modular 8 - Testing - x86_64 - D disabled
epel-testing-modular-source    Extra Packages for Enterprise Linux Modular 8 - Testing - x86_64 - S disabled
epel-testing-source            Extra Packages for Enterprise Linux 8 - Testing - x86_64 - Source    disabled
extras                         Rocky Linux 8 - Extras                                               enabled
ha                             Rocky Linux 8 - HighAvailability                                     disabled
ha-debug                       Rocky Linux 8 - High Availability - Source                           disabled
ha-source                      Rocky Linux 8 - High Availability - Source                           disabled
media-appstream                Rocky Linux 8 - Media - AppStream                                    disabled
media-baseos                   Rocky Linux 8 - Media - BaseOS                                       disabled
nfv                            Rocky Linux 8 - NFV                                                  disabled
plus                           Rocky Linux 8 - Plus                                                 disabled
powertools                     Rocky Linux 8 - PowerTools                                           disabled
powertools-debug               Rocky Linux 8 - PowerTools - Source                                  disabled
powertools-source              Rocky Linux 8 - PowerTools - Source                                  disabled
resilient-storage              Rocky Linux 8 - ResilientStorage                                     disabled
resilient-storage-debug        Rocky Linux 8 - Resilient Storage - Source                           disabled
resilient-storage-source       Rocky Linux 8 - Resilient Storage - Source                           disabled
rt
````

Para instalar los packages de epel (extra packages for enterprise linux) se usa el comando dnf-3

No se descarga software se descarga ficheros y claves.

### EPEL

```bash
yum install epel-release
```

Arquitectura con un máquina que sirva de repositorio de paquetes desde dónde se leen estos paquetes desde todas las otras máquinas de la red linux.

De esta forma sólo se saldría a internet con esta máquina específicamente.

### Instalar screen

```bash
[root@formacion yum.repos.d]# dnf-3 install screen
Last metadata expiration check: 23:42:49 ago on Wed 15 Nov 2023 04:31:04 PM CET.
Dependencies resolved.
======================================================================================================================
 Package                   Architecture              Version                            Repository               Size
======================================================================================================================
Installing:
 screen                    x86_64                    4.6.2-12.el8                       epel                    581 k

Transaction Summary
======================================================================================================================
Install  1 Package

Total download size: 581 k
Installed size: 955 k
Is this ok [y/N]: y
Downloading Packages:
screen-4.6.2-12.el8.x86_64.rpm                                                        3.3 MB/s | 581 kB     00:00
----------------------------------------------------------------------------------------------------------------------
Total                                                                                 1.2 MB/s | 581 kB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                              1/1
  Running scriptlet: screen-4.6.2-12.el8.x86_64                                                                   1/1
  Installing       : screen-4.6.2-12.el8.x86_64                                                                   1/1
  Running scriptlet: screen-4.6.2-12.el8.x86_64                                                                   1/1
  Verifying        : screen-4.6.2-12.el8.x86_64                                                                   1/1

Installed:
  screen-4.6.2-12.el8.x86_64

Complete!

```

### Screen

screen se encuentra dentro de los repositorios de epel.

Esto en un enotrno conectado a internet. En un entorno desconectado este paquete no se podría instalar. Sino que se tendría que meter con un cd o con un drive usb y luego referencia el ehecutable en la ruta del .exe.

Con la instalación de los repos que hemos instalado anteriormente y los hemos puesto cómo enabled y tenemos activos, se puede instalar screen.

```bash
[root@formacion yum.repos.d]# tldr screen

  screen

  Hold a session open on a remote server. Manage multiple windows with a single SSH connection.
  See also `tmux` and `zellij`.
  More information: https://manned.org/screen.

  - Start a new screen session:
    screen

  - Start a new named screen session:
    screen -S session_name

  - Start a new daemon and log the output to `screenlog.x`:
    screen -dmLS session_name command

  - Show open screen sessions:
    screen -ls

  - Reattach to an open screen:
    screen -r session_name

  - Detach from inside a screen:
    Ctrl + A, D

  - Kill the current screen session:
    Ctrl + A, K

  - Kill a detached screen:
    screen -X -S session_name quit
```

### yum list

Nos lista los repositorios activos.

### dnf-3 update

Este comando sirve para actualizar los paquetes que tenemos instalados en el sistema y en los que aparecen nuevas versiones.

La actualización de estos paquetes dependerá de las política de actualización de la empresa.

### dnf-3 groupinstall

Instala un grupo de paquetes interrelacionados.

### Instalacion de ficheros rpm // tar.gz

Nos podemos hacer un:

wget urldelfichero

```bash
[root@formacion ~]# cd
[root@formacion ~]# wget http://baseinfo.es/cursos/23023_linux/repo/jdk-8u151-linux-x64.rpm
--2023-11-16 16:31:38--  http://baseinfo.es/cursos/23023_linux/repo/jdk-8u151-linux-x64.rpm
Resolving baseinfo.es (baseinfo.es)... 79.117.12.198
Connecting to baseinfo.es (baseinfo.es)|79.117.12.198|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 174163338 (166M) [application/x-rpm]
Saving to: ‘jdk-8u151-linux-x64.rpm’

jdk-8u151-linux-x64. 100%[===================>] 166.09M  17.1MB/s    in 10s

2023-11-16 16:31:48 (16.6 MB/s) - ‘jdk-8u151-linux-x64.rpm’ saved [174163338/174163338]

[root@formacion ~]# wget http://baseinfo.es/cursos/23023_linux/repo/jdk-8u201-linux-x64.tar.gz
--2023-11-16 16:32:01--  http://baseinfo.es/cursos/23023_linux/repo/jdk-8u201-linux-x64.tar.gz
Resolving baseinfo.es (baseinfo.es)... 79.117.12.198
Connecting to baseinfo.es (baseinfo.es)|79.117.12.198|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 191817140 (183M) [application/x-gzip]
Saving to: ‘jdk-8u201-linux-x64.tar.gz’

jdk-8u201-linux-x64. 100%[===================>] 182.93M  17.6MB/s    in 11s

2023-11-16 16:32:12 (17.3 MB/s) - ‘jdk-8u201-linux-x64.tar.gz’ saved [191817140/191817140]

```

el fichero rpm es para las instalaciones de paquetes rpm.

Una vez instalado el nuevo java se puede entrar en opt y cambiar el vínculo simbolico al ejecutable de Java instaldado con el rpm o el tar.gz.

Se tiene que entrar en /opt

rm jdk

y luego ln -s /usr/java/jdk1.8.0_151 jdk

En alternatives/java puede dar alternativas mmás modernas a la versión de java que tenemos instalada. Sin que el usuario tenga que cambiar ninguna variable de entorno ni nada.
