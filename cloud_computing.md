# Arquitectura de alta concurrencia
Hablamos de una arquitectura de alta concurrencia cuando las necesidades de computación superan las capacidades de un solo servidor, es decir, cuando el numero de usuarios o el numero de tareas superar la capacidad computacional de un solo servidor y esto genera que se deban dividir las tareas en multiples servidores.

## Monolitica:
esto consiste en crear una aplicacion autosuficiente que contenga todas las funcionalidades necesarias para realizar las tareas que requiere el proyecto. lo cual implica que corre en un solo servidor.

## Microservicios:
Microservicios: Cuando se empieza a desarrollar con muchas personas a la vez.
Metodologías para la concurrencia de un sistema.
Los microservicios se usan por:
*Poder escalar de forma independiente
*Nos permiten desarrollar mucho mas fácil
Que modelos y patrones debe conocer un desarrollador
*Uso de proveedores en la Cloud

AUTOSCALING ANIDADO
Es un poco complejo implementar el escalado, ya que en mi caso requerí de mucha información y parametrización para poder implementar lo que le llamamos escalado horizontal anidado.

Teníamos una aplicación corriendo en Kubernetes y que tenía mínimo 1 pod y máximo 3 corriendo. Todo bien, después con el tiempo nos dimos cuenta de que la usabilidad de la aplicación iba creciendo exponencialmente y al no estar preparados la aplicación comenzó a experimentar fallos (a pesar de usar kubernetes en AWS).

Que decidimos hacer?

medimos las horas pico de usabilidad
medimos la cantidad de recursos que se utilizan en esas horas
con base a ello se parametrizó de manera más eficiente la cantidad de pods que se utilizarán y los disparadores que crearán estos pods.
Pero la legión del mal atacó nuevamente. Sin embargo esta vez el servidor que servía como worker node estaba saturado por lo que teníamos que tomar una decisión:
¿Le incrementamos en recursos?
Sabíamos que incrementar en recursos no era muy eficiente, puesto que solo se utilizaría en cierta cantidad de tiempo. Por otro lado el hecho de incrementarle recursos implicaba apagar la máquina virtual así como tratar de parametrizar la hora más eficiente para subir los recursos

¿Qué decidimos hacer??

volver a medir, medir y medir.
separamos el plano de datos (media) que vivían en el servidor (worker node) y lo implementamos via EFS con el fin de evitar inconsistencias de datos.
implementamos crecimiento horizontal de los worker nodes con el uso de autoscaling groups.
voila (como dicen en España ese servicio no lo tumba ni Dios)

# como se sabe cuando un microservicio necesita escalamiento horizontal o vertical.

escalamiento vertical: agrandar el tamaño de la instancia (aumentar ram, procesador etc.) cuando el procesamiento de las tareas (como cuando una sola tarea es muy pesada) es mejor utilizar el escalamiento vertical.
escalamiento horizontal: creamos mas instancias (mas servidores) cuando la implementacion de una tarea supera la capacidad computacional se usa el escalamiento horizontal.

MySQL (escalamiento vertical) las relacionales es mejor hacer escalamiento vertical
MongoDB (escalamiento horizontal) las no relacionales es mejor hacer escalamiento horizontal


# stateless o stateful

Para construir una arquitectura de alta concurrencia no cabe duda que tambien es necesario ayuda de los devs, ya que las apps a desplegar escalaran mejor si son stateless (no siempre se puede pero se prefiere que sean asi).

Una buena practica para que las app que los devs construyan sean escalables (por ende que soporten la alta concurrencia) es que sean Dockerizables, para esto existe una serie de “normas” que deben cumplir llamada The twelve-factor app https://12factor.net/es/

https://12factor.net/es/


Stateless: El estado está fuera de la aplicación.
Statefull: El estado está dentro de la aplicación.

Un servidor stateless lo puedo crear sin el servidor viejo, pero un servidor statefull como el de una base de datos se necesitan los registros del historial, es decir, guarda ESTADOS como lo podrían ser los registros.

Es preferible que una aplicación sea stateless.

en la recomendacion 6, es donde se menciona que sean stateless

statess: procesamiento de datos, lo procesa y lo devuelve al cliente. con esto el servidor no necesita contener el estado anterios para poder crear un nuevo servidor.

stateful: se necesita el "historial" para poder crear un nuevo servidor (base de datos)

por ejemplo si hacemos un stateful que almacene imagenes al hacer un escalamiento horizontal va a ser mas dificil ya que este escalamiento de copiarse con todo e imagenes.

resiliencia en un sistema de alta concurrencia.

Para garantizar la Resiliencia de un sistema, debemos probar nuestro systema, desde la app hasta la infra de nuestra appa, para esto podemos hacer uso de estas dos grandes teorias:

Functional Testing
Son los tests que se llevan acabo para probar la funcionalidad de los features desarrollados de la app, podemos desarrollar por ej:

Unit Testing
Integration Testing
end to end testing
Non-Functional Testing
Estos son los tests que se llevan acabo en la aplicacion ya desplegada, no en produccion sino un hambiente controlado, lo mas parecido a prod, por ejemplo:

Performance Testing o pruebas de stress: donde medimos la capacidad de nuestra app de respodenr normalmente bajo una carga de stress
Recovery Testing: comprobamos que tan bien un sistema se recupera de un fallo de hardware
Security testing

cdn - content distribution network: correr un proxy

escalar bases de datos.

SQL es mas dificil, lo importante es utilizar correctamente bien los indices
usar replicas de lectura (se crea copias de la bd) y se crea un servidor que solo se encarga de las lecturas.

separar los servidores por ubicacion


CDN

un content delivery network o content distribution network (CDN), es un geographically servidor proxy donde esta cahcado tu contenido estatetico (puedes tener mas de uno en diferentes regiones al rededor del mundo, o donde mas clientes tengas), se usa para distribuir tu contenido en diferentes zonas geoghraficas con el fin de:
 

Mejorar la esperiencia de usuario: al distribuir tu contenido en varias zonas geograficas, tus usuarios se conectaran al CDN mas cernano, la latencia es menor.
Garantizar la disponibilidad de tu contenido (quizas un sitio web o videos): si tienes mas de un servidor de conetenido, si uno ya no esta disponible tus clientes pueden conectarse a otro, mas lejos seguramente, pero se conectaran a otro al final.
soportar alta concurrencia: puedes repartir la carga de request a travez de muchos mas servidores de contenido para no saturar a un solo server
 

Recomiendo complementar esta clase con este video de Fredy Vega llamado :
Cómo hacen los sitios más populares para estar siempre en línea
https://www.youtube.com/watch?v=7EiSiIIXAQQ&t=27s


lenguajes utilizados para servidores de alta concurrencia.

ptyhon
golang
c#

autenticacion de usuarios
Usuarios - Contraseñas - Tokens

Sistema externo
Sistema rápido (Redis - Mencach)
BackEnd de forma segura(Encargado IT) para contraseñas de acceso a base de datos.

los logs no deben almacenar los datos sensibles.

Gestores de orquestadores
kubernetes
openshift
docker swarm
K8s

Serverless
te permite correr funciones en la nube sin necesidad de un servidor.
permite escalar automaticamente con la alta concurrencia.
ventaja: cobros se puede tener delay al correr las funciones.

motores de bases de datos.
SQL - mySQL

NO SQL - MongoDB

¿Qué motores de bases de datos son recomendables utilizar para este tipo de aplicaciones?

Podríamos dividir los motores de bases de datos en dos grandes grupos: bases de datos relacionales y bases de datos no relacionales.

El motor principal para las bases de datos relacionales es MySQL, y el motor principal para las bases de datos no relacionales es MongoDB.

La principal diferencia entre una base de datos en cada uno de los motores mencionados anteriormente, es que MongoDB es un gestor de bases de datos orientado a documentos, que por lo tanto tiene un enfoque totalmente diferente en cuanto al almacenamiento de datos. La diferencia fundamental es que mientras todas las filas de una tabla de una tabla MySQL tiene la misma estructura, en MongoDB los documentos no están sujetos a un orden fijo. Las filas de las tablas de MySQL tienen un mismo número de valores (cada uno con los mismos tipos de datos), por su parte, los documentos individuales de MongoDB tienen su propia estructura; de esta manera es posible crear nuevos campos con cualquier valor, mientras que para una base de datos relacional, se necesitaría una re-estructuración completa.

Otra diferencia fundamental que resulta de la comparativa de estos dos tipos de motores de bases de datos, es el enfoque dado a la recuperación de datos: como base de datos NoSQL, MongoDB no utiliza SQL como lenguaje de consulta, disponiendo de su propio lenguaje para el procesamiento de datos; esto permite la comunicación entre MongoDB y el respectivo cliente. Para este fin, la base de datos utiliza los métodos específicos del correspondiente lenguaje de programación del cliente, valiéndose de la ayuda de las librerías que pueden ser descargadas desde su página web oficial.

Al ser un motor de bases de datos no relacional, escalar MongoDB es mucho más fácil, ya que cada parte de datos está hospedada en un shard. Al tener estos shards, podríamos comenzar a crear y agregar más datos y más shards a medida que nuestra aplicación crece. Este no es el caso con un motor de bases de datos relacional.

Escalar un servidor de bases de datos relacional puede ser muy complejo. Posiblemente la única forma de escalar este tipo de servidores de bases de datos es agregando réplicas o escalando verticalmente. Hay algunas soluciones para escalar este tipo de servidores de bases de datos de manera horizontal, pero son complicada y dependen totalmente del equipo de infraestructura.

Una de las herramientas que se pueden utilizar para escalar horizontalmente un servidor de bases de datos relacional, es Vitess, que es una herramienta Open Source que viene de la mano de la CNCF (Cloud Native Computing Foundation), que es una de las aceleradoras que se encargan de fundar proyectos Open Source. Vitess es usado por YouTube para escalar sus servidores MySQL de manera horizontal.

¿Qué tipo de caché es recomendable utilizar?

Aquí, hay dos grandes grupos de caché. Generalmente se utilizan para almacenar sesiones, valores pequeños y sobre todo para la autenticación. Este tipo de caché generalmente es usado porque es muy rápido de acceder y las principales herramientas son Redis y Mencach. Estas herramientas están disponibles en la mayoría de los proveedores y es muy fácil de integrar con cualquier aplicación.

Otro tipo de caché es el caché de internet, como por ejemplo, para permitir que nuestra página web funcione más rápido o se descarguen los archivos estáticos de una manera más rápida para nuestros clientes, y la tecnología más usada son los CDNs (Content Delivery Network).

CDN recomendado. principal uso cachear archivos estaticos.
https://platzi.com/blog/6-tips-para-gestionar-un-nombre-de-dominio-y-evitar-el-caso-notion/
https://www.cloudflare.com/es-es/case-studies/platzi/
cloudflare

Como manejar ataques DDOS en plataformas de alta recurrencia.
ataque de negacion de servicio. sobrecarga la aplicacion.
Un ataque de denegación de servicio distribuido (DDoS) es un intento malintencionado de interrumpir el tráfico normal de un servidor, servicio o red determinada, sobrecargando el objetivo o su infraestructura asociada con una avalancha de tráfico de Internet.

La efectividad de los ataques DDoS reside en el uso de sistemas informáticos vulnerables desde los que se origina el ataque de tráfico. Entre los equipos afectados puede haber ordenadores y otros recursos de red, tales como dispositivos IoT.

En términos generales, un ataque DDoS es como un atasco de tráfico que impide que llegues a tu destino.

Se bloquea en capa 4 y no en capa 7. Mediante IpTables

WAF: Nos ayuda a filtrar más que DDoS o es un complemento.

protocolos que se utilizan en las aplicaciones de alta concurrencia (API).
REST: formatos soportados xml json.
gRPC: El gRPC es recomendado para su uso en microservicios o para integraciones de APIs internas gracias a que ofrece una mayor escalabilidad y una optimizada respuesta por su baja latencia en el envío de mensajes por el formato binario de HTTP/2.

Por otro lado, REST es recomendado para integraciones con clientes y APIs públicas, muy fácil de usar y con unas restricciones de protocolo sencillas de implementar, además JSON es un lenguaje fácilmente interpretable por el humano. También posee una gran comunidad detrás que alimenta la documentación y las buenas prácticas del método de comunicación. Como desventaja hay que recalcar que por su formato es más pesado que gRPC (pero para los casos de uso donde es recomendado no es un gran factor a tener en cuenta).

https://www2.deloitte.com/es/es/blog/todo-tecnologia/2021/grpc-vs-rest-api.html

HTTP2 VS HTTP1.1


como comenzar con el negocio.

Empezar

Crear un monolito. Se puede utilizar Cache (sesiones - autenticaciones) - CDNs - Contenedores - Orquestadores
Después separar en funciones.
Usar funciones ServeLess para tareas asíncronas.
Estar cómodo **SUMERCED **con el lenguaje de desarrollo.

Todo en contenedores, preferible en **DOCKER **y un orquestador posiblemente K8s.

Métricas mediante CPU - RAM - Colas de mensajes.





