---
id: 1778102107-file-system-ii
aliases:
  - File System II
tags:
  - sistemas
---
- [[#Unix File System syscalls|Unix File System syscalls]]
	- [[#Unix File System syscalls#open()|open()]]
	- [[#Unix File System syscalls#creat()|creat()]]
	- [[#Unix File System syscalls#close()|close()]]
	- [[#Unix File System syscalls#read()|read()]]
	- [[#Unix File System syscalls#write()|write()]]
	- [[#Unix File System syscalls#lseek()|lseek()]]
	- [[#Unix File System syscalls#readdir()|readdir()]]
	- [[#Unix File System syscalls#Hard links y Soft links|Hard links y Soft links]]
- [[#Implementación de un file system|Implementación de un file system]]
	- [[#Implementación de un file system#Very Simple File System|Very Simple File System]]
	- [[#Implementación de un file system#Requisitos de diseño|Requisitos de diseño]]
		- [[#Requisitos de diseño#Organización general|Organización general]]

# File System II

## Unix File System syscalls

Suelen dividirse en 2 clases:
- Las que operan sobre los **archivos** propiamente dichos.
- Las que operan sobre los **metadatos** de los archivos.

### open()
La syscall open() convierte el nombre de un archivo en una entrada de la tabla de descriptores de archivos, y devuelve dicho valor. Siempre devuelve el descriptor más pequeño que no está abierto.

### creat()
Permite crear un archivo. Es equivalente a llamar open() con los flags O_CREAT|O_WRONLY|O_TRUNC.

### close()
syscall que cierra un file descriptor. Si ya está cerrado, devuelve error.

### read()
La llamada read se utiliza para hacer intentos de lecturas hasta un número dado de bytes de un archivo. La lectura comienza en la posición señalada por el file descriptor, y tras ella se incrementa ésta en el número de bytes leídos.

### write()
La syscall write() escribe hasta una determinada cantidad (count) de bytes desde un buffer que comienza en buf al archivo referenciado por el file descriptor.
Nota: El número de bytes escrito puede ser menor al indicado por count.

### lseek()
La syscall lseek() reposiciona el desplazamiento (offset) de un archivo abierto cuyo file descriptor es fd de acuerdo con el parámetro whence (de donde):
- SEEK_SET: el desplazamineto.
- SEEK_CUR: El desplazamiento es sumado a la posición actual del archivo.
- SEEK_END: El desplazamiento se suma a partir del final del archivo.


> [!Info] Dirent.h: struct dirent
> - char d_name[]: Este es el componente del nombre null-terminated. Es el único campo que está garantizado en todos los sistemas posix
> - ino_t d_fileno: este es el número de serie del archivo.
>```c 
>struct dirent {
>	ino_t d_fileno;
>	char d_name[MAXNAMLEN + 1]
>}
>```


### readdir()
Esta función lee la próxima entrada de u n

### Hard links y Soft links
**Hard Links**: Se produce cuando más de un dentry apunta al mismo inodo
**Soft link**: Es un archivo de tipo especial que contiene la ruta al archivo de destino.

![[Pasted image 20260506191106.png]]

## Implementación de un file system

### Very Simple File System

Este file system es una versión simplificada de un típico sistema de archivos unix-like. Existen diferentes sistemas de archivos y cada uno tiene ventajas y desventajas. 

Para pensar en un file system hay que comprender dos conceptos fundamentales: 
-  El primero es la estructura de datos de un sistema de archivos. En otras palabras cómo se guarda la información en el disco para organizar los datos y metadatos de los archivos. El sistema de archivos vsfs emplea una simple estructura, que parece un arreglo de bloques. 
-  El segundo aspecto es el método de acceso, como se machean las llamadas hechas por los procesos , como open(), read(), write(), etc. en la estructura del sistema de archivos.

### Requisitos de diseño
El objetivo principal del diseño de un filesystem es poder construir la abstracción de "archivo" sobre un medio de almacenamiento basado en bloques.

Todos los file systems contienen lo siguiente:
- La **estructura de índice** de un archivo proporciona una forma de localizar cada bloque del archivo. Las estructuras de índice suelen ser algún tipo de árbol para lograr escalabilidad y soportar la localidad.
- El **mapa de espacio libre** de un sistema de archivos proporciona una forma de asignar bloques libres para expandir un archivo.

#### Organización general
- Se divide al disco en bloques. En sistemas de archivos simples, los bloques suelen tener un solo tamaño. Los bloques tienen un tamaño de 4 kBytes.
- La visión del sistema de archivos debe ser la de una partición de N bloques de un tamaño de N * 4 KB bloques.
- Se va a llamar *data region* a la region del file system donde se guardan los datos del usuario. Este va a ocupar la mayor cantidad del espacio en un file system.

El sistema de archivos debe mantener información sobre cada uno de estos archivos. Esta información es la metadata y se almacena en un inodo
Los inodos también se guardan en el disco. Se guardan en un array de inodos llamada *inode table*.
Los inodos no suelen ser estructuras muy grandes. Normalmente ocupan unos 128 o 256 bytes. Si ocupan este último, un bloque de 4KB entonces guardaría 5 nodos y nuestro sistema tendría como máximo 80 nodos -> representa la cantidad máxima de archivos que podría tener nuestro file system.

Otro tema a tener en cuenta para un file system es cómo saber cuáles inodos y cuáles bloques están siendo utilizados o están libres. La técnica más popular para solucionar esto es usar una estructura llamada *bitmap*: Estructura en la cuál se mapea 0 si un objeto esta libre y 1 si está ocupado.

![[Pasted image 20260506192917.png]]

Entonces se podrá observar que queda un único bloque libre en todo el disco. Este bloque es llamado Super Bloque (S), el cuál contiene la información de todo el file system:
- La cantidad de inodos
- La cantidad de bloques
- Donde comienza la tabla de inodos -> bloque 3
- Donde comienzan los bitmaps.

![[Pasted image 20260506193659.png]]

> [!Warning] Aprender como armar un vsfs ya que lo pueden preguntar para un parcial.


> [!Todo] Leer Buffer caché

