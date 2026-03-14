#flashcards
Jerarquía de memoria
?
1. Acceso directo (CPU, Caché).
2. Memoria RAM
3. Discos duros, sólidos, etc.
4. Fuentes de entrada (mouse, teclado, etc)

Limitaciones en el rendimiento del computador
?
Son las limitaciones que afectan el rendimiento general del computador y, por lo tanto, al tiempo que tarda el CPU en acceder a los datos en la memoria.
- *Latencia*: El tiempo necesario para que el CPU obtenga un dato de memoria o realice una escritura en esta. Es importante porque sin importar la velocidad del CPU, la memoria puede ser mas lenta en comparación
- *Ancho de banda*: Es la máxima cantidad de datos que puede ser transferida durante un acceso en memoria. Se mide en bits/segundo (mb/s, Gb/s). También es la capacidad de la memoria de realizar operaciones de lectura/escritura simultáneamente.

Tipos de memoria
?
- ROM: Es no volátil, solo puede leerse y no puede modificarse bajo condiciones normales
	- Tipos:
		- PROM
		- EPROM
		- EEPROM
- Memoria RAM: Almacena temporalmente los datos con los que el procesador está trabajando
- Memoria caché: Tipo de memoria cercano al CPU que es rápido y es utilizado para guardar las instrucciones más usadas por el procesador.

Tipos de memoria RAM
?
- *SRAM* (Static RAM): El contenido de cada posición de la memoria se mantiene en tanto se mantenga la alimentación eléctrica del circuito integrado. Es más rápida que la DRAM dado que no necesita ser refrescada.
- *DRAM* (Dynamic RAM): Más económica y grande que la SRAM, pero requiere un proceso constante de refresco ya que los capacitores, donde se guardan los bits, pierden la carga con el tiempo y necesitan refrescarse para evitar la péridida de datos.

¿Cómo se organiza la memoria RAM?::Se organiza en una matriz de celdas, y el acceso a estas celdas se realiza a través de decodificadores de direcciones
Organización "2-D"
?
- Un decodificador recibe la dirección y habilita solo la salida correspondiente
- Permite direccionar los registros dentro del microprocesador.

Estructura "2-1/2D":
?
- Circuitos integrados: líneas de dirección y datos.
- Decodificador de direcciones: filas y columnas.
El decodificador de fila activa una línea y todos los bits se leen simultáneamente. Luego del decodificador de columna selecciona el bit específico que pidió el usuario de la fila.
- Ventajas
	- Menor número de pines.
	- Menor tiempo de acceso de palabras sucesivas.
	- Los 8 bits correspondientes a una posición de memoria son seleccionados simultáneamente.

Arquitectura multibanco
?
- Un sólo módulo de memoria está conformado por varios chips.
- Todos los bits definen una dirección de memoria dentro del módulo y se dividen según:
	- Banco: Especifica cada chip.
	- Fila.
	- Columna.

¿Qué es el acceso entrelazado?::Es una forma de mejorar la eficiencia de la RAM, donde se lee 2 bits consecutivos de un banco de una memoria mientras el otro es accedido para refrescar la información. **Mejora el rendimiento** si las posiciones sucesivas están en bancos diferentes.

Criterios para reducir el tiempo de acceso:
?
1. Bancos entrelazados:
	- Utiliza la técnica de acceso a bancos alternados. Significa que mientras se accede a un banco de memoria, otro esta siendo refrescado.
	- Ventaja: Permite que el proceso de refresco no interfiera con los accesos a memoria, lo cual mejora el rendimiento cuando se accede a posiciones de memoria consecutivas almacenadas en bancos diferentes.
2. Mayor cantidad de bits leídos en paralelo (banda ancha):
	- Utilizar un buz de mayor ancho permite leer mas datos a la vez.
	- Ventaja: Incrementa la velocidad de acceso ya que se pueden transferir mas datos simultaneamente.
3. Mayor velocidad de clock (*SDRAM*):
	- La SDRAM (Synchronous Dynamic RAM) está sincronizada con el reloj del sistema y permite un acceso mas rápido.
	- Desventaja: Al aumentar la velocidad del reloj, esto consume mas potencia y puede provocar errores de almacenamiento de bits en la memoria.
4. Memoria DDR (*Double Data Rate*):
	- Con memoria DDR, se lee en flancos ascendentes y descendentes de reloj, lo que dobla la velocidad de acceso.
	- Ventaja: Aumenta el rendimiento sin tener que aumentar la velocidad del reloj, lo que mejora la estabilidad del sistema.

¿Qué es la memoria caché?::Es un tipo de memoria que es rápida y es utilizada para guardar las instrucciones más usadas por el procesador.

Características de la memoria caché:
?
- Niveles de memoria caché: L1, L2, L3 (mayor nivel => mas capacidad, mas lento).
- Principios de localidad:
	- **Localidad temporal**: Principio donde se propone que si un dato fue accedido recientemente, ese mismo dato es probable que se vuelva a acceder de nuevo en el corto plazo.
	- **Localidad espacial**: Principio donde se propone que si los datos cercanos a un dato accedido también son propensos a ser accedidos en el corto plazo.
- Electrónica, más rápida.
- Costosa y de menor tamaño
- Decodificación eficiente por menor cantidad de direcciones.
- Cercanía a la CPU => menor retraso en transferencias.

¿Cómo funciona la memoria caché?
?
- Verifica si el dato esta en la caché.
- Si no lo está, lo busca en la memoria principal y luego actualiza el caché almacenando este dato. Este proceso es conocido como *falla de caché*.

¿Qué es la asignación asociativa?
?
Es un tipo de asignación de memoria caché donde cualquier bloque de memoria principal puede asignarse a cualquier línea de la caché, optimizando el uso del espacio disponible.
- El usuario no necesita un mecanismo de conversión
- Campos de etiqueta y palabra: Se usan para identificar y localizar datos dentro de la caché. También se usan para la asignación de los bloques de la memoria principal.
- Bits de control:
	- Validez: Indica si la línea pertenece al programa en ejecución
	- Suciedad (*dirty bit*): Controla si un bloque modificado debe reescribirse en la memoria principal antes de ser reemplazado.

Ventajas y desventajas de la asignación asociativa:
?
Ventajas: Alta flexibilidad y búsqueda rápida mediante memorias asociativas.
Desventajas: Complejidad en la administración y control y decodificar que línea reemplazar es costoso.

¿Qué es la asignación directa?
?
Cada línea de memoria caché corresponde a un conjunto explícito de bloques de memoria principal
1. Memoria principal dividida en bloques de 32 palabras.
2. Caché con líneas específicas (ejemplo: 214 líneas).
3. Cada línea de caché puede almacenar uno de los 213 bloques posibles, identificado por un campo de etiqueta de 13 bits.
División de direcciones en Etiqueta, Linea (ubicada en caché) y Palabra.
Funciona similar a la asignación asociativa.

Ventajas y desventajas de asignación directa
?
Ventajas: menor complejidad y tamaño. No requiere búsqueda asociativa ya que el campo de línea dirige directamente la comparación.
Desventajas: Cuando varias referencias acceden a bloques que mapean en la misma línea, provoca fallas frecuentes.

Tipos de niveles de memoria caché
?
- L1
	- Ubicación: dentro del núcleo del CPU
	- Velocidad: Rápida
	- Propósito: Almacena datos e instrucciones de **uso inmediato**
- L2
	- Ubicación: cerca de los núcleos pero mas grande que L1
	- Velocidad: Mas lento que L1
	- Propósito: Almacenar instrucciones y datos usados en el corto plazo.
- L3
	- Ubicación: Compartida entre todos los núcleos del CPU
	- Velocidad: Mas lento que L2
	- Propósito: Almacena datos e instrucciones de uso frecuente que puede ser requerido x cualquier núcleo del procesador.

¿Qué es la memoria virtual?::Es una expansión de la memoria principal con almacenamiento en disco. Esto se logra mediante una gestión flexible de la memoria mediante esquemas de asignación complejos.
¿Cuál es el propósito de la memoria virtual?::Genera mayor capacidad de almacenamiento.

La memoria virtual permite que
?
el sistema operativo se cargue parte en la memoria principal y otra parte entre la memoria física y el disco.

¿Qué son las superposiciones de memoria?::Es un método para aumentar la capacidad de la memoria principal. Permite que un programa sobreescriba partes de su código en memoria con otras partes según sea necesario.

¿Cómo funcionan las superposiciones de memoria?
?
- La rutina principal actua como controlador, permaneciendo residente en memoria.
- Las subrutinas se cargan o descargan según las invoca la rutina principal.

¿Qué es la paginación?::Técnica de administración de memoria. Divide el espacio de direcciones en bloques llamado **páginas** (virtuales) y **marcos** (físicos) del mismo tamaño.

¿Qué sucede cuando hay una *falla de página*?
?
- Identificación: Se selecciona un marco para sobreescribir.
- Resguardo: Si el marco fue modificado, se guarda en memoria secundaria antes de sobreescribir para preservar los cambios.
- Carga: Se busca la página virtual requerida en memoria secundaria y se carga en el marco seleccionado.
- Actualización: La tabla de página se actualiza para reflejar la asignación de la nueva sección de memoria virtual al marco de memoria física.
- Continuación: El programa retoma su ejecución

¿De qué esta formada la tabla de páginas?
?
- Bit de presencia
- Dirección de disco
- Marco de página

Políticas y técnicas para optimizar el rendimiento de la caché:
?
- Lectura
	- Si están en caché, enviar a la CPU.
	- Si no, **carga inmediata**: Envia la palabra tan solo se llene la línea de caché
- Escritura
	- Están en caché
		- **Escritura inmediata**: Escribe datos en memoria principal y caché.
		- **Escritura diferida**: Escribe datos solo a la caché. Diferir escritura de memoria principal hasta haber limpiado el bloque
	- No están en caché
		- **Escritura con asignación**: Traer la línea a la memoria caché, luego actualizar.
		- **Escritura sin asignación**: Actualizar solo memoria principal.

¿Qué son las tasas de acierto?
?
El % de accesos en los que la memoria caché contiene la palabra requerida
$$\text{Tasa de acierto} = \frac{\text{n}^\circ \text{ de veces de la palabra en caché}}{\text{n}^\circ \text{ total de accesos a memoria}}$$

¿Qué es el tiempo efectivo de acceso (TEA)?
?
$$TEA = \frac{(\text{n}^\circ \text{ aciertos} \cdot \text{Tiempo por Acierto}) + (\text{n}^\circ \text{ fallas} \cdot \text{Tiempo por Falla})}{\text{n}^\circ \text{ total de accesos a memoria}}$$
- Las tasas altas no garantizan tiempos bajos si los fallos son costosos
- Los tiempos de transferencia de la memoria principal afectan de manera desproporcionada el rendimiento general => Fundamental reducir fallos en caché.

¿Cuál es la ventaja y desventaja de la memoria caché multinivel?
?
- Mejora el rendimiento al reducir los accesos a la memoria principal
- El costo de los fallos aumenta con el nivel de la caché.

¿Cómo se administra la memoria caché?
?
- El problema de la memoria caché es que los datos en algún momento quedan desactualizados o diferentes con la memoria principal.
- La solución son las políticas de escritura inmediata o control y las políticas de reemplazo (FIFO, LRU), las cuáles son esenciales para mantener la coherencia de los datos y maximizar el rendimiento del sistema.

¿Qué es la memoria entrelazada?::Técnica de diseño de memoria que divide la memoria principal en múltiples módulos independientes. Permite acceder a secciones de memoria simultáneamente, mejorando el rendimiento.

Funcionamiento de la memoria entrelazada
?
- Se descompone en módulos con accesos independientes.
- Uno de los elementos de diseño es el orden de entrelazado de las direcciones:
	- Orden superior: Las direcciones de memoria consecutivas se distribuyen entre los bancos de forma cíclica.
		- Ventaja: Ideal para acceso secuenciales
	- Orden inferior: Los bloques consecutivos de direcciones se asignan al mismo banco.
		- Ventaja: útil en patrones de acceso no secuenciales.

¿Qué es la segmentación?::Técnica de administración de memoria que divide el espacio de direcciones lógicas en bloques de tamaño variable llamados *segmentos*.

Traducción de direcciones en segmentos
?
1. El programa indica el n° de segmento
2. Se da una dirección relativa al inicio del segmento
3. El sistema operativo convierte la dirección segmentada a una física.

Características de la segmentación
?
- Cada segmento puede tener permisos específicos cómo:
	- Solo lectura
	- Solo ejecución
	- Lectura/escritura exclusiva para ciertos usuarios.
- Estos permisos protegen áreas de memoria
- *Asignación Dinámica*: No se reserva memoria física para un segmento hasta que se necesita => da más flexibilidad.

Paginación vs Segmentación
?
- Las páginas son de tamaño fijo, mientras que los segmentos son de tamaño variable
- El usuario no puede ver los límites de las páginas, mientras que si puede ver la de los segmentos
- El propósito de la paginación es la optimización de memoria y el acceso rápido a la información, mientras que la segmentación busca una organización lógica y protección de los datos.
- La paginación no distingue permisos por páginas, mientras que la segmentación permite asignar permisos por segmento.

¿Qué es la Fragmentación?::Ocurre cuando los programas se cargan y eliminan del sistema, dejando espacios libres no contiguos que dificultan la reutilización de la memoria.

Causas de la fragmentación
?
1. La memoria no se libera en bloques completos después de la ejecución de programas.
2. Los programas cargados tiene tamaños variables, dejando espacios sobrantes al asignar áreas de memoria.

Algoritmos para asignación de memoria:
- *First fit*:
	- Busca la primera área libre suficientemente grande para el programa
	- Ventaja: Rápido, pero genera más fragmentación al dejar espacios en áreas iniciales
- *Best fit*:
	- Busca el área libre que desperdicie menos espacio
	- Reduce la fragmentación, pero es más lento al evaluar todas las áreas libres.

¿Qué es el TLB?::El *Translation Lookaside Buffer* una memoria asociativa pequeña que guarda las traducciones más recientes de direcciones virtuales a físicas.
¿Qué solución provee el TLB?::Provee una solución a la hora de acceder a un valor en memoria en un sistema de memoria virtual. En general, se requieren al menos dos accesos para esto, lo cuál es lento.
¿Cuál es la solución que propone el TLB?
?
Propone que al generar el CPU una dirección virtual, se consulta el TLB para verificar si la traducción ya ha sido traducida.
- Si acierta => El sistema obtiene directamente la dirección física, acelerando el acceso.
- No acierta => Se procede normalmente y se actualiza el TLB con la nueva traducción.

Tipos de TLB
?
- TLB unificado:
	- Almacena instrucciones y datos en un mismo TLB
	- Ventaja: Simplicidad. Solo se necesita un único conjunto para almacenar ambos tipos de información.
- TLB dividido:
	- Divide el TLB en instrucciones y datos.
	- Ventajas:
		- Reducción de colisiones entre la traducción de instrucciones y datos
		- Mejora del paralelismo al hacerse las traducciones de direcciones para instrucciones y datos de manera independiente y simultánea.
- TLB totalmente asociativo:
	- Permite almacenar asignaciones en cualquier entrada del TLB, sin restricciones de lugar.
	- Ventaja: Flexible al poder utilizar una ubicación adecuada para cualquier traducción.
- TLB asociativo por conjuntos:
	- Lo divide en conjuntos con límites de entrada.
	- Ventaja: Ofrece flexibilidad y complejidad, optimizando el acceso mientras mantiene una estructura organizada.

¿Cómo funciona el TLB?
?
El TLB actúa como un intermediario entre la CPU y la memoria, acelerando el proceso de traducción.
1. Caché con direccionamiento virtual: CPU accede a caché. Si no encuentra los datos, consulta el TLB para ver si la traducción ya ha sido realizada.
2. Caché con direccionamiento físico: CPU consulta el TLB y luego la caché para obtener la dirección física.

Ventajas y desventajas del TLB
?
Ventajas:
- Reduce el tiempo de traducción
- Mejora el rendimiento general del sistema.
Desventajas:
- No puede almacenar todas las traducciones
- Posibilidad de *TLB thrashing* con patrones de acceso desfavorable.

¿Qué es el Buffering?::Espacio de memoria usado para guardar temporalmente datos mientras se están procesando o transfiriendo.
¿Cuál es el objetivo del Buffering?::Evitar que un programa o dispositivo quede sin datos durante transferencias irregulares o de distinta velocidad.

Principios básicos del Buffering
?
- Actuar como regulador de dispositivos de distintas velocidades
- Almacenamiento temporal para prevenir la pérdida de datos.
- Sincronizar la comunicación entre dispositivos asíncronos.

Tipos de buffering
?
- Unbuffed I/O:
	- Método simple y directo
	- Mayor riesgo de pérdida de datos
- Buffered I/O:
	- Mayor eficiencia en sistemas con operaciones de E/S frecuentes
	- Mayor uso de memoria y complejidad
- Double Buffering:
	- Dos buffers alternan en el almacenamiento de datos. Mientras uno se llena, otro se vacía. Ideal para gráficos, multimedia y procesador en tiempo real.
	- Ventaja: Mayor rendimiento, ya que el sistema nunca queda inactivo.
- Circular Buffer:
	- Se organiza como una estructura circular, lo que permite reutilizar el espacio de manera continua. 
	- Usando en sistemas de streaming, redes y procesamiento de señales.

¿Qué son las interrupciones?
?
- Eventos generados por hardware
- Asíncrona: No ocurre en puntos predecibles del código de usuario
- Pasiva: El controlador espera que suceda eventualmente.

¿Qué son las traps?
?
- Excepción en un proceso de usuario
- Sincrónica: Suspende el código de usuario y continua después.
- Activa: El código espera su ocurrencia y depende de ello.

Modelos de memoria
?
Los procesadores pueden organizar la memoria de diferentes formas dependiendo de cómo los núcleos acceden y comparten datos.
- Memoria uniforme (UMA): Todos los núcleos tienen acceso a la memoria principal con la misma latencia
- Memoria no uniforme (NUMA): La memoria está dividida en regiones, cada una cercana a un grupo de núceos.

Ventajas y Desventajas de procesadores multicore
?
Ventajas:
- Mayor rendimiento y eficacia
- Mejor multitarea
- Optimización de software moderno
- Mejor gestión energética
- Escalabilidad.
Desventajas:
- Dependencia de software
- Costos mas altos
- Consumo de energía en cargas altas
- Compatibilidad

Memoria en multicore
?
- **Memoria compartida**: Todos los núcleos comparten el acceso a la memoria RAM.
- **Memoria caché multinivel**: Los procesadores multicore utilizan caché de multinivel, lo que reduce la latencia.

¿Qué es la taxonomía de Flynn?::Se usa para clasificar la arquitectura de una computadora en función del flujo de datos y de instrucciones

Tipos de la taxonomía de Flynn
?
- SISD => Procesadores secuenciales convencionales que ejecutan una única instrucción en cada instante de tiempo sobre un único flujo de datos.
- SIMD => Varios procesadores ejecutan la misma instrucciones simultáneamente, pero cada uno trabaja sobre un flujo de datos diferentes.
- MISD => Varias unidades funcionales operan sobre un único flujo de datos aplicando distintas instrucciones
- MIMD: Procesadores independientes ejecutan distintas instrucciones sobre flujos de datos diferentes. Todos están coordinados para trabajar en un programa paralelo.