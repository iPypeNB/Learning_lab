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
  "published_date": "2023-06-20"
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

<br>En Los casos donde se desee actualizar un campo y no crear todo un documento, esta operación de escritura se puede realizar utilizando la propiedad `_update` de la API, la diferencia está en que en el body debemos incluir el contenido a actualizar en una llave `doc`.

_**Ejemplo:**_

```json
POST library/_update/1
{
    "doc": {
        "author": "John Doe",
    }
}
```

Anteriormente hemos visto como crear y actualizar un documento. Pero, ¿que pasa si queremos actualizar o crear varios documentos?, Cuando se quieren crear o actualizar varios documentos se utiliza la propiedad `_bulk` de la API
_**Nota: Hay que tener en cuenta que las peticiones bulk deben estar en formato ND-JSON**_
_**Ejemplo:**_
```json
POST _bulk
{"index": {"_index": "library", "_id": "1"}}
{"name": "Harry Potter y la piedra filosofal"}
{"index": {"_index": "library", "_id": "2"}}
{"name": "Superman"}
{"index": {"_index": "library", "_id": "3"}}
{"name": "Batman"}

```
_**Nota: Hay que tener en cuenta que si realizamos una operación bulk de esta manera por mas que se puedan agregar multiples docs, esto va a tener un limite máximo y no es la mejor opción cuando se quieren agregar grandes cantidades de datos o docs**_

Cuando se quieren enviar grandes cantidades de datos en una operación bulk, existe una manera en la que podemos generar un archivo con la operación bulk y cargar el archivo para que este suba.


# Acceso

## Terminal
Para poder acceder a un usuario desde la terminal podemos hacer una prueba para verificar la existencia del usuario, ingresando el siguiente comando en la terminal (Linux)
```bash
curl -k https://<username>:<password>@localhost:9200
```
Al realizar esta petición el servidor de ElasticSearch nos debe responder de la siguiente manera:
```json
{
  "name" : "pc-host-name",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "jguJOqo0Q5Sb0w5fJOYYzw",
  "version" : {
    "number" : "8.14.1",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "93a57a1a76f5526haee6a90d1a95b06187501310",
    "build_date" : "2024-06-10T23:35:17.114581191Z",
    "build_snapshot" : false,
    "lucene_version" : "9.10.0",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```
_**Nota: Este ejemplo se realizó con un servidor de ElasticSearch ubicado en el localhost, la url inscrita se debe cambiar cuando se hace una petición remota**_

### Bulk desde Curl
desde la terminal usando curl o desde una petición http podemos realizar una operación bulk
```bash
curl -k -H "Content-Type: application/x-ndjson" -XPOST https://<username>:<password>@localhost:9200/_bulk --data-binary @test_bulk.ndjson
```
Esto puede llegar a ser util cuando necesitemos hacer una operación bulk de forma remota a una gran cantidad de datos.

# LogStash
LogStash es una herramienta de procesamiento de datos de código abierto desarrollada por Elastic, que se utiliza para recopilar, transformar y enviar datos hacia un almacén de datos como ElasticSearch. Es parte esencial del stack ELK (ElasticSearch, logStash, Kibana) y es ampliamente utilizada en aplicaciones de análisis de logs, monitoreo de sistemas y análisis de datos en tiempo real. LogStash es un pipeline de datos flexible y escalable que permite la ingestión de datos de diversas fuentes, su transformación y su entrega a diferentes destinos. Funciona como un middleware que facilita la integración de datos y su procesamiento.

## Arquitectura de LogStash
LogStash sigue una arquitectura de **pipelines**, que se configura mediante archivos de configuración escritos en un lenguaje específico de logStash. La Arquitectura básica se compone de tres secciones principales.
- **Input:** Define la fuente de datos. Ejemplos incluyen la lectura de archivos log, la captura de mensajes de una cola de mensajes, o la recolección de datos desde una API.
- **Filter:** Define las transformaciones y filtrados de los datos. Ejemplos incluyen la deserialización de JSON, la normalización de datos, y el enriquecimiento de eventos con datos adicionales.
- **Output:** Define el destino de los datos procesados. Ejemplos incluyen el envío de datos a ElasticSearch, bases de datos SQL, o sistemas de almacenamiento en la nube.

_**Ejemplo:**_
```json
input {
  file {
    path => "/var/log/syslog"
    start_position => "beginning"
  }
}

filter {
  grok {
    match => { "message" => "%{SYSLOGTIMESTAMP:timestamp} %{SYSLOGHOST:host} %{DATA:program}: %{GREEDYDATA:message}" }
  }
  date {
    match => ["timestamp", "MMM  d HH:mm:ss", "MMM dd HH:mm:ss"]
  }
}

output {
  elasticsearch {
    hosts => ["localhost:9200"]
    index => "syslog-%{+YYYY.MM.dd}"
  }
}

```
- **Input:** Se configura LogStash para leer datos desde el archivo `/var/log/syslog`
- **Filter:** Se utiliza el plugin `grok` para descomponer los logs y extraer campos específicos. También se usa el plugin `date` para convertir el campo `timestamp` a un formato de fecha adecuado.
- **Output:** Se envían los datos procesados a ElasticSearch, creando un índice diario basado en la fecha de los logs.

# Análisis
Consiste en aplicar una serie de transformaciones y normalizaciones a los tokens (los tokens son componentes más pequeños que el texto en sí) para aumentar la precision de la búsqueda. Es importante en cuenta que debemos tener lo conocimientos necesarios para poder comprender en que tipo de situaciones y que tipo de abstracciones queremos obtener de un análisis de datos. Este proceso es esencial para indexar el texto de manera eficiente y para realizar búsquedas precisas, el análisis se realiza mediante un `analyzer`  que se compone de 3 partes principales:

1. **Character Filters (Filtros de caracteres):** Modifica el texto antes de ser tokenizado, por ejemplo, eliminando el HTML o reemplazando caracteres especiales.
2. **Tokenizar:** Divide el texto en tokens individuales. Por ejemplo el texto "ElasticSearch es genial" de dividirá en ["ElasticSearch", "es", "genial"].
3. **Token Filters (Filtro de tokens):** Aplican transformaciones a los tokens generados como convertirlos a minúsculas, eliminar palabras comunes (stop words), y aplicar stemming.

# ¿Como mejorar el proceso de análisis?
Para poder mejorar el proceso de análisis de ElasticSearch y, en consecuencia, la precisión de las búsquedas, podemos seguir varias prácticas recomendadas y técnicas avanzadas:

_**Ejemplo:**_
```json
{
  "settings": {
    "analysis": {
      "char_filter": {
        "my_html_filter": {
          "type": "html_strip"
        }
      },
      "tokenizer": {
        "my_tokenizer": {
          "type": "standard"
        }
      },
      "filter": {
        "my_lowercase_filter": {
          "type": "lowercase"
        },
        "my_stop_filter": {
          "type": "stop",
          "stopwords": ["the", "a", "an"]
        }
      },
      "analyzer": {
        "my_custom_analyzer": {
          "type": "custom",
          "char_filter": ["my_html_filter"],
          "tokenizer": "my_tokenizer",
          "filter": ["my_lowercase_filter", "my_stop_filter"]
        }
      }
    }
  }
}

```
En este ejemplo se define un **analyzer** que elimina las etiquetas HTML, divide el texto en tokens utilizando el tokenizador estándar, convierte los tokens a minúsculas y elimina palabras comunes (stop words). para poder integras de forma correcta los **analyzers** y así optimizar las búsquedas, se deben tomar en cuenta los siguientes aspectos:

1. **Uso correcto de los Analyzers personalizados:** ElasticSearch proporciona una variedad de analyzers predefinidos, pero a menudo es beneficioso crear un analyzer personalizado para adaptarse mejor a las necesidades específicas de la aplicación.
2. **Optimización de tokenizers y filters:** Seleccionar el tokenizador y los filtros adecuados es fundamental, por ejemplo:
   - **tokenizadores:** Puedes usar el `standard`, `whitespace`, `keyword`, entre otros según las características del texto.
   - **Filtros de tokens:** Utiliza filtros como `lowercase`, `asciifolding` (para manejar acentos y caracteres especiales), `stemmer` (para reducir palabras a su raíz)
3. **Gestión de sinónimos:** La gestión de sinónimos es crucial para mejorar la relevancia de las búsquedas. Puedes configurar filtros de sinónimos para expandir las consultas y encontrar términos relacionados.