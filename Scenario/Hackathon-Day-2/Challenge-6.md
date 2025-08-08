# Desafío-06: Implementar el Monitoreo y el Registro de Azure OpenAI utilizando el Servicio API Management

## Introducción:

Basándose en el éxito de la mejora de la aplicación de chat de Contoso impulsada por IA con el procesamiento de documentos sin servidor, su próximo objetivo es poner en funcionamiento estas soluciones de Azure OpenAI con mecanismos de registro y monitoreo sólidos. En este desafío, profundizará en las complejidades de la configuración y el análisis de sistemas de monitoreo avanzados mediante el Servicio API Management de Azure y el área de trabajo de Log Analytics. Este es un paso crucial para garantizar el buen funcionamiento y mantenimiento de las soluciones de IA que ha desarrollado, proporcionando información valiosa sobre el rendimiento del sistema y las interacciones de los usuarios.

Su tarea consiste en implementar un monitoreo exhaustivo para el servicio Azure OpenAI, aprovechando la configuración de diagnóstico y las consultas de Kusto para realizar un análisis en profundidad de los registros. Además, integrará el servicio API Management para supervisar las respuestas de los prompts de chat y analizar más a fondo los prompts y los resultados. Este nivel de supervisión es esencial para que Contoso mantenga una aplicación de chat de IA de alta calidad, eficiente y fácil de usar.

## Objetivos del Desafío:

> **Importante**: Al implementar servicios en este desafío, ¡asegúrese de utilizar el grupo de recursos denominado **rg-activategenai**!  !

1. **Monitorear el Servicio Azure OpenAI:**
   - Establezca configuraciones de diagnóstico para los servicios de Azure OpenAI existentes.
   
   - Use Chat Playground con GPT-3.5 o superior para ingerir e interactuar con registros adicionales mediante la API de Chat Completions.
      > **Nota:** Configure Chat Playground para que el modelo se comporte como un profesor de IA.
   
   - Realice análisis de registros utilizando **Consultas Kusto** para monitorear el rendimiento y el uso del servicio.

      - Utilice esta consulta para obtener una vista previa rápida de los eventos de diagnóstico recientes y centrarse en detalles clave como la hora, el recurso, la categoría y el tipo de operación.

           ```
           AzureDiagnostics
           take 100
           project TimeGenerated, _ResourceId, Category, OperationName
           ```
     
      > **Nota:** Los registros pueden tardar entre 10 y 15 minutos en aparecer, así que espere un tiempo si no aparecen de inmediato.

2. **Monitorear los prompts de OpenAI utilizando Azure API Management:**

    - Configure Azure API Management en el Grupo de recursos : **rg-activategenai** con plan de tarifa : **Estándar (99.95% SLA)**.
    
    - Implemente el servicio API Management y habilite también las **Identidades administradas asignadas por el sistema**.

    - Asigne el rol **Usuario de Cognitive Services** a la identidad administrada del servicio API Management en la configuración de **Control de acceso (IAM)** del servicio OpenAI.

    - Del recurso OpenAI creado previamente, recupere los valores de clave y punto de conexión para Azure OpenAI.  

    - Configure Azure API Management para capturar las solicitudes de usuario y las respuestas del modelo OpenAI, que no se registran únicamente en el área de trabajo de Log Analytics.
        
        - Importe la especificación OpenAPI mediante la siguiente URL:

          ```
          https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json
          ```

          > **Nota:** Para evitar duplicar la API, seleccione el método Actualizar, no "Crear nuevo". Además, asegúrese de que la URL de OpenAPI sea correcta y accesible; de lo contrario, la importación fallará silenciosamente sin errores claros. 

    - Revise la API recién agregada para confirmar que existen varias operaciones POST y, a continuación, actualice su configuración para usar el encabezado de clave de suscripción correcto. 

    - Cree un nuevo **Producto** en API Management y vincúlelo a la API del servicio Azure OpenAI.

    - Agregue una nueva **Suscripción** en API Management para realizar pruebas. 
    
    - Edite la política de entrada usando la política proporcionada a continuación para todas las operaciones mediante el Editor de código.

      ```
      <inbound>
      <base />
      <set-header name="api-key" exists-action="delete" />
      <authentication-managed-identity resource="https://cognitiveservices.azure.com" output-token-variable-name="msi-access-token" ignore-error="false" />
      <set-header name="Authorization" exists-action="override">
      <value>@("Bearer " + (string)context.Variables["msi-access-token"])</value>
      </set-header>
      <set-backend-service base-url="https://<<Azure_OpenAI_Endpoint>>/openai" />
      </inbound>
      ```

      > **Nota:** Reemplace https://<<Azure_OpenAI_Endpoint>> con el punto de conexión copiado anteriormente.
    
    - Configure **Diagnósticos** para la API recién agregada habilitando el registro de Azure Monitor. Esto ayudará a capturar cargas útiles detalladas de solicitudes y respuestas para la supervisión y la solución de problemas.
    
    - Pruebe la API configurada ejecutando una solicitud **POST** para generar finalizaciones de chat y validar la integración.
        
        -  En la sección **Cuerpo de la solicitud (Request body)** actualice el contenido de ejemplo con el siguiente prompt::

            ```
            {"model":"gpt-35-turbo","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
            ``` 
    - Utilice **Consultas Kusto** dentro del servicio de administración de API para analizar los registros de OpenAI.
        
        - Cree una nueva consulta insertando la siguiente consulta en el editor para supervisar el uso de tokens por modelo de IP.

            ```
            ApiManagementGatewayLogs
            | where tolower(OperationId) in ('completions_create','chatcompletions_create')
            | where ResponseCode  == '200'
            | extend modelkey = substring(parse_json(BackendResponseBody)['model'], 0, indexof(parse_json(BackendResponseBody)['model'], 
            '-', 0, -1, 2))
            | extend model = tostring(parse_json(BackendResponseBody)['model'])
            | extend prompttokens = parse_json(parse_json(BackendResponseBody)['usage'])['prompt_tokens']
            | extend completiontokens = parse_json(parse_json(BackendResponseBody)['usage'])['completion_tokens']
            | extend totaltokens = parse_json(parse_json(BackendResponseBody)['usage'])['total_tokens']
            | extend ip = CallerIpAddress
            | where model !=  ''
            | summarize
            sum(todecimal(prompttokens)),
            sum(todecimal(completiontokens)),
            sum(todecimal(totaltokens)),
            avg(todecimal(totaltokens))
            by ip, model
            ```

             > **Nota:** Si recibe el error "No results found from the custom time range, intente <u>seleccionar otro intervalo de tiempo</u>. Tardará un tiempo en reflejarse.

     <validation step="6fd15003-a2d4-44d6-b213-91ca9dee3c47" />

## Criterios de Éxito:

Los participantes serán evaluados en función de los siguientes criterios:

1. Configurar correctamente el servicio Azure OpenAI con la configuración de diagnóstico adecuada y analizar sus registros mediante Consultas Kusto.
2. Crear y configurar eficazmente Azure API Management, garantizando una visibilidad clara de los registros y los prompts de OpenAI mediante un análisis detallado de Consultas Kusto.

## Recursos Adicionales:

- Consulte [Cómo configurar el Servicio Azure API Management](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md) para obtener información detallada.
- Consulte este video sobre [Registro y Monitoreo de Todo en Azure OpenAI con el Servicio API Management](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md).
- Consulte el [Tutorial de Consultas Kusto](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial) para obtener información detallada.
