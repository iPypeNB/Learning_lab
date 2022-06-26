arquitectura

nos permite estructurar, diseñar y proyectar

arquitectura de software
- indica la estructura, funcionamiento e interaccion entre las partes de software.
- Nos permite tener un codigo organizado y legible, permitiendo tener posteridad y mantenimiento a futuro.

principios SOLID

Roles en un equipo.

UX designer
IU designer
DB Admin
DEV (desarrollador)
PM (Project management)

Tipos de arquitecturas

Vanilla:

En esta arquitectura la lógica y la vista se colocan en el Widget. Su principal beneficio es que es simple y autónoma. Conectado en cualquier parte de tu aplicación, recuperará y renderizará datos.

Por otro lado, escribir widgets de esta manera puede generar caos en el documento de vista de la app, sobre todo cuando la lógica empieza a extenderse a bifurcarse o es más avanzado.
´´´flutter
Widget _buildInit() {
    return Center(
      child: RaisedButton(
        child: const Text('Load user data'),
        onPressed: () {
          setState(() {
            _isLoading = true;
          });
          widget._repository.getUser().then((user) {
            setState(() {
              _user = user;
              _isLoading = false;
            });
          });
        },
      ),
    );
  }
´´´

patrones de diseño de software

Scope Model

Este es una librería de terceros Puedes encontrar toda la información aquí que no está incluída. Es extraída del código base del Sistema operativo Fuchsia.

En esta arquitectura cuando un Widget cambia de estado se reconstruye el árbol completo (Toda la pantalla). En realidad esto no es tan conveniente pues lo que quisiéramos que sucediera idealmente es reconstruir solo el widget que está cambiando y no los otros.

https://pub.dev/packages/scoped_model

Esta arquitectura es buena pues cumple con el Principio de Single Responsability pues separa la lógica del negocio de la UI, pero en general el mantenimiento de este se vuelve complejo por la grande dependencia entre Widgets, debes controlar muchos casos para lograr el efecto que quires dar a tu aplicación.

BLoC business logic components.
es un patron de diseño que nos va a ayudar a separar la logica del negocios y la interfaz grafica.

BLoC pattern

view - vista se divide en 2 partes, en screens y en widgets.
BLoC - logica de negocio, funciones logicas, casos de uso. define la respuesta de ciertas acciones.
Repository - clases que se conectan a una fuente de datos.
data/model - PODO: plain old dart object

carpetas
- src
    - bloc
    - models
    - resources
    - ui
    - app.dart
- main.dart

Clean Arquitecture: es exponer las entidades para que sea mas claro comprender de que se trata el bloyecto.

blocprovider -> esto se debe a que muchas vistas necesitan de una misma logica bloc, lo que genera la necesidad de que el blocprodiver este en el mismo nivel que material app. hay una libreria en flutter que nos permite hacer el manejo de bloc de forma generica.






