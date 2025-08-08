# Desafío 05: Procesamiento de Documentos por Lotes Sin Servidor

### Tiempo Estimado: 90 minutos

## Introducción:

Bienvenido a un desafío fundamental en el que Contoso Ltd. pretende mejorar su aplicación de chat impulsada por IA con un sólido sistema de procesamiento de documentos. Este desafío se centra en la creación de una solución sin servidor (serverless) para procesar nuevos documentos, traducirlos según sea necesario y almacenarlos sin problemas en Azure AI Search. Este sistema garantizará que estos documentos estén disponibles de forma continua para que Azure OpenAI los utilice, mejorando la base de conocimientos y la precisión de las respuestas de la aplicación de chat.

Basándose en sus logros anteriores en el balanceo de carga de los recursos de Azure OpenAI, ahora se embarcará en un viaje para optimizar el procesamiento de documentos. Esto implica configurar un servicio de traducción, crear una arquitectura sin servidor para el procesamiento por lotes mediante los servicios de Azure y aprovechar tecnologías como Form Recognizer y Azure AI Search. Su tarea consiste en garantizar que los documentos recién añadidos se procesen, analicen e indexen rápidamente, de modo que estén disponibles para que la IA de la aplicación de chat los utilice.

Este desafío se desarrolla en tres etapas principales: traducción de idiomas, procesamiento de documentos por lotes sin servidor mediante servicios de Azure y aprovechamiento de funciones avanzadas como Form Recognizer y AI Search. Comenzamos traduciendo archivos para cumplir con los requisitos del idioma. A continuación, implementa una arquitectura sin servidor, utilizando servicios de Azure, para un procesamiento eficiente de documentos por lotes. Entrena y prueba nuestro modelo, establece un pipeline para convertir documentos a un formato de Form Recognizer e incorpora el servicio de AI Search de Azure para verificar la presencia de documentos específicos en el conjunto de datos procesados ​​desde donde pueden ser utilizados por Azure OpenAI.

Utilizará el servicio Form Recognizer y el Acelerador de Automatización de Procesos Empresariales (BPA) para construir pipelines a través de varios servicios de Azure, creando una solución de procesamiento de documentos sin fisuras. Este desafío es un paso hacia la creación de una solución de IA que pueda adaptarse y crecer con las necesidades empresariales de Contoso.

## Objetivos del Desafío:

> **Importante**: Al implementar servicios en este desafío, ¡asegúrese de utilizar el grupo de recursos denominado **<inject key="Resource Group Name"/>**  !

1. **Bifurque el repositorio y genera un token de acceso personal (PAT) de GitHub.**

   - Bifurque el repositorio de Business Process Automation en su GitHub: `https://github.com/CloudLabs-MOC/business-process-automation`.
   - Genere un token de acceso personal (PAT) de GitHub con un token de nivel de flujo de trabajo.

2. **Implemente la infraestructura de Azure en el portal de Azure**:

   - Haga clic en el botón "Implementar en Azure" (TODO):

     [![Implementar en Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FCloudLabs-MOC%2Fbusiness-process-automation%2Fmain%2Ftemplates%2Foneclickoai.json)

   - Actualice el token del repositorio y la URL del repositorio Git bifurcado, sin modificar el resto de la configuración.

      > **Nota:** Asegúrese de que la región principal esté configurada en **EASTUS2**.

3. **Configurar Azure Blob Storage.**
   - Cree contenedores de origen y destino obligatorios en Azure Blob Storage para el procesamiento de documentos otorgando acceso a blobs.

4. **Inicializar el Entorno C#/.NET para el Procesamiento de Documentos:**
   - Configure un proyecto de C#/.NET en Visual Studio para la traducción de documentos con la versión 7 de .NET.
   - Instale los paquetes necesarios, incluyendo Newtonsoft.Json.

5. **Traducir Documentos y Ejecutar la Aplicación:**
   - Implemente código de traducción de documentos en el proyecto C#/.NET.
   - Ejecute la aplicación para traducir todos los documentos en el contenedor de almacenamiento.

      > Nota: Puede encontrar los documentos en C:\LabFiles\Documents.


   <validation step="4c00a88c-8fb8-44a7-a1f4-f0afaca4918b" />

**Utilizando Doc Intelligence:**
> **Importante**: Al implementar servicios en este desafío, ¡asegúrese de utilizar el grupo de recursos denominado **<inject key="Resource Group Name"/>**  !

1. **Usando un recurso de Azure Document Intelligence (Form Recognizer):**
    - Navegue hasta los servicios de Azure AI y utilice el recurso Azure Document Intelligence (Form Recognizer).
    - Cargue y etiquete los documentos de entrenamiento para entrenar el modelo de Azure Document Intelligence (Form Recognizer).
    > Nota: Puede encontrar los documentos en C:\LabFiles\Documents.


2. **Creando un Nuevo Pipeline con un Módulo de Modelo Personalizado en BPA:**
    - Utilice el modelo entrenado de Azure Document Intelligence para crear un nuevo pipeline en BPA.
    - Configure el pipeline para un procesamiento eficiente de documentos y la integración con Azure Cognitive Search.
    > Sugerencia: utilice una aplicación web estática.

3. **Configurando Azure AI Search:**
    - Conéctese a Azure Blob Storage y configure la importación e indexación de datos.
    - Configure un indexador para la recuperación organizada de datos.


4. **Actualizando el Modelo de Azure OpenAI para usar Azure AI Search**
    - Actualice su implementación existente del modelo de Azure OpenAI para conectarse al índice de AI Search recién creado y realice pruebas con Azure OpenAI Playground.
      
## Criterios de Éxito:

- Traducción satisfactoria de documentos y almacenamiento en el contenedor de destino de Azure Blob Storage.
- Configuración y utilización efectivas del recurso Form Recognizer y del pipeline de BPA.
- Configuración adecuada de Azure Cognitive Search para los documentos procesados.
- Validación de la funcionalidad de búsqueda y procesamiento de documentos utilizando la aplicación de búsqueda de ejemplo en BPA.

## Recursos Adicionales:

- Consulte [traducción de documentos](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/quickstarts/document-translation-rest-api?pivots=programming-language-csharp#code-sample) para ver un código de ejemplo que se utilizará para la traducción de documentos con C#.
- Consulte [operaciones de Traducción de Documentos](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/reference/rest-api-guide) para comprender las API REST que utilizamos para la traducción de documentos.
