# Comandos bash LINUX - UBUNTU
- La forma en como se organizan los elementos en el sistema operativo es a travez del arbol de directorios, este está conformado por carpetas (directorios) y archivos (binarios y no binarios).
- comando para listar archivos.
    - ls || ls <path> : lista los elementos (no ocultos) en el directorio seleccionado, si no se agrega path se listan los elementos en el directorio actual (en el que se encuentra ubicado).
    - la || ls -a <path>: lista todos los elementos de un directorio, incluido los ocultos.
    !nota¡: los elementos ocultos son todos lo elementos que tiene un punto inicial en su nombre; en todo directorio existen dos directorios ocultos que son directorios virtuales, estos apuntan a el directorio actual (.) o a el directorio anterior (..)
    - ls -d */ : lista todos los directorios dentro del path presente.
    - ls -d *<ext>: lista todos los elementos terminados con la extención especificada.
    - ls -d <ini>*: lista todos los elementos que inicien con las letras especificadas.
    - ll || ls -l: lista todos los archivos en formato largo mostrando sus permisos y demas caracteristicas.
    - ls -lh || ll -h: imprime el tamaño de los archivos de forma entendible, con acotaciones.
    - ls -d: imprime solo el nombre del subdirectorio, sin mostrar los aarchivos internos.
    - ls -lt || ll -t: lista los elmentos del directorio ordenados por la fecha de modificación, del mas reciente a el menos reciente (con -r se invierte este orden).
    - ls .1: lista los elementos del directorio en forma de columna.
    - ls -i: muestra el numero de i-nodo antes del nombre del elemento.
    !nota¡: el numero de i-nodo: es un identificador para el inodo del elemento, el inodo contiene las caracteristicas de in archivo regular o directorio o cualquier otro elemento que se pueda obtener en el sistama de ficheros.
    - ls -m: muestra todos los elementos de un directorio separados por una coma.
    - ls -R: hace un listado recursivo (muestra los elementos dentro de los elementos).
    - ls -s: muestra delante del nombre el tamaño en kilobytes del elemento.
- cambiar de directorio.
    !nota¡: de forma predeterminada existen 2 acotamientos de directorios importantes, el directorio raiz es (/) y el directorio home (~); el home es el directorio predeterminado del usuario y el directorio raiz el el directorio inicial.
    - cd <path>: (change directory) permite movernos en la terminal cambiando de directorio, existen dos maneras de moverse, absoluta (se coloca el path completo), relativa (se va avanzando carpeta por carpeta).
    - cd ~: lleva al directorio home.
    - cd /: lleva al directorio raiz.
    - cd -: lleva al ultimo directorio visitado.
- mostrar la ubicación actual.
    - pwd : (print working directory) muestra la direccion actual.
- crear elementos.
    - mkdir <name directory> : crea carpetas o directorios.
    - touch <name file> : crea archivos vacios.
    - nano <name file>: crea archivos utilizando el editor de texto nano.
    - vim <name file>: crea archivos utilizando el editor de texto vim.
- copiar elementos.
    - cp <path file origin> <path destiny>: copia un archivo o elemento a el directorio destino seleccionado. 
    - cp -r <path file origin> <path destiny>: copia un archivo o elemento de forma recursiva a el destino seleccionado.
- elimidar elementos.
    - rm <name file>: se utiliza principalmente para eliminar archivos.
    - rm -f <name file>: elimina un archivo de forma forzada.
    - rmdir <name directory>: elimina solo los directorios vacios.
    - rm -rf <name directory>: elimina el directorio especificado con los elementos que contenga (de forma recursiva).




    