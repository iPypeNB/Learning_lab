# Django

## Breve historia de la web
en los inicios de la web, los sitios web era sitios basados en texto, es decir la construcción del sitio estaba basada solo en **HTML** y no eran sitios interactivos con el usuario, con el paso del tiempo los sitios web tuvieron la necesidad de tener conexión a las bases de datos por lo que se implementaron en los sitios web los **CGI Scripts** (common gateway intarface: son una interfaz en los sitios web que les permite ejecutar scripts como aplicaciones de consola en el servidor, generando así paginas dinámicas), el problema de los **CGI Script** era que no eran muy escalables y su sostenibilidad no era optima, es de este problema donde **PHP** toma popularidad.

**PHP** tomó gran popularidad ya que permitía agregar la lógica de los Scripts dentro de los Templates en los sitios web, esto tenía el problema de que en muchas ocasiones se tenía que repetir el código dentro de los templates, es de ahí donde nacen los **Frameworks web** estos Frameworks permiten resolver muchos de los problemas que existían en la web en esos momentos ya que manejan: peticiones **HTTP**, conexiones a una base de datos, consultas a tablas, interacciones con las vistas o los templates **HTML**, etc.

## Historia Django
Django nace en 2003, gracias a dos desarrolladores que trabajaban en un sitio de noticias, donde había la necesidad de publicar muchos sitios web. Estos desarrolladores diseñaron **Django** con la filosofía de poder crear sitios web de forma ágil y que estos sitios web pudieran ser escalables.

## Conceptos

### WSGI
**Web server gateway intarface** es una especificacion que describe como se comunica un servidor web con una aplicación web y como se puede llegar a encadenar diferentes aplicaciones web para procesar una solicitud/peticion (reuqest), **WSGI** es un standar python que está escrito en detalle en la especificación _PEP 3333_. 

¿Porque nace la necesidad de crear un **WSGI**? Esto es necesario ya que antes la peticiones recibidas por el servidor web no eran completamente comprendidas por la aplicación web de python, esto dificultaba el trabajo de lo desarrolladores ya que tenian que escribir diferentes códigos _uno para cada tipo de peticion recibida por el servidor web_. **WSGI** permitó estandarizar la manera en como un servidor web se comunica con la aplicación web de python.

Actualmente el servidor **HTTP WSGI** más utilizado para el desarrollo de aplicaciones web en python es **_Gunicorn_**.

### ASGI


## Iniciar un proyecto django
siempre que se trabaja con python es importante crear un entorno virtual ya que este nos permite instalar los paquetes necesarios del proyecto deseado sin generar conflicto con lo paquetes instalados para otro proyecto. Teniendo el entorno virtual de Python se instala el paquete de Django con el siguiente comando:

- pip install django -U

teniendo el paquete de django instalado ya tenemos acceso al comando **django-admin** este comando nos permite iniciar un proyecto:

- django-admin startproject  _`name_project`_

### Contenido de un nuevo projecto
cuando se crea un nuevo proyecto en django el contenido del proyecto es el siguiente:

- __`name project/`__: Carpeta que contiene los archivos necesarios para el funcionamiento del **service web**.
    - **__ init__.py**: El objetivo de este archivo es declarar al proyecto creado como un modulo de python.
    - __settings.py__:  Define todas la configuraciones del proyecto (web service).
    - __urls.py__: Es el archivo encargardo de administrar la peticiones que lleguen al web service
    - __wsgi.py__: Es el archivo usado durante el deplyment durante la produccion y es la interfaz wsgi con nuestro proyecto en django.
- __manage.py__: Este archivo lo que hace es generar una intefaz sobre _django-admin_ y permite ejecutar ciertos codigos desde consola para interactuar con el proyecto en django.

## Comandos django-admin consola

## Comandos manage.py consola

## Objeto Request
El objeto request es el encargado de almacenar las peticiones realizadas por el usuario, en django cuando se recibe una solicitud (request) el objeto request se procesa de la siguiente manera:
1. En el archivo settings.py busca el contenido de la variable **ROOT_URLCONF**. Esta variable debe contener una direccion a un archivo, que por defecto es el archivo url.py.
1. Dentro del archivo definido por **ROOT_URLCONF** busca la variable **urlpatterns** que debe ser una lista de _paths_ que van a corresponder a los _paths_ del sitio web.
1. Va a recorrer la lista de **urlpatterns** hasta encontrar una ruta que conincida con la recibida en la petición (request).
1. Cuando se encuentra la ruta especificada se utiliza la funcion definida como segundo parametro en la ruta _path_, a esta funcion se le pasan lo siguientes valores:
    - instancia del objeto httpRequest.
    - si la url pasa mas argumentos para lo argumentos.
    - si se definen arugmentos adicionales (kwargs) se envian estos argumentos.
1. si la url en le request no coincide se envia una excepcion.

## Apps Django
El concepto de **proyecto** en django hace referencia a la aplicacion web, el paquete del proyecto python se define principalmente en el modulo settings.py. Cuando se incia un proyecto Django el directorio raiz (el que contiene el archivo manage.py) del proyecto suele ser el contenedor de todas las aplicaciones que no se instalan por separado (todas las aplicaciones creadas por el desarrollador).

Una App en Django describe a un paquete de python que proporciona un conjunto de caracteristicas. las Apps pueden ser reutilizadas en varios proyectos, para instalar una aplicacion en un proyecto django se pueden utilizar los siguientes comandos:
- python3 manage.py startapp _`name_app`_
- django-admin startapp _`name_app`_




 



