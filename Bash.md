---
id: 1742336685-bash
aliases:
  - bash
tags:
  - intro-desarrollo
---

# Bash

## ¿Qué es Bash?
Bash (Bourne-again shell) es un **Intérprete de comandos** y un **lenguaje de scripting**
- #### **Intérprete de comandos**
	- Es un programa que lee y ejecuta comandos ingresados por el usuario
	- Permite la **entrada de comandos**, **procesamiento de comandos**, **ejecución del comando** y **retorno de resultados**

#### Stdin, stdout, stderror
- stdin (Standard Input)
	- Es el flujo a través del cual los comandos **reciben datos**
	- El stdin en general proviene del teclado, pero podemos usar archivos o otros comandos para redirigir la entrada al stdin.
- stdout (Standard output)
	- Es el flujo a través del cual los comandos **envían datos** que se **muestran al usuario**
	- Podemos redirigir el output usando '1>'. Ejemplo: cat archivo.txt 1> output.txt
- stderror (Standard error)
	- Es el flujo a través del cual los comandos **envían mensajes de error**
	- Podemos redireccionar el error a un archivo usando '2>'. Ejemplo: ls 2> output.txt


## Comandos Básicos de terminal

#### ls
- Muestra los archivos del directorio actual
- **Flags**
	- -a --> Muestra los archivos ocultos
	- -l --> Muestra los permisos de cada archivo
	- -lrt --> Muestra los permisos, el usuario que tiene el *ownership* del archivo (a quien le pertenece), el *grupo* (Conjunto de usuarios que tienen los mismos permisos)
#### cat
- Muestra el contenido de un archivo (Lee el archivo y lo manda al stdout)
- Se puede mandar el output a otro archivo. Ejemplo: cat helloWorld.txt > output.txt
	- Usando solo '>' reescribe el archivo output.txt
	- Usando '>>' lo añade al final del archivo.
#### wc (Word Count)
- Se utiliza para contar las palabras, letras, etc de un archivo
- Flags:
	- `wc -w`: Cuenta las palabras de tal archivo
	- `wc -l`: Cuenta la cantidad de filas
- Ejemplos:
	- `cat output.txt | wc -w`: Esto va a contar las palabras del archivo output.txt
	- `ls | wc -l`:  Va a contar la cantidad de filas del ls
#### Head
- Muestra las líneas de un archivo
- Ejemplos
	- `head output.txt`: Va a mostrar las primeras 10 líneas 
	- `head -n 3 output.txt`: Va a mostar las primeras 3 líneas

#### TAIL
- Lo mismo que el HEAD pero desde las últimas lineas
- Flags:
	- -f: Muestra en tiempo real las nuevas líneas añadidas al archivo.

#### GREP
- Busca y muestra líneas que coinciden con un patrón de texto.
- Utiliza regex como patrón.
- `grep [opciones] [patron] [archivo]`
- Flags:
	- -i: Ignora mayúsculas y minúsculas.
	- -r: Realiza la búsqueda de manera recursiva en directorios.
	- -v: Muestra las líneas que NO coinciden con el patrón.
	- -E: Permite el uso de expresiones regulares extendidas
	- -l: Muestra solo el nombre de los archivos.
	- -o: Muestra solo las coincidencias

#### sed
- Herramienta para procesar y manipular texto
- `sed [script] [archivo]`
- Lo usamos para buscar y reemplazar, a diferencia de grep.
- flags:
	- -i: Modifica el archivo
	- -e: Concatena operaciones
	- -r: Usa expresiones regulares extendidas
	- Nd: Elimina la N-ésima línea
	- /patron/d: Elimina las líneas que matchean
	- /patron/p: Imprime las líneas que coinciden
	- s/patron/reemplazo/g: Aplica la sustitución en todas las coincidencias
	- s/patron/reemplazo/l: Ignora el ase

```bash
# Este es un ejemplo de una suma
num1=1
num2=1
resultado=$(($num1 + $num2))
echo $resultado
```

### Funciones

```bash
function nombre() {
  NOMBRE=$1 # el $1 es el primer parámetro que se le pase a la función
  echo "Hola $NOMBRE"
}
nombre "Marcos" # Así se llama a una función
```

```bash
# Verificar si una variable esta vacía
if [ -z "$1"]; then
  echo "Pasame un valor"
  exit 1
fi
```

### Importar funciones de otro archivo

```bash
# Así se importan funciones de otro archivo 
source ./script.sh  

funcion_de_otro_archivo # Llamo a la función
```
---
## Preguntas

#bash
#bash/que-es-bash
¿Qué es Bash?::Es un intérprete de comandos y un lenguaje de scripting que lee y ejecuta órdenes ingresadas por el usuario.
¿Qué rol cumple stdin en Bash?::Es el flujo de entrada por el que los comandos reciben datos; por defecto proviene del teclado, pero puede redirigirse desde archivos o la salida de otros comandos.
¿Qué rol cumple stdout en Bash?::Es el flujo de salida estándar donde los comandos envían sus resultados; puede redirigirse a archivos usando `1>`.
¿Qué rol cumple stderr en Bash?::Es el flujo de error estándar donde los comandos envían mensajes de error; puede redirigirse a archivos usando `2>`.
¿En qué consiste la ejecución de un comando en Bash?::Una vez interpretado, Bash envía la instrucción al sistema operativo para que la lleve a cabo; el SO realiza la acción solicitada.
¿Cómo devuelve Bash los resultados de la operación?::Tras la ejecución, Bash muestra el output en la terminal: si fue exitoso, verás el resultado esperado; si hubo errores, aparecerá un mensaje de error.
#bash/comandos
¿Cómo listamos archivos ocultos y con detalles en un directorio?::Con `ls -al` (o `ls -a -l`), donde `-a` muestra también los archivos ocultos y `-l` muestra permisos, propietario y grupo.
¿Cómo mostramos el contenido de un archivo y redirigimos la salida a otro?::Reescribir: `cat archivo.txt > salida.txt`  |  Añadir al final: `cat archivo.txt >> salida.txt`
¿Para qué sirve el comando wc y cuáles son sus flags más comunes?::Cuenta líneas, palabras o bytes de un archivo.  `wc -l` → líneas; `wc -w` → palabras
¿Cómo ver las primeras 10 líneas de un archivo? ¿Y las primeras 3?::Primeras 10 líneas: `head archivo.txt`  |  Primeras 3 líneas: `head -n 3 archivo.txt`
¿Cómo ver las últimas líneas de un archivo en tiempo real?::Con `tail -f archivo.txt`, que muestra las últimas líneas y observa nuevas adiciones.
¿Qué hace grep -i -r -v "patrón" .?::Busca recursivamente (`-r`) en el directorio actual líneas que no coinciden con “patrón” (`-v`), ignorando mayúsculas/minúsculas (`-i`).
¿Para qué sirve sed 's/viejo/nuevo/g' archivo?::Reemplaza todas (`g`) las ocurrencias de “viejo” por “nuevo” en la salida (sin modificar el archivo a menos que uses `-i`).
¿Cómo inicia Bash una sesión y recibe tus comandos?::Al abrir una terminal, se inicia una sesión de Bash donde escribís comandos que el intérprete lee línea por línea (por ejemplo `ls` o `cd`).
¿Qué sucede durante el procesamiento de comandos en Bash?::Bash interpreta tu comando y lo traduce en acciones que el sistema operativo puede ejecutar (por ejemplo `mkdir nueva_carpeta` se convierte en “crear un directorio llamado nueva_carpeta”).
