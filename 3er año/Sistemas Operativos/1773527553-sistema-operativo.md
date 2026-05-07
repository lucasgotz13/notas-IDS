---
id: 1773527553-sistema-operativo
aliases:
  - sistema-operativo
tags:
  - sistemas
---

# sistema-operativo
## Sistema Operativo

**¿Qué hace un sistema operativo?**

- **Compartir hardware:** Múltiples programas usan la misma CPU, memoria y dispositivos simultáneamente.
- **Abstraer hardware:** Un procesador de texto no necesita saber qué disco duro está instalado.
- **Comunicación controlada.**
### El diseño de la interfaz

- **Problema:** $\rightarrow$ El SO quiere ser simple y reducido pero las aplicaciones quieren potencia.
- **Solución:** $\rightarrow$ Diseñar interfaces basadas en pocos mecanismos ortogonales que se combinen con gran generabilidad.
    - $\hookrightarrow$ _Unix y xv6 lo lograron._

### Kernel y los Procesos
```
Proceso A      Proc. B      Proc. C      Shell (Proc. D)
      \             |            |             /
       \            |            |            /
        \---------- | ---------- | ----------/
                    ↓
        Kernel (Espacio privilegiado)   <--- [Llamadas al sistema (Syscalls)]
        - Único, gestiona los procesos
                    ↓
                 Hardware
```
### Memoria y Llamadas al Sistema
- Cualquier programa, excepto el kernel, se ejecuta en modo usuario.
```
[ Espacio del Proceso ]                 [ Kernel ]
|---------------------|                 |---------|
| stack      ↓        |                 |         |
|---------------------|                 |         |
| ///////////////     |---------------->|   PCB   | (Process Control Block)
|---------------------|                 |         |
| heap       ↑        |                 |---------|
|---------------------|                  Process ID
| data (Variables)    |
|---------------------|
| text (Código)       |
|---------------------|
```
- Llamada al sistema
[[Drawing 2026-03-14 19.37.05.excalidraw|Ilustración]]

### El Shell de xv6

**¿Por qué importa?**

El Shell es un programa ordinario de usuario.
- $\hookrightarrow$ Demuestra el poder de la interfaz.
- $\hookrightarrow$ Es reemplazable (bash, zsh, etc.).

**Bucle Principal del Shell**

1. `getcmd()` - leer línea de usuario.    
2. `fork()` - crear proceso hijo. 
3. _(hijo)_ `exec()` - ejecutar comando. 
4. _(padre)_ `wait()` - esperar al hijo. 

## Procesos y Memoria

Todo proceso tiene un **file descriptor**:
$\hookrightarrow$ Un entero pequeño que representa un objeto de E/S gestionado por el kernel.
### **Tabla de FDs del Proceso**

| FD  | Nombre   | ==>              |
| --- | -------- | ---------------- |
| 0   | stdin    | Consola          |
| 1   | stdout   | Archivo en disco |
| 2   | stderr   | Mensaje de error |
| 3+  | archivos | Tubería (pipe)   |
#### La abstracción
Archivos, tuberías y dispositivos se ven igual: **flujos de bytes**. 
Un programa no necesita saber a qué está conectado.

Todos los comandos de Linux leen de '0' y escriben en '1'.

`dup()` => Duplicar descriptores de archivo
```
Fd = 1 (stdout)      \
                      ---> Objeto de archivo compartido (OFFSET COMPARTIDO)
Fd = 3 (dup del 1)   /
```

## Tuberías (pipes)
Un pipe es un buffer que tiene un Fd de entrada y un Fd de salida.
### Esquema de un pipe
```
[ Kernel ]
                   |
             |-----------|
   Fd in --->|  Buffer   |---> Fd out
             |-----------|
                   |

Ejemplo: 
[ CMD 1 ] ---------------> [ CMD 2 ]
(Proceso Escritor)         (Proceso Lector)

ls | grep ".txt"  (por ejemplo)
```