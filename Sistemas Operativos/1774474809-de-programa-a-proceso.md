---
id: 1774474809-de-programa-a-proceso
aliases:
  - De programa a proceso
tags:
  - sistemas
---

# De programa a proceso

## El programa

### Compilación
Cuando compilamos, estamos haciendo uso de varios programas.
![[Pasted image 20260325184258.png]]

#### Fase 1 - El Preprocesador (cpp)
- La fase mas "textual" de todas. Su trabajo es producir una traducción limpia antes de que el compilador real entre en juego.
- Ejemplo: `#include`: Reemplaza la directiva por el contenido completo del archivo referenciado.

#### Fase 2 - El Compilador (cc1)
Aquí ocurre la mayor parte del "trabajo inteligente". El compilador toma el .i y produce código ensamblador (.s). Esta fase tiene varias [[Final Orga#El proceso de compilación|subfases internas]]:
- **Generación de código intermedio**: Muchos compiladores (GCC, Clang/LLVM) no pasan directamente a ensamblador, sino que generan una representación intermedia (IR) agnóstica de la arquitectura.
- **Optimización**: La fase mas compleja. El compilador puede reordenar instrucciones, eliminar código muerto, hacer inlining de funciones, propagar constantes, etc. Los niveles *-O0*, *-O1*, *-O2*, *-O3* controlan cuánto se optimiza (utilizar *O0* en general)
- **Selección de instrucciones y generación de ensamblador**: Genera el .s para la arquitectura objetivo. (Assembly)

#### Fase 3 - El Ensamblador (as)
Convierte cada mnemónico de instrucción en su opcode binario correspondiente.
- Resuelve las etiquetas locales
- Deja una entrada de **reubicación** (relocation entry) para los símbolos externos.
- Genera la tabla de símbolos.
Para más información, ver [[Final Orga#Ensamblador|Ensamblador]].
El archivo .o resultante **tiene estructura ELF**, pero no es ejecutable todavía: Las direcciones no están resueltas y los segmentos no están organizados en el layout final de memoria.

#### Fase 4 - El Enlazador (ld)
El enlazador toma todos los .o y los combina en un único ejecutable ELF final.
Tareas:
- **Resolución de símbolos**: El linker encuentra la definición de un símbolo y "conecta" la referencia. Si no la encuentra, tira un error de "undefined reference".
- **Reubicación (relocation)**: 


> [!TODO] Completar enlazador

### Formato ejecutable
Un **programa** es un archivo que posee toda la información de como construir un proceso en memoria
- **Instrucciones de Lenguaje de Máquina**: Almacena el código del programa.
- **Dirección del Punto de Entrada del Programa**: Identifica la dirección de la instrucción con la cual la ejecución del programa debe iniciar.
- **Datos**: El programa contiene valores de los datos con los cuales se deben inicializar las variables.
- **Símbolos y Tablas de Realocación**.
- **Bibliotecas compartidas o Dinámicas**.

Un archivo ELF es una secuencia de bytes con una organización muy precisa.

> [!Warning] Importante
> El mismo archivo tiene dos lecturas paralelas y complementarias dependiendo de quién lo lee.

La idea central es que el archivo ELF cambia su significado dependiendo de quién lo lea.

Los offsets a la *Program Header Table* y la *Section Header Table* le dicen al lector del ELF **dónde encontrar cada tabla adentro del archivo**.

![[Pasted image 20260325192250.png]]

¿Qué es un archivo .ld?
Es un *linker script* (script de enlazador). Es un archivo de texto que le indica al enlazador cómo debe construir el binario final: qué secciones existirán, en qué orden, y crucialmente, en qué dirección de memoria virtual deben ubicarse.
## OpenSBI
OpenSBI es una implementación de la especificación SBI (*Supervisor Binary Interface*), que es básicamente la API que el firmware le ofrece al kernel.

## Proceso

> [!Info]- Definicion
> Un proceso es una entidad abstracta, definida por el Kernel, en la cual los recursos del sistema son asignados

Un proceso incluye:
- Los archivos abiertos
- Las señales pendientes
- Datos internos del kernel
- El estado completo del procesador
- Un espacio de direcciones de memoria
- Uno o más hilos de ejecución

### Virtualización de memoria
Dos tipos:
- Virtualización de Memoria. (Cómo maneja el SO el concepto de memoria para un proceso)
- Virtualización de Procesamiento.

### El proceso en memoria

El **Loader** usa el "plano del proceso" que es el archivo ELF y arma el espacio de direcciones.

Todos los procesos tienen la misma estructura del espacio de memoria.

#### Virtualización de Memoria
- Uno de estos mecanismos es denominado **Memoria Virtual**, la cual es una abstracción por la cual la memoria física puede ser compartida por diversos procesos.
- Un componente clave para esta son las **direcciones virtuales** => Para cada proceso su memoria inicia en el mismo lugar, la dirección 0.
- Cada proceso piensa que tiene toda la memoria de la computadora para sí mismo, si bien obviamente esto en la realidad no sucede. El hardware traduce la dirección virtual a una dirección física de memoria.

#### Traducción de Direcciones
Se traduce una Dirección Virtual en una Dirección Física. Este mapeo se realiza por la MMU.

![[Pasted image 20260325203051.png]]

### brk() vs malloc()
- brk()
	- Syscall. Opera con bloques grandes
- malloc()
	- Se implementa en espacio de usuario.
	- Utiliza brk().
	- Maneja estructuras de datos propias (en user space) para optimizar la memoria provista por brk.

### Virtualización del procesador
Consiste en dar la ilusión de la existencia de un único procesador para cualquier programa que requiera de su uso.

### Estados de un proceso
- **Corriendo (Running)**: El proceso se encuentra corriendo en un procesador. Está ejecutando instrucciones.
- **Listo (Ready)**: En este estado el proceso está listo para correr pero por algún motivo el SO ha decidido no ejecutarlo por el momento.
- **Bloqueado (Blocked)**: En este estado el proceso ha ejecutado algún tipo de operación que hace que éste no esté listo para ejecutarse hasta que algún evento suceda.

![[Pasted image 20260325204600.png]]

### El Contexto
- El **contexto** de un proceso **es la información necesaria para describir completamente el estado de un proceso**.
- Cada proceso posee su propio contexto.