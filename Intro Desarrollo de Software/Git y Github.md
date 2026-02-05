---
id: Git-Github
aliases:
  - git
  - github
tags:
  - intro-desarrollo
---
#intro-desarrollo 
# Git

## ¿Qué es Git?

Git es un sistema de control de versiones distribuido que te permite gestionar y rastrear los cambios que realizas en tus archivos a lo largo del tiempo

- Nos permite controlar las versiones de nuesto proyecto, crear copias, etc.

### Características
- Distribuido
- Colaborativo
- Permite guardar el historial de las versiones y acceder a ellas
- Permite ramificar el proyecto

### ¿Por qué usar Git?
- Permite crear copias lcoales de un proyecto (clones).
- Realiza un seguimiento de los cambios a nivel archivo.
- Facilita la colabración entre equipos.
- Permite volver a versiones anteriores del código.

### Estados de los archivos
- Untracked: No estan siendo **rastreados** por Git.
	- Archivos que **no fueron** añadidos al seguimiento de Git.
	- Para añadirlos usar el comando: *git add 'archivo' *.
- Unstaged: Los archivos fueron modificados pero **no estan listos para ser confirmados**.
	- Son los archivos que **estan siendo seguidos** por Git y fueron detectados como **modificados** pero **no fueron confirmados** para el proximo commit (confirmación).
	- Para confirmarlos usar: *git add 'archivo_modificado'*
- Staged: **Están listos** para ser **confirmados**.
	- Son los archivos modificados que estan confirmados para el próximo commit.
	- Para confirmar los cambios, usar el comando: *git commit -m "mensaje de commit"*
- Committed: **Han sido confirmados** y están en el **historial** de Git.
	- Los archivos commited son los archivos **guardados de forma permanente** en el historial del proyecto.

### Comandos básicos
- `git init`
	- Sirve para **inicializar el repositorio** / que git empieze a trackear los archivos de tal directorio
- `git clone`
	- Sirve para **clonar un repositorio**. 
	
- `git status`
	- Me muestra el **estado actual del repositorio** (Archivos no confirmados, archivos confirmados)
- `git diff`
	- Muestra la diferencia de un archivo entre **los cambios de la ultima version** (del ultimo commit) y los **ultimos cambios hechos por el usuario**
- `git stash`
	- Te permite **poner tus cambios en una lista de espera**. Es útil para poder ir a otras ramas sin que se borren tus cambios
	- git stash pop -> Devuelve los ultimos cambios stasheados a tu entorno de trabajo
	- git stash list -> Muestra los cambios stasheados
- `git log`
	- Muestra el **historial** de commits
	
- `git add`
	- Nos permite **cambiar el estado** de nuestros archivos
- `git commit`
	- Nos permite **confirmar los cambios**
	
- `git pull`
	- Nos permite **obtener los ultimos cambios del repositorio** (o de determinada rama)
- `git push`
	- Nos permite **subir los cambios locales** a GitHub

- `git branch`
	- Muestra las ramas actuales
	- `git branch <nombre-rama>`: **Crea** una nueva rama
- `git checkout <nombre-rama>`
	- **Cambia** a una rama diferente
	- `git checkout -b <nombre-rama>`: **Crea** una nueva rama y **se cambia** a esta.
- `git merge <nombre-rama>`
	- **Fusiona** la rama especificada con la **rama actual**.
	
- `git restore <archivo>`
	- **Deshace** los cambios locales no confirmados en el archivo, **restaurándolo a la versión del último commit**
	- `git restore --staged <archivo>`: **Quita un archivo** del área de preparación **sin perder los cambios locales**.
	- `git restore --source=<commit> <archivo>`: **Restaura un archivo** a su estado en un **commit específico**.
	- `git restore .`: **Deshace** los cambios no confirmados en **todos los archivos** del directorio actual.
- `git reset <archivo>`
	- **Elimina un archivo** del área de preparación.
	- `git reset --hard`: **Revierte** el repositorio al último commit.
	- `git checkout -- <archivo>`: Deshace los cambios en un archivo que aún no ha sido añadido al área de preparación.
### Buenas prácticas
- Siempre crear una rama nueva para trabajar.
- Realizar commits por funcionalidad.
- Crear ramas con nombres acorde a la funcionalidad.
- La rama main (o master) siempre tiene que funcionar.

## GitHub
### Issues
Herramienta para **registrar**, **rastrear** y **gestionar** tareas, errores o solicitudes de nuevas funcionalidades en un proyecto. Se resuelven en un *pull request*.

### Pull requests (PR)
Solicitud para **fusionar cambios** de una rama a otra en un repositorio remoto. Se usa para que otra persona verifique los cambios y, si es aprobado, los integren (en general a la rama principal / main).

## Flashcards
¿Qué es Git?::Git es un sistema de control de versiones distribuido que te permite gestionar y rastrear los cambios que realizas en tus archivos a lo largo del tiempo.  
¿Cuáles son las características principales de Git?::Distribuido, colaborativo, permite guardar el historial de versiones y permite ramificar el proyecto.  
¿Por qué usar Git?::Permite crear copias locales de un proyecto (clones), realizar seguimiento de cambios a nivel de archivo, facilitar la colaboración entre equipos y volver a versiones anteriores del código.  
¿Qué significa que un archivo esté en estado Untracked en Git?::Significa que no está siendo rastreado por Git; son archivos no añadidos al seguimiento de Git. Para añadirlos, usar `git add 'archivo'`.  
¿Qué significa que un archivo esté en estado Unstaged en Git?::Son archivos seguidos por Git que han sido modificados pero no están preparados para el próximo commit. Para moverlos a staged, usar `git add 'archivo_modificado'`.  
¿Qué significa que un archivo esté en estado Staged en Git?::Son archivos modificados que están listos para ser confirmados en el próximo commit. Para confirmarlos, usar `git commit -m "mensaje de commit"`.  
¿Qué significa que un archivo esté en estado Committed en Git?::Son archivos que han sido confirmados y guardados de forma permanente en el historial de Git.  
¿Para qué sirve el comando git init?::Inicializar un repositorio y empezar a rastrear los archivos del directorio con Git.  
¿Para qué sirve el comando git clone?::Clonar un repositorio remoto creando una copia local en tu máquina.  
¿Qué muestra git status?::El estado actual del repositorio, indicando archivos no confirmados (unstaged), preparados (staged) y confirmados (committed).  
¿Qué muestra git diff?::Las diferencias entre los cambios del último commit y los cambios actuales no confirmados por el usuario.  
¿Para qué sirve git stash?::Poner tus cambios en una lista de espera para cambiar de rama sin perderlos; `git stash pop` devuelve los cambios, y `git stash list` muestra lo stasheado.  
¿Qué muestra git log?::El historial de commits del repositorio.  
¿Para qué sirve git add?::Agregar archivos al área de preparación (staging area) para incluirlos en el próximo commit.  
¿Para qué sirve git commit?::Confirmar los cambios preparados en el área de staging con un mensaje descriptivo.  
¿Para qué sirve git pull?::Obtener y fusionar los últimos cambios del repositorio remoto (o de una rama específica) en tu copia local.  
¿Para qué sirve git push?::Enviar tus commits locales al repositorio remoto en GitHub u otro servidor.  
¿Qué hace git branch?::Mostrar las ramas actuales; `git branch <nombre-rama>` crea una nueva rama.  
¿Para qué sirve git checkout <nombre-rama>?::Cambiar a una rama diferente; con `-b` crea y cambia a una nueva rama en un solo paso (`git checkout -b <nombre-rama>`).  
¿Para qué sirve git merge <nombre-rama>?::Fusionar la rama especificada con la rama activa actual.  
¿Para qué sirve git restore <archivo>?::Deshacer cambios locales no confirmados restaurando el archivo a la versión del último commit; `--staged` lo quita del área de preparación sin perder cambios, `--source=<commit>` lo restaura a un commit específico, y `.` deshace cambios en todos los archivos del directorio.  
¿Para qué sirve git reset <archivo>?::Quitar un archivo del área de preparación; `--hard` revierte todo el repositorio al último commit; `git checkout -- <archivo>` deshace cambios en un archivo no añadido aún al staging.  
#git/buenas-practicas
¿Cuáles son las buenas prácticas en Git?::Crear siempre una rama nueva para trabajar, realizar commits por funcionalidad, nombrar ramas acorde a la funcionalidad y asegurar que la rama main (o master) siempre funcione.  
¿Qué son las ramas?::Una bifurcación del proyecto que permite avanzar en paralelo sin modificar lo que ya está hecho.
¿Cuales son las estrategias ideales a la hora de usar ramas?
?
- Main, develop, feature
- Gitflow (main, develop, release, hotfix, feature)
¿Qué son los Issues en GitHub?::Herramienta para registrar, rastrear y gestionar tareas, errores o solicitudes de nuevas funcionalidades en un proyecto; se resuelven mediante pull requests.  
¿Qué son los Pull Requests en GitHub?::Solicitudes para fusionar cambios de una rama a otra en un repositorio remoto; sirven para que otros revisen y aprueben los cambios antes de integrarlos en la rama principal.
