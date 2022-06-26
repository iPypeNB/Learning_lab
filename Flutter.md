# Que es flutter
leguaje de programacion


en flutter todo es un widget.

# lenguaje crossplatform vs nativos
jasfdsfdjñioadsfjio

# lenguaje declarativo
asdf

# Caracteristicas de flutter
- En flutter todo es un widget
- programacion declarativa

# que es un widget
es un elemento de una interfaz gráfica de usuario que muestra la información o proporciona una forma específica para que el usuario interactue con el sistema y o aplicacion.

# que es un arbol de widgets
esto nace de la forma en como los widgets se van colocando el el codigo. en flutter existe un widget principal mediante el cual se van derivando muchos mas widgets (childrens) y esto a su vez pueden contener mas. como un tronco derivando en sus ramas.

# materialapp
es la principal importacion de flutter

# myhomepage
una clase que hereda material app creo.

# scaffold
estructura donde se soportan muchos widgets.
appBar, Center (body), floatingactionbutton (no soporta mas hijos).
no tiene atributo children, pero tiene atributos que soportan el contenido de lo children.

# children
recibe muchos "hijos" un array de widgets indefinido.
# child
recibe un solo hijo.

# widget hijos
- cero hijos: image, text, richtext, icon, etc.
- un hijo: container, padding, raisedbutton, center, positioned, align.
- varios hijos: column, row, stack, wrap.

# Widgets basicos de flutter
- Text: el widget de texto permite insertar texto y manejar sus propiedades
- Row: El widget row, se compone de propiedades children que permite conteneer multiples widgets y ordenaros en una fila
- Colum: El widget column, se compone de propiedades childer que permite coteneer multiples widgets y ordenarlos en una columna
- Stack: El widget stack permite acomodar un elemento sobre otro (sobre poniendolo). contiene childrens.
- Container: El widget container genera un elemento como si fuera una caja a la cual le ponemos agregar otros elementos y definir sus propiedades margenes, border, paddding, etc. esto seria como un div en html.

# tipos de widgets
- widgets con estado (statefull widget):
    - son lo widgets en los cuales el usuario tiene una interaccion directa con la interfaz ( checkbox, form, button (segun el caso), etc.)
- widgets sin estado (stateLess widget):
    - son los widgets con los que el usuario no tiene interaccion (texto, icono, imagenes, contenedor de color).

# metodo build
se encarga de retornar un arbol de widgets que se van a dibujar en la interfaz.

# layout
- diagramar los layouts: nos permite decomponer una interfaz o mockup en sus diferentes partes para poder identificar cuales son los widgets o contenedores que necesita la interfaz.
- diagrama widget tree: nos permite organizar todo en un diagrama de arbol.


## Flutter desde la terminal
- flutter create nombre_del_proyecto : crea un nuevo proyecto en flutter
- flutter emulators: muestra los emuladores disponibles para el desarrollo del proyecto.
- flutter emulators --create nombre_del_emulador
- flutter emulators --launch nombre_del_emulador
- flutter run: ejecuta el proyecto.

## patron de diseño
singleton - bloc -clean

## como manejar la arquitectura bloc en una aplicacion profesional.
el bloc debe estar de forma general, en flutter hay componentes que nos permiten manejar el bloc de forma general en toda la app (provider) Global singleton (el componente se llama provider) expone el contenido del bloc a un nivel general en la aplicacion. Con esto podemos manejar varios bloc con diferentes providers. por eso se genera un bloc provider de forma global y que sea lo mas generico posible.

como implementar bloc provider: https://pub.dev/packages/generic_bloc_provider

para el diseño de aplicaciones mobile, siempre es mejor no quemar codigo y menos en los tamaños, es mejor utilizar porcentajes esto se puede lograr en flutter con MediaQuery.

