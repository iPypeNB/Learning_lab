*   comandos para iniciar un repositorio de Git
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
    -   git log : muestra un historial de los commits realizados
    -   git log --oneline: muestra el historial simplificado de los commits realizados.
    -   git log --stat: muestra el historial de commints espcificando por archivo cuantos cambios ha tenido

* Comandos para regresar a commits anteriores (Regresar en el tiempo)
# Estos comandos nos permitiran borrar commits o revertir un commit creando uno nuevo en base a uncommit viejo.
# el comando reset lo que hace es mover la direccion a donde apunta el HEAD
    -   git reset <code commit>: hace que el HEAD apunte a el commit indicado (no cambia ni el working directory y y los archivo tranked los vuelve untracked).
    -   git reset <code commit> --hard: cambia el estado del repositorio al commit seleccionado (cambia los archivos al estado del commit seleccionado).
    -   git reset <code commit> --soft: cambia el estado del repositorio conservando los cambios y trackeados (no los vuelve untracked).
# el checkout lo que hace es crear una cabeza desprendida (HEAD detached) que permite visualizar los archivos en el estado del commit seleciconado.
    -   git checkout <cod commit>: lleva el HEAD a la version del commit seleccionado, para volver al head "origianl" se ingresa el comando: git switch -
    -   git switch -c <name branch> (dentro de git checkout <cod commit>): permite crear una nueva branch a partir del commit selccionado por el checkout.
    -   git checkout <cod commit> <name file>: permite visualizar el estado del archivo en la version del commit seleccionado.
    



