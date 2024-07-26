# Apuntes reunión Julio 25

* Distribución de HC3 en 3 grandes unidades.
* Apuntar a los primeros 3 años de especialidad.

## Unidades Grandes

### 1. IDE (VS Code) y CLI.

  1. Informes de trabajo en Markdown.
  2. Tener un repositorio GitHub para hacer entregas.
  3. Enseñar Layout de teclado en Español e Inglés.

La primera unidad se enfoca en el uso de programas gráficos para
programar y la generación de scripts en ellos que pueden ejecutarse
dentro de la terminal.

La tecnologia más avanzada a enseñar sería python venvs, puesto que
son integrados dentro del CLI y permiten visualizar la relación entre
el IDE para programar y la terminal para establecer el environment
de trabajo.

El uso de Makdown para los informes de trabajo permite acostumbrar al
uso de su sintaxis.

La entrega desde repositorios de GitHub (Pull Requests)
permite dar un acercamiento naïve del uso de la tecnología git y dar
un impulso a la necesidad de utilizarlo correctamente.

Enseñar las diferencias del layout permite mostrar cómo utilizar un teclado
corréctamente y mostrar la eficiencia del teclado en inglés en cuanto
la posición de los chars más frecuentes en un entorno CLI o de programación.

### 2. Shell de Linux en un servidor

  1. Conexión SSH en un servidor.
  2. Uso de coreutils
  3. Uso de User Web Directory para servir archivos.
  4. Uso de Curl / Scp para descargar archivos.
    4.1 Uso de SSH Tunnel para redireccionar web services.
  5. MIME Types (manejo de archivos sin exensión)
  6. Archivos comprimidos, sus programas y formatos.
  7. Empujar una incompatibilidad a git y obligar a resolver conflictos

El curso debe contar un servidor SSH análogo al de Anakena donde se pueda
trabajar múltiples usuarios a la vez, esto para representar un entorno real
donde se debe conectar a un servidor arbitrario para trabajar.

Estar en un servidor Linux vuelve necesario manejar coreutils para realizar
manipulación básica de archivos y llevar a cabo las tareas designadas dentro
del servidor, donde no se tiene acceso a una interfaz gráfica.

Anakena ya permite web directories, más es importante recalcar que pueden
servirse archivos para su descarga. Por ejemplo, Google Colab no tiene
almacenamiento persistente y este método resulta de utilidad para extraer
archivos csv para manejar bases de datos o alimentar machine learning.

Scp es la forma genérica de descargar o subir archivos a un servidor,
por lo que es importante conocerlo. Curl es la herramienta estándar de
Linux utilizada para descargar programas, es importante la correspondencia:
necesito descargar -> utilizo curl.

Existen programas como generadores de sitios web estáticos o Django que
emiten un webserver para probar cambios en vivo, pero un servidor con acceso
únicamente por por SSH no tiene salida gráfica. Es posible redireccionar
la interfaz gráfica, sea el desktop en sí o el servicio web,
mediante un tunel de SSH a la máquina local.

En Windows la convención mandata que la extensión del archivo determina
el tipo de archivo, no obstante es un estándar que los archivos contengan
como metadata el MIME Type, esto es, el tipo de archivo que son. Linux
ignora las extensiones en mayor parte y se guía en la metadat para determinar
el tipo de archivo que intenta manipular.

Se propone como una tarea entregar un tarball comprimido con miles de archivos
de diferente tipo (binarios, scripts, texto plano) sin extensión. Este deberá
subirse al servidor, filtrar por el tipo de archivo objetivo, volver a comprimir
y servirlo en el user web directory dejándolo disponible para descarga.

Esta activiad sencilla refuerza múltiples habilidades computacionales
necesarias para el correcto desarrollo de próximos cursos y el posterior
ingreso al mundo laboral.

De momento se está exigiendo git sin enseñarlo, por lo que el flujo de trabajo
es débil y propenso a pérdida de información. Forzando un conflictos desde upstream
se crea la necesidad de aprender git para no perder información y poder
resolver los conflictos creados en git.

### 3. Git

  1. Conventional commits.

git es una herramienta poderosa y extensiva en sus características. El cronograma
de esta unidad puede acomodarse específicamente a las necesidades de los cursos
posteriores, intentando siempre empujar a mayores conocimientos para exponer
las capaciades de la herramienta e incentivar su aprendizaje.

## Siguiente milestones del borrador de HC3

* Trabajar async con git en el forge GitHub.
* Discutir avances en GitHub Issues.
* Proponer nuevas ideas mediante GitHub Pull Requests
* Estructurar HC3:
  * Establecer metodología de evaluación.
  * Establecer conjunto de contenidos objetivo.
  * Establecer metodología de cátedras


## Cursos relacionados a los intereses de HC3


// Arquitectura de Sistemas de Alta Disponibilidad 
// Diseño de Sistemas de Internet de las Cosas
// Taller de Hacking Competitivo
// Redes

## Recursos a invertir para HC3

Un servidor dedicado capaz de soportar la carga de múltiples conexiones.
