# CLASE 4

install tldr

Para tener un resumen de los comandos menos extenso que man

```bash
[root@formacion ~]# yum install tldr
```

ejemplo de uso

```bash
[root@formacion ~]# tldr ls
```

## mkdir

De base te va a crear un directorio en el directorio actual

```bash
[root@formacion ~]# mkdir directorio
```

Con el -p el mkdir si tu le pones una ruta que no existe te la crea

```bash
[root@formacion ~]# mkdir -p directorio1/directorio2/directorio3
```

```bash
[usuario@formacion home]$ tldr mkdir

  mkdir

  Create directories and set their permissions.
  More information: https://www.gnu.org/software/coreutils/mkdir.

  - Create specific directories:
    mkdir path/to/directory1 path/to/directory2 ...

  - Create specific directories and their [p]arents if needed:
    mkdir -p path/to/directory1 path/to/directory2 ...

  - Create directories with specific permissions:
    mkdir -m rwxrw-r-- path/to/directory1 path/to/directory2 ...
```

hay más si seguimos el link o usamos `man mkdir`

Si encuentro algo y hay un symbolic-link pues sigue el vinculo simbolico que se encuentra establecido

## CP

Copiar

```bash
[usuario@formacion home]$ tldr cp

  cp

  Copy files and directories.
  More information: https://www.gnu.org/software/coreutils/cp.

  - Copy a file to another location:
    cp path/to/source_file.ext path/to/target_file.ext

  - Copy a file into another directory, keeping the filename:
    cp path/to/source_file.ext path/to/target_parent_directory

  - Recursively copy a directory's contents to another location (if the destination exists, the directory is copied inside it):
    cp -r path/to/source_directory path/to/target_directory

  - Copy a directory recursively, in verbose mode (shows files as they are copied):
    cp -vr path/to/source_directory path/to/target_directory

  - Copy multiple files at once to a directory:
    cp -t path/to/destination_directory path/to/file1 path/to/file2 ...

  - Copy text files to another location, in interactive mode (prompts user before overwriting):
    cp -i *.txt path/to/target_directory

  - Follow symbolic links before copying:
    cp -L link path/to/target_directory

  - Use the full path of source files, creating any missing intermediate directories when copying:
    cp --parents source/path/to/file path/to/target_file
```

Con tar o con gzip también permite cómo cp que se pueda almacenar los archivos y los permisos adecuados para cada uno de los archivos copiados.

El cp se puede usar también de forma recursiva:

```bash
[root@formacion ~]# cp -r /etc/ ./
```

En este caso se copiaria la propia carpeta y todos los archivos.

Colocando el asterisco después de instanciar la carpeta que queremos copiar, copiaremos todos los archivos que se encuentran dentro de la carpeta. Pero no la carpeta.

```bash
[root@formacion ~]# cp -r /etc/* ./
```

Al copiar los vínculos símbolico con una definición absoluta, se recibe la copia al archivo al que apunta el vínculo.

[vínculosimbolico] -> <span style="color:blue;">/etc/authselect/nsswitch.conf</span>

Al copiar los vínculos símbolicos con una definición relativa, normalmente reciben errores.

Por ejemplo si el vinculo:

[vinculosimbolico] -> <span style="color:red;">..usr/share/doc/HTML/index.html</span>

No puedes ir una carpeta hacia atras y no encontraras los mismos archivos
