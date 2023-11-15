# Clase 5

(Se entró a la clase 30 min tarde)

## Hacer los discos Permanentes

Probar de hacer una edición al fstab pero esto no siempre es lo más recomendable.

En discos SATA puede no dar problemas pero en otros protocolos de montaje si que puede ser peligroso.

## Comandos

#### lsblk

Nos muestra los distintso discos.

```bash
[root@formacion dev]# tldr lsblk

  lsblk

  Lists information about devices.
  More information: https://manned.org/lsblk.

  - List all storage devices in a tree-like format:
    lsblk

  - Also list empty devices:
    lsblk -a

  - Print the SIZE column in bytes rather than in a human-readable format:
    lsblk -b

  - Output info about filesystems:
    lsblk -f

  - Use ASCII characters for tree formatting:
    lsblk -i

  - Output info about block-device topology:
    lsblk -t

  - Exclude the devices specified by the comma-separated list of major device numbers:
    lsblk -e 1,7

  - Display a customized summary using a comma-separated list of columns:
    lsblk --output NAME,SERIAL,MODEL,TRAN,TYPE,SIZE,FSTYPE,MOUNTPOINT
```

Comandos usados:

#### blkid

En el fstab es mejor usar el UUID así les va a preguntar a los dispositivos el blkid del disco y va a montarlos cada inicio en el sitio que le toca y con el nombre que le toca.

sda1 cómo sda1

sdb cómo sdb

```bash
[root@formacion dev]# tldr blkid

  blkid

  Lists all recognized partitions and their Universally Unique Identifier (UUID).
  More information: https://manned.org/blkid.

  - List all partitions:
    sudo blkid

  - List all partitions in a table, including current mountpoints:
    sudo blkid -o list

```

#### Si no se trebaja con entrono gráfico

```bash
[root@formacion dev]# blkid /dev/sdc1 >> /etc/fstab
```

Este comando nos va a dar el UUID del disco y lo va a añadir al fstab.

## Máquina virtual de vbox (instantaneas)

Tomar instantaneas

![Alt text](image.png)

En la carpeta snapshots se van a crear los archivos de las instantaneas. (replicando los discos que conforman la máquina virtual)

### Modo de emergencia

You are in emergency mode. Sin entorno grafico.

![Alt text](image-1.png)

Le das la contraseña del root y te da una línea de comandos.

usamos df -h para ver lo que hay montado.

En /var/log podemos meternos a ver los mensages con un cat messages y nos damos cuenta de que nos ha montado un disco que siempre monta. Por lo que vamos a df -h y vemos que los discos normales no los monta.

El problema está en el fstab.

Ahora tenemos que recordar cómo y qué se monta en el datos. Por lo que vamos a usar el comando

lsblk -f

Para ver si los sistemas de archivos están bien. y los uuid coinciden con los del fstab.

## Montaje permanente de otro disico

```bash

[root@formacion ~]# blkid /dev/sdc2
/dev/sdc2: UUID="1c39e72d-d1c6-41f3-b5f4-8c292eafe538" BLOCK_SIZE="512" TYPE="xfs" PARTUUID="b229a37d-02"
[root@formacion ~]# nano /etc/fstab
[root@formacion etc]# cat fstab

#
# /etc/fstab
# Created by anaconda on Sun Mar 13 20:35:22 2022
#
# Accessible filesystems, by reference, are maintained under '/dev/disk/'.
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
#
# After editing this file, run 'systemctl daemon-reload' to update systemd
# units generated from this file.
#
UUID=6a464459-ea7f-4533-bfd7-a1aacd302170 /                       xfs     defaults        0 0
UUID=af791686-6373-4e41-a9de-3afd3e7148db none swap defaults 0 0
UUID=6a4960b9-4da1-4ad2-861e-06a785a28c59 /datos1 ext4 defaults 0 0
UUID=1c39e72d-d1c6-41f3-b5f4-8c292eafe538 /datos2 xfs defaults 0 0

[root@formacion ~]# df -h |grep datos
/dev/sdc1       7.9G   36M  7.4G   1% /datos1
[root@formacion ~]# mount /datos2
[root@formacion ~]# df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        1.9G     0  1.9G   0% /dev
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           2.0G  9.3M  2.0G   1% /run
tmpfs           2.0G     0  2.0G   0% /sys/fs/cgroup
/dev/sda1        32G  7.0G   26G  22% /
/dev/sdc1       7.9G   36M  7.4G   1% /datos1
tmpfs           393M   24K  393M   1% /run/user/1000
/dev/sr0         51M   51M     0 100% /run/media/usuario/VBox_GAs_7.0.12
/dev/sdc2       4.0G   61M  4.0G   2% /datos2
[root@formacion ~]# df -h |grep /datos
/dev/sdc1       7.9G   36M  7.4G   1% /datos1
/dev/sdc2       4.0G   61M  4.0G   2% /datos2
```

### Llevarnos un directorio de disco y montarlo en otro

Desde el home puede salir más o menos bien

Desde el usr puede tener más problemas y nos podemos cargar el sistema.

Moveremos home.

Mover /home a una partición. Otra carpeta útil de mover es opt que es donde se instalan los programas. También es útil mover /var que es donde se guardan los logs.

##### A continuación se hace la demostración de mover home a una partición

Al hacer eesta acción si los usuarios están logueados no se va a poder hacer o si se puede hacer se van a generar muchos errores.

Los ususarios se conectan al inodo, por lo tanto si tu cambias el inodo al hacer esta acción se van a generar muchos errores y afectación a los usuarios.

1 . Crear el sistema de archivos para el nuevo home

fdisk ---- creando /dev/sdc5

2. Dar formato a la partición

mkfs.xfs /dev/sdc5

3. Carpeta para montar el futuro home

mkdir /home2

_esta carpeta la creamos en la / del root_

_Lo estamos creando realmente en la / del sda1. si montamos el home2 los datos del home inicial no se van a poder acceder aunque no se va a perder la información_

4. Copia de home a home2

_Nos tenemos que asegurar que todo vaya a copiarse igual. Permisos, vinculos simbolico, vinculo duro, etc_ --- investigarlo con anterioridad a la copia

cp -raf /home/\* /home2

5. Comparar home con home2

du -csh /home (cuánto ocupa home)
du -csh /home2 (cuánto ocupa home2)

si los datos son iguales podemos seguir adelante.

ls -lah /home2

Para poder ver los archivos que contiene. SI són los mismos podemos seguir adelante.

Podemos incluso usar : tree

6. Cambio de /home a /home3 y /home2 a /home

_Esto se hace para poder mantener el home original por si algo falla mientras solucionamos los problemas_

mv /home /home3

umount /home2
mkdir /home
mount /dev/sdc5 /home

7. Probamos si está funcionando

Accedemos a un usuario

[root@formacion ~]# su - usuario

y entramos en el home del usuario

(escribimos en un archvio de megas)

Y comporbamos con df -h SI SE ESTA ESCRIBIENDO EN EL DISCO asociado al /home

8. Cambiamos el archivo fstab con el blkid del disco que montamos en el /home

Hacemos un

blkid /dev/sdc5

y luego modificamos el fstab

vi /etc/fstab
nano /etc/fstab

Copiamos el UUID y asignamos los valores necesarios en el fstab

![Alt text](image-3.png)

8.1 Cambio definitivo

Un reboot

### si la liamos y no podemos iniciar sesión

ctrl + alt + f2 ---- inicia un terminal y nos podmos conectar cómo root

![Alt text](image-2.png)

En el vi fstab // nano fstab

![Alt text](image-3.png)

![Alt text](image-4.png)

Y luego montar el /home en los comandos

mount /home

9. Luego ya podemos borrar el /home3 (datos antiguos que se encuentran en el disco sda1)

df -h | grep sda1

## Practica

\*\* No existe /datos4 sino que es /datos3

![Alt text](image-5.png)

## LVM

(Aparece en el libro)
