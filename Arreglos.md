---
id: 1745435574-arreglos
aliases:
  - arreglos
tags:
  - fundamentos
---

# Clase de Arreglos

## Repaso de tipo de datos

### Atómicas

- Enteros (int, long)
- Reales (float, double)
- Caracteres (char)
- Definidos por el usuario / Enumerados (enum)
- Booleanos (bool)

Son los tipos de datos con los que venimos trabajando

### Estructuradas

- Arreglos
    - Unidimensionales -> Se le suele llamar *vectores*
    - Multidimensionales -> Se le suele llamar *matrices*
- Cadena de caracteres
- Registros
- Tablas
- Archivos

## Arreglos Unidimensionales

Tienen dos caracteristicas

- Posicion (subíndice)
- Valor (tipo base) -> El tipo base **tiene que tener el mismo concepto (tipo)**

## Arreglos Multidimensionales

Comparte las mismas caracteristicas que los unidimensionales excepto que **puede tener varios subinidices**.

### Sintaxis de Arreglos

La declaración se hace de la siguiente manera:

```c
int vector[10]; // <tipo de dato> nombre[cantidad]
```

Para modificar el valor en una posición determinada se utiliza el **subindice**, por ejemplo:

```c
vector[1] = 6; // Cambiamos el valor de la posición 1, a 6
```

! IMPORTANTE: El subíndice puede ser **una variable**

Para inicializar el vector:

```c
int vector[10];
int i;

for (i = 0; i < 10; i++) {
    vector[i] = 0; // Inicializamos el vector en 0
}
```

Tambien se puede inicializar el vector al momento de declararlo:

```c
int vector[4] = {1, 2, 3, 4}; // Inicializamos el vector con los valores 1, 2, 3 y 4
```

### Pasaje de arreglos como paramétro

```c
#include <stdio.h>

void imprimirVector(int vec[], int tamanio) {
    printf("\nValores almacenados en el vecctor:\n");
    for (int i = 0; i < tamanio; i++) {
        printf("%d ", vec[i]);
    }
    printf("\n");
}

void modificarVector(int vec[], int tamanio) {
    for (int i = 0; i < tamanio; i++) {
        vec[i] = vec[i] * 2; // Multiplicamos cada elemento por 2
    }
}

int main() {
    int vector[] = {1,2,3,4,5};
    // Calculamos el tamaño del vector. El segundo sizeof va cambiando segun el tipo de dato de array o le podemos pasar vector[0]
    int tamanio = sizeof(vector) / sizeof(int); 

    imporimirVector(vector, tamanio); // Pasamos el vector como parámetro

    modificarVector(vector, tamanio); // vector equivale a &vector[0]

    return 0;
}
```

### Sintaxis de matrices

```c
#include <stdio.h>

#define FILAS 3
#define COLUMNAS 3

int main() {
    int matriz[FILAS][COLUMNAS]; // Declaramos una matriz de 3x3

    for (int i = 0; i < FiLAS; i++) {
        for (int j = 0; j < COLUMNAS; j++) {
            matriz[i][j] = i + j;
        }
    }

    printf("Matriz\n");
    for (int i = 0; i < FILAS; i++) {
        for (int j = 0; j < COLUMNAS; j++) {
            printf("%d ", matriz[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
