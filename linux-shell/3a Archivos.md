---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
footer: Material OSEC - CC BY-NC-SA
---

# **Archivos de sistema**

Introducción al coreutil *stat*.
Introducción a *file types*, *perms* y *ownership*.
Introducción a opciones de *ls*.

---

# Everything is a file

En sistemas UNIX todo es un archivo. Dicho de otra forma, el Sistema Operativo expone sus servicios en forma de archivos.

Se accede a ellos mediante rutas dentro del árbol de directorios, para ello es importante conocer los siguientes atributos:

* Tipo de archivo.

* Permisos del archivo.

* *Ownership* del archivo.

---

# Atributos de archivo

Para ver los atributos de un archivo o directorio.

```
$ stat <ruta>
```

* La ruta puede ser relativa o absoluta.

* Puede aplicarse a cualquier archivo o directorio presente dentro del árbol de directorios.

A continuación un desgloce de los atributos elementales.

---

# File Type

Para ver el atributo *tipo de archivo*.

```
$ stat -c %F <ruta>
```

* **directory** - directorio, con o sin elementos en su interior.

* **regular file** - archivo con contenido escrito en su interior.

* **regular empty file** - archivo sin contenido escrito en su interior.

* **symbolic link** - puntero a otro archivo o directorio.

---

# Permissions &ndash; Human readable

Para ver el atributo *permisos del archivo.*

```
$ stat -c %A <ruta>
```

* `r` - permiso de lectura del archivo.
* `w` - permiso de escritura del archivo.
* `x` - permiso de ejecución del archivo.

Si aparece un `-` en lugar de una letra, no se cuenta con ese permiso.

---

# Permissions &ndash; Human readable

Los permisos listados por *stat* forman tres conjuntos.
```
- rwx rwx rwx
          ^^^
          Permisos de `others`
      ^^^
      Permisos de `group`
  ^^^ 
  Permisos de `owner`
```

Esta agrupación también se encontrará en otros programas.

---

# Permissions &ndash; Human readable

El primer caracter en los permisos indica el tipo de archivo.

* `-` - un archivo.

* `d` - un directorio.

* `l` - un *symlink*.

Esta información adicional se incluye porque los permisos gatillan un comportamiento distinto en cada uno de ellos.

---

# Permissions &ndash; Octals

Para ver el atributo *permisos del archivo* en su forma octal.

```
$ stat -c %a <ruta>
```

Al automatizar comandos con bash y coreutils, se utiliza la forma octal en los argumentos que establecen permisos.

* Si bien es posible utilizar la forma *human readable*, el Sistema Operativo guarda internamente  los permisos en la forma octal.

---

# Permissions &ndash; Octals

La forma octal resume cada conjunto en un número. Este número corresponde a la suma de los respectivos permisos.

* `4` - hay permiso de lectura.
* `2` - hay permiso de escritura.
* `1` - hay permiso de ejecución.

Cada combinación de permisos dentro de un conjunto tiene una y sólo una representación numérica.

---

# Ownership

Para ver los atributos de *ownership* se puede ejecutar.

```
$ stat -c %U <ruta>
```

* Esto imprime en pantalla al *owner*.

```
$ stat -c %G <ruta>
```

* Esto imprime en pantalla al *group*.

---

# Ownership &ndash; Owner

Cada archivo y directorio cuenta con un *atributo de propiedad* que se respeta, independiente del *user* de la sesión actual.

* Aplican los permisos del primer conjunto, correspondiente al antepenúltimo número en la forma octal.

* Por defecto, el *user* de la sesión sólo tiene permisos de escritura dentro de su \$HOME.

---

# Ownership &ndash; Group

Cada archivo y directorio cuenta con un *atributo de grupo* que permite a más de un *user* acceder al recurso.

* Aplica los permisos del segundo conjunto, correspondiente al penúltimo número en la forma octal.

* Por defecto, el *user* de la sesión actual pertenece al grupo de su mismo nombre. Si un *user2* es includio a este grupo, tendrá acceso al \$HOME de *user* conforme a lo estipulado en el *atributo grupo*.

* Un *user* puede pertenecer a más de un grupo.

---

# Ownership &ndash; Others

Cada archivo y directorio cuenta con un *atributo de otros*. Todo *user* que no sea *owner* ni pertenezca a *group* sigue estos permisos.

* Aplica los permisos del tercer conjunto, correspondiente al último número en la forma octal.

* Archivos que conforman bases de datos o listados de contraseñas quitan el permiso de lectura a este conjunto.

* La mayoría de los archivos y directorios del sistema otorgan permisos de lectura y ejecución en este conjunto.

---

# Listado de atributos de archivo

Los archivos y directorios contienen atributos de archivo, lo que permite listarlos todos juntos bajo un mismo comando.

```
$ ls -l <ruta>
```

* Si `<ruta>` termina en un directorio, lista los atributos de los elementos que contiene.

* Si `<ruta>` termina en un archivo, lista los atributos del archivo.

---

# Listado de atributos de archivo

El comando `ls -l` también imprime información adicional.

```
                         +── tamaño (bytes)     
                        _|__
drwxr-xr-x 2 sammy root 4096 2008-11-04 16:58 Documents
           | _____ ____      ________________
           |   |    |               |
hardlinks <+   |    |               └──> última fecha de
               |    |                    modificación
               |    └──> group
               |
               └──> owner
```

---

# Listado de atributos de archivo

El comando `ls -l` también imprime información adicional.

* **Hardlinks** - número de archivos que apuntan a la misma información dentro del disco (lo normal es 1).

* **Tamaño** - espacio que utiliza el archivo o directorio en el disco.

El resto de los atributos es explícito. Para mostrar el tamaño en kilo/mega/giga utilizar como opciones `-lh`. Para incluir archivos que comienzan con un punto utilizar como opciones `-lha`.