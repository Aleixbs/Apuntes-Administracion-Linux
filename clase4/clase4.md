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
    cp -r path/to/source_directory path/to/target_directory (./ is the current directory)

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

Copiar tanto archivos ocultos cómo visibles con -ra

```bash
[root@formacion ~]# cp -ra /etc/* ./
```

Copiar con el punto al final, copia el contenido de la carpeta pero no la carpeta. Con archivos ocultos y visibles de una forma segura.

```bash
[root@formacion ~]# cp -raf /etc/. ./
```

Al copiar los vínculos símbolico con una definición absoluta, se recibe la copia al archivo al que apunta el vínculo.

[vínculosimbolico] -> <span style="color:blue;">/etc/authselect/nsswitch.conf</span>

Al copiar los vínculos símbolicos con una definición relativa, normalmente reciben errores.

Por ejemplo si el vinculo:

[vinculosimbolico] -> <span style="color:red;">..usr/share/doc/HTML/index.html</span>

Generalmente al hacer una copia de un archivo a otra carpeta, no puedes ir una carpeta hacia atras y encontraras los mismos archivos y directorios. A menos que hagas esta copia del vínculo relativo a la misma altura de la carpeta o el archivo al que se copia.

## tree

```bash
[usuario@formacion home]$ tldr tree

  tree

  Show the contents of the current directory as a tree.
  More information: http://mama.indstate.edu/users/ice/tree/.

  - Print files and directories up to 'num' levels of depth (where 1 means the current directory):
    tree -L num

  - Print directories only:
    tree -d

  - Print hidden files too with colorization on:
    tree -a -C

  - Print the tree without indentation lines, showing the full path instead (use `-N` to not escape non-printable characters):
    tree -i -f

  - Print the size of each file and the cumulative size of each directory, in human-readable format:
    tree -s -h --du

  - Print files within the tree hierarchy, using a wildcard (glob) pattern, and pruning out directories that don't contain matching files:
    tree -P '*.txt' --prune

  - Print directories within the tree hierarchy, using the wildcard (glob) pattern, and pruning out directories that aren't ancestors of the wanted one:
    tree -P directory_name --matchdirs --prune

  - Print the tree ignoring the given directories:
    tree -I 'directory_name1|directory_name2'

```

## MV

mueve y/o renombra

```bash
[usuario@formacion home]$ tldr mv

  mv

  Move or rename files and directories.
  More information: https://www.gnu.org/software/coreutils/mv.

  - Rename a file or directory when the target is not an existing directory:
    mv path/to/source path/to/target

  - Move a file or directory into an existing directory:
    mv path/to/source path/to/existing_directory

  - Move multiple files into an existing directory, keeping the filenames unchanged:
    mv path/to/source1 path/to/source2 ... path/to/existing_directory

  - Do not prompt for confirmation before overwriting existing files:
    mv -f path/to/source path/to/target

  - Prompt for confirmation before overwriting existing files, regardless of file permissions:
    mv -i path/to/source path/to/target

  - Do not overwrite existing files at the target:
    mv -n path/to/source path/to/target

  - Move files in verbose mode, showing files after they are moved:
    mv -v path/to/source path/to/target
```

## rm/rmdir

```bash

[usuario@formacion ~]$ tldr rm

  rm

  Remove files or directories.
  See also: `rmdir`.
  More information: https://www.gnu.org/software/coreutils/rm.

  - Remove specific files:
    rm path/to/file1 path/to/file2 ...

  - Remove specific files ignoring nonexistent ones:
    rm --force path/to/file1 path/to/file2 ...

  - Remove specific files interactively prompting before each removal:
    rm --interactive path/to/file1 path/to/file2 ...

  - Remove specific files printing info about each removal:
    rm --verbose path/to/file1 path/to/file2 ...

  - Remove specific files and directories recursively:
    rm --recursive path/to/file_or_directory1 path/to/file_or_directory2 ...

[usuario@formacion ~]$ tldr rmdir

  rmdir

  Remove directories without files.
  See also: `rm`.
  More information: https://www.gnu.org/software/coreutils/rmdir.

  - Remove specific directories:
    rmdir path/to/directory1 path/to/directory2 ...

  - Remove specific nested directories recursively:
    rmdir --parents path/to/directory1 path/to/directory2 ...
```

`rm dir3nuevo/fich*` este \* indica que removerá todos los archivos que empiecen por fich

rm sólo remueve ficheros

los rmdir sólo remueve directorios vacios

con `rm -r nombredirectorio` remueve el directorio y todo lo que contiene

Ejemplo:

```bash
[usuario@formacion dirs]$ tree -a
.
├── .bash_logout
├── .bash_profile
├── .bashrc
├── bienvenida
├── cuenta_usuario_creada
└── dir3nuevo
    └── .ficheroculto

1 directory, 6 files
[usuario@formacion dirs]$ rm dir3nuevo
rm: cannot remove 'dir3nuevo': Is a directory
[usuario@formacion dirs]$
[usuario@formacion dirs]$ mkdir dirvacio
[usuario@formacion dirs]$ rm dirvacio
rm: cannot remove 'dirvacio': Is a directory
[usuario@formacion dirs]$

[usuario@formacion dirs]$ rm -r dirvacio
[usuario@formacion dirs]$
[usuario@formacion dirs]$ tree
.
├── bienvenida
├── cuenta_usuario_creada
└── dir3nuevo
```

```bash
-- rm pregunta al borrar por ficheros que no son del usuario que está borrando
[usuario@formacion dir]$ pwd
/home/usuario/dirs/dir
[usuario@formacion dir]$ ls -l
total 0
-rw-r--r--. 1 u3      u3      0 Nov 14 15:51 file
-rw-rw-r--. 1 usuario usuario 0 Nov 14 15:51 fileusuario
[usuario@formacion dir]$ cd ..
[usuario@formacion dirs]$ rm -r dir
rm: remove write-protected regular empty file 'dir/file'? n
rm: cannot remove 'dir': Directory not empty
[usuario@formacion dirs]
```
