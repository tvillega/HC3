---
marp: true
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
footer: Material OSEC - CC BY-NC-SA
---

# **Utilizando Comandos**

Introducción a las opciones largas, cortas y *flags*.
 Extended Backus–Naur form.

---

# Argumentos

Se entiende por argumento a toda plabra separada por un espacio que es escrita dentro del intérprete de comandos.

```
$ myComando arg1 arg2 arg3 arg4 arg5
```

* El ejemplo anterior tiene 6 argumentos.

* El argumento con el index 0 siempre es el nombre del comando.

---

# Opciones cortas

Las opciones cortas modifican el comportamiento original del comando y *pueden* aceptar cero o más argumentos.

* Son una sola letra precedida por un guión corto (`-`).

* Pueden agruparse tras un mismo guión (e.g. `-vxf`).
  * Sólo la última letra del grupo puede aceptar argumentos.

* No son mandatorias para el uso del programa.

---

# Opciones largas

Las opciones largas modifican el comportamiento original del comando y *deben* aceptar uno o más argumentos.

* Son una palabra precedida por dos guiones cortos (`--`).

* Puede ser una frase separada por guiones.
  * Por ejemplo `--block-size` o `--time-style`.

* No son mandatorias para el uso del programa.

---

# Flags

Las flags son opciones largas binarias, es decir, no aceptan argumentos y sólo habilitan o deshabilitan una función del programa.

* Al no recibir argumentos parecen banderas (de allí su nombre).

* Puede ser una frase separada por guiones.
  * Por ejemplo `--preserve-root` o `--no-preserve-root`.

* Se debe consultar el manual del programa para saber el orden de precedencia de dos flags opuestas.

---

# Extended Backus–Naur form

La EBNF, formalizada bajo ISO/IEC 14977, es un conjunto de notaciones utilizado en la sección de ayuda de los comandos.

Es importante tener en cuenta lo siguiente:

* Define una *gramática libre de contexto* no ambigua.

* Puede resultar ilegible al compactar múltiples elementos.

* Es una *formalización* y no un estándar, por lo que existen variantes de notación y no todos los programas lo honran.

---

# < > &ndash; Placeholder

Los caractéres `<`, `>` son utilizados para encapsular nombres de variables que deben ser reemplazadas por sus valores.

Por ejemplo:

```
  inscripcion <nombre> <apellido>
```

* Una variante de notación utiliza la fuente *cursiva* en lugar de encapsular en `<>` el nombre de la variable.

---

# [ ] &ndash; Optional Symbols

Los caractéres `[`, `]` son utilizados para encapsular uno o más argumentos opcionales mediante un nombre representativo.

```
  comando [OPTIONS] # cero o más opciones
```

```
  comando [FILES] # cero o más archivos
```

```
  comando [OBJECTS] # cero o más items
```

---

# { } - Required Symbols

Los caractéres `{`, `}` son utilizados para encapsular un grupo de argumentos, de los cuales sólo uno es requerido.

```
  comando [OPTIONS]

  OPTIONS := { opt1 | opt2 | opt3 }
```

* Cada opción sólo puede ser `opt1` ó`opt2` ó `opt3`.

* El comando acepta cero o más opciones

---

# { } - Required Symbols

Los caractéres `{`, `}` son utilizados para encapsular un grupo de argumentos, de los cuales sólo uno es requerido.

```
  comando COMMAND

  COMMAND := { cmd1 | cmd2 | cmd3 }
```

* Cada subcomando sólo puede ser `cmd1` ó `cmd2` ó `cmd3`.

* El comando requiere exactamente un subcomando.

---

# { } - Required Symbols

Los caractéres `{`, `}` son utilizados para encapsular un grupo de argumentos, de los cuales sólo uno es requerido.

```
  comando OBJECT

  OBJECT := { obj1 | obj2 | obj3 }
```

* Cada objeto sólo puede ser `obj1` ó `obj2` ó `obj3`.

* El comando requiere exactamente un objeto.

---

# Extracto de manpage

```
       ip [ OPTIONS ] OBJECT { COMMAND | help }

       OBJECT := { address | addrlabel | fou | help | ila | ioam |
               l2tp | link | macsec | maddress | monitor | mptcp |
               nexthop | ntable | ntbl | route | rule | sr | tap |
               tcpmetrics | token | tunnel | tuntap | vrf | xfrm }

       OPTIONS := { -V[ersion] | -h[uman-readable] | -s[tatistics] |
               -d[etails] | -r[esolve] | -iec | -f[amily] { inet |
               inet6 | link } | -4 | -6 | -B | -0 | -l[oops] { maxi‐
               mum-addr-flush-attempts } | -o[neline] | -rc[vbuf]
               [size] | -t[imestamp] | -ts[hort] | -n[etns] name |
               -p[retty] }
```

---

# ( ) - Mutual Exclusion

Los caractéres `(`, `)` son utilizados para indicar exclusión mutua para un conjunto de reglas.

```
  comando ( cmd1 [OPTIONS] | cmd2 OPTIONS )

  OPTIONS := { opt1 | opt2 | opt3 }
```

* `cmd1` acepta cero o más opciones.

* `cmd1` requiere exactamente una opción.

* El uso de `cmd1` y `cmd2` es mutuamente excluyente.

---

# Notación especial

* `|` - o lógico.

```
  comando ( opt1 | opt2 )
```
* `...` - puede repetirse cero o más veces

```
  comando [OPTION]... # equivalente a [OPTION...] y [OPTIONS]
```

* `--key=<value>` - notación para mencionar el tipo de valor que acepta la opción (añadir el símbolo `=` rara vez es mandatorio).