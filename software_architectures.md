# Arquitecturas de software



# Arquitecturas de 3 capas
Las arquitecturas de 3 capas son un estilo muy común de arquitecturas de software y se caracterizan por dividir la aplicación en 3 capas distintas, cada una de ellas con responsabilidades especificas. Este enfoque facilita la modularidad, mantenibilidad y escalabilidad del sistema. A continuación te voy a explicar cada una de las capas que puede contener este tipo de arquitecturas:
1. **Capa de presentación:** Esta es la capa con la que interactúan los usuarios finales, sus principales responsabilidades son:
   - Presentar la información al usuario de forma adecuada (UI/UX).
   - Capturar y validar datos introducidos por el usuario.
   - manejar la navegación e interacción del usuario.

    La capa de presentación por lo general se encarga de interactuar con la capa de lógica de negocio o **Dominio**.

2. **Capa de Dominio (Lógica de negocio):** También conocida como capa de aplicación, es el núcleo funcional lógico de la aplicación y sus principales responsabilidades son:
   - Implementar la lógica de negocio y reglas del dominio.
   - Procesar y coordinar operaciones solicitadas desde **la capa de presentación**
   - Realizar cálculos, validaciones y toma de decisiones basadas en las reglas de negocio.

    La capa de dominio es la encargada de comunicarse con **la capa de acceso de datos** para persistir o recuperar la información necesaria.

3. **Capa de Acceso de datos:** Es la encargada de interactuar con el almacenamiento persistente de datos, como una base de datos. Entre sus principales responsabilidades están:
   - Realizar operaciones CRUD (crear, leer, actualizar, eliminar) sobre los datos.
   - Abstraer el acceso especifico a la base de datos o sistema de almacenamiento.
   - Optimizar consultas y transacciones para mejorar el rendimiento.
   - Mantener la integridad y consistencia de los datos almacenados.











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






