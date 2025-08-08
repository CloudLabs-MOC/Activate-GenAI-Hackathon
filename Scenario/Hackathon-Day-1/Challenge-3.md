# Desafío 03: Implementar una Aplicación de Chat con Tecnología de IA

### Tiempo Estimado: 150 minutos

## Introducción:

En este desafío, implementará una aplicación de chat impulsada por IA diseñada específicamente para Contoso Electronics. Esta aplicación, creada con React para el frontend y Python para el backend, presenta funciones avanzadas como interfaces de chat y preguntas y respuestas (Q&A), todas ellas mejoradas con capacidades de IA. Es una excelente oportunidad para que explore la integración del Servicio Azure OpenAI con el modelo GPT-3.5 Turbo y Azure Cognitive Search para una indexación y recuperación de datos eficientes.

Esta aplicación de ejemplo es más que una interfaz de chat; demuestra el patrón de Generación Aumentada de Recuperación, ofreciendo una experiencia enriquecida similar a ChatGPT sobre los datos propios de Contoso. Entre las características de la aplicación se incluyen la evaluación de la confiabilidad de las respuestas con citas, el seguimiento de las fuentes de contenido, la preparación de datos, la construcción de prompts y la orquestación de la interacción entre el modelo ChatGPT y Cognitive Search. También encontrará configuraciones ajustables en la UX para la experimentación y el seguimiento y monitoreo del rendimiento opcional con Application Insights.

En este desafío, su tarea consiste en desplegar esta completa solución de chat para Contoso, permitiéndoles evaluar sus capacidades e integrarla en su entorno. El repositorio incluye datos de ejemplo que representan una solución integral lista para usar. Esta aplicación es una herramienta valiosa para que los empleados de Contoso consulten sobre los beneficios de la empresa, las políticas internas, las descripciones de los puestos y los roles.

Usará bicep para implementar la aplicación de chat.

La aplicación de chat se integra perfectamente con diferentes servicios de Azure para brindar una experiencia de usuario inteligente. A continuación, se incluye una descripción general simple de cada servicio que utiliza la aplicación:

- **Container Apps:** Las aplicaciones de contenedor de Azure implementan y escalan aplicaciones en contenedores sin esfuerzo, garantizando la confiabilidad con el escalado automático y la integración con Azure Monitor.
- **Application Insights:** Monitorea de manera proactiva el rendimiento de la aplicación, ocupándose de los problemas antes de que se vuelvan importantes.
- **Document Intelligence:** Utilizando IA, comprende el contenido de los documentos cargados, lo que hace que la información del usuario sea más perspicaz.
- **Azure OpenAI:** Mejora las capacidades de la aplicación con respuestas y comprensión del lenguaje natural.
- **Shared Dashboard:** Actúa como un eje central para la colaboración en equipo y el uso compartido de datos.
- **Smart Detector Alert Rule:** Supervisa el estado de salud de la aplicación, notificando al equipo si surge algún problema.
- **Search Service:** Brinda a los usuarios una funcionalidad de búsqueda dinámica y eficiente dentro de la aplicación.
- **Área de Trabajo de Log Analytics:** Rastrea y analiza la actividad de la aplicación, ofreciendo información y registros valiosos.
- **App Service Plan:** Optimiza la asignación de recursos para un rendimiento óptimo de la aplicación.
- **Cuenta de almacenamiento:** Almacena de forma segura los datos que utilizará el servicio Azure AI Search para proporcionar las entradas a la aplicación de chat.

Juntos, estos servicios crean una aplicación de chat con capacidad de respuesta que combina funciones de IA, capacidades de monitoreo y gestión de datos eficiente, lo que le brinda a Contoso una experiencia de usuario excepcional.

## Diagrama de arquitectura:

![](../media/Active-image258.png)

## Requisitos previos

Asegúrese de que dispone de lo siguiente del ambiente integrado proporcionado por CloudLabs:


> Nota: Los requisitos previos ya están configurados en el entorno proporcionado por CloudLabs. Si está usando su computadora personal o portátil, asegúrese de que todos los requisitos previos necesarios estén instalados para completar este hackathon.


  - [Suscripción a Azure](https://azure.microsoft.com/en-us/free/)
  - Acceso a [Azure OpenAI](https://aka.ms/oai/access) disponible con los siguientes modelos: 
    - gpt-35-turbo
    - text-embedding-ada-002
  - Bicep 
  - Azd 
  - Poweshell 7 

## Objetivos del Desafío:

> **Nota**: Al implementar servicios en este desafío, asegúrese de usar el grupo de recursos llamado Activate-GenAI.

> **Importante**: Inicie PowerShell 7 o superior.

1. **Clonar el repositorio:**
   - Clone el repositorio de Active Gen AI: `https://github.com/Azure-Samples/azure-search-openai-demo`.
   - Verifique si Bicep está instalado en su equipo. Si no es así, siga la [guía de instalación de Bicep](https://learn.microsoft.com/en-us/azure/azure-resource-manager/bicep/install).

1. **Implemente la Aplicación de Chat con Tecnología de IA:**
   - Implemente una aplicación de chat con tecnología de IA en Azure, integrando los servicios de IA de Azure y Azure Search, y asegurándose de que es accesible y funcional después del despliegue.
     > Sugerencia: Comience por asegurarse de que tiene las credenciales adecuadas. Este comando lo guiará para iniciar sesión en su cuenta de Azure mediante la CLI de Azure Developer. Una vez autenticado, tendrá acceso a sus recursos de Azure.

     > Sugerencia: Inicialice su proyecto con una plantilla específica. Este comando le ayudará a configurar el entorno de su proyecto.
     
     > Sugerencia: Ponga en marcha su proyecto. Este comando desplegará su aplicación en Azure, estableciendo todos los recursos y configuraciones necesarios de forma automática.

   <validation step="cf48b1e0-f073-4ad2-a631-7661559fa36d" />

## Criterios de Éxito:

- Implementación exitosa de Chat App.
- Valide si los siguientes servicios se implementaron correctamente en el RG (Grupo de recursos).
  - Container App
  - Document Intelligence
  - Azure OpenAI
  - Shared Dashboard
  - Smart Detector Alert Rule
  - Search Service
  - Área de Trabajo de Log Analytics (Log Analytics Workspace)
  - App Service Plan
  - Storage Account (Cuenta de Almacenamiento)
- Valide si los datos se insertan en el contenedor de almacenamiento denominado `content`.
- La aplicación de Chat debe ser accesible mediante Azure App Service.

## Recursos Adicionales:

- Consulte el [repositorio de GitHub de demostración de Azure Search OpenAI](https://github.com/cmendible/azure-search-openai-demo) para obtener información detallada sobre la arquitectura.
- [Azure copilot](https://learn.microsoft.com/en-us/azure/copilot/overview)
