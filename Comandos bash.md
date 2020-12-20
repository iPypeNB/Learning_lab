# Comandos bash LINUX - UBUNTU
- La forma en como se organizan los elementos en el sistema operativo es a travez del arbol de directorios, este está conformado por carpetas (directorios) y archivos (binarios y no binarios).
- es recomendable crear los nombres de las carpetas y los archivos en minusculas y sin acentuación para que así sea mas facíl moverse en el directorio del pc.
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
- eliminar elementos.
    - rm <name file>: se utiliza principalmente para eliminar archivos.
    - rm -f <name file>: elimina un archivo de forma forzada.
    - rmdir <name directory>: elimina solo los directorios vacios.
    - rm -rf <name directory>: elimina el directorio especificado con los elementos que contenga (de forma recursiva).
- mover elementos:
- el comando mv también se puede utilizar para cambiar el nombre del archivo.
    - mv <name file> <new name file>: cambia el nomvre del archivo.
    - mv <path file origin> <parh file destiny>: mueve el archivo de una carpeta a otra.

# editores de texto en la consola de linux
- vim: es el editor de texto por defecto en todos los sitemas operativos basados en UNIX, vim se caracteriza por tener 3 modos de manejo principales, estos modos de manejo son:
    - Modo comando: permite al usuario navegar por el documento y así introducir comandos a ejecutar dentro del archivo, por defecto cuando se abre un archivo con vim se entra en este modo, si se cambia de modo con ESC se regresa al modo de comandos.
    - Modo insercion: para entrar en modo de inserción de texto se preciona la tecla (i), en este modo se puede ingresar texto en el archivo y editarlo.
    - modo Ex: en este modo se manipula el estado del arhcivo (guardar, cerrar, etc) para entrar en este modo de debe ingresar (:).
- comandos de vim:
    - H: desplazamiento a la parte superior de la pantalla.
    - L: desplazamiento a la parte inferior de la pantalla.
    - G: desplazamiento hasta el final del documento.
    - w: desplazamiento una palabra a la derecha.
    - b: desplazamiento una palabra a la izquierda.
    - 0: desplazamiento al incio de la linea actual.
    - $: desplazamiento al final de la linea actual.
    - i: activa el modo inserción de texto.
    - I: modo inserción de texto al inicio de la linea donde se encuentra el cursor.
    - O: insertar una linea en blanco antes de la linea actual.
    - o: insertar una linea en blanco despues de la lina actual.
    - r: sustituye el caracter en la posicion actual del cursor.
    - R: sobreescribe desde la posicion aztual del cursor.
    - x: borrar el caracter de la posicion actual del cursor.
    - X: borrar el caracter siguiente al de la posicion actual del cursor.
    - dd: corta la linea actual (queda disponible en el portapapeles).
    - D: cortar desde la posicion actual del cursor hasta el final de la linea.
    - yy: copiar la linea completa donde se encuentra el cursor.
    - y#: copia el numero de caracteres desde la posicion actual del cursor.
    - P: pegar en la linea anterior a la que se encuentre el cursor.
    - p: pegar en la linea siguiente a la que se encuentre el cursor actualmente.
    - .: repite el ultimo comando.
    - u: deshace el ultimo comando.
    - :w: guarda el estado actual del archivo.
    - :wq: guardar y salir.
    - :q: salir sin guardar.
    - ZZ: guardar y salir.
    - :x: guardar y salir.

# batch
- procesamiento por lotes o batch, son programas que procesan texto y emiten un resultado.
- utilidades batch:
    - cat: muestra todo el contenido de un archivo de texto.
    - head: muestra las primeras 10 lineas de un archivo de texto.
    - tail: muestra las ultimas 10 lineas de un archivo de texto.
    - head || tail -n <number>: muestra el numero de lineas especificadas.
- utilidades avanzadas de batch:
    - grep <word> <file name>: busca la palabra en el archivo y muestra las lineas de texto que contienen esa palabra.
    - grep -i <word> <file name>: busca la palabra sin tomar en cuenta las mayusculas o minusculas.
    - grep "<word>$" <file name>: busca una lina del archivo que temine con la palabra especificada.
    - sed 's/<word>/<sustitute>/g': sustituye una palabra por otra de forma global en el documento. (este comando no modifica el archivo)
    - sed '$d': elimina la ultima linea del documento. (este comando no modifica el archivo)
    - awk: es un comando que nos permite trabajar archivos de texto estructurados (separados por comas, etc.).
    




    