---
id: 1744767684-clase-docker
aliases:
  - clase-docker
tags:
  - intro-desarrollo
---

# Docker

## Comandos de docker

- **docker** run 'nombre-contenedor' -> Corre el contenedor. Si no existe localmente pero existe en **docker-hub**, lo descarga.
    - **docker** run -dp port:port 'contenedor' -> Corre el contenedor en segundo plano. -d: detached, -p: puerto.
- **docker** pull -> Descarga la imagen.
- **docker** images -> Muestra las imagenes que se crearon/descargaron.
- **docker** ps -> Muestra los contenedores que están corriendo.
- **docker** logs 'id' -> Muestra los logs de un contenedor. Siempre devuelve stdout y stderr.
- **docker** exec -it 'id' sh -> Entra al contenedor. -i: interactivo, -t: terminal.
- **docker** build -t 'nombre imagen' . -> Crea una imagen a partir de un Dockerfile. -t: tag, .: directorio donde está el Dockerfile.
- **docker** push 'user/contenedor' -> Sube la imagen a docker hub.

