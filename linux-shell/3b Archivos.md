---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
footer: Material OSEC - CC BY-NC-SA
---

# **Creando texto plano**

Introducción a coreutils *touch*, *cat* y *chmod*.
Introducción a *file descriptors* y *redirections*.

---

# ASCII

Acrónimo de **American Standard Code for Information Interchange**, corresponde al conjunto mínimo de caracteres en un sistema.

La forma más básica de texto plano sólo incluye caracteres en ASCII, los cuales son suficientes para escribir texto en inglés.

* Todo programa es capaz de leer y escribir estos caracteres.

---

# UTF-8

Acrónimo de **Unicode Transformation Format – 8-bit**, corresponde al conjunto máximo de caracteres compatibles en un sistema.

Es el conjunto de caracteres que permite escribir en más de un idioma, extendiendo la lista provista por ASCII.

* Un Sistema Operativo moderno es capaz de leer estos caracteres.

* Microsoft Windows utiliza la variante UTF-16, la cual es incompatible con ASCII.

---

# Plain Text

Se entiende por *texto plano* a un archivo con una secuencia de caracteres presentes en el listado de ASCII o en el listado de UTF-8.

* Existen numerosas *coreutils* que manipulan este tipo de archivos, de allí la importancia de categorizarlos como texto plano.

* Las coreutils en sí corresponden a *binary files* (archivos binarios) y contienen instrucciones de máquina.

  * Al no seguir el estándar ASCII, intentar leerlas como texto plano sólo mostrará texto basura en pantalla.

---

# touch &ndash; change file timestamp

Este programa **modifica la fecha de último acceso** de un archivo.

```
$ touch <archivo>
```

* Si `<archivo>` no existe, el programa creará un archivo vacío.

* **El propósito de este programa no es crear un archivo vacío.**

  * Es sólo una característica conveniente.

  * Django utiliza *touch* para actualizar su caché manualmente.

---

# *Be better than touch*

Para crear un archivo vacío con Bash.

```
$ >myArchivo
```

Para entender cómo funciona `>`, primero hay que aprender sobre los descriptores de archivos y las redirecciones.

---

# File Descriptor

Cada proceso de un Sistema Operativo tiene un descriptor de archivo (*fd*) dentro del cual puede leer y escribir para sus operaciones.

En UNIX todo es un archivo, por esta razón el *fd* puede ser un archivo de texto plano, un disco duro, una terminal, un mouse, etc.

Cada vez que un *fd* es utilizado, el Sistema Operativo le asigna un número. Hay tres valores reservados denominados *standard streams.*

---

# Standard Streams

Existen tres *flujos de datos estándares*.

* `/dev/fd/0` &ndash;> Standard Input

* `/dev/fd/1` &ndash;> Standard Output

* `/dev/fd/2` &ndash;> Standard Error

Bash los utiliza para sus operaciones bajo los nombres especiales `/dev/stdin`, `/dev/stdout` y `/dev/stderr`, respectivamente.

---

# /dev/stdin &ndash; Standard Input

* **Entrada estándar**, correspondiente al *fd* número 0.

* Conectada a la entrada dada por el Sistema Operativo.

* Lee los caracteres ingresados por el teclado físico.

En el ejemplo a continuación.

```
$ cmd1 > cmd2
```

La salida estándar de *cmd1* alimenta la entrada estándar de *cmd2*.

---

# /dev/stdout &ndash; Standard Output

* **Salida estándar**, corresponiente al *fd* número 1.

* Conectada a la terminal activa.

* Escribe lo que un comando imprime.

  * ¡Originalmente en papel con una impresora!

El stdout de printf se vuelve el stdin para un archivo.

```
$ printf "Hello" > myArchivo
```

---

# /dev/stderr &ndash; Standard Error

* **Error estándar**, correspondiente al *fd* número 2.

* Conectada a la terminal activa.

* Cuando un programa informa de un error, escribe en este fd.

El stderr de printf se vuelve el stdin para un archivo.

```
$ printf "--" 2> myArchivo
```

Para stderr debe explicitarse el número de su fd.

---

# Redirections &ndash; *the bash shorthand*

Bash permite manipular el stdin, stdout y stderr utilizado por los programas mediante el uso de símbolos entre comandos.

* `a > b` - El *stdout* de **a** se vuelve el *stdin* de **b**.

* `a 2> b` - El *stderr* de **a** se vuelve el *stdin* de **b**.

* `a &> b` - El *stdout* y *stderr* de **a** se vuelven el *stdin* de **b**.

  * `a > b 2>&1` - Compatible con versiones antiguas de bash.

Utilizar `>>` hará *append* en lugar de sobre escribir el archivo.

---

# *Be better than touch*

Para crear un archivo vacío con Bash.

```
$ >myArchivo
```

Bash crea **myArchivo** como fd en reemplazo de *stdout* y luego prepara la redirección de *stdin* gatillada por el símbolo `>`. Al no haber un stream de stdin, se trunca el archivo y quedan 0 bytes escritos.

**Si el archivo existe, su contenido será destruido**.

---

# cat &ndash; concatenate

Creados dos archivos nuevos.

```
$ echo "Texto1" > Archivo1
$ echo "Texto2" > Archivo2
```

Se puede concatenar su contenido a un nuevo archivo.

```
$ cat Archivo1 Archivo2 > ArchivoCompleto
```

Sin la redirección de stdout, la concatenación se imprime en pantalla.

---

# Redirections &ndash; *the other way*

De momento sólo se ha utilizado `>`, esto es, volver el stdout de alguien en el stdin de alguien. ¿Pero qué tal al revés?

```
$ cat < ArchivoCompleto
```

* El contenido de *ArchivoCompleto* se ha vuelto el stdin de cat.

* El comando cat sin argumentos lee stdin.

El stdout de cat se imprime en pantalla, pero podemos cambiar eso.

---

# Redirections &ndash; *both ways*

Sea *myDocumento* el nombre de un archivo de texto plano.

```
$ cat < myDocumento > myDocumentoCopia
```

* El archivo *myDocumento* se ha vuelto el stdin de cat.

* El archivo *myDocumentoCopia* se ha vuelto el stdout de cat.

El stderr se imprime en pantalla, pero podemos cambiar eso.

---

# Redirections &ndash; *everywhere*

Sea *myDocumento* el nombre de un archivo de texto plano.

```
$ < myDocumento > myStdoutFile 2> myStderrFile cmd arg1 arg2...
```

* El fd *stdin* es reemplazado por el archivo *myDocumento*.

* El fd *stdout* es reemplazado por el archivo *myStdoutFile*.

* El fd *stderr* es reemplazado por el archivo *myStderrFile*.

El programa *cmd* realiza sus operaciones normales con los nuevos fd.

---

# Redirections &ndash; Here Document

Combinar `cat` con las redirecciones permite escribir múltiples líneas de texto dentro de un archivo sin recurrir a echo o printf.

```
$ cat << EOF > myDocumento
Este es un texto hecho en $HOME y sera
escrito dentro de un archivo, su delimitador
es la ultima linea y termina la lectura de stdin
EOF
```

Para no expandir $HOME utilizar `'EOF' >`; para no sobre escribir el contenido del archivo utilizar `>>` en lugar de `>`.

---

# chmod &ndash; change mode

Para cambiar los permisos de los archivos creados.

```
$ chmod 655 myDocumento
```

Para editar recursivamente los permisos de un directorio.

```
$ chmod 655 -R myDirectorio
```

* Utilizando octales se pueden definir todos los permisos a la vez.

---

# chmod &ndash; change mode

Para añadir permisos a *user*, *group* y todos a la vez, respectivamente.

```
$ chmod u+r myDocumento
$ chmod g+w myDocumento
$ chmod o+x myDocumento
$ chmod ugo+rwx myDocumento
```

* Para quitar los permisos reemplazar `+` por `-`.

* Las operaciones son agrupables.

---

# umask &ndash; user file-creation mode mask

Define los permisos por omisión en la sesión de la shell al momento de crear nuevos archivos.

```
$ umask
```

* Retorna *la máscara* en forma octal.

```
$ umask -S
```

* Retorna *los permisos resultantes* en notación simbólica.