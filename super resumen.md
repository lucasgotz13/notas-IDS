
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