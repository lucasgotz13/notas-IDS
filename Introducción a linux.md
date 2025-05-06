---
id: introduccion-linux
aliases:
  - linux
  - unix
tags:
  - intro-desarrollo
---
# Linux

## Descubriendo Linux

### ¿Qué es Linux?
- Es el **kernel del sistema operativo**, si bien en general se usa para referirse al sistema operativo en si. El sistema operativo se llama *GNU/LINUX*
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
