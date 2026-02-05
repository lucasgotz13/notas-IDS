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
# Conexionado tipo bus
Si bien el modelo Von Neumann sigue vigente, este fue modernizado debido a que se necesitaba reducir la cantidad de conexiones entre el CPU y sus subsistemas
Para mejorar el tema del conexionado de esta arquitectura, las computadoras comenzaron a utilizar el sistema de interconexión a través del **bus del sistema**. En lugar de tener caminos de comunicación diferentes con la memoria y otros dispositivos, la CPU se interconecta con estos a través del bus del sistema.
Este modelo considera que el sistema de computación esta constituido por tres subconjuntos:
- La **CPU** (La combinación de la ALU y la unidad de control)
- La memoria
- La entrada-salida (combinadas en un solo conjunto)
Lo más importante de este modelo es la forma en que se realizan las comunicaciones entre los componentes por medio del bus del sistema, el cuál está constituido por tres tipos distintos de buses:
- **Bus de datos** => Transporta la información
- **Bus de direcciones** => Determina hacia donde está siendo enviada dicha información
- **Bus de control** => Describe aspectos de la forma en que se está llevando a cabo la mencionada transferencia de información
Los buses están constituidos por conjuntos de cables agrupados de acuerdo a su función.
Un bus de datos de 32 bits contiene 32 cables individuales, donde cada uno transporta **un bit de datos**

![[Pasted image 20260202173238.png]]

No todos los componentes del sistema se conectan de la misma manera al bus. La CPU, por ejemplo, genera las direcciones que viajan a través del bus de direcciones, mientras que la memoria recibe esas direcciones. La memoria nunca genera direcciones, así que la CPU nunca recibe direcciones, por lo cuál no hay interconexión en ese sentido.

Cuando el bus tiene que ser compartido por varios elementos que se comunican entre sí, se debe poder distinguir a estos, lo cuál se logra utilizando **direcciones**.
## Dirección de memoria
La dirección de memoria identifica una celda de memoria en la que se almacena información (se puede pensar como una dirección postal en la cual una persona recibe o envía correos). Durante una operación de lectura o escritura, el bus de direcciones contiene la dirección a la cuál debe leerse o escribirse el dato. Luego, el bus de datos contiene el dato a leerse o escribirse por el CPU

# Memoria
La memoria de una computadora consiste en un **conjunto de registros numerados (direccionados)** en forma consecutiva, en los cuales normalmente se almacena un **byte** de información (conjunto de 8 bits).
Dependiendo el tipo de arquitectura, el tamaño de las **palabras** varían (en general entre 16, 32, 64 y 128 bits).
Es habitual que las máquinas puedan leer palabras de más de un byte, las cuales se almacenan en la memoria como una **secuencia de bytes**, y se direccionan a partir del byte menos significativo de la palabra almacenada. 
Para almacenar este tipos de palabras, existen dos alternativas:
- *Big Endian* => Se almacena el byte mas significativo en la dirección **mas baja** de la memoria
- *Little Endian* => Se almacena el byte menos significativo en la dirección mas baja de memoria

## Estructura
Consiste en un arreglo lineal de las diversas locaciones ordenadas en forma consecutiva.
![[Pasted image 20260202180446.png]]
Cada una de las direcciones identificadas con un valor numérico se corresponde con una palabra específica almacenada en la misma. Este número se define como su **dirección**.
La dirección mas alta corresponde a una unidad menos que el tamaño de la memoria. En el caso de un sistema de 32 bits, la última dirección es 2³² - 1, mientras que la primera dirección es 0.

El modelo de memoria utilizado en estos sistemas es el siguiente:
![[Pasted image 20260202180718.png]]

El espacio de direcciones de la arquitectura en este ejemplo esta dividido en diferentes sectores, lo que se denomina **mapa de memoria**. Estos mapas pueden diferir entre una implementación y otra, lo cuál lleva a que algunos programas compilados para el mismo tipo de procesador puedan no ser compatibles entre sistemas.