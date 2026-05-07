---
id: 1743019400-fundamentos-segunda-clase
aliases:
  - fundamentos segunda clase
tags:
  - fundamentos
---

# fundamentos segunda clase

### Mostrar valor de una variable

```c
printf("%i", edad) // entero en base 10 con signo (int)
printf("%d", edad) // entero en base 10 con signo (int)
printf("%f", pi) // Coma flotante decimal de precisión simple (float)
printf("%.2f") // float con dos decimales
printf("%c", caracter) // caracter (char)
printf("%s", nombre) // cadena de caracteres (string)
```

### Solicitar el valor de una variable

```c
// scanf(tipo, &variable)
scanf("%i", &edad)
```

### Ciclo for

```c
int i; // Por buenas prácticas, se declara la variable i afuera del ciclo

for (i = 0; i < 10; i++) {
  printf("%i", i)
}
```
