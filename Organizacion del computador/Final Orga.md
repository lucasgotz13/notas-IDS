---
tags:
  - orga-computador
---
# Modelo Von Neumann

El Modelo Von Neumann consta de cinco componente principales
- **Unidad de entrada**
- **Unidad de memoria**
- **Unidad arimético-lógica** (ALU)
- **Unidad de control**
- **Unidad de salida**
![[Pasted image 20260202171123.png]]
Los programas se almacenan **en la memoria de la computadora** con los datos a procesar, siendo este el aspecto mas importante del modelo.
La unidad de control va a interactuar con la ejecución de todas las otras unidades.

La gran mayoría de los procesadores que se usan hoy en día están basados en este diseño
# Conexionado tipo bus
Si bien el modelo Von Neumann sigue vigente, este fue modernizado debido a que se necesitaba reducir la cantidad de conexiones entre el CPU y sus subsistemas
Para mejorar el tema del conexionado de esta arquitectura, las computadoras comenzaron a utilizar el sistema de interconexión a través del **bus del sistema**. En lugar de tener caminos de comunicación diferentes con la memoria y otros dispositivos, la CPU se interconecta con estos a través del bus del sistema.

> [!orga] Bus de sistema
> Permite la comunicación a través de distintas unidades a través de un mapa lógico. El bus en un sistema de comunicación se utiliza para la transferencia de datos entre componentes que tienen direcciones y que están controlados para indicar quien puede escribir y quien no.

Este modelo considera que el sistema de computación esta constituido por tres subconjuntos:
- La **CPU** (La combinación de la ALU y la unidad de control)
- La memoria
- La entrada-salida (combinadas en un solo conjunto)
Cuando hablamos de un conexionado tipo BUS, hablamos de que todas las unidades están conectados a través de un medio físico único que es compartido.
Un bus permite conectar:
- Componentes de una computadora (CPU, GPU, RAM, etc.)
- Varias computadoras entre sí
- Componentes electrónicos dentro de un microprocesador
Los componentes compatibles son:
- Hardware: cables, fibra óptica, circuitos integrados
- Software: protocolos de comunicación
Lo más importante de este modelo es la forma en que se realizan las comunicaciones entre los componentes por medio del bus del sistema, el cuál está constituido por tres tipos distintos de buses:
- **Bus de datos** => Transporta la información. Acá se obtiene el dato que voy a escribir/leer
- **Bus de direcciones** => Determina hacia donde está siendo enviada/leída dicha información
- **Bus de control** => Describe aspectos de la forma en que se está llevando a cabo la mencionada transferencia de información. Controla el estado de operación de lectura/escritura
Los buses están constituidos por conjuntos de cables agrupados de acuerdo a su función.
Un bus de datos de 32 bits contiene 32 cables individuales, donde cada uno transporta **un bit de datos**

![[Pasted image 20260202173238.png]]



> [!CPU] ¿Cuál es la función principal del CPU en el bus del sistema?
> La CPU genera las direcciones que viajan a través del bus de direcciones, mientras que la memoria y las entradas y salidas recibe esas direcciones. La memoria nunca genera direcciones, así que la CPU nunca recibe direcciones, por lo cuál no hay interconexión en ese sentido.

Cuando el bus tiene que ser compartido por varios elementos que se comunican entre sí, se debe poder distinguir a estos, lo cuál se logra utilizando [[Direcciones]].

## ¿Qué hace el CPU?
La función específica del CPU es **ejecutar programas**.
![[Pasted image 20260209160324.png]]
¿Cómo los ejecuta? => [[Ciclo de fetch]]
# Memoria 
La memoria de una computadora consiste en un **conjunto de registros numerados (direccionados)** en forma consecutiva, en los cuales normalmente se almacena un **byte** de información (conjunto de 8 bits).
A la dirección del registro también se la denomina *locación de memoria*
Dependiendo el tipo de arquitectura, el tamaño de las **palabras** varían (en general entre 16, 32, 64 y 128 bits).
Es habitual que las máquinas puedan leer palabras de más de un byte, las cuales se almacenan en la memoria como una **secuencia de bytes**, y se direccionan a partir del byte menos significativo de la palabra almacenada. 
Para almacenar este tipos de palabras, existen dos alternativas:
- *Big Endian* => Se almacena el byte **mas** significativo en la dirección mas baja de la memoria
- *Little Endian* => Se almacena el byte **menos** significativo en la dirección mas baja de memoria

## Estructura
Consiste en un arreglo lineal de las diversas locaciones ordenadas en forma consecutiva.
![[Pasted image 20260202180446.png]]
Cada una de las direcciones identificadas con un valor numérico se corresponde con una palabra específica almacenada en la misma. Este número se define como su **dirección**.
La dirección mas alta corresponde a una unidad menos que el tamaño de la memoria. En el caso de un sistema de 32 bits, la última dirección es 2³² - 1, mientras que la primera dirección es 0.

El modelo de memoria utilizado en estos sistemas es el siguiente:
![[Pasted image 20260202180718.png]]

El espacio de direcciones de la arquitectura en este ejemplo esta dividido en diferentes sectores, lo que se denomina [[mapa de memoria.]] Cada procesador tiene un mapa de memoria. Estos mapas pueden diferir entre una implementación y otra, lo cuál lleva a que algunos programas compilados para el mismo tipo de procesador puedan no ser compatibles entre sistemas.

¿Cómo se identifican las direcciones? => Se cuentan en secuencia a partir de 0. En el caso de querer hacer un programar por nuestra cuenta, podemos acceder en este caso a las direcciones desde la 2048 hasta que nos encontremos con la pila del sistema.

El mapa de memoria no esta compuesto enteramente por memoria, sino que hay direcciones reservadas para los demás componentes del sistema, como por ejemplo el espacio para la entrada y salida. A esto se le denomina **entrada/salida mapeada en memoria**

Para mas información sobre el mapa de memoria en específico => [[#ARC A Risc Computer]]

## Trayecto de datos de la CPU
Cuando hablamos de trayecto de datos, hablamos de lo que sucede adentro del [[#¿Qué hace el CPU?|datapath]]
![[Pasted image 20260207001556.png]]Si queremos por ejemplo sumar 2 + 2, va a suceder lo siguiente:
- rs1 y rs2 va a ser donde se guarden los datos a sumar
- La ALU va a hacer las operaciones aritméticas necesarias y esta va a devolver *flags*
- Con esos flags, la unidad de control va a tomar decisiones
- La ALU va a entregar el resultado y lo va a cargar en un registro.

La unidad de control va a determinar ==desde donde toma los datos== para ==cargar en los registros== para realizar la ==operación en la ALU==. Selecciona las operaciones que se van a realizar y los operandos que se van a cargar en la ALU (los puede buscar en el conjunto de registros o en otro componente del sistema), que se van a cargar en rs1 y rs2.
La diferencia principal entre el conjunto de registros y la memoria del sistema es que **los registros están en la CPU**. Esto hace que el CPU funcione con mayor rapidez, además de que almacenan **temporalmente** los operandos y los resultados.
Además, podemos observar que existen varios buses dentro del CPU, ==lo que permite la búsqueda simultanea de dos operandos que estén almacenados en el conjunto de registros, que puedan ser procesados por la ALU y poder devolverlo al conjunto de registros.==

# Desde el Lenguaje de alto nivel a código de máquina
![[Pasted image 20260207155630.png]]

> [!NOTE] ¿Qué hace el compilador?
> Transforma los lenguajes de alto nivel a un **código de máquina**, donde este código va a ser para un procesador específico. 

En el proceso de compilación de un programa, el código fuente escrito por una persona se transforma en un lenguaje simbólico y luego pasa por un **ensamblador** que traduce el código en lenguaje *Assembly* a **código de máquina**.

La traducción de lenguaje de alto nivel a lenguaje simbólico se denomina *compile time*.
La traducción de lenguaje simbólico a código de maquina se denomina *assembly time*.
Esto resulta en un programa objeto el cuál puede vincularse con otros programas objetos en el momento del enlace (*linking time*) y luego continua con los procesos de carga (*load time*).

## [[Acceso a Memoria RAM]]
Para guardar palabras de varios bytes en RAM utilizamos **Little-Endian** o **Big-Endian**

# ARC: A RISC Computer

> [!RISC] RISC
> *Reduced instruction Set Computer*. Son procesadores que tienen un set de instrucciones **reducido**

![[Pasted image 20260207163731.png]]
- Es una máquina de 32 bits con capacidad de direccionamiento por bytes.
- Puede manejar tipos de datos de 32 bits, pero la información se almacena en memoria en forma de bytes
- Las primeras 2048 direcciones están reservadas para el sistema operativo
- El espacio del usuario es el que se reserva para la carga de los programas del usuario.
- Pila del sistema crece en direcciones inferiores de memoria.
- Zona reservada para dispositivos de entrada-salida. Cada dispositivo tiene asignada una serie de direcciones de memoria para el almacenamiento de sus datos: entrada mapeada en memoria
- La arquitectura ARC funciona con el byte más significativo almacenado en la menor de las direcciones asignada a la palabra (big endian).
## Memoria
- Espacio de direcciones: 2^32
- Para más de un byte: Big-endian
## Set de instrucciones
- Es un subconjunto de SPARC.
- Todas las instrucciones ocupan 32 bits.
- 32 registros de 32 bits.
- Program Status Register (PSR) guarda los flags de ALU.
- Sólo dos instrucciones acceden a memoria principal:
	1. Leer memoria a registro.
	2. Escribir desde registro a memoria.
## Algunas instrucciones de ARC
![[Pasted image 20260208142806.png]]
### Registros de Accesibles al programador
![[Pasted image 20260208142835.png]]
El registro PSR tiene el estado del procesador.
El registro PC (program counter) controla la dirección de la instrucción de la ejecución.
Cada vez que hago un call, en el registro *r15* se guarda la dirección desde la cuál fue llamada la instrucción. Esto se hace llamando `jmpl %r15 + 4, %r0`
En el *r14*, me va a señalar donde esta pila (cuál fue el último valor accedido).
Los registros *r14* y *r15* tienen aplicación de puntero de pila.
### Directivas al Ensamblador (ARCtools)
- Indican al ensamblador como procesar una sección de programa.
- Las instrucciones son espeíficas de un procesador.
- Las pseudo-instrucciones o directivas son específica de un programa ensamblador.
- Algunas generan información en la memoria, otras no.

![[Pasted image 20260208143502.png]]
# Subrutina
### ¿Qué es?
Es una secuencia de instrucciones a la que se invoca como si se tratara de una única instrucción. Cuando se llama a una subrutina, se transfiere el control del programa a esta. Se ejecutan sus instrucciones y luego vuelve a la siguiente instrucción del que generó el llamado, con el *jmpl*
### Subrutinas vs Branch
La diferencia es que la subrutina deja el PC en la dirección donde esta, mientras que el Branch no vuelve automáticamente.
### ¿Cómo se llega/termina una subrutina?
Se llega por un *call* y se termina con un *jmpl link*.
### ¿Cómo se intercambian argumentos con una subrutina?
Se pasan aparte (se invoca a la subrutina guardando los argumentos)
## Llamado a subrutinas
![[Pasted image 20260208145756.png]]
# Macros
### ¿Qué es una macro?
Una macro es una **operación que ejecuta un conjunto de operaciones**.
Con la macro uno le da un nombre a un conjunto de instrucciones para que el compilador las pueda interpretar (parecido a un copiar y pegar).
No es igual a una subrutina porque la macro se ejecuta en **tiempo de compilación**, mientras que la subrutina se ejecuta en **tiempo de ejecución**.
![[Pasted image 20260208150546.png]]

| **Macro**                                                                                                                          | **Subrutina**                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Se accede en tiempo de ensamblado<br>(expansión de macros) convirtiéndola en su<br>código equivalente.                             | Se accede por un *call* en tiempo de <br>ejecución y termina con un <br>*jmpl* en tiempo de ejecución. |
| Sus parámetros son interpretados por el<br>**ensamblador** y reemplazados por lo que<br>corresponda en cada lugar que es invocada. | Sus parámetros (valores) le llegan<br>en tiempo de su ejecución (pila o<br>registros).                 |
| Su código de máquina está repetido tantas<br>veces como la macro fue invocada.                                                     | Su código de máquina está localizado en<br>un lugar específico y único en memoria.                     |
# Localización de variables
Las podemos manipular a través de:
- Registros
- "Segmentos de datos" (RAM)
- Stack (RAM)
Siempre en los registros la velocidad de acceso es **mayor**. Es donde está la memoria de usuario y el código de máquina. La ventaja es que tengo **mayor capacidad**.
La ventaja del Stack es que permite declarar variables locales que ocupan un espacio que nadie tiene acceso y cuando termina la subrutina lo que se hace es liberar el Stack. La desventaja es que al acceder a la memoria RAM, estoy accediendo al bus de sistema lo cuál es **mas lento**

# Conformación de un Set de Instrucciones
Set de instrucciones: Conjunto de instrucciones + Registros disponibles
Características:
- Tamaño de las instrucciones (espacio ocupado por el código de máquina)
- Tipo de operaciones admitidas
- Tipo de operandos (ubicación y tamaño)
- Tipo de resultados (ubicación y tamaño)
- Formas de indicar la ubicación de los datos (modos de direccionamiento)

# RISC vs CISC
RISC: Reduced Instruction Set Computer
CISC: Complex Instruction Set Computer

Con RISC se busca la máxima eficiencia respecto de la cantidad de ciclos de reloj que debe realizar el CPU para ejecutar una instrucción. Por eso RISC tiene menos instrucciones.
CISC tiene instrucciones mas complejas => El procesador cuenta con instrucciones que me resuelven mas cosas que en un procesador RISC requiere mas instrucciones. Sin embargo, esto consume mas ciclos de reloj.

## [[Diferencias]]

---
# Arquitectura de un CPU
A través de un **set de instrucciones** yo tengo acceso a las **diferentes implementaciones** que tenga la microarquitectura de un CPU. 

## Organización del [[#Trayecto de datos de la CPU]]

> [!preguntas] ¿Cuáles son los elementos que conforman el Trayecto de Datos?
> Los buses, los registros y la ALU

> [!preguntas] ¿Qué objetivo cumple la organización de estos elementos?
> Realizar las operaciones entre cada uno de los datos que ponga en los registros *rs1* y *rs2* y disponibilizarlo para que pueda ser almacenado además de entregar los flags de la operación

Cuando hablamos de trayecto de datos, estos pueden estar organizados en distintos buses.
![[Pasted image 20260209162359.png]]
En este bus, para realizar una operación se debe cargar un dato en el bus, luego leerlo y cargarlo en el registro y repetir lo mismo para el otro registro. Luego se hace la operación en la ALU, se lee el resultado y se coloca en el bus.
![[Pasted image 20260209164541.png]]
==¿Qué sucede cuando tenemos un trayecto de datos organizado en 2 buses?==
Lo primero que podemos ver es que desaparecieron los **registros auxiliares**. Entonces con un solo clock puedo guardar un dato en cada bus, la ALU calcula y entrega el resultado y lo guarda en un registro auxiliar. Todo esto se realiza en 2 clock (con el primer clock coloco los datos en los buses y con el segundo coloco el resultado en uno de los buses). Conclusión: **minimize** la cantidad de ciclos de reloj que requiero para realizar una operación
![[Pasted image 20260209165036.png]]
==¿Qué sucede cuando tenemos un trayecto de datos organizado en 3 buses?==
En este caso la salida de la ALU ya está conectada a un bus. Entonces de esta manera en **un solo clock** tengo los dos operandos y la salida conectada a los registros pertinentes.
Esta arquitectura es **mas compleja** pero también **más rápida**.
## ALU: Operaciones aritméticas en ARC
![[Pasted image 20260209170300.png]]
Funciones que debe realizar la ALU:
- Operaciones aritméticas y lógicas
- Desplazamientos a derecha e izquierda
Soluciones alternativas:
- Para las operaciones aritmético-lógicas
	- Sol. 1: Circuitos sumadores, restadores, etc.
	- Sol. 2: Usar una "tabla de consulta" (LUT)
- Para los desplazamientos
	- Sol. 1: Registros de desplazamiento
	- Sol. 2: Desplazador rápido o "Barrel-shifter"

### Tabla de consulta (Look-up table)
![[Pasted image 20260209182458.png]]
¿Cómo se implementa esta tabla? => Mediante la grabación en **memoria ROM**.
![[Pasted image 20260209183311.png]]
### Barrel-shifter
Es un hardware que me permite, con un ciclo de reloj, **desplazar n posiciones**.
![[Pasted image 20260209184453.png]]
Según los valores de "amt" (bits de control de los multiplexores), los bits se van a desplazar n posiciones der/izq.
Funciones:
- Shift lógico de n bits der/izq.
- Shift aritmético de n bits der/izq.
- Shift circular (rotación) der/izq.
Principio de funcionamiento:
- Organización por niveles.
- Cada nivel desplaza 2^n al anterior.
- Bits de control definen rango del shift.
![[Pasted image 20260209190520.png]]
Los registros r0 a r31 son accesibles por el usuario.
Los registros *temp* **no** son accesibles por el usuario. Estos se utilizan para interpretar el conjunto de instrucciones.
El usuario tiene acceso al *program counter* a través las instrucciones *call* y *jumper link*.
El *instruction register* (*ir*) es el que ==contiene la instrucción que se esta ejecutando==.
A través de multiplexores vamos a poder colocar el dato proveniente del resultado de la ALU (para ser guardado) o colocar un dato proveniente de una posición de memoria que **no forme parte** del trayecto de datos.
Los decodificadores permiten indicar qué registro se va a poder utilizar para cargar sus datos en cada uno de los buses para que **pueda ser operado por la ALU**.
Cada registro tiene una **posición** que permite habilitarlo para **leerlo o escribirlo**.
La unidad de control es quien realiza o no la escritura en memoria **leyendo el bus del sistema**.

## Estructura interna de los registros
![[Pasted image 20260210170249.png]]
Si yo quiero desconectar el registro del bus de sistema para ser escrito/leído, se utiliza un dispositivo denominado *buffers tri-state*, el cuál permite desconectar **electrónicamente** las salidas. Básicamente, este hardware actúa como llave.
### Registros que no responden a la estructura general
- Registro de instrucción (IR): Tiene salidas específicas por campos del código de máquina. Estas salidas responden al código de máquina 
  ![[Pasted image 20260210170908.png]]
  La unidad de control utiliza las salidas para interpretar **qué** instrucción ejecutar. Con esto, el IR **interpreta y gobierna**. 
## Diseño de una unidad de control
Podemos diseñar una ==unidad de control== por:
- Lógica microprogramada (firmware. Lo usado hoy en día)
- Lógica cableada
El trayecto de datos es **esencialmente idéntico** en ambos casos.

## Microarquitectura
![[Pasted image 20260210173536.png]]
El  Control Store Address Incrementer CSAI es donde se encuentra el microprograma que tiene particularmente 2048 posiciones, donde el decodificador de abajo permite seleccionar la dirección de qué código del programa ir a buscar y colocarlo en un registro llamado ___MIR___ (Microcode Instruction Register). En este, cada una de sus salidas están conectadas físicamente a cada uno de los bloques que gobiernan el trayecto de datos. Todo esto **permite que se ejecute la instrucción**.
#### Control Store (ROM)
- Contiene 2048 palabras de 41 bits el cuál contiene todas las líneas que deben controlarse para **implementar una instrucción** al nivel del programa que nosotros tenemos. Se la suele considerar una **memoria de control**.
- Cada palabra de 41 bits es una microinstrucción.

#### MIR
- **Guarda microinstrucciones**. Así como el IR guarda instrucciones del set del procesador.
#### Ejecución del microcódigo:
- La unidad de control va a ser responsable de buscar las microinstrucciones y ejecutarlas. La ejecución de las microinstrucciones se controla a través del MIR, del registro de estado %psr y de un mecanismo interno que permite determinar cuál es la siguiente microinstrucción a ejecutar llamado *Control Branch Logic* (CBL) y el multiplexor de direcciones de la memoria de control. En resumen:
	- CS-Addr-MUX apunta a la próxima microinstrucción.
	- Microinstrucción: se copia desde CS al MIR.
	- Control de flujo: CBL y CS-Addr-MUX
#### IR con salidas por cada campo
- Registros origen y destino: rd, rs1, rs2.
- Si es direccionamiento inmediato: `Bit[13]`.
- Códigos de operación: op, op2 y op3 (bits 31-30, 24-22- 24-19 respectivamente).
## Formato de palabra de microcódigo
![[Pasted image 20260210175425.png]]
- Cada palabra tiene 41 bits, los cuáles comprenden 11 campos distintos.
- El campo A determina cuál es el registro del trayecto de datos cuyo contenido debe colocarse sobre el bus A.
	- A MUX selecciona si ese decodificador obtiene su entrada desde el campo A del MIR o desde el campo rs1 del IR.
- Ídem A con B.
- Ídem A con C.
	- El C MUX determina si la entrada al decodificador C se obtiene desde el campo C del MIR o desde el campo *rd* del IR.
## Assembler vs Microprograma
### Programa en lenguaje de bajo nivel
- Se implementa en Assembler del procesador (ej. ARC).
- Visible al programador
- Implementa programas de propósito general.
### Microprograma
- Código que implementa cada instrucción del Assembler ARC.
- Invisible al programador.
- El microcódigo en binario está grabado en ROM (firmware).
- Debe definirse un lenguaje ad-hoc.
- Un mismo set de instrucciones admite ser implementado con muchas versiones de firmware.
---
# El lenguaje y la máquina
![[Pasted image 20260211223546.png]]
El lenguaje de alto nivel es [[compilado]] y traducido a un lenguaje [[Assembler]], el cuál es ensamblado en código de máquina.
El código de máquina, dependiendo de cómo nosotros lo hayamos diseñado, puede tener distintos módulos, el cuál a través de un proceso de **linkeo** lo convierte a un **código ejecutable** el cuál puede ser decodificado por el microprocesador y cargada cada una de sus instrucciones al registro MIR. 

## Compiladores

> [!compilador] ¿Qué es un compilador?
> Me permite completar el proceso del programa fuente para traducirlo a un código de Assembler

Cuando hablamos de compiladores, hay distintos tipos:
- Compilador de **una sola pasada o de pasadas múltiples**: Completa el proceso en un solo recorrido del programa fuente o en varios.
- **Compilador incremental**: Genera código instrucción por instrucción (no para todo el programa) cuando un usuario pulsa una tecla especial. Entorno de depuración. Intérpretes
- **Cross-compilador**: Genera código en lenguaje assembler para una máquina diferente de la que se está utilizando para compilar.
### El proceso de compilación
![[Pasted image 20260211224631.png]]
Escribimos un código fuente, donde se leen **datos de entrada**. A partir de este, hay una salida del proceso donde esa salida genera el código de assembler.
![[Pasted image 20260211224846.png]]
- Análisis léxico: Distinguir palabras clave del lenguaje e identificadores. Crea la tabla de símbolos.
- Análisis sintáctico: Detecta la estructura comparándolas con las permitidas por el lenguaje.
- Análisis semántico: Asociar a cada variable, tipo, ámbito, una congruencia de tipo en expresiones.
- Mapeo de acciones: Asociar código assembler a cada sentencia del programa.
  Se traduce una linea de alto nivel a lineas de ensamble. Los tipos de instrucciones que se traducen son:
	- Operaciones aritméticas/lógicas.
	- Control del flujo del programa.
	- Movimiento de datos.
- Generación de código: Salida del sistema.
#### Mapeo de acciones
Donde se almacenan las variables en RAM?
- Variables estáticas (globales): Permanecen a lo largo del tiempo de ejecución de la aplicación. Se guardan en posición de memoria **conocida en tiempo de compilación**.
- Variables locales a un procedimiento: Desaparecen cuando termina el procedimiento en el que están declaradas. Se guardan en **el stack**.
Es más óptimo guardar variables en registros porque son las que más rápido se acceden.
## Ensamblador

> [!Ensamblador] ¿Qué hace el ensamblador
> El ensamblador es un traductor de código Assembler a código de máquina

- Transcódificación: Relación 1 a 1 entre código Assembler y código de máquina.
- Ofrece al programador:
	- Representación simbólica para direcciones y constantes
	- Definir la ubicación de las variables en memoria
	- Variables inicializadas antes de ejecución
	- Provee cierto grado de aritmética en tiempo de ensamblado
	- Utilizar variables declaradas en otros módulos
	- Utilizar macros (dar nombre a fragmentos de texto)

Ejemplo: `ld %r3, [array]+20, %r7`
En este caso el ensamblador va a calcular **dónde esta el array** en **tiempo de ensamblado**, y en tiempo de ejecución lo va a cargar en *r3* y lo va a correr en *r7*.
### Obtención de código de máquina
![[Pasted image 20260211230651.png]]
El proceso de ensamblado, podemos concluir, es la conjunción de **el texto en Assembler** y el **formato de las instrucciones (ISA)**. El resultado de ambos genera el código máquina.
### Proceso de ensamblado en dos pasadas
- **Preproceso**: Expansión de macros => (1) Registrar definiciones (2) Reemplazar
- **Primer pasada**:
	- Detecta identificadores y les asigna una posición de memoria.
	- Crea la tabla de símbolos.
- **Segunda pasada**:
	- Cada instrucción es convertida a código de máquina.
	- Cada identificador es reemplazado por su ubicación en memora según indica la tabla de símbolos.
	- Cada línea es procesada completamente antes de avanzar a la siguiente.
	- Genera el código objeto (código que tiene el código de máquina) y el listado (texto para el programador).
## Creación de la tabla de símbolos
![[Pasted image 20260211231449.png]]
En la primera pasada, va a crear la tabla y no va a anotar ningún valor, para luego en la segunda identificar en qué **posición de memoria** esta cada símbolo.
### Archivos creados por el ensamblador
Se completa en la segunda pasada.
Salidas:
1. Archivo de texto (listado)
2. Archivo con código objeto. Incluye:
	- Código de máquina
	- Un encabezamiento de archivo conteniendo:
		- Dirección de primera instrucción a ejecutar (si corresponde): main()
		- Librerías externas que son utilizadas por el módulo.
		- Tabla de símbolos con información sobre:
			- Símbolos que están declarados en otros módulos externos
			- Símbolos que se declaran localmente pero se le da permisos de acceso desde otros módulos.
			- Información sobre la relocalización del código.
![[Pasted image 20260211231938.png]]

> [!pasada] ¿Cuál es la diferencia entre el ensamblador de una pasada vs dos pasadas?
>  Todas las etiquetas las tenemos que declarar antes de ser utilizadas
### Localización del programa en memoria
En general no se sabe donde va a ser cargado el programa.
Si varios módulos son vinculados no se sabe donde va a ser cargado el programa ni cada módulo.

Si la aplicación está conformada por un determinado código y debe sumarse a otro código, donde en ambos códigos utilicemos por ejemplo `.org 2048`, un código va a terminar desplazando al otro. => El ensamblador es responsable de **marcar direcciones relocalizables y direcciones absolutas** para que el linker pueda **realizar la conjunción de distintos códigos**, permitiendo vincularlos para generar un archivo ejecutable. Esta acción se denomina **proceso de linkeo**.

El linker va a modificar la tabla de símbolos ajustando las posiciones de memoria donde se cargue cada uno de los códigos de máquinas.
#### El ensamblador y el linker
- El ensamblador combina dos o más módulos que fueron ensamblados. Origen de estos módulos:
	- Aplicación
	- Librería del ambiente de desarrollo
	- Sistema operativo
- El linker:
	- Resuelve referencias de memoria externa al módulo.
	- Relocaliza los módulos combinándolos y reasignando las direcciones internas a cada uno para reflejar su nueva localización.
	- Define en el módulo a cargar la dirección de la primer instrucción a ser ejecutada ("main").

#### Referencias externas
En un módulo dado hay:
- Símbolos locales 
- Símbolos globales

No todas las etiquetas son relocalizables. El ensamblador es responsable de comunicar al linker esta situación. Ejemplo:
![[Pasted image 20260213141632.png]]
El linker, por instrucción del ensamblador, asigno en otra tabla de símbolos al "sub".
Ensamblador:
- Determina cuáles símbolos son relocalizables y cuáles no.
- Marca direcciones como relocalizables o no relocalizables (absolutas).
- Identifica código que debe ser modificado como resultado de la localización.
- No son relocalizables: entrada/salida del sistema, rutinas del sistema.
- Si son relocalizables: Posiciones de memorias relativas a un .org.
Linker => Redefine las direcciones relocalizables a partir de la nueva dirección de origen.
## Carga de programa en memoria
El **loader** toma el programa del disco y lo carga en memoria principal
#### ¿En qué dirección de memoria?
- En ambientes multitarea la ram es compartida entre varios procesos
- El assembler no puede saber donde puede ser cargado
- El linker no puede saber donde puede ser cargado
Conclusión: El loader debe relocalizar todos los símbolos relocalizables.
### Linking & Loading
**Link-editor**:
- Produce una versión linkeada del programa que normalmente es guardada en archivo para ser ejecutada en otro momento.
**Relocating loader**:
- Linkea en tiempo de carga.
- Relocaliza y carga el programa en memoria para su ejecución.
**Linking loader**:
- Linkea en tiempo de carga.
- Relocaliza, busca automáticamente librerías, linkea y carga el programa en memoria para su ejecución.
**Linking Loader dinámico**:
- Linkea en **tiempo de ejecución**.
- Carga rutinas sólo cuando el programa las necesita.
- Utiliza *Dynamic Link Libraries* (dll).
![[Pasted image 20260213144540.png]]
### Archivos objeto
- **Archivo objeto relocateable**: código binario y datos en un formato que permite combinarlo con otros archivos objeto relocateables (linking).
- **Archivo objeto ejecutable**: código binario y datos en un formato que permite cargarlo directamente a memoria y ejecutarlo.
- **Archivo objeto compartido**: tipo especial de archivo objeto relocateable que puede ser cargado en memoria y vinculado dinámicamente.
