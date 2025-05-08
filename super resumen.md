
#superquiz

#superquiz/bash
### 🔧 BASH

¿Qué comando muestra el directorio actual?::`pwd`

¿Cómo cambias de directorio en Bash?::Con `cd <ruta>`, por ejemplo `cd /home/usuario`

¿Qué comando lista archivos incluyendo ocultos?::`ls -a`

¿Cómo se crea un archivo vacío?::Con `touch archivo.txt`

¿Qué comando elimina una carpeta con su contenido?::`rm -r carpeta`

¿Qué hace `chmod +x script.sh`?::Da permiso de ejecución al archivo `script.sh`

¿Cómo se cambia el propietario de un archivo?::Con `chown usuario:grupo archivo`

¿Qué hace `wc -l archivo.txt`?::Muestra el número de líneas del archivo

¿Para qué se usa `grep`?::Para buscar texto dentro de archivos

¿Qué hace `sed -i 's/viejo/nuevo/g' archivo`?::Reemplaza todas las ocurrencias de “viejo” por “nuevo” en el archivo

¿Qué hace la redirección `>` y `>>`?::`>` sobrescribe; `>>` agrega al final

¿Qué hace la tubería `|`?::Conecta la salida de un comando con la entrada de otro

---

### 🔍 Expresiones Regulares (Regex)
#superquiz/regex

¿Qué hace el símbolo `^` en una regex?::Coincide con el **inicio de línea**

¿Para qué sirve `$` en regex?::Coincide con el **final de línea**

¿Qué hace `\b` en regex?::Indica **límite de palabra**

¿Qué matchea `[a-z]`?::Cualquier letra minúscula

¿Qué hace `\d{3}-\d{2}-\d{4}`?::Coincide con formato tipo “123-45-6789”

¿Qué hace `+`, `*`, `?` en regex?::`+`: uno o más, `*`: cero o más, `?`: cero o uno

¿Qué hace `|` en regex?::Actúa como **“o”** lógico (alternancia)

¿Cómo buscar palabras que terminan con “fin”?::`grep 'fin$' archivo.txt`

---

### 🐳 Docker
#superquiz/docker

¿Qué hace `docker run`?::Crea y ejecuta un contenedor desde una imagen

¿Cómo se lista los contenedores activos?::Con `docker ps`, y `docker ps -a` muestra todos

¿Qué hace `docker build -t imagen:v1 .`?::Crea una imagen desde un Dockerfile

¿Qué define un Dockerfile?::Instrucciones para construir una imagen

¿Qué hace `docker-compose up -d`?::Levanta servicios definidos en `docker-compose.yml` en segundo plano

¿Qué significa `ports: - "9000:3000"` en docker-compose?::Mapea el puerto 9000 del **host** al 3000 del **contenedor**

---

### 🧬 Git

#superquiz/git

¿Qué comando inicia un repositorio Git?::`git init`

¿Cómo se clona un repositorio remoto?::`git clone <url>`

¿Qué hace `git add <archivo>`?::Agrega el archivo al área de staging

¿Para qué sirve `git commit -m "mensaje"`?::Crea un commit con los cambios preparados

¿Cómo enviar cambios al repositorio remoto?::Con `git push`

¿Cómo traer cambios del repositorio remoto?::Con `git pull`

¿Qué hace `git branch <nombre>`?::Crea una nueva rama

¿Cómo fusionar ramas?::Con `git merge <rama>`

¿Qué comando muestra el historial de commits?::`git log`

---

### 🛠️ Ingeniería de Software

#superquiz/ingenieria-de-software

¿Qué es el modelo en cascada?::Un enfoque **lineal y secuencial** donde se completa una fase antes de pasar a la siguiente

¿Qué es una metodología ágil?::Un enfoque **iterativo e incremental** con entregas frecuentes y feedback continuo

¿Cuáles son las fases típicas del ciclo de vida del software?::Requerimientos → Diseño → Implementación → Pruebas → Mantenimiento

¿Qué es un requerimiento funcional?::Lo que el sistema **debe hacer**

¿Qué es un requerimiento no funcional?::Cómo debe comportarse (rendimiento, usabilidad, seguridad)

---

### 🐧 Linux

#superquiz/linux

¿Qué es Linux?::El **kernel** del sistema operativo; junto a GNU forma GNU/Linux

¿Cómo se estructura el sistema de archivos en Linux?::Con un **único árbol jerárquico** desde `/`

¿Qué diferencia hay con Windows en cuanto a estructura de archivos?::Linux no usa unidades como C:, sino un único sistema jerárquico

¿Qué significa `.` y `..` en rutas relativas?::`.` es el directorio actual, `..` es el directorio padre

¿Qué significa POSIX?::Un estándar que asegura la **compatibilidad entre sistemas Unix-like**

---

### 🗃️ SQL / Bases de Datos

#superquiz/sql

¿Qué hace `SELECT` en SQL?::Consulta y recupera datos

¿Qué hace `INSERT INTO`?::Inserta un nuevo registro en una tabla

¿Qué hace `UPDATE`?::Modifica registros existentes

¿Qué hace `DELETE`?::Elimina registros

¿Qué significa que SQL es declarativo?::Se especifica **qué se quiere obtener**, no cómo hacerlo

¿Qué hace un `JOIN`?::Combina datos de dos o más tablas relacionadas

¿Qué función tiene `GROUP BY`?::Agrupa filas para aplicar funciones agregadas como `COUNT()`, `AVG()`, etc.

#superquiz/supersuper
### 🐚 **Bash**

¿Qué es Bash?::Un lenguaje de programación y un lenguaje de scripting completo (.sh), y también una shell que interactúa con el usuario mediante comandos en la terminal.

La shell es lo opuesto al kernel, ¿qué hace el kernel?::El kernel administra el software y trabaja internamente.

¿Cuáles son los tres flujos principales en Bash?::standard in (0), standard out (1) y standard error (2).

¿Qué comando se utiliza para pasar el contenido de 'archivo1' a 'archivo2', sobrescribiendo 'archivo2' si ya existe?::cat archivo1 > archivo2

¿Cómo agregar contenido de 'archivo1' a 'archivo2' sin borrar lo existente?::cat archivo1 >> archivo2

¿Qué hace el comando 'touch archivo.txt'?::Crea un archivo vacío llamado archivo.txt (o actualiza su timestamp si ya existe).

¿Para qué sirve `mkdir`?::Para crear **directorios**.

En Bash, ¿para qué sirve el símbolo `$`?::Para acceder al valor de las **variables de entorno**.

¿Qué hace `cd $HOME`?::Te lleva al directorio **home** del usuario.

¿Qué hace el pipe `|` en Bash?::Concatenar comandos, la salida estándar del primer comando se convierte en la entrada estándar del segundo.

Ejemplo de uso de pipe con grep: ls -l | grep "txt"::Muestra las líneas del listado largo que contienen la cadena "txt".

¿Qué significa `#!/bin/bash` al inicio de un script?::Indica al sistema operativo que el script debe ejecutarse usando Bash.

¿Cómo hacer un script ejecutable?::Con el comando `chmod +x archivo.sh`.

En un script de Bash, ¿qué significa `$1`?::Se refiere al **primer argumento** pasado al script.

Sintaxis básica de un condicional `if` en Bash?
?
if [ condición ]; then 
	código
elif [ otra_condición ]; then 
	código 
else 
	código 
fi

¿Qué hace `eq` en Bash?::Comparar si dos valores son **iguales**.

¿Cómo declarar un arreglo en Bash?::mi_vector=("nombre1" "nombre2")

¿Cómo acceder al primer elemento de un arreglo?::${mi_vector[0]}

¿Cómo obtener todos los elementos de un arreglo?::${mi_vector[@]}

¿Qué hace `ln -s archivo_original.txt enlace.txt`?::Crea un **enlace simbólico** llamado enlace.txt que apunta a archivo_original.txt.

¿Qué hace `wc -l archivo.txt`?::Cuenta las **líneas** del archivo.

---

### 🧬 **Git**

¿Qué es Git?::Un sistema de manejo de versiones.

---

### 🏗️ **Ingeniería de Software**

¿Cuál es una característica clave de un buen software?::Que sea **mantenible** en el tiempo, evitando código ilegible o espagueti.

¿Cuáles son las 5 etapas principales de la Ingeniería de Software?::

1. Análisis de Requerimientos
    
2. Diseño
    
3. Implementación
    
4. Testing y validación
    
5. Despliegue (y Mantenimiento)
    

---

### 🐳 **Docker**

¿Qué es un proceso en un sistema operativo?::Todo lo que está corriendo en el sistema operativo, consumiendo recursos como CPU, GPU y memoria.

¿Por qué Docker es una "máquina virtual minimalista"?::Porque corre sobre el sistema operativo anfitrión como un proceso más, permitiendo ejecutar aplicaciones aisladas (contenedores) con sus dependencias.

¿Qué es una Imagen en Docker?::La definición de qué necesita un contenedor para correr.

¿Qué es un Contenedor en Docker?::Una instancia en ejecución de una imagen.

¿Qué es un Dockerfile?::Un archivo de texto estándar y declarativo que contiene instrucciones para construir una imagen Docker.

¿Para qué sirven los volúmenes en Docker?::Para almacenar datos fuera de los contenedores, permitiendo la **persistencia de información**.

¿Qué es Docker Compose?::Una herramienta que simplifica la gestión de aplicaciones Docker de **múltiples contenedores**, definiéndolos en un archivo YAML.

Comando para mostrar las imágenes Docker descargadas::docker images

Comando para mostrar los contenedores Docker activos::docker ps

¿Cómo ver los logs de un contenedor en tiempo real?::docker logs -f <CONTAINER ID>

¿Qué hace `docker exec -it <ID_contenedor> bash`?::Ejecuta **interactivamente bash dentro de un contenedor en ejecución**.

¿Qué hace `FROM node:22-alpine` en un Dockerfile?::Especifica la **imagen base** sobre la cual se construirá la nueva imagen.

¿Qué hace `WORKDIR /app` en un Dockerfile?::Define el **directorio de trabajo** dentro del contenedor para los comandos subsecuentes.

¿Cuál es la diferencia entre RUN y CMD en un Dockerfile?::RUN ejecuta comandos al **construir** la imagen; CMD especifica el comando que se ejecutará cuando el contenedor **inicie**.

¿Cómo construir una imagen llamada 'mi_app' desde un Dockerfile en el directorio actual?::docker build -t mi_app .

¿Qué hace `docker stop $(docker ps -q)`?::Detiene **todos los contenedores en ejecución**.

---

### 🗃️ **SQL**

¿Qué significa SQL?::Structured Query Language.

¿Cómo crear una tabla 'clientes' con columnas id (INT), nombre (VARCHAR(50)) y apellido (VARCHAR(50))?::CREATE TABLE clientes (id INT, nombre VARCHAR(50), apellido VARCHAR(50));

¿Cómo insertar un cliente en la tabla 'clientes' con id=1, nombre='Juan', apellido='Pérez'?::INSERT INTO clientes (id, nombre, apellido) VALUES (1, 'Juan', 'Pérez');

¿Para qué sirve la cláusula WHERE?::Para **filtrar los resultados** según una condición.

¿Qué es una PRIMARY KEY en SQL?::Un atributo que asegura valores **únicos** en una columna.

¿Para qué se usa COUNT(*) en SQL?::Para **contar el número de filas** que cumplen una condición.

¿Para qué sirve GROUP BY en SQL?::Para **agrupar filas** con los mismos valores en una o más columnas.

¿Para qué sirve HAVING en SQL?::Para **filtrar los grupos** después de aplicar GROUP BY.

¿Qué devuelve un INNER JOIN?::Solo las filas donde hay una **coincidencia en ambas tablas**.

¿Qué devuelve un LEFT JOIN?::Todas las filas de la tabla de la **izquierda** y las coincidentes de la derecha; NULL si no hay coincidencia.