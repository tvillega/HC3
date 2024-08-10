# Linux Shell

Conjunto de presentaciones para enseñar los fundamentos de una shell de Linux. El aprendizaje esperado es el manejo dentro de una shell dentro de una máquina aritraria ejecutándo Linux.

Los apuntes en Jupyter Notebook son un WIP.

## Acceso a Linux

Para seguir estas clases es mandatorio contar con un sistema Linux.

A continuación se listan diferentes formas de acceder a uno:

* [Virtual Box](#virtual-box)
* [WSL](#wsl)
* [SSH](#ssh)

### Virtual Box

OSEC mantiene una imagen pre-configurada de Debian 12 bajo [este enlace](https://drive.google.com/drive/u/0/folders/10iD8wigZoSM0zLrD1rCKyt2CtvD6BEr7).

Las credenciales de acceso son:

* Usuario: `osec`
* Contraseña: `countessoflovelace`

Para tener acceso root ejecutar `su` y utilizar la misma contraseña anterior.

### WSL

Abrir una ventana de PowerShell o Windows Terminal y ejecutar:

```
wsl --install -d Debian
```

### SSH

Si cuenta con acceso a un servidor Linux externo también puede seguir estas clases, dado que no se necesita acceso privilegiado (`sudo`).