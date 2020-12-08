# Comandos de docker

# ¿qué es docker?
- Es una plataforma de software que le permite crear, probrar e implementar aplicaciones de una forma rapida y segura, que garantiza que sin importar el OS sobre el cual se monte esta app el software diseñado va a funcionar, Docker empaqueta software en unidades estandarizadas llamadas CONTENEDORES que incluyen todo lo necesario para que el software se ejecute.
    - Docker, el software de TI, es una tecnología de cración de contenedores que permite la creación y el uso de contenedores de Linux.
    - la empresa Docker Inc. Desarrolla el trabajo de la comunidad de docker, lo hace más seguro y comparte estos avances con el resto de la comunidad, el software docker es un proyecto open source que permite a los desarrolladores de la comunidad trabajar en el proyecto y darle una mejora continua.

# ¿Qué es docker engine?
- Docker engine es una aplicación de codigo abierto diseñada para crear contenedores. Docker engine actua como una aplicación cliente-servidor cont:
    - un servidor con un proceso daemon de larga ejecución (dockerd)
    - una API que especifica las interfaces a traves de los cuales los programas se comunican con el docker daemon.
    - Una interfaz de linea de comandos (CLI) (docker)  

# ¿Cómo funciona Docker?
    - Docker es una tecnología que utiliza el kernel de linux y la funciones de este, como Cgroups y namespaces, para segregar los procesos, de modo que puedan ejecutarse de manera independiente.
    - Las herramientas desarrolladas como docker ofecen un modelo de implementacíon basado en imagenes. Esto permite compartir una aplicación, o conjunto de servicios, con todas sus dependencias en varios entornos. Docker También automatiza la implementación de la aplicación en este entorno de contenedores.
    
# ¿Qué es un contenedor?
    - El proposito de los contenedores es generar independencia, dar la capacidad de ejecutar varios procesos y aplicaciones por separado para hacer un mejor uso de su infraestructura y, al mismo tiempo, conservar la seguridad que tendría con los sistemas separados.

# Diferencia entre los contendores de docker y los contenedores tradicionales de linux
    - La tecnología de docker se desarrollo a partir de la tecnología LXC (contendores tradicionales de linux), aunque desde entonces con el desarrollo de la comunidad se a lejado de esa dependencia. LXC era utíl como virtualización ligera, pero no ofrecia una buena experiencia al desarrollador ni al usuario. Docker no solo aporta la capacidad de ejecutar contenedores, sino que también facilita el prceso de creación y diseño de los mismos ademas de el envio de imagenes y de creación de versiones de imagenes, entre otras cosas.

# comandos
- !nota¡: los nombres de los container no se pueden repetir, los contenedores se dejan de ejecutar cuando el proceso pincipal temina (genera un exit).
    - docker --version : ver la version de docker
    - docker run --name <name container> <name type image>: iniciar un nuevo contenedor
    - docker run -d <name type image>: se utiliza el modificador -d ó --detach para ejecutar el comando en segundo plano
    - docker ps: lista de contendores
    - docker ps -a: lista de contenedores completa (a: all)
    - docker ps -aq: lista de contenedores completa "resumida" (lista solo los id, q: quiet)
    - docker inspect <id container> || docker inspect <name container>: muestra los detalles internos del contenedor
    - docker inspect -f '{{}}' <id container>: filtra una variable en especifico del contenedor
    - docker rm <name container> || docker rm <id container>: elimina un contenedor
    - docker rm $(ps-aq): borra TODOS los contenedores que no estan corriendo.
    - docker rm -f $(docker ps-aq) || docker container prune: borra TODOS los contenedores (incluso los que estan corriendo, -f: force).
    - docker logs <name container> : muestra el output generado en la ultima ejecución del contenedor.
    - docker run -it <name image>: crea un contenedor de forma interactiva (se pueden ejecutar inputs y outputs, t: asignar pseudo terminal i: manten stdin abierto)
    - docker run <name image> <command>: crea un nuevo contenedor basado en la imagen con un comando especifico.
    - docker exec -it <name container>: ejecuta un comando de forma interactiva sobre un container ya creado (funciona con los contenedores que estan corriendo)
    - docker kill <name container>: "mata" los procesos que está ejecutando el contenedor
    - docker pause <name container> <command>: supende los comandos especificados en el proceso.
    - docker stop <name container>: detiene el proceso principal del contenedor.
- !nota¡:   que un puerto esté abierto en un docker no significa que exista una conexion por el puerto desde la maquina local, es decir en estos casos podemos interpretar a los contenedores como una maquina virtual en la que al estar aislado los puertos hanilitados (por defecto) estan habilitados internamente en el mismo contenedor, para poder generar la conexión desde la maquina local hasta el contenedor se debe poner:
    - docker run -d --name <name container> -p <port host: port container> <name type image>
- !nota¡: hay que tener en cuenta que cuando asignamos un puerto de conexión entre el host y los containers, los puertos del host no se pueden repetir. (ya que por ej: solo existe un puerto 8080 en el host.)
- Generar conexión entre el container y un volumen (directorio) de nuestra maquina host, este metodo se conoce como bind mount.
    - docker run -d --name <name containe> -v <directory host machine: directory container> <name type image>:crea un docker con conexion con un directorio de la maquina host.
- conectar contenedor a volumen creado.
    - docker run -d --name <name container> --mount src=<name volume>,dst=<directory container> <name type image>
    - docker history <tag contenedor>: permite visualizar los layer o capas de un contendor


# Como generar volumenes con docker (metodo alternativo a bind mount)
- como se sabe los contenedores son agrupaciones de procesos aislados de la maquina host y/o otros contenedores, lo que sucede es que cuando se elimina un contenedor todos los datos contenidos en el contenedor se eliminan junto al contenedor, está es la solucion que se ofrece con lo volumenes (como alternativa al bind mount). Los volumenes son un directorio o fichero en el docker engine, el objetivo o la eficiencia de crear unos volumenes está en conectarlos con un storage remoto y trabajar en un entorno basado en la nube.
    - docker volume ls : lista todos los volumenes que han sido creados por los contenedores.
    - docker volume prune: elimina todos los volumenes que no son utilizados por ningun contenedor.
    - docker volume create <name volume>: crea un nuevo volumen.

# Manejar imagenes con docker
- Las imagenes en docker son plantillas que funcionan para le creación de contenedores
    - docker pull <name type image>: trae una imagen de un repositorio remoto, por defecto el trae la ultima version de una imagen, para cambiar esto se puede expecificar la version.
    - docker pull <name type image>:<number version>: esto trae una version especifica de una imagen.
- como crear una imagen con dockerfile
    - para crear una imgaen propia se utiliza un archivo llamado Dockerfile en el que se van a ingresar los parametros necesarios para crear la imagen.
    - docker build -t <name image>:<version tag> <path>  : se contruye una imagen a partir del docker file, se tiende a utilizar como nombre de la imagen a el nombre de la imagen base(:) nombre de la imagen propia, el path es importante tenerlo en cuenta ya que es el directorio de donde docker va a generar el build 

# Repositorios en docker
- cuando nosotros descargamos una imagen de docker lo que estamos haciendo es descargar una imagen de un reporitorio oficial, estos repositorios vienen de un servidor o serivicio web creado por docker (docker hub), este funciona como github y git (se manejan versionamientos, repositorioa publicos, privados, etc.)
- para poder compartir imagenes propias de debe crear una cuenta en docker hub a la cual se van a subir las imagenes creadas.
    - docker pull <name type image>: trae una imagen de un repositorio remoto, por defecto el trae la ultima version de una imagen, para cambiar esto se puede expecificar la version.
    - docker push <name image>:<version tag>: se sube la imagen creada, hay que tener en cuenta que si estas imagenes están basadas de otra en un repositorio oficial se intentaran subir al mismo si no se especifica que se suban al repositorio propio, por lo que no vamos a tener los permisos otrogados, en estos casos se puede utilizar:
    - docker tag <name image>:<version tag> <user>/<name image>:<version tag>: se crea un nuevo tag con la imagen ya creada.
    - docker push <user>/<name image>:<version tag>: esto sube al reposirotio personal la imagen creada.

# matriz de carácteristicas de un contenedor en docker
    - id: codigo hash que identifica al contenedor
    - image: es la imagen en la que basamos el contenedor (es la plantilla de los procesos que ejecuta el contenedor, ej: ubuntu (crear un OS ubuntu))
    - command: los comandos que se ejecutaron dentro del contenedor (el proceso que se ejecutó)
    - created: fecha de creación del contenedor
    - status: estado en el que se encuentra el contenedor (exited: no se está ejecutando, up: ejecutando)
    - ports: muestra los puertos que están expuestos en el contenedor (esto es lo que permite aislar los contenedores o generar conexion entre ellos)
    - names: nombres de los contenedores (no se pueden repetir)



