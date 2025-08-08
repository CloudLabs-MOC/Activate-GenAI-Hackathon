# Desafío 02: Implementar la Búsqueda de Documentos con Azure AI Search

### Tiempo Estimado: 120 minutos

## Introducción:

Contoso está aprovechando Azure AI Search y Azure OpenAI (GPT-3.5-Turbo) para crear una solución de búsqueda de documentos que no solo facilita la búsqueda de documentos de soporte, sino que también utiliza el potente modelo de lenguaje de OpenAI para comprender y procesar las consultas de los clientes de forma eficaz. Esta integración permitirá a Contoso proporcionar respuestas precisas y relevantes, agilizando así sus servicios de soporte.

Azure AI Search se utilizará para organizar e indexar los grandes volúmenes de documentos de soporte de Contoso, mientras que Azure OpenAI interpretará las consultas de los clientes para realizar búsquedas semánticas, mejorando la relevancia de los resultados de búsqueda. Esta fusión de tecnologías ayudará a tomar decisiones informadas y a extraer información vital de datos no estructurados, lo que en última instancia proporcionará un sistema de recuperación de información sin inconvenientes que mejora la experiencia de soporte al cliente de Contoso.

En este desafío, clonará un repositorio proporcionado para sentar las bases para Azure AI Search, lo integrará con Azure AI Services y creará un potente indexador para capacidades de búsqueda avanzadas. Por último, trabajará en el perfeccionamiento de las consultas de búsqueda y dará inicio al desarrollo de una aplicación de búsqueda que aproveche tanto Azure AI Search como el modelo de lenguaje de OpenAI.

## Objetivos del Desafío:

> **Importante**: Al implementar servicios en este desafío, asegúrese de usar el grupo de recursos denominado **<inject key="Resource Group Name"/>** !

1. **Clonar el Repositorio:**
   - Clone el repositorio dentro de Visual Studio Code: `https://github.com/CloudLabsAI-Azure/mslearn-knowledge-mining.git`.
   > Sugerencia: Puede utilizar el siguiente repositorio, https://github.com/CloudLabsAI-Azure/mslearn-knowledge-mining.git, a fin de explorar y ejecutar los escenarios que se enumeran a continuación.

2. **Configurar Recursos de Azure:**
   - Cree un recurso de Azure AI Search con nivel de tarifa Básico.
   - Cree una cuenta de Azure AI services multiservicio con el SKU Standard S0.
      > Nota: Asegúrese de usar tanto la cuenta multiservicio de Azure AI Services como el recurso de Azure AI Search en la misma región.
   - Cree una Cuenta de Almacenamiento de Azure (Azure Storage Account) con el nivel Estándar.

3. **Preparar la Carga de Documentos:**
   - En Visual Studio Code, dentro del repositorio clonado, navegue hasta la carpeta 01-azure-search.
   - Edite el archivo por lotes UploadDocs.cmd con los valores requeridos.

4. **Ejecutar el Script de Carga:**
   - Abra y examine el archivo por lotes UploadDocs.cmd utilizando VS Code.
   - Ejecute el archivo por lotes para asegurarse de que se creen los recursos y archivos necesarios en Azure.
      > Sugerencia: Comience por asegurarse de que tiene las credenciales adecuadas. Este comando lo guiará para iniciar sesión en su cuenta de Azure mediante la CLI de Azure.

5. **Importar e Indexar datos:**
   - Importe datos para AI Search mediante Blob Storage.
   - Proporcione el nombre **margies-data**.
   - Configure el origen de datos en AI Search.
      > Sugerencia: Proporcione la cuenta de almacenamiento existente y seleccione el contenedor.
   - Vincule con Azure AI Services y personalice el índice.
      > Nota: Seleccione solo el recurso **Cuenta multiservicio de Azure AI Services**.
      - Nombre del conjunto de habilidades: margies-skillset
      - Habilite OCR → Fusionar en merged_content
      - Importe datos seleccionando varias habilidades cognitivas, incluyendo Extraer.
   
        | Habilidad Cognitiva | Parámetro | Nombre del Campo |
        | --------------- | ---------- | ---------- |
        | Extraer nombre de ubicaciones | | locations |
        | Extraer frases clave | | keyphrases |
        | Detectar idioma | | language |
        | Generar etiquetas a partir de imágenes | | imageTags |
        | Generar subtítulos a partir de imágenes | | imageCaption |

   - Vincule con Azure AI Services y personalice el índice de destino. Configure las propiedades de campo según los requisitos.
      - El índice es margies-index  
      - Establezca la clave (Key) en metadata_storage_path
      - Mantenga el modo de búsqueda (Search mode) en su valor predeterminado
      - Actualice únicamente estos campos—deje los demás con su configuración predeterminada: (Desplácese hacia la derecha en la interfaz de usuario para ver la tabla completa si es necesario)..
     
          | Nombre del campo | Recuperable | Se puede filtrar | Se puede ordenar | Clasificable | Se puede buscar |
          | ---------- | ----------- | ---------- | -------- | --------- | ---------- |
          | metadata_storage_size | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
          | metadata_storage_last_modified | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | |
          | metadata_storage_name | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | metadata_author | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | locations | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | keyphrases | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |
          | language | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; | | | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&#10004; |

   -  Nombre del indizador: margies-indexer, Programar: Una vez, Habilite la codificación Base-64 de las claves.

       > Nota: Si la codificación Base-64 para las claves no está disponible durante la configuración del indexador, una vez creado el índice, siga estos pasos.
         
   - Navegue a **Indizadores** en el recurso de Azure AI Search.
   - Edite el JSON y reemplace la sección fieldMappings.

     ```json
     "fieldMappings": [
        {
         "sourceFieldName": "metadata_storage_path",
         "targetFieldName": "metadata_storage_path",
          "mappingFunction": {
              "name": "base64Encode",
              "parameters": null
         }
        }
     ]
     ```

6. **Consultar Documentos Indexados:**
   - Ajuste las consultas para incluir recuentos y campos específicos.
   - Actualice los archivos **modify-search.cmd** y **skillset.json** con los valores adecuados.
      > Nota: Seleccione únicamente los recursos **Azure AI Search** y **cuenta de Azure AI services multiservicio**.
   - Cree componentes de búsqueda ejecutando el archivo **modify-search.cmd**.
   - Consulte el índice modificado para recuperar información detallada y específica.
      > Sugerencia: Refine sus consultas para contar los resultados, elija campos específicos, configure los componentes de búsqueda y utilice el índice actualizado para obtener información detallada y específica.

7. **Implementar y Probar una Aplicación Cliente de Búsqueda:**
   - Instale el paquete del SDK de Azure AI Search según su preferencia de lenguaje.
      > Nota: Asegúrese de que las extensiones necesarias ya estén instaladas en VS Code.
   - Actualice los archivos de configuración (el archivo **appsettings.json** para C# y el archivo **.env** para Python) con los valores adecuados.
   - Actualice la configuración de la aplicación y configure la aplicación web.
   - Ejecute la aplicación localmente para probar la funcionalidad de búsqueda.
   - Verifique que los resultados de la búsqueda se muestren correctamente en la aplicación.
      > Sugerencia: La aplicación admite varios idiomas; elija el que se adapte a los requisitos de su proyecto. Ajuste la configuración de la aplicación y configure la aplicación web según sea necesario. Luego, ejecute la aplicación localmente para probar la funcionalidad de búsqueda antes de proceder a la implementación.


   <validation step="4240749f-2035-4086-92d1-0ff181674a07" />

   
## Criterios de éxito:

Para completar este desafío con éxito, debe:

   - Implementar el Servicio Azure AI Search y Azure Storage Account.
   - Agregar datos a la cuenta de almacenamiento.
   - Indexar los documentos en Azure AI Search mediante el portal de Azure.
   - Personalizar el índice y configurar el indexador en Azure AI Search.
   - Modificar y explorar los componentes de búsqueda mediante definiciones JSON.
   - Utilizar el SDK de Azure AI Search para crear una aplicación cliente para búsquedas.
   - Ejecutar la aplicación web localmente, realizar búsquedas y refinar los resultados de búsqueda de forma eficaz.

## Recursos Adicionales:

- Consulte [¿Qué es Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-azure-search) como referencia.
- [¿Qué son los Índices en Azure AI Search?](https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index)
- [Búsqueda de texto de documentos a escala mediante Azure Cognitive Search](https://benalexkeen.com/searching-document-text-at-scale-using-azure-cognitive-search/)
