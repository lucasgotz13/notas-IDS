# Parciales

## Parcial 19/05/26

1. En Unix, una aplicación de usuario accede al hardware ejecutando directamente las instrucciones correspondientes, sin intervención del kernel => Falso, debido a que Unix utiliza el concepto de Ejecución Directa Limitada, donde los programas del usuario son ejecutados con derechos restringidos y para acceder al hardware necesitan permisos otorgados por el kernel.
2. Verdadero. El timer interrupt envía una excepción por hardware que obliga a saltar a un handler del kernel que desaloja al CPU del proceso
3. Verdadero. El registro donde se guarda la tabla de páginas se llama "satp" y es un puntero que apunta a esta.
4. Falso. El cambio de contexto requiere si o si de involucar al kernel, debido a que requiere de manipular estructuras de datos del sistema como la tabla de páginas del proceso, lo cuál requiere utilizar instrucciones privilegiadas que solo pueden ser ejecutadas por el kernel.
5. Falso. El CFS de Linux elige el proceso ejecutable con el menor vruntime ya que los procesos se ordenan en un arbol Red-Black donde el CFS selecciona la hoja mas a la izquierda del arbol, la cual contiene el proceso con menor vruntime
6. Falso. Cada vez que se hace un cambio de proceso, el TLB se limpia debido a que las direcciones virtuales del proceso pueden haberse visto modificadas en el proceso, por lo cuál utilizar su traducción podría darnos una dirección física errónea
7. Falso. En ese caso se debería utilizar el sleep-lock, ya que el spinlock hace que el procesador se quede esperando a que ocurra un evento, pero como solo hay un único procesador no existe ningún otro proceso corriendo que pueda sacar el lock.
8. Falso. La estructura que contiene el nombre del archivo como uno de sus campos es un Dentry. 
9. 
10. 
	1. Raiz
	2. d
	3. Tres
	4. Raiz
	5. a
	6. uno


Ejercicio 9:
Direcciones virtuales: 10 bits primera tabla, 10 bits segunda tabla, 12 bits offset
Cada directorio tiene 1024 page table
Cada page table tiene 1024 paginas
Codigo: 2 paginas
Heap: 2 paginas
Stack: 2 paginas
Pagina directorio: 1 pagina
total = 7
kb = 7 x 4 = 28kb
## Parcial 1c2025 (espina)
Ejercicio 9:
Cada bloque => 4kb de almacenamiento
1 archivo = 1 bloque de almacenamiento
Cada archivo => inodo que contiene:
- 12 punteros directos
- 1 puntero indirecto simple
- 1 puntero indirecto doble
- 1 puntero indirecto triple
En un bloque de punteros, cada puntero ocupa 4 bytes.

Bloque de punteros = 4096 / 4 = 1024 punteros en un bloque

## Parcial 1c2025 (mendez)
Array de bytes de 64KB
dir 0x00402000
Página de 4KB
2 niveles de tablas de páginas