---
title: Creación de un indexador
titleSuffix: Azure Cognitive Search
description: En un indexador se pueden establecer propiedades que determinen el origen y los destinos de los datos. Se pueden establecer parámetros para modificar los comportamientos en el tiempo de ejecución.
manager: nitinme
author: HeidiSteen
ms.author: heidist
ms.service: cognitive-search
ms.topic: conceptual
ms.date: 01/28/2021
ms.openlocfilehash: 5fc47599d09e5be60311dbda15868d87de4d91d2
ms.sourcegitcommit: b85ce02785edc13d7fb8eba29ea8027e614c52a2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2021
ms.locfileid: "99509391"
---
# <a name="creating-indexers-in-azure-cognitive-search"></a>Creación de indizadores en Azure Cognitive Search

Los indexadores de búsqueda proporcionan un flujo de trabajo automatizado para transferir documentos y contenido de un origen de datos externo a un índice de búsqueda del servicio de búsqueda. Su diseño original le permitía extraer texto y metadatos de un origen de datos de Azure, serializar documentos en JSON y pasar los documentos resultantes a un motor de búsqueda para su indexación. Y, posteriormente, se ha ampliado para poder usar el [enriquecimiento con IA](cognitive-search-concept-intro.md) para el procesamiento de contenido profundo. 

El uso de indexadores reduce significativamente no solo la cantidad del código que se debe escribir, sino la complejidad del mismo. Este artículo se centra en la mecánica de creación de un indexador como preparación para la realización de un trabajo más avanzado con [conjuntos de aptitudes](cognitive-search-working-with-skillsets.md) e indexadores específicos del origen.

## <a name="whats-an-indexer-definition"></a>¿Qué es una definición del indexador?

Los indexadores se usan para la generación de índices de texto que extraen contenido alfanumérico de los campos de origen para llevarlo a los campos de índice, o bien para realizar un procesamiento mediante IA que analiza la estructura del texto no diferenciado o el texto y la información de las imágenes, además de agregar este contenido a un índice. Las siguientes definiciones de índice son las típicas que se podrían crear para cualquier escenario.

### <a name="indexers-for-text-content"></a>Indexadores para contenido de texto

El fin original de un indexador era simplificar el complejo proceso de cargar un índice mediante el uso de un mecanismo al que conectarse y leer contenido numérico y de texto de los campos de un origen de datos, serializar este contenido como documentos JSON y entregar esos documentos al motor de búsqueda para la indexación. Este es aún uno de sus principales usos y, para esta operación, deberá crear un indexador con las propiedades definidas en el ejemplo siguiente.

```json
{
  "name": (required) String that uniquely identifies the indexer,
  "dataSourceName": (required) String indicated which existing data source to use,
  "targetIndexName": (required) String,
  "parameters": {
    "batchSize": null,
    "maxFailedItems": null,
    "maxFailedItemsPerBatch": null
  },
  "fieldMappings": [ optional unless there are field discrepancies that need resolution]
}
```

Las propiedades **`name`** , **`dataSourceName`** y **`targetIndexName`** son necesarias y, en función de cómo se cree el indexador, tanto el origen de datos como el índice deben existir en el servicio para poder ejecutar el indexador. 

La propiedad **`parameters`** modifica comportamientos en tiempo de ejecución, como el número de errores que se aceptan antes de que se produzca un error en todo el trabajo. Los parámetros también son la forma en que se especifican los comportamientos específicos del origen. Por ejemplo, si el origen es Blob Storage, puede establecer un parámetro que filtre por extensiones de archivo: `"parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }`.

La propiedad **`field mappings`** se usa para asignar explícitamente campos del origen al destino si esos campos varían por nombre o tipo. Otras propiedades (no se muestran) se usan para [especificar una programación](search-howto-schedule-indexers.md), crear el indexador en un estado deshabilitado o especificar una [clave de cifrado ](search-security-manage-encryption-keys.md) para el cifrado complementario de datos en reposo.

### <a name="indexers-for-ai-indexing"></a>Indexadores para la indexación de IA

Al ser el mecanismo por el que los servicios de búsqueda realizan solicitudes salientes, los indexadores se ampliaron para admitir enriquecimientos con IA y se agregaron una infraestructura y objetos para implementar este caso de uso.

Todas las propiedades y parámetros anteriores se aplican a los indexadores que realizan el enriquecimiento con IA. Las siguientes propiedades son específicas del enriquecimiento con IA: **`skillSets`** , **`outputFieldMappings`** , **`cache`** (solo versión preliminar y REST). 

```json
{
  "name": (required) String that uniquely identifies the indexer,
  "dataSourceName": (required) String, name of an existing data source,
  "targetIndexName": (required) String, name of an existing index,
  "skillsetName" : (required for AI enrichment) String, name of an existing skillset,
  "cache":  {
    "storageConnectionString" : (required for caching AI enriched content) Connection string to a blob container,
    "enableReprocessing": true
    },
  "parameters": {
    "batchSize": null,
    "maxFailedItems": null,
    "maxFailedItemsPerBatch": null
  },
  "fieldMappings": [],
  "outputFieldMappings" : (required for AI enrichment) { ... },
}
```

El enriquecimiento con IA va más allá del ámbito de este artículo. Para más información, consulte estos artículos: [Enriquecimiento con IA en Azure Cognitive Search](cognitive-search-concept-intro.md), [Conceptos de conjunto de aptitudes en Azure Cognitive Search](cognitive-search-working-with-skillsets.md) y [Creación de un conjunto de aptitudes (REST)](/rest/api/searchservice/create-skillset).

## <a name="choose-an-indexer-client-and-create-the-indexer"></a>Elección de un cliente del indexador y creación de este

Cuando esté listo para crear un indexador en un servicio de búsqueda remota, necesitará un cliente de búsqueda en forma de herramienta, como Azure Portal o Postman, o bien el código que cree una instancia de un cliente de indexador. Se recomienda Azure Portal o las API REST para realizar las primeras pruebas de desarrollo y de prueba de concepto.

### <a name="permissions"></a>Permisos

Todas las operaciones relacionadas con los indexadores, incluidas las solicitudes GET de estado o definiciones, requieren que la solicitud tenga una [clave de API de administración](search-security-api-keys.md).

### <a name="limits"></a>Límites

Todos los [niveles de servicio limitan](search-limits-quotas-capacity.md#indexer-limits) el número de objetos que se pueden crear. Si va a probar en el nivel Gratis, solo puede tener 3 objetos de cada tipo y 2 minutos de procesamiento del indexador (sin incluir el procesamiento de los conjuntos de aptitudes).

### <a name="use-azure-portal-to-create-an-indexer"></a>Uso de Azure Portal para crear un indexador

Azure Portal permite crear un indexador de dos formas distintas: El [**Asistente para la importación de datos**](search-import-data-portal.md) y la opción **New Indexer** (Nuevo indexador), que proporciona los campos necesarios para especificar una definición de indexador. El asistente es único en el sentido de que crea todos los elementos necesarios. Otros enfoques requieren que se haya predefinido un origen de datos y un índice.

En la siguiente captura de pantalla se muestra en qué parte del portal se pueden encontrar estas características. 

  :::image type="content" source="media/search-howto-create-indexers/portal-indexer-client.png" alt-text="indexador de hoteles" border="true":::

### <a name="use-a-rest-client"></a>Uso de un cliente REST

Tanto Postman como Visual Studio Code (con una extensión para Azure Cognitive Search) pueden funcionar como cliente de un indexador. Con cualquiera de las dos herramientas puede conectarse al servicio de búsqueda y enviar solicitudes de [creación de indizadores (REST)](/rest/api/searchservice/create-indexer). Hay numerosos tutoriales y ejemplos en los que se pueden encontrar clientes REST para crear objetos. 

Para más información acerca de los distintos clientes, puede empezar por leer estos artículos:

+ [Creación de un índice de búsqueda mediante REST y Postman](search-get-started-rest.md)
+ [Introducción a Visual Studio Code y Azure Cognitive Search](search-get-started-vs-code.md)

Consulte el artículo sobre [operaciones de indexador (REST)](/rest/api/searchservice/Indexer-operations) para obtener ayuda con la formulación de solicitudes del indexador.

### <a name="use-an-sdk"></a>Uso de un SDK

En el caso de Cognitive Search, los SDK de Azure implementan características disponibles con carácter general. Como tales, puede utilizar cualquiera de los SDK para crear objetos relacionados con el indexador. Todos ellos proporcionan un elemento **SearchIndexerClient** que tiene métodos para crear indizadores y objetos relacionados, incluidos conjuntos de aptitudes.

| SDK de Azure | Cliente | Ejemplos |
|-----------|--------|----------|
| .NET | [SearchIndexerClient](/dotnet/api/azure.search.documents.indexes.searchindexerclient) | [DotNetHowToIndexers](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToIndexers) |
| Java | [SearchIndexerClient](/java/api/com.azure.search.documents.indexes.searchindexerclient) | [CreateIndexerExample.java](https://github.com/Azure/azure-sdk-for-java/blob/master/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/indexes/CreateIndexerExample.java) |
| JavaScript | [SearchIndexerClient](/javascript/api/@azure/search-documents/searchindexerclient) | [Indizadores](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/search/search-documents/samples/javascript/src/indexers) |
| Python | [SearchIndexerClient](/python/api/azure-search-documents/azure.search.documents.indexes.searchindexerclient) | [sample_indexers_operations.py](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/search/azure-search-documents/samples/sample_indexers_operations.py) |

## <a name="run-the-indexer"></a>Ejecución del indexador

Los indexadores se ejecutan automáticamente al crearlos en el servicio. Este es el momento en el que averiguará si hay errores de conexión en el origen de datos, problemas de asignación de campos o problemas del conjunto de habilidades. 

Hay varias maneras de ejecutar un indexador:

+ Enviar una solicitud HTTP para [crear un indexador](/rest/api/searchservice/create-indexer) o [actualizar un indexador](/rest/api/searchservice/update-indexer) para agregar o cambiar su definición, y ejecutar el indexador.

+ Enviar una solicitud HTTP para [ejecutar un indexador](/rest/api/searchservice/run-indexer) sin realizar cambios en la definición.

+ Ejecutar un programa que llame a los métodos de SearchIndexerClient para crear, actualizar o ejecutar.

> [!NOTE]
> Para evitar que se ejecute inmediatamente un indexador tras su creación, incluya **`disabled=true`** en su definición.

Como alternativa, incluya el indexador [en una programación](search-howto-schedule-indexers.md) para invocar el procesamiento a intervalos regulares. 

Por lo general, el procesamiento programado coincide con una necesidad de indexación incremental del contenido cambiado. La lógica de detección de cambios es una funcionalidad integrada en las plataformas de origen. El indexador detecta automáticamente los cambios realizados en un contenedor de blobs. Para obtener una guía para aprovechar la detección de cambios en otros orígenes de datos, consulte los documentos de indexador de los orígenes de datos específicos:

+ [Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
+ [Azure Data Lake Storage Gen2](search-howto-index-azure-data-lake-storage.md)
+ [Azure Table Storage](search-howto-indexing-azure-tables.md)
+ [Azure Cosmos DB](search-howto-index-cosmosdb.md)

## <a name="know-your-data"></a>Conozca los datos

Los indexadores esperan un conjunto de filas tabular, en el que cada fila se convierte en un documento de búsqueda completo o parcial del índice. A menudo, hay una correspondencia uno a uno entre una fila y el documento de búsqueda resultante, donde todos los campos del conjunto de filas rellenan por completo cada documento. No obstante, puede usar indexadores para generar solo parte de un documento, por ejemplo, si usa varios indexadores o enfoques para crear el índice. 

Para acoplar los datos relacionales a un conjunto de filas, debe crear una vista SQL, o bien crear una consulta que devuelva los registros primarios y secundarios de la misma fila. Por ejemplo, el conjunto de datos del ejemplo de hoteles integrado es una base de datos SQL que tiene 50 registros (uno para cada hotel), vinculados a los registros de las habitaciones de una tabla relacionada. La consulta que acopla los datos colectivos a un conjunto de filas inserta toda la información de las habitaciones en los documentos JSON de cada registro del hotel. La información de las habitaciones insertada la genera una consulta que usa una cláusula **FOR JSON AUTO**. Para más información sobre esta técnica, consulte el apartado [Definición de una consulta que devuelve JSON insertado](index-sql-relational-data.md#define-a-query-that-returns-embedded-json). Este es solo un ejemplo; puede encontrar otros enfoques que producirán el mismo efecto.

Además de los datos acoplados, es importante extraer solo los datos en los que se puedan realizar búsquedas. Los datos en los que pueden realizar búsquedas son alfanuméricos. Cognitive Search no puede realizar búsquedas en datos binarios en ningún formato, pero puede extraer y deducir descripciones de texto de los archivos de imagen (consulte [Enriquecimiento con IA](cognitive-search-concept-intro.md)) para crear contenido en el que se puedan realizar búsquedas. Del mismo modo, mediante el enriquecimiento con IA, los modelos de lenguaje natural pueden analizar textos grandes para buscar estructuras o información relevante, lo que genera contenido nuevo que se puede agregar a un documento de búsqueda.

Dado que los indexadores no solucionan problemas de datos, es posible que se necesiten otras formas de limpieza o manipulación de datos. Para más información, consulte la documentación del [producto de Azure Database](/azure/?product=databases).

## <a name="know-your-index"></a>Conozca su índice

Recuerde que los indexadores pasan los documentos de búsqueda al motor de búsqueda para la indexación. Del mismo modo que los indexadores tienen propiedades que determinan el comportamiento de la ejecución, un esquema de índice tiene propiedades que influyen considerablemente en la forma en que se indexan las cadenas (solo se analizan y acortan las cadenas). En función de las asignaciones del analizador, las cadenas indexadas pueden ser diferentes de las que ha pasado. Los efectos de los analizadores se pueden ver mediante [Analizar texto (REST)](/rest/api/searchservice/test-analyzer). Para más información acerca de los analizadores, consulte el artículo sobre [analizadores para el procesamiento de texto](search-analyzers.md).

En cuanto a cómo interactúan los indexadores con los índices, los indexadores solo comprueban los nombres y tipos de campo. No hay ningún paso de validación que asegure que el contenido entrante sea correcto para el campo de búsqueda correspondiente en el índice. Como paso de comprobación, puede ejecutar consultas en el índice rellenado que devuelven documentos completos o campos seleccionados. Para más información sobre cómo consultar el contenido de un índice, consulte [Creación de una consulta básica](search-query-create.md).

## <a name="next-steps"></a>Pasos siguientes

+ [Programación de indexadores](search-howto-schedule-indexers.md)
+ [Definición de asignaciones de campos](search-indexer-field-mappings.md)
+ [Supervisión del estado del indexador](search-howto-monitor-indexers.md)
+ [Conexión mediante identidades administradas](search-howto-managed-identities-data-sources.md)