# Historia de los servidores
avance la virtualizacion
# Que es la nube
Son unos servicios de computo ofrecidos por unos proveedores que permiten a los usuarios disminuir los costos de crear un servicio en la web.
En la actualidad existe un concepto de pago por uso de los servicios y yendo un poco mas alla se esta utilizando una arquitectura llamada serverless en la que el proveedor se encarga de ofrecer servicios completamente administrados siendo ellos los que actualizan el software, se encargan del mantenimiento y demas tareas que requieren los servidores. La ventaja actual con estas nuevas infraestructuras y servicios es que "teoricamente" no existe un limite en cuanto a computo y almacenamiento, ya que a medida que se va necesitando mas poder de computo el proveedor me lo puede ofrecer de forma automatica.

## caracteristicas de un servicio de la nube
- Autoservicio.
- Amplio acceso de conectividad.
- Recursos compartidos.
- Elasticidad rapida.
- Servicio medible.

# Como es la infraestructura de Google
conectividad de ultima milla.
sustentabilidad, fuentes renovables.
flexibilidad en cobro.
estandares de lenguaje.
Portafolio de soluciones.
- computo.
    - compute engine
    - kubernetes engine
    - app engine
    - cloud functions
- Storage.
    - Bigtable.
    - Cloud Storage.
    - Cloud SQL.
    - Cloud Spanner.
    - Cloud datastore.
- Big Data.
    - Bigquery.
    - Pub/sub.
    - DataFlow.
    - Dataproc.
    - Datalab.
- Machine Learning.
- IOT.

# Como se organiza la administracion de servicios en google cloud platform.
Lo primero que debemos tener en google cloud platform debe ser un pryecto el cual cuenta con las siguientes caracteristicas.
- Proyect name:  es enteramente estetico y se puede cambiar.
- Proyect Id: es unico y no se puede cambiar.
- Proyect number: es un numero que asigna google, esta asociado a temas de facturacion y soporte, esta caracteristica tampoco se puede cambiar.

Los proyectos sirven para tener todos los recursos agrupados de forma tal que se puede diferenciar y delimitar de forma muy sencilla, ejemplo de organizacion: proyecto para  produccion, proyecto para QA, proyecto para desarrollo.

## integraciones con herramientas populares.
- visual studio IDE.
- microsoft powershell.
- Jet brains.
- Android studio.
- API's REST.
- google cloud shell.
- Bibliotecas para multiple lenguajes.
- Aplicacion movil.

## Permisos para los usuarios.
la administracion de las personas en google cloud se hace a traves de IAM.
- Viewer: solo tiene acceso de nivel de lectura.
- Editor: tiene permisos de editar y leer los elementos dentro del servicio de google cloud.
- Owner: Es el usuario que tiene el control absoluto en el proyecto. (es recomendable tener como minimo 2 cuentas Owner)
    - se recomienda tener cuentas de servicio que tengan permisos de editor para que puedan crear diferentes servicios y que no esten ligadas a una persona.

