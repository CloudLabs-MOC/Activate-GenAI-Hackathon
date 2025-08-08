# Desafío 1: Implementar el Servicio Azure OpenAI y los Modelos LLM

### Tiempo Estimado: 30 minutos

## Introducción

El **Servicio Azure OpenAI** brinda acceso REST API a los potentes modelos de lenguaje de OpenAI, incluídas las series de modelos GPT-4, GPT-4 Turbo with Vision, `gpt-35-turbo` y Embeddings. Además, las nuevas series de modelos `GPT-4` y `gpt-35-turbo` ya han alcanzado la disponibilidad general.

Un **Modelo de Lenguaje Grande (LLM)** es un algoritmo de aprendizaje profundo que puede realizar una variedad de tareas de procesamiento del lenguaje natural (NLP). Los modelos de lenguaje grande utilizan modelos de transformadores y se entrenan utilizando conjuntos de datos masivos (es decir, grandes). Esto les permite reconocer, traducir, predecir o generar texto u otro contenido.

**Contoso Ltd.**, una empresa tecnológica líder, busca mejorar sus operaciones de soporte de productos. Reciben una gran cantidad de consultas a diario, lo que genera tiempos de espera más prolongados y una menor satisfacción del cliente. Para hacer frente a esta situación, Contoso planea implementar una solución basada en IA que pueda manejar las consultas de los clientes de manera eficaz y eficiente.

Han optado por implementar el Servicio Azure OpenAI junto con sus Modelos de Lenguaje Grande (LLM), tales como `gpt-35-turbo` y `text-embedding-ada-002`. Estos modelos son conocidos por su capacidad para procesar y generar texto similar al de los humanos, lo que los hace ideales para esta aplicación.

Como parte de este desafío, su tarea es crear un servicio Azure OpenAI e implementar Modelos de Lenguaje Grande (LLM). Los LLM incluyen **gpt-35-turbo** y **text-embedding-ada-002**.

### Accediendo al Portal de Azure

1. Para acceder al portal de Azure, abra una ventana privada o de incógnito en su navegador y visite el portal de Azure.

1. En la pestaña **Iniciar sesión en Microsoft Azure**, verá una pantalla de inicio de sesión. Ingrese el siguiente correo electrónico o nombre de usuario y, luego, haga clic en **Siguiente**.

   - **Correo electrónico/Nombre de usuario:** <inject key="AzureAdUserEmail"></inject>

1. Ahora ingrese la siguiente contraseña y haga clic en **Iniciar sesión**.

   - **Contraseña:** <inject key="AzureAdUserPassword"></inject>

1. Si ve la ventana emergente **¿Desea permanecer conectado?**, haga clic en No.

1. Si ve la ventana emergente **¡Tiene recomendaciones gratuitas de Azure Advisor!**, cierre la ventana para continuar con el desafío.

1. Si aparece una ventana emergente **Bienvenido a Microsoft Azure**, haga clic en **Quizás más tarde** para omitir el recorrido.

## Requisitos previos

Asegúrese de que dispone de lo siguiente del ambiente integrado proporcionado por CloudLabs:

> Nota: Los requisitos previos ya están configurados en el entorno proporcionado por CloudLabs. Si está usando su computadora personal o portátil, asegúrese de que todos los requisitos previos necesarios estén instalados para completar este hackathon.

  - [Suscripción a Azure](https://azure.microsoft.com/en-us/free/)
  - Acceso a [Azure OpenAI](https://aka.ms/oai/access) disponible con los siguientes modelos: 
    - gpt-35-turbo
    - text-embedding-ada-002

## Objetivos del Desafío:

1. **Implementación del Servicio Azure OpenAI:**
   - Configure una instancia del Servicio Azure OpenAI con el tamaño de SKU estándar `S0`.
   - Impleméntelo en el grupo de recursos existente llamado - **<inject key="Resource Group Name"/>**
   - Obtenga la clave y el punto de conexión de Azure OpenAI necesarios.


   <validation step="ad89350a-8a60-4fcd-88f1-38493f6f74f7" />



2. **Implementar Modelos de Lenguaje Grande (LLM):**
   - Azure OpenAI ofrece un portal basado en web llamado **Azure AI Foundry** que puede usar para implementar, administrar y explorar modelos. Comenzará su exploración de Azure OpenAI usando Azure AI Foundry para desplegar un modelo.
   - Inicie Azure AI Foundry desde el panel de Información general e implemente dos modelos OpenAI, es decir, `gpt-35-turbo` y `text-embedding-ada-002`, con una capacidad de TPM de 20k.


   <validation step="22eb5371-de7d-426c-be18-594c9e05c080" />

## Criterios de Éxito:

- Verifique que el servicio Azure OpenAI se haya implementado correctamente en el grupo de recursos existente - <inject key="Resource Group Name"/>.
- Verifique que los Modelos de Lenguaje Grande (LLM), `gpt-35-turbo` y `text-embedding-ada-002`, se hayan implementado correctamente en el Servicio Azure OpenAI.

## Recursos Adicionales

- Consulte la [documentación del Servicio Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) para obtener instrucciones sobre cómo implementar el servicio. 
