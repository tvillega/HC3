---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
footer: Material OSEC - CC BY-NC-SA
---

# **$HOME en el Árbol**

Repaso del comando *pwd*.
Introducción al comando *tree*.
Uso de rutas absolutas como argumentos.
Introducción al builtin *cd*.

---

# Filesystem Hierarchy Standard

* Árbol de directorios presente en todos los sistemas Linux.

* El árbol comienza en `/`, el directorio raíz.

* Rutas de directorios que comienzan con `/` son denominadas **rutas absolutas** y son leídas desde la raíz del árbol.

  * Las rutas relativas utilizan como raíz el *Working Directory*.


---

# Current Working Directory

* Puede verse con el coreutils *pwd*.

* Por defecto es `/home/user` para el *user* de la sesión.

* El directorio `user` se encuentra contenido en `home`.

* El directorio `home` se encuentra contenido en `/`.

* El directorio `/` es la raíz del árbol.

---

# $HOME dentro del árbol

Para ver los subdirectorios de la raíz `/`.

```
$ tree -L 1 /
```

* Puede leerse *Tree Level One Root*.

  * Imprime sólo los archivos y directorios contenidos en `/`.

* No utilizar la opción *L* saturará la pantalla imprimiendo todos los archivos y directorios existentes en el sistema.

---

# $HOME como su propio árbol

Para ver los subdirectorios de $HOME.

```
$ tree -L 1 $HOME
```

* Puede leerse como *Tree Level One Home*

  * Imprime sólo los archivos y directorios contenidos en *$HOME*

* *$HOME* se *expande* como `/home/user` antes de ejecutarse.
   * La shell reemplazará *user* con el nombre que corresponda.

---

# Cambiar Working Directory

Para cambiar el directorio actual.

```
$ cd <ruta>
```

* Puede leerse como *Change Directory to <ruta>*
  * Reemplazar *<ruta>* con una ruta absoluta o relativa.

* El atajo `cd -` regresa al *Working Directory* anterior.

* El atajo `cd ~` lleva al $HOME del usuario de la sesión.