* Link donde muestra los comandos.
-   https://bluuweb.github.io/tutorial-github/guia/fundamentos.html
-   https://www.git-scm.com/

* Comandos para configurar y ver opciones en git.
# comandos que permiten ver los parametros almacenados en git
    -   git config --global -l: permite ver los parametros almacenados en git
    -   git config --global -e: permite editar los parametros almacenados en git.
    -   git version: permite ver la version de git.

*   Comandos para iniciar un repositorio de Git
# cuando se inicia un repositorio git se crea una carpeta oculta (.git) que va a ser la que almacena el repositorio.
    -   git init: crea un repositorio vacio.
    -   git clone: clona un repositorio ya creado.

* Comandos para cambiar el estado de un archivo en Git.
# los archivo en git pueden tener 3 estados : untracked, tracked and upload 
# untracked: modificado pero no agregado en el stage.
# tracked: modificado y agregado en el area de stage.
# upload: el archivo fue actualizado en el repositorio.
    -   git add: agrega el archivo a el area de stage
    -   git commit; git commit -m "messagge": sube y actualiza los archivos en el repositorio.
    -   git commit -am "messagge": este me permite realizar el add y el commit en un solo comando, colocando el mensaje.
    -   git restore <name file>: funciona cuando se tiene el archivo en untracked y se desea descartar los cambios hechos en el working directory.
    -   git restore --staged <name file> : funciona cuando se tiene un archivo tracked y se desea regrear del area de stage a el area del working directory.
    -   git mv: este permite mover un archivo o cambiarle el nombre sin perder el tracking sobre el mismo.
    -   git rm: remueve los archivos del repositorio sin perder su historial durante el mismo.

* comando para conocer los cambios de un archivo en el repositorio
# estos comandos permiten visualizar los cambios que han tenidos los archivos a lo largo de los commits realizados o en comparacion entre 2 commits.

    -   git show <name file>: muestra los cambios que ha tenido un archivo entre el HEAD y el commit anterior.
    -   git diff <code commit1> <code commit2> : visualiza la diferencia entre 2 commits seleccionados.
    -   git diff : evalua la diferencia que hay entre staging area y el working directory

* comandos para conocer estados del repositorio
# Estos comandos nos permiten ver el historial de commits y los estados en los que se encuentran los archivos en el repositorio
    -   git status : muestra el estado actual de los archivos dentro del repositorio.
    -   git status -s: solo muestra los archivos modificados en el working directory.
    -   git log : muestra un historial de los commits realizados
    -   git log --oneline: muestra el historial simplificado de los commits realizados.
    -   git log --stat: muestra el historial de commints especificando por archivo cuantos cambios ha tenido.
    -   git log -p: te especifica por linea los cambios que han tenido los archivos y la diferenia entre estos.
    -   git log --graph: Muestra de forma decorativa los estados de las rammas. 
    -   git reflog: muestra todos los commits realizados incluso los commits borrados.
    -   git shortlog: muestra los cambios que ha realizado el usuario.
    -   gitk: muestra una interfaz grafica en la que podemos visualizar el historial del respositorio.

* Comandos para regresar a commits anteriores (Regresar en el tiempo)
# Estos comandos nos permitiran borrar commits o revertir un commit creando uno nuevo en base a uncommit viejo.
# el comando reset lo que hace es mover la direccion a donde apunta el HEAD
    -   git reset <code commit>: hace que el HEAD apunte a el commit indicado (no cambia ni el working directory y y los archivo tranked los vuelve untracked).
    -   git reset <code commit> --hard: cambia el estado del repositorio al commit seleccionado (cambia los archivos al estado del commit seleccionado).
    -   git reset <code commit> --soft: cambia el estado del repositorio conservando los cambios y trackeados (no los vuelve untracked).
# el checkout lo que hace es crear una cabeza desprendida (HEAD detached) que permite visualizar los archivos en el estado del commit seleciconado.
    -   git checkout <cod commit>: lleva el HEAD a la version del commit seleccionado, para volver al head "original" se ingresa el comando: git switch -
    -   git switch -: se sale del estado HEAD desconectado y regresa a el ultimo commit realizado, este comando funcion si no se uso git switch -c <branch name> ya que si se uso este comando para regresar al commit original se usa: git switch master.
    -   git switch -c <name branch> (dentro de git checkout <cod commit>): permite crear una nueva branch a partir del commit selccionado por el checkout.
    -   git checkout <cod commit> <name file>: permite visualizar el estado del archivo en la version del commit seleccionado.

* Comandos para tener el manejo de las branchs.
# las branchs son una copia del repositorio actual que se crea en una nueva rama lo que permite desarrollar soluciones diferentes, hacer desarrollos experimentales, solucionar bugs, etc. Luego de completar con el proposito de la rama esta se puede unir a la rama principal del repositorio.
    -   git branch: permite ver las ramas que actualmente tiene el repositorio.
    -   git branch <name branch>: crea una nueva rama copiando el commit en el que se encuentra el HEAD.
    -   git branch -d <name branch>: eliminar una rama.
    -   git checkout <name branch>:  cambia la rama a la que HEAD apunta. (cambiar entre ramas)
    -   git merge <name branch>: unifica dos ramas, esto funcion trayendo la verison de la rama mencionada hacia la rama en donde se ejecuta el comando.

* Comandos para crar y editar Tags.
# los tags permiten establecer una guia de avance del proyecto, esto permiten por ejemplo establecer cuando un proyecto se encuentra en una version alpha.
    -   git tag: listar los tag realizados.
    -   git tag <name tag> -m "messagge": crea un tag sobre la ultima version del repositorio (HEAD).
    -   git tag -a <name tag> <cod commit> -m "message": establece un tag en la version del commit seleccionada.
    -   git tag -d <name tag>: elimina el tag seleccionado.
    -   git show <name tag>: muestra la informacion del tag.

* Comandos para manejar un repositorio remoto
# los repositorios remotos son los que permiten establecer una copia en un servidor sobre los proyectos que se trabajan, estos pueden ser por ejemplo github, gitlab.
    -   git remote add <name origin> <link origin>: permite conectar un origen remoto (un repositorio creado en un server) con el repositorio local, por convenio los repositorios remotos tienen el nombre de origin.
    -   git remote: permite ver todo los origenes remotos que se han asignado al repositorio local.
    -   git push <name origin> <name branch>: envia los archivos del repositorio local a el origen remoto.
    -   git fetch <name origin> <name branch>: recupera la informacion del repositorio remoto y la almacena el el repositorio local, este comando no modifica los archivos, por lo que para poder modificar los archivos locales falta ingresar el comando: git merge
    -   git pull <name origin> <name branch>: es como utlizar el comando fetch y merge ya que este trae los archivos del repositorio remoto actualizando los archivos del repositorio local.






