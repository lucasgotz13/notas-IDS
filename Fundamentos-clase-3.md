---
id: 1744227104-fundamentos-clase-3
aliases:
  - fundamentos-clase-3
tags:
  - fundamentos
---
# fundamentos-clase-3
## Memoria: Métricas

- **Capacidad de almacenamiento**: en bytes o múltiplos de bytes (KB, MB, GB, TB).
- **Tiempo de acceso**: en segundos o submúltiplos. (ns, ms)
- **Velocidad de transferencia**: en bytes por segundo o múltiplos (KB/s, MB/s).
- **Consumo de energía**: en Watts
- **Tamaño físico**: en cm³ 

## Unidades de almacenamiento
- El *bit* es la unidad mínima de almacenamiento. Esta formada por un 0 o un 1.
- Un *byte* es una unidad de información formada por una secuencia de 8 bits.
- Para representarlo se utiliza la letra B (mayúscula).

## Punteros
Las variables en C tienen 4 elementos que hay que tener presente:
- El nombre
- El tipo
- El valor
- La *dirección de memoria*

### Punteros en C

```c
#include <stdio.h>
#include <stdlib.h>

int main() { 
    int edad;
    int* p1;

    edad = 12;

    printf("edad = %d\n", edad); // 12

    p1 = &edad; 

    printf("p1 = %p\n", p1); // Dirección de memoria de edad

    *p1 = 15;
    
    printf("edad = %d\n", edad); // 15
}
```
