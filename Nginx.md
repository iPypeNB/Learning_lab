# que es nginx.
- nginx es un servidor http que fue creado a partir de la necesidad de multiples sitios web que tenian altas demandas diarias en su paginas, nginx esta "especializado" en sitios web estaticos aunque tambien puede manejar sitios web dinamicos. nginx también funciona como balanceador de carga, proxy inverso, y servidor proxy.

# comandos y directivas de Nginx

# comandos
- nginx: sirve para lanzar el servidor nginx
- nginx -s stop: detiene el proceso nginx o el servidor nginx que está corriendo (cierre rapido).
- nginx -s quit: cierre "elegante" se podria considerar como cierre completo.
- nginx -s reload: recarga el servidor nginx que esté corriendo en ese momento.
- nginx -s reopen: reapertura de los archivos de registro.
- nginx -t: hace un testing al archivo de configuracion de nginx.

# directivas de gninx
- NGINX consiste en modulos controlados por directivas especificadas en el archivo de configuración, las directivas se dividen entre directivas simples y directivas de bloque.
    - una directiva simple consta de el nombre de la directiva, los parametros y finaliza en punto y coma: <name directive> <params>;
    - una directiva de bloque consiste en el nombre de la directiva y finaliza con llaves donde se puede agregar contenido o mas directivas, si una directiva de bloque puede contener otras directivas de bloque a esta se le llama contexto: <name directive>{}
- las directivas de nucleo son la directivas que se encuentran en la parte externa del archivo (no estan dentro de la llaves), funcionan de forma "global".
- las directivas son el proceso o grupo de procesos que pueden  ser ejecutados a traves del archivo .conf.

# directivas simples
- las directivas simples son aquellas directivas que no contiene un contenido interpretado por llaves.
    - daemon on || off : hace que nginx se ejecute en segundo plano.
    - debug_points: activa los puntos de depuracion.
    - env: redefinir variables de entorno (variables globales).
    - worker_processes: crear varias instancias o varios procesos del mismo nginx.
    - load_module: permite al archivo nginx cargar diferentes modulos.
    - error_log: define las rutas para el archivo de error log, en este archivo se pueden agregar diferente informaciones:
        -  debug, info, notice, warn, error, crit, alert.
    - lock_file: nos permite crear un archivo de bloqueo.
    - log_not_found: permite crear un archivo con los informes de paginas no encontradas (error 404).
    - pid: permite almacenar en un archivo de texto el id del proceso.
    - master_process: permite que nginx se ejecute varias veces en el equipo. 
    - user: define un usuario que le permita otorgar permisos de administrador en en el sistema operativo instalado.

# directivas contexto.
- son aquellas directivas que pueden contener otras directivas dentro
# directiva de eventos.
- esta directiva nos permite definir la eficiencia con la que trabaja nginx dentro de la red (afectan el procesamiento de la red).
    - worker_connections: define el numero de usuarios que se pueden conectar de forma simultanea en nginx.
    - use: define el modelo de eventos, la forma en como va a trabajar nginx en el sistema operativo (epoll es el default en linux)
    - accept_mutex: permite habilitar o deshabilitar que los procesos de trabajo acepten nuevas conexiones por turno.
    - accept_mutex_delay: define el tiempo de espera para los turnos de las conexiones.
    - debug_connection: permite definir un archivo log para ciertas direcciones ip.
    - multi_accept: permite aceptar multiconecciones simultaneas.

# directiva http
- la directiva http es donde va la función principal de nginx que permite definir los servicios html, proxy o de balanceo de carga, este contexto proporciona las configuraciones especificadas para los servidores http.
    - server: nos permite definir la configuración de un servidor virtual, en esta directiva no existe una separacion clara entre servidores virtuales basados en ip (direcciones ip) y servidores virtuales basados en nombres (basados en el campo de encabezado de solicitus "host").
    - listen: esta directiva describe todas las direcciones y puertos que se deberian permitir para establecer conexiones con el servidor. puede establecer la direccion con el puerto para una conexion ip, o la ruta para un socket de dominio UNIX en el que el servidor aceptará solicitudes, se puede especificar la direccion sin puerto o el puerto sin direccion  y una dirección también puede ser un nombre de host.
        - direcciones ipv4
            - por defecto si no se especifica el puerto el utilizado es el 80.
            - listen <address>:<port>;
            - listen <address>;
            - listen <port>;
            - listen <name host>:<port>;
        - direcciones ipv6
            - listen [::]:8000;
            - listen [::1];
        - dominio UNIX unix socket
            - listen unix:/var/run/nginx.sock
        - default_server: es un parametro que define el servido que funcionara como servidor por defecto.
            - listen <address>:<port> default_server.
        - ssl: este parametro permite especificar que todas las conexiones aceptadas en este puerto deben funcionar como ssl.
        - http2: configura el puerto para aceptar conexiones http/2, normalmente para que esto funciones también se debe especificar el parametro ssl.
        - proxy_protocol: permite especificar que todas las conexiones aceptadas en este puerto deben utilizar el protocolo proxy.
        - en la directiva listen hay varios parametros adicionales para las conecciones de socket-relacionado, estos parametros pueden ser especificados para cada directiva listen utilizada, pero solo pueden ser usados una ves por cada par de puertos <address>:<port>, algunos de estor parametros pueden ser:
            - ipv6only: este parametro determina si un socket ipv6 que escucha en una direccion comodin [::] aceptará solo conecciones ipv6 o tanto conecciones ipv4 como ipv6.
            - bind: instruye para hacer una llamada bind separada para una dirección dada <address>:<port>, esto es utíl si hay varias directivas listen con el mismo puerto pero diferentes direcciones y una con todas la direcciones asignadas a ese mismo puerto.
            - backlog: limita la longitud maxima de conexiones en cola, de la lista de conexiones pendientes.
    - location: establece la configuracion de un "servidor" en funcion de su dirección URI establecida. (establece las configuraciones de las direcciones internas del servidor.), la directiva location puede estar definida por una cadena de prefijo (prefix string) o por una expresion regular.
        - las espresiones regulares pueden ser especificada con el precedente "~*" que no diferencia entre mayusculas o minuscular o con "~" que si diferencia entre mayusculas o minusculas. 
    - default_server: define un servidor en especifico como el servidor por defecto.
    - server_name: permite listar los nombres de los servidores virtuales.
    - server_name_in_redirect: se utiliza para poder redireccionar un servidor virtual a otro URL, esto se utiliza cuando se está implementando un formato de URL'S amigables.
    - port_in_redirect: permite definir si se redirecciona el numero del puerto.
    - tcp_nodelay: define el tiempo de espera de las conexiones socket.
    - tcp_nopush: intenta emitir varias respuestas http en un paquete tcp.
    - sendfile: permite hailitar el kernel sendfile para la transmision de archivos.
    - reset_timedout_connection: permite que la info de usuario se conserve a pesar de que se supere el tiempo de espera.
    - sendfile_max_chunk: permite definir el maximo tamaño de datos que se va a utilizar cuando se va a enviar con sendfile.
    - send_lowat: permite hacer uso del slowat, define el numero minimo de bytes en el buffer.
    - server_name_hash_max_size: permite definir el tamaño maximo para las tablas de hash que maneja nginx.
    - root: establece el directorio raiz para la solicitudes, define el lugar donde se encuentran los archivos dentro del sitio web, esta directiva se puede especificar dentro de http, server, location, if. En root la direccion se coloca pero no se coloca el slash (/) al final.
    - alias: define el reemplazo para una ubicacion especificada. esta directiva solo va dentro de la directiva location.
    - error_page: defien la URI (pagina web) que se mostrara para los errores especificados, con esta directiva se puede definir un location @error que redireccione a la pagina especificada como error.
    - if_modified_since: Especifica como comparar el tiempo de modificación de una respuesta con el tiempo en el request de cabecera, verifica las fechas de modificación de un servidor con el estado actual. 
    - index: define los archivos que se van a utilizar como indice, el nombre del archivo puede contener variables, los archivos se verifican en el orden especificado. 
    - try_files: comprueba la existencia de los archivos en el orden especificado y utiliza el primer archivo encontrado para procesar la solicitud.
    - keepalive_requests: permite tener autenticado al usuario dentro del servidor, esto se define según el numero de peticiones, de forma predeterminada está en 100.
    - keepalive_timeout: define que tanto debe esperar el servidor para cerrar una conexion, por defecto viene con un valor de 75.
    - keepalive_disable: sirve para desactivar el keepalive y resolver esos temas de compatibilidad con los navegadores.
    - send_timeout: especifica el tiempo despues del cual nginx cierra una conexion inactiva, el valor por defecto es de 60.
    - client_body_in_fiel_only: define que las peticiones realizadas por el cliente sean almacenadas en el disco en vez de ser almacenadas en la memoria.
    - client_body_in_single_buffer: permite definir si se deberia almacenar las peticiones de forma simple en el buffer de memoria.
    - clietn_body_temp_path: permite definir el directorio donde almacenara los archivos con el cuerpo de las peticiones, con esto se puede defirni una estructura de niveles para almacenar las peticiones.
    - client_body_timeout: define la inactividad mientras se está leyendo una petición del cliente, define el tiempo de espera.
    - client_header_buffer_size: define el tamaño del buffer que nginx asigna a las cabeceras.
    - client_header_timeout: definer el tiempo de espera de inactividad mientras lee una peticion por la cabecera del sitio web.
    - large_client_header_buffers: permite alargar el tamaño del buffer, funciona como extención del tamaño del buffer.
    - lingering_time:  esta directiva define el tiempo de espera para que lleguen más datos del cliente.
    


    