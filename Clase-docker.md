---
id: 1744767684-clase-docker
aliases:
  - clase-docker
tags:
  - intro-desarrollo
---
#intro-desarrollo 
# Docker
### ¿Para qué Docker?
Permite correr tu aplicación siempre **en un mismo entorno**
### ¿Qué contiene una imagen?
- OS -> La distribución de linux, windows o Mac
- Software -> Lo que va a **permitir** que **corra nuestra aplicación**
- App -> El código de la aplicación.
### ¿Cómo se generan las imagenes?
- A través de un *dockerfile*
	- Es un archivo que contiene una serie de instrucciones que **indican** cómo crear una imagen
- Luego para generar la imagen se corre en la terminal, en el directorio donde esta el dockerfile, el comando: `docker build`
### ¿Que es un contenedor?
Un **contenedor** va a *correr* una imagen
### Ejemplo de *dockerfile*

```dockerfile

FROM node:12.22.1-alpine3.11
# /app -> Donde vamos a hacer todo nuestro trabajo. 
# Todos los comandos se van a correr dentro de este directorio.
WORKDIR /app
# El primer punto va a copiar todos los archivos
# que estan en el directorio '/app' en la imagen
COPY . .
# Va a compilar todo el codigo de node
RUN yarn install --production

# SIEMPRE hay que especificar el comando que vaya a correr
CMD ["node", "/app/src/index.js"]
```

### Volumenes
Forma con la cual podemos crear persistencia en nuestro contenedor.

### docker-compose
Docker compose es una forma fácil de **escribir las líneas de docker run** con el objetivo de **facilitar la administración de estas líneas**.

Ejemplo:
```yaml
# docker-compose.yaml
version: "3.7" # la versión de la sintaxis del archivo YAML
# Acá declaramos los servicios que queremos correr dentro del docker compose.
# Nos va a permitir correr varios contenedores en un mismo archivo y meterlos en la misma red.
services:
# primer contenedor
	app:
		image: pablokbs/getting-started:v1
		ports:
			- 3000:3000
		environment:
			MYSQL_HOST: mysql
			MYSQl_USER: root
			MYSQL_PASSWORD: secret
			MYSQL_db: todos
# segundo contenedor
	mysql:
		image: mysql:5.7
		volumes:
			- ./todo-sql-data:/var/lib/mysql
		environment:
			MYSQL_ROOT_PASSWORD: secret
			MYSQL_DATABASE: todos
```

## Comandos de docker

- `docker run 'nombre-contenedor'` -> **Corre el contenedor**. Si no existe localmente pero existe en **docker-hub**, lo descarga. 
    - `docker run -dp port:port 'contenedor'` -> Corre el contenedor **en segundo plano**. `-d`: detached, `-p`: puerto. 
        - El `-p` va a **exponer el puerto de nuestro internet** y lo va a **redireccionar al puerto del contenedor** (`port_internet:port_contenedor`) 
- `docker pull` -> **Descarga** la imagen. 
- `docker images` -> **Muestra las imágenes** que se crearon/descargaron. 
- `docker ps` -> **Muestra los contenedores** que están corriendo. 
    - `docker ps -a` -> Muestra todos los contenedores que **estan corriendo o no**. 
- `docker logs 'id'` -> **Muestra los logs** de un contenedor. Siempre devuelve `stdout` y `stderr`. 
- `docker exec -it 'id' sh` -> **Entra al contenedor**. `-i`: interactivo, `-t`: terminal. 
- `docker build -t 'nombre imagen' .` -> Crea una imagen **a partir de un Dockerfile**. `-t`: tag, `.`: directorio donde está el Dockerfile. 
- `docker push 'user/contenedor'` -> Sube la imagen a Docker Hub.
- `docker compose up -d` -> Corre el docker-file.yaml
- `docker compose down` -> **Para todos los contenedores y borra la red** (no borra volumenes)

## Preguntas
¿Para qué sirve Docker?::Para correr tu aplicación siempre en un mismo entorno.

¿Qué contiene una imagen de Docker?::Un sistema operativo, el software necesario y la aplicación (código).

¿Cómo se genera una imagen en Docker?::A través de un archivo `Dockerfile` con instrucciones y luego ejecutando `docker build`.

¿Qué es un Dockerfile?::Archivo que contiene instrucciones para crear una imagen Docker.

Diferencia entre `RUN` y `CMD`:: `RUN` se corre cuando se construye la imagen, mientras que `CMD` se corre cuando se corre el contenedor

¿Qué hace el comando `docker build`?::Genera una imagen desde un Dockerfile en el directorio actual.

¿Qué es un contenedor en Docker?::Es una instancia en ejecución de una imagen.

¿Qué hace un contenedor?::Corre una imagen y ejecuta la aplicación en un entorno aislado.

¿Qué permite un volumen en Docker?::Crear persistencia de datos en un contenedor.

¿Qué es Docker Compose?::Una herramienta para administrar múltiples contenedores desde un solo archivo YAML.

¿Para qué sirve Docker Compose?::Facilita la administración de contenedores al declarar servicios y redes en un archivo `docker-compose.yaml`.

¿Qué comando corre un contenedor desde una imagen?::`docker run 'nombre-contenedor'`.

¿Qué hace el comando `docker run -dp port:port 'contenedor'`?::Corre un contenedor en segundo plano y mapea puertos (`-d`: detached, `-p`: puerto).
¿Para qué sirve `docker pull`?::Descargar una imagen desde Docker Hub.

¿Para qué sirve `docker images`?::Listar las imágenes descargadas o creadas localmente.

¿Qué muestra `docker ps`?::Los contenedores que están corriendo.

¿Qué muestra `docker ps -a`?::Todos los contenedores, estén corriendo o no.

¿Qué muestra `docker logs 'id'`?::Los logs (`stdout` y `stderr`) de un contenedor.

¿Para qué sirve `docker exec -it 'id' sh`?::Para ingresar al contenedor de forma interactiva usando una terminal.

¿Qué hace el comando `docker build -t 'nombre imagen' .`?::Crea una imagen con nombre (tag) desde el Dockerfile en el directorio actual.

¿Para qué sirve `docker push 'user/contenedor'`?::Subir una imagen a Docker Hub.

¿Para qué sirve `docker compose up -d`?::Levanta los contenedores definidos en el archivo `docker-compose.yaml`.

¿Para qué sirve `docker compose down`?::Detiene todos los contenedores y elimina la red creada (no elimina volúmenes).
