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
```md
----------------       ----------------       ----------------
| Capa de        | <-- | Capa de        | <-- | Capa de        |
| Presentación   |     | Lógica de      |     | Acceso a       |
| (UI/UX)        |     | Negocio        |     | Datos          |
|                | --> | (Aplicación)   | --> | (Persistencia) |
----------------       ----------------       ----------------
```
- **Capa de Presentación:** Interactúa con el usuario final a través de una interfaz gráfica (como una aplicación web, móvil o de escritorio).

- **Capa de Lógica de Negocio:** Implementa las reglas del negocio y procesa las solicitudes recibidas desde la capa de presentación.

- **Capa de Acceso a Datos:** Gestiona la persistencia de los datos en un repositorio, como una base de datos relacional o no relacional.



