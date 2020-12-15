# que es nginx.
- nginx es un servidor http que fue creado a partir de la necesidad de multiples sitios web que tenian altas demandas diarias en su paginas, nginx esta "especializado" en sitios web estaticos aunque tambien puede manejar sitios web dinamicos. nginx también funciona como balanceador de carga, proxy inverso, y servidor proxy.

# comandos y directivas de Nginx

# comandos
- nginx: sirve para lanzar el servidor nginx
- nginx -s stop: detiene el proceso nginx o el servidor nginx que está corriendo.
- nginx -s reload: recarga el servidor nginx que esté corriendo en ese momento.
- nginx -t: hace un testing al archivo de configuracion de nginx.

# directivas de gninx
- las directivas son el proceso o grupo de procesos que pueden  ser ejecutados a traves del archivo .conf.
    - daemon on || off : hace que nginx se ejecute en segundo plano.
    - debug_points: activa los puntos de depuracion.
    - env: redefinir variables de entorno (variables globales).
    - worker_processes: crear varias instancias o varios procesos del mismo nginx.
    - load_module: permite al archivo nginx cargar diferentes modulos.
    - error_log: define las rutas para el archivo de error log.
    - lock_file: nos permite crear un archivo de bloqueo.
    - log_not_found: permite crear un archivo con los informes de paginas no encontradas (error 404).
    - pid: permite almacenar en un archivo de texto el id del proceso.
    - master_process: permite que nginx se ejecute varias veces en el equipo. 
    - user: define un usuario que le permita otorgar permisos de administrador en en el sistema operativo instalado.

# directiva de eventos.
- esta directiva nos permite definir la eficiencia con la que trabaja nginx.
    - worker_connections: define el numero de usuarios que se pueden conectar de forma simultanea en nginx.
    - use: define el modelo de eventos, la foma en como va a trabajar nginx en el sistema operativo (epoll es el default)
    - accept_mutex: permite habilitar o deshabilitar que los procesos de trabajo acepten nuevas conexiones por turno.
    - accept_mutex_delay: define el tiempo de espera para los turnos de las conexiones.
    - debug_connection: permite definir un archivo log para ciertas direcciones ip.
    - multi_accept: permite definir aceptar multiconecciones simultaneas.

# directiva http
- la directiva http es donde va la función principal de nginx que permite definir lso servicios html, proxy o de balanceo de carga.
    - server: nos permite definir un sitio web.
    - location: 
    - listen: especifica el puerto por el cual se va a estar escuchando.
    - default_server: define un servidor en especifico como el servidor por defecto.
    - server_name: permite especificar el nombre del dominio el cual va a tener el servidor.
    