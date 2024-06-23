# ElasticSearch
ElasticSearch es un motor de analítica y análisis distribuido y open-source para todos los tipos de datos, incluidos textuales, numéricos, geo-espaciales, estructurados y desestructurados. En muchas ocasiones se define como un motor de búsqueda, ya que se usa para buscar dentro de una colección de datos, sin embargo *ElasticSearch* sirve para búsqueda, observabilidad, visualización de datos, entre otros.

# Etapas de la búsqueda
## Indexación
Consiste en el proceso mediante el cual se organizan y estructuran los datos para hacerlos fácilmente buscables y recuperables. En esta etapa se incluyen varios subprocesos:
  - **Extracción:** Se extraen los datos que se van a indexar desde sus fuentes originales, como bases de datos, documentos, etc.
  - **Análisis:** Los datos se analizan y procesan. Esto incluye tokenización (división del texto en unidades como palabras), normalización (transformar todas las letras a minúsculas, etc.) y eliminación de palabras comunes (stop words).
  - **Almacenamiento en índices:** Los datos procesados se almacenan en un índice, que es una estructura de datos optimizada para búsquedas rápidas.
  <br>**_Nota: En ElasticSearch, el índice es similar a la tabla de una base de datos relacional, y cada documento es como una fila en dicha tabla_**
## Consulta
La etapa de consulta implica formular una solicitud para recuperar datos relevantes del índice, esto incluye:
  - **Formulación de la consulta:** Crear la consulta que especifica qué datos se están buscando.
  <br>_**Nota: En ElasticSearch, esto se hace a través de un lenguaje de consulta llamado Domain Specific Language - DSL.**_
  - **Expansión de la consulta:** En algunos casos, la consulta se puede ampliar automáticamente para incluir sinónimos o términos relacionados que puedan mejorar la relevancia de los resultados.
  - **Optimización de la consulta:** Ajustar la consulta para mejorar el rendimiento y la relevancia de los resultados. Esto puede incluir el uso de filtros, rangos y operadores booleanos.
  - **Ranking de relevancia:** Los documentos recuperados se ordenan en función de su relevancia con respecto a la consulta.
  <br>_**Nota: ElasticSearch utiliza un algoritmo de puntuación basado en TF-IDF (Term Frequency-Inverse Document Frequency)**_
## Presentación
Los resultados se presentan al usuario de una manera que sea fácil de entender y navegar:
  - **Formateado de resultados:** Los resultados se formatean para que puedan ser presentados al usuario. Esto puede incluir resúmenes, fragmentos de textos relevantes y destacando las palabras clave.
  - **Visualización:** Se le presentan los datos a los usuarios en una interfaz de usuario amigable que les permita analizar y explorar, además de poder agregar filtros adicionales.

# Documento
Un documento en ElasticSearch es la unidad básica de almacenamiento que se almacena y busca dentro de un índice. Es un objeto de datos estructurados para intercambio, y en ElasticSearch generalmente se utiliza el formato JSON.
```json
{
  "title": "Elasticsearch: The Definitive Guide",
  "author": "Clinton Gorey",
  "published_date": "2015-02-07",
  "genre": "Technology",
  "pages": 724
}

```
# Operaciones
## Escritura
La operación de escritura en ElasticSearch se refiere principalmente a la indexación de documentos, que incluye la creación, actualización y eliminación de documentos.
  - **Recepción de documento:** Un cliente (como una aplicación o usuario) envía una solicitud a ElasticSearch para indexar un documento. Esta solicitud contiene el documento en formato JSON y puede incluir un identificador `(_id)`.
  <br>_**Nota: Cuando no se agrega un identificador a un documento, ElasticSearch puede agregar uno por defecto automáticamente**_
    ```json
    POST /mi_indice/_doc/1
    {
      "title": "Introducción a Elasticsearch",
      "author": "Jane Doe",
      "published_date": "2022-01-15",
      "content": "Este libro es una guía completa sobre Elasticsearch."
    }
    ```
  - **Determinación del fragmento:** ElasticSearch un fragmento o *shard* es una unidad fundamental de almacenamiento y procesamiento de datos, estos permiten que un índice se divida en partes más pequeñas y manejables, lo que facilita la escalabilidad y la distribución de la carga de trabajo entre multiples nodos en un clúster. ElasticSearch utiliza un algoritmo de hash para determinar en cuál de los fragmentos (shards) del indice debe almacenarse el documento. Si no se proporciona un `_id`, ElasticSearch genera uno automáticamente.
  - **Análisis del documento:**
    - **Tokenización y Normalización:** ElasticSearch analiza el contenido del documento. Esto incluye dividir el texto en términos (tokenizar), convertir el texto a minúsculas (normalizar), eliminar palabras comunes (stopwords), etc.
    - **Creación de índice inverso:** Los términos resultantes se indexan en una estructura llamada índice invertido, que permite búsquedas rápidas basadas en palabras clave.
  - **Almacenamiento en el fragmento primario:**
    - **Escritura en fragmento primario:** El documento, junto con su índice invertido, se almacena en el fragmento primario correspondiente.
    - **Confirmación de escritura:** Una vez que el documento se almacena correctamente en el fragmento primario, se confirma la escritura de este fragmento.
  - **Replicación del documento:** ElasticSearch copia el documento a los fragmentos de réplica para garantizar la alta disponibilidad y redundancia de los datos, cada fragmento primario tiene uno o más fragmentos de réplica.
  - **Respuesta del cliente:** ElasticSearch envía una respuesta al cliente confirmando que la operación de escritura ha sido exitosa y proporciona detalles como el identificador del documento y el índice en el que se almacenó.
### Indexación a través de una API
  - **PUT:** Se utiliza para crear o actualizar un recurso en un indice. Es idempotente, lo que significa que realizar la misma operación varias veces tendrá el mismo efecto que realizarla una sola vez.
    - cuando se usa **PUT** para indexar un documento, se debe proporcionar un identificador único `_id` para el documento. Si el documento con ese `_id` ya existe, se reemplazará por el nuevo documento.
    - se utiliza **PUT** para crear índices, donde se especifica la configuración y el mapeo del índice.
  - **POST:** La petición se utiliza para la creación de recursos sin necesidad de especificar un identificador `_id`, y para realizar operaciones que pueden no ser idempotentes, como la búsqueda o actualizaciones parciales de documentos.
  <br>_**Nota: La principal diferencia entre la petición PUT y POST es que en la petición PUT debemos especificar el `_id` que vamos a operar, en la petición POST no es necesario**_

_**Ejemplo:**_ vamos a realizar un ejemplo práctico de como se indexa un documento en ElasticSearch.<br>
1. Se crea el índice en ElasticSearch llamado `library`:
```json
POST /library
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 1
  },
  "mappings": {
    "properties": {
      "title": { "type": "text" },
      "author": { "type": "text" },
      "published_date": { "type": "date" },
      "content": { "type": "text" }
    }
  }
}

```
2.  Indexamos un documento en el índice `library`
```json
PUT /library/_doc/1
{
  "title": "Aprendiendo Elasticsearch",
  "author": "John Doe",
  "published_date": "2023-06-20",
  "content": "Este documento trata sobre cómo funciona Elasticsearch y cómo se pueden realizar operaciones de escritura en él."
}

```
<br>_**Nota: Cuando se escribe una request como las presentadas en el ejemplo hay que prestar atención en que el JSON no puede tener más de un ENTER ya que ElasticSearch no lo va a interpretar como el BODY de la petición**_

<style>
  .warning-box {
    border-left: 2px solid orange;
    padding: 10px;
    background-color: rgba(211, 211, 211, 0.1);
    border-radius: 0 5px 5px 0;
  }
</style>

<div class="warning-box">
  <strong>⚠️ Warning:</strong> Las operaciones de escritura donde se incluye el body son operaciones replace, por lo que si se escribe un JSON en "Library" todo el contenido será reemplazado por el body de la petición, esto si no se comprende bien puede generar eliminación de datos no deseados.
</div>


