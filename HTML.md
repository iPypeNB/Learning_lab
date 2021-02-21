# HTML
HTML (Hyper text markup language) es un lenguaje de marcado para la elaboracion de paginas web, este es el lenguaje que se utiliza para darle estructura a la informacion presentada, siempre que se trabaja en html el documento (.html) principal se debe llamar "index.html" esto de debe a que cuando un servidor inicia un proyecto con html este busca por defecto el archivo llamado "index.html", a pesar de que esto se puede cambiar este nombre se convirtio en una convencion. 

## Tipos de paginas web

### Pagina estatica
Las paginas estaticas son aquellas paginas que estan construidas esclusivamente para la presentacion de informacion y no interactuan de forma dinamica con el usuario, es decir el usuario no tiene la posibilidad de cambiar esta informacion presentada a estas paginas tambien se les conoce como paginas informativas por lo que estan diceñadas solo para presentar informacion, estas paginas no estan conectadas con una base de datos ya que no se necesitan hacer cambios de informacion.

### Pagina Dinamica
Las paginas dinamicas son aquellas que estan diseñadas para la interaccion con el usuario ya que el usuario puede cambiar la informacion presentada y generar interacciones con la pagina, a estas paginas se les conoce web apps y si deben estar conectadas con una base de datos.

etiquetas contenedores - tienen mas etiquetas adentro
etiquetas de contenido - son la que llevan el texto imagene, o cualquier cosa que se va a renderizar en el proyecto.

## Etiquetas de multimedia 

### tipos de imagenes
En HTML cuando se habla de tipo de imagenes (mas alla de la extension de las imagenes) hay dos tipos de imagenes que se definen como imagenes con perdida (lossy) o imagenes sin perdida (lossless)

- Imagenes Lossless: los formatos de imagenes sin perdida son formatos que capturan todos los datos de su archivo original. no se pierda la calidad, resolucion, etc. del archivo original. esto toca tomarlo en cuenta ya que estas imagene puede tener un gran peso sobre la pagina web.
- Imagenes lossy: los formatos de imagenes con perdida son formatos donde la imagen resultando en la pagina web tiene perdidas con respecto al archivo original pero siempre se tiende a aproximar a el archivo original, una imagen con perdida podria reducir la cantidad de colores o analizar el archivo original en busqueda de daos innecesarios, esto puede reducir el tamaño de la imagen, la resolucion, etc. dando como resultado la reduccion de la calidad de la imagen.

extension con sus formatos:
- Gif: lossless. (graphics interchange format)
- png: lossless. (png 8 - 256 colores, png 24 - mas de 256 colores) (portable network graphics)
- jpg/jpeg: lossy. (Join photographic experts group).
- svg: lossless (Scalable vector graphics)

NOTA! tamaño optimo promedio de las imagenes 70 Kb.
- para comprimir png y jpeg: Tiny PNG.
- retirar los metadatos: Verefix.


- repo para descargar imagenes pexels.com

Etiqueta imagen
etiqueta IMG
- tienes 2 parametros:
    - src: fuente origen de la imagen, puede ser un link (un repo donde se encuentran almacenadas las imagenes (s3 amazon)) o puede ser una direccion local. (importante es que las carpetas no pueden contener un espacio en su nombre.)

par poder poner un espacio poner un espacio y que el navegador lo pueda comprender hay que utilizar caracteres especiales para que el link http lo pueda interpretar.

en esta pagina se encuentran los coding especiales para las url. https://secure.n-able.com/webhelp/NC_9-1-0_SO_en/Content/SA_docs/API_Level_Integration/API_Integration_URLEncoding.html

tambien para reemplazar los espacion se puede usar _

- parametro alt: es la descripcion de la imagen, sirve para tener accesibilidad a la imagen.

etiqueta FIGURE
nos permite crear un contenedor donde podemos poner las imagenes.
figcaptio: es una etiqueta que nos permite poner una descripcion de la imagen que va a ser visual.

### etiqueta video
esta contiene varios atributos,
src: fuente origen del video
controls: muestra los controles del reproductor.
preload: permite que el video se precargue cuando la pagina se renderiza en el navegador.
dentro de src se puede ponder como estension #t="tiempo inicio","tiempo fin".












