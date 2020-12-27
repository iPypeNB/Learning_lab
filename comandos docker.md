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
    - docker build: crea una imagen a partir de un dockerfile.
    - docker run --name <**name container**> <**name type image**>: iniciar un nuevo contenedor
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

# conservar los datos de un contenedor
- Generar conexión entre el container y un directorio de nuestra maquina host, este metodo se conoce como bind mount.
    - docker run -d --name <name containe> -v <directory host machine: directory container> <name type image>:crea un docker con conexion con un directorio de la maquina host.
- conectar contenedor a volumen creado.
    - docker run -d --name <name container> --mount src=<name volume>,dst=<directory container> <name type image>
    - docker history <tag contenedor>: permite visualizar los layer o capas de un contendor


# Como generar volumenes con docker (metodo alternativo a bind mount)
- como se sabe los contenedores son agrupaciones de procesos aislados de la maquina host y/o otros contenedores, lo que sucede es que cuando se elimina un contenedor todos los datos contenidos en el contenedor se eliminan junto al contenedor, está es la solucion que se ofrece con los volumenes (como alternativa al bind mount). Los volumenes son un directorio o fichero en el docker engine, el objetivo o la eficiencia de crear unos volumenes está en conectarlos con un storage remoto y trabajar en un entorno basado en la nube.
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

# archivo dockerfile
- los archivos dockerfile son archivos que se utilizan para crear imagenes de docker personalizadas, estos archivos pueden contener:
    - FROM <name type image>: este comando !SI O SI¡ debe estar en el dockerfile y es con lo que comienza el archivo, este comando define la imagen en la cual se va a basar nuestra imagen personalizada, ej: FROM  ubuntu, FROM scratch (from scartch es practicamente traer solo el kernel de linux)
    - COPY [<dirrectory local context>, <directory container context>]: copia los archivos presenten en el contexto de build (segun donde definamos el contexto de build) en el contenedor, como dirección del servidor se usa normalmente: /usr/src/
    - WORKDIR <directory workspace container>: este comando especifica la dirección del entorno de trabajo para el contenedor, funciona como un cd de la linea de comandos.
    - RUN <command>: ejecuta el comando especificado.
    - EXPOSE <port>: expones el puerto del contenedor para que pueda ser accedido de forma externa.
    - CMD [<COMMANDS>]: ejecuta los comandos expecificados cuando en el build no se le especifica otro comando.
- es importante tener en cuenta como es que docker maneja el cache (este trabaja como git al generar una imagen), docker busca como son los cambios entre las imagenes y define la nueva imagen segun los cambios (si una nueva imagen se crea igual que otra ya utilizada, lo hace uttilizando el cache ya que asi se ahorra proceso.), para poder utilizar esto de forma correcta lo que se hace es utilizar los comando de tal forma que las dependencias "que no se suelen cambiar" se integran primero y los archivos que si se suelen modificar se integran despues para que así docker utilice el cache en el maximo numero de pasos posibles.
- como actualizar el contenido de un contenedor sin tener que hacer un build a la imagen:
    - se montan los archivos en el docker a traves del metodo de bind mount. (esto permite que el contenedor monitoree un directorio de la maquina host y quita la necesidad de actualizar la imagen.)

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

# como crear conexiones entre los contenedores.
- para poder crear conexiones entre los contenedores docker nos ofrece una herramienta que es docker network, con este comando se pueden crear conexiones utilizando los diferentes metodos.
    - bridge: en terminos de redes una red bridge es una red que que trabaja en la capa de enlace, que reenvía el tráfico entre segmentos de red. Un bridge puede ser un dispositivo de hardware o un software que se ejecuta dentro de un kernel de la maquina host, bridge es una red que utiliza un parametro link, este metodo ya no es tan utilizado debido a temas de retrocompatibilidad.
    - host: es la forma que tiene docker de representar la red de la maquina host. Cuando se utiliza una red de tipo host  lo que sucede es que la pila de red del contenedor deja de estar aislada de la maquina host y el contenedor pasa a obtener una dirección IP asignada, ej: si uno utiliza un contenedor que se une al puerto 80 y utiliza una red host la aplicación del contenedor estará disponible en el puerto 80 en la dirección ip del host, lo que sucede con este comando es que expone todos los puertos del contenedor y tanto la maquina host como el contenedor quedan "expuestos".
    -none: esto gener que el contenedor quede totalmente aislado dado que desconecta de todos los puertos al contenedor.
    - docker network create <name network>: con esto se crea una red personalizada, este tipo de red dura el mismo timempo que el container.
    - docker network create --attachable <name network>: con este comando se especifica que contenedores nuevos tengan la capacidad de conectarse a travez de esta red.
    - docker network connect <name network> <name container>: conectar un contenedor a la red especificada, es importante tomar en cuenta de que el contendor debe esta "corriendo" ejecutandose o no se conectara a la red.
    - docker network inspect <name network>: docker muestra todos los parametros de la red especificada.
- si dos contenedores estan conectados bajo la misma red, se pueden comunicar utilizando su nombre como host name.
- cuando conectamos diferentes contenedores a la misma red es importante tener en cuenta la forma en como los interconectamos entre ellos, como se mencionó antes esto se puede lograr llamando a los contenedores por su nombre, en el caso de una web app con una db (Js y mongo), ej: se crea un contenedor de db el cual se va a conectar a a la red, a este NO se le configura ningun puerto de expose (-p), se crea un contenedor con el backend al que se le va a configurar un puerto de expose (-p, con este puerto se va a comunicar con la maquina host) y se le configura una variable de entorno que se va a encargar de conectarse con el contenedor de db a travez del mismo nombre, los comandose serian algo así.
    - docker network create --attachable <name network>
    - docker run -d --name <name container> <name type image> <--- "este es el contenedor de la base de datos(db)"
    - docker network connect <name network> <name container> <--- "se conecta al contenedor de la db"
    - docker run -d --name <name container> -p <port host machine>:<port container> --env MONGO_URL=mongodb://<name container (db)>:<port>/<name db> <name type image> <--- "se crea una variable env suponiendo que la base de datos es MONGO"
    - docker network connect <name network> <name container> <--- "contenedor del backend"

# docker compose
- docker compose es un archivo tipo yml (utiliza la sintaxis yaml) que se encarga de construir la estructura de la aplicación de forma declarativa, configura las conexiones entre los contenedores, los puertos, los tipoes de imagen etc, en docker compose podemos encontrar:
    - version: indica la version por la cual docker compose va a realizar la estructura.(esto puede cambiar la sintaxis)
    - services: describe los servicios que va a tener la aplicación (asi es como se pueden interpretar los contenedores en docker-compose, la diferencia entre un servicio y un contenedor es que un servicio puede contener varios contendores).
        - <name service>: dentro de los servicios se definen los nombres de cada uno de los servicios.
        - name_container: define el nombre del contenedor.
        - image: define el tipo de imagen que va a ser el contenedor
        - environment: se definen las variable de entorno del contenedor
            - <name variable>: <command>
        - depends_on: define las dependencias de los servicios o contenedores, sirve para definir el orden de la creación de los contenedores, pero no define como tal el orden de inizialicación.
        - ports:  define los puertos de conexion entre el host y el contenedor o servicio, en los puertos de host se puede seleccionar un rango de puerto para que cuando se haga scale no se obstaculicen los puertos.
        - build: permite construir un contenedor de forma presonalizada a partir de un dockerfile, "evitando en parte" la creacion  de un servicio desde una imagen standar.
- !nota¡ cuando vemos en la imagenes el nombre <none> es porque son versiones viejas de docker que fueron ejecutados a partir de build; cuando se buildea una imagen se puede utilizar el docker-compose up -d y docker correra los contenedores a partir de la imagen ya buildeada.
        - volumes: nos permite crear fuentes de almacenamiento compartida y/o perpetuas como: bind-mount, volumenes.
- cuando creamos un volumes a partir de un bind-mount hay que tener en cuenta que el bind-mount sobree escribe todo el directorio que se ha seleccionado en el contenedor, para solicitar que una parte no se sobre escriba podemos poner en volumes: <directory in container> (la direccion dentro del contenedor que no queremos que se borren (no se colocan los (:)))
- !nota! para poder crear una actualizacion automatica de los documentos (ej: nodemon identifique los cambios) podemos crear un bind-mount y asi se van a actualizar los archivos de forma automatica en el contendor.


# comandos docker-compose
- docker-compose tiene unos comandos que nos permite manipular las costrucciones realizadas.
    - docker-compose up -d: levanta un docker-compose basandose en el archivo yml creado (-d: para ejecutarlo en segundo plano), se puede hacer 2 veces el docker-up y docker busca las diferencias para el mismo actualizar los contendores.
    - docker-compose logs logs -f: muestra los posibles errores en los registros y peticiones.
    - docker-compose ps: al igual que docker ps nos muestra los contenedores
    - docker-compose down: detiene los contenedores y las redes creadas.
    - docker-compose down -v: detiene los contenedores, las redes y borra los volumenes creados.
- !nota¡ por defecto docker toma el nombre del directorio para crear los nombres de los contenedores y redes.
    - docker-compose logs <service>: me muestra los log generados por el servicio especificado.
    - docker-compose exec <service> bash: executa el comando en el servicio especificado.
    - docker-compose scale <service>=<number>: crea mutiples contenedores del servicio seleccionado, esto sirve para poder escalar un servicio web y a través de un balanceador de carga, distribuir el numero de peticiones en los contenedores, cuando se hace scale la conexion entre los puertos debe ser por rango (ports: 300-3010:3000)

# docker ignore 
- para poder ignorar algunos elementos que no queremos que se monten en el contenedor podemos hacer uso del archivo .dockerignore que tiene un funcionamiento muy parecido al de git.
    - nomarlmente en el contenedor se ignora el dockerfile: no es necesario subirlo, ¿para qué si ya se buildeo la imagen?.
    - modulos descargados de las dependencias, ej: node_modules.
    - los readme o archivos de log que no sean necesarios para el funcionamiento del contenedor.

# docker a nivel de producción.
- cuando creamos el dockerfile y construimos la imagen podemos crear distintos archivos de tipo docker file y con esto diferenciar el docker de desarrollo y el de produccion, ej: development.dockerfile, production.dockerfile, para correr un docker file especifico debemos poner. 
    - docker build -t <container> -f <name dockerfile>

# docker multi-stage build
- este concepto parte de que se pueden crear archivos de dockerfile que generen "stage" y se pueda hacer una diferenciación entre docker-development y docker-production, con este concepto también se puede hacer que exista una comunicación entre ellos.
    - en el primer stage: FROM <image> as <name>
    - en el segundo stage: <comman> --from=<name>

# docker in docker
- como manejar docker desde un contenedor, este concepto parte de que se necesita crear un contenedor sin la necesidad de poder correr docker sin que sea de forma nativa en la maquina host (escribir los comandos directamente), con docker in docker, podemos ejecutar un contenedor que contenga docker y a través de una conexion por socket podemos ejecutar los comandos de docker.
    - docker run -it -v /var/run/docker.sock:/var/run/docker.sock docker:<version>


