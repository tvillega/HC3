---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
footer: Material OSEC - CC BY-NC-SA
---

# **Modificando $HOME**

Introducción a las coreutils *mkdir* y *rmdir*.
Repaso de *ls* y rutas relativas como argumentos

---

# Crear un directorio

Para crear un directorio en el *Working Directory*

```
$ mkdir patata
```

* Puede leerse *Make Directory patata*

* Si un archivo o directorio del mismo nombre existe, el programa retornará un error.

---

# Crear un directorio anidado

Para crear un directorio dentro de un directorio.

```
$ mkdir -p vegetales/patata
```

* Puede leerse *Make Directory Parent patata*

* Si el directorio `vegetales` no existe, lo creará primero.

* Si un directorio del mismo nombre existe, el programa ignorará el error. Sólo lo mostrará si es un archivo.

---

# ¿Qué hay dentro del directorio?

Para listar el contenido de un directorio en *Working Directory*.

```
$ ls vegetales
```

* El programa acepta como primer argumento la ruta a otro directorio dentro del *Working Directory*.

  * Esta es una **ruta relativa** al directorio.

---

# Borrar un directorio

Para borrar un directorio en el *Working Directory*.

```
$ rmdir patata
```

* Puede leerse *Remove Directory patata*

* Si el directorio no está vacío, el programa retornará un error.

* Si el directorio no existe, el programa retornará un error.

* Si es un archivo, el programa retornará un error.

---

# Borrar un directorio anidado

Para borrar un directorio dentro de un directorio.

```
$ rmdir vegetales/patata
```

* Puede leerse como *Remove Directory patata*

* Sólo elimina el último directorio en la ruta.

* Tiene el mismo funcionamiento base.