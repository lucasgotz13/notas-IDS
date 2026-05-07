---
id: introduccion-linux
aliases:
  - linux
  - unix
tags:
  - intro-desarrollo
---
#intro-desarrollo 
# Linux

## Descubriendo Linux

### ¿Qué es Linux?
- Es el **kernel del sistema operativo**, si bien en general se usa para referirse al sistema operativo en si. El sistema operativo se llama *GNU/LINUX*
- Un sistema operativo seria por ejemplo **Ubuntu**, **Fedora**, etc.
- Esta basado en un sistema operativo *unix-like*. 
	- Comparte **características y conceptos fundamentales** con los sistemas operativos basados en **Unix**.
	- Le proporciona a Linux una **estructura robusta y flexible**, con una fuerte **orientación** hacia la **multitarea**, la **seguridad** y la **estabilidad**.
	- La similitud también se refleja en la **terminal** y en las **herramientas estándar** del sistema operativo
### ¿Qué es un sistema operativo "UNIX-LIKE"?
- Es un tipo de software que sigue algunas de las ideas que introdució **UNIX**
	- *Estructura de archivos*: Organizan los archivos de forma **jerárquica**, parecida a un árbol.
		- Comienza desde el **directorio raíz** (/) y se va dividiendo en **carpetas** y subcarpetas
		- A diferencia de Windows, Linux tiene un **único** árbol con los archivos del sistema
	- Dos formas de **navegar** la estructura
		- **Rutas absolutas** (*Absolute pathnames*): Comienzan desde la raíz y siguen la jerarquía del sistema de archivos hasta llegar.
		- **Rutas Relativas** (*Relative pathnames*): Comienzan desde el **directorio de trabajo actual**. Utiliza símbolos especiales para representar posiciones relativas:
			- "." -> Directorio actual
			- ".." -> Directorio padre
### Árbol de directorios de LINUX
- **Interfaz de línea de comandos**: Permiten a los usuarios **escribir comandos en lugar de solo hacer clic con el ratón**. Esto puede ser muy útil para realizar tareas y controlar el sistema.
- **Multitarea y multiusuario**: Pueden manejar varias tareas al mismo tiempo y **permitir que múltiples personas usen el sistema simultáneamente** sin interferir entre sí.
- **Permisos y seguridad**: Controlan **quién puede acceder a qué archivos y recursos del sistema**, asegurando que solo las personas autorizadas puedan hacer ciertas cosas.
- **POSIX**: Muchos sistemas _Unix-like_ siguen un estándar llamado POSIX, que significa **Portable Operating System Interface** (Interfaz de Sistema Operativo Portátil). Este estándar **define reglas y especificaciones sobre cómo deben comportarse los sistemas operativos para garantizar la compatibilidad entre ellos**. En otras palabras, POSIX asegura que los programas escritos para un sistema _Unix-like_ puedan ejecutarse también en otros sistemas similares que cumplan con este estándar.
## Preguntas
¿Qué es Linux?::Es el **kernel** del sistema operativo. Aunque comúnmente se le llama “Linux”, el nombre correcto del sistema es **GNU/Linux**.

¿Qué es un sistema operativo basado en Unix?::Es un sistema que sigue ideas introducidas por UNIX, como la estructura de archivos jerárquica, multitarea, multiusuario, y comandos en terminal similares.

¿Qué sistemas operativos son ejemplos de GNU/Linux?::Ubuntu, Fedora, Debian, entre otros.

¿Qué significa que Linux es "Unix-like"?::Significa que comparte conceptos fundamentales con UNIX, como multitarea, seguridad, estabilidad y uso de terminales con herramientas estándar.

¿Qué estructura tienen los archivos en Linux?::Estructura **jerárquica en forma de árbol**, comenzando desde el directorio raíz `/`.

¿Cuál es la diferencia principal en estructura de archivos entre Linux y Windows?::Linux tiene un **único árbol de archivos**, mientras que Windows tiene múltiples unidades (como C:, D:, etc.).

¿Qué son las rutas absolutas en Linux?::Rutas que **comienzan desde el directorio raíz** `/` y siguen la jerarquía hasta el archivo o carpeta deseado.

¿Qué son las rutas relativas en Linux?::Rutas que parten desde el **directorio actual de trabajo**, usando símbolos como `.` para el actual y `..` para el directorio padre.

¿Qué significa el símbolo `.` en una ruta relativa?::Representa el **directorio actual**.

¿Qué significa el símbolo `..` en una ruta relativa?::Representa el **directorio padre** del actual.

¿Qué es la interfaz de línea de comandos (CLI) en Linux?::Una interfaz donde los usuarios **escriben comandos** en lugar de usar el ratón, útil para automatizar y controlar el sistema eficientemente.

¿Qué es la multitarea en Linux?::Capacidad del sistema para ejecutar **varias tareas al mismo tiempo**.

¿Qué significa que Linux es multiusuario?::Permite que **múltiples usuarios trabajen simultáneamente** sin interferencias.

¿Cómo maneja Linux la seguridad?::Mediante **permisos de acceso** que controlan quién puede ver, modificar o ejecutar archivos y recursos.

¿Qué es POSIX?::Es un **estándar** llamado Portable Operating System Interface que define reglas para asegurar compatibilidad entre sistemas Unix-like.

¿Para qué sirve POSIX?::Garantiza que los programas escritos para un sistema Unix-like puedan ejecutarse en otros que sigan el mismo estándar.