# Desafío 01: Implementar el Servicio Azure OpenAI y los modelos LLM
### Tiempo Estimado: 30 minutos
## Introducción

¡Bienvenido al Desafío de Implementación del Servicio Azure OpenAI! Este desafío está diseñado para poner a prueba sus habilidades en la implementación de Azure OpenAI Service y sus Modelos de Lenguaje Grande (LLM). El objetivo es configurar el Servicio OpenAI e implementar modelos LLM.

El **Servicio de Azure OpenAI** proporciona acceso REST API a los potentes modelos de lenguaje de OpenAI, incluidas las series de modelos GPT-4, GPT-4 Turbo con Vision, `gpt-35-turbo` y Embeddings. Además, las nuevas series de modelos `GPT-4` y `gpt-35-turbo` ya están disponibles para el público general.

Un **Modelo de Lenguaje Grande (LLM)** es un algoritmo de aprendizaje profundo (deep learning) que puede realizar una variedad de tareas de procesamiento del lenguaje natural (NLP). Los modelos de lenguaje grande utilizan modelos transformadores y se entrenan utilizando conjuntos de datos masivos (por lo tanto, grandes). Esto les permite reconocer, traducir, predecir o generar texto u otro contenido.

**Contoso Ltd.**, una empresa tecnológica líder, busca mejorar sus operaciones de soporte de productos. Reciben un gran número de consultas a diario, lo que se traduce en tiempos de espera más largos y una menor satisfacción del cliente. Para hacer frente a esta situación, Contoso tiene previsto implementar una solución impulsada por IA que pueda manejar las consultas de los clientes de manera eficaz y eficiente.

Han optado por implementar el Servicio de Azure OpenAI junto con sus Modelos de Lenguaje Grande (LLM), tales como `gpt-35-turbo` y `text-embedding-ada-002`. Estos modelos son conocidos por su capacidad de procesar y generar texto similar al humano, lo que los hace ideales para esta aplicación.

Como parte de este desafío, su tarea consiste en crear un recurso del Servicio de Azure OpenAI e implementar Modelos de Lenguaje Grande (LLM). Los Modelos de Lenguaje Grande incluyen **gpt-35-turbo** y **text-embedding-ada-002**.

## Descripción

Su tarea es implementar el Servicio Azure OpenAI e implementar Modelos de Lenguaje Grande (LLM).

### Accediendo al Portal de Azure

>**Importante**: Puede encontrar el Nombre de Usuario y la Contraseña dentro del ambiente navegando a la pestaña **Ambiente** **(1)** en el panel izquierdo, luego copie el **Nombre de Usuario de Azure** **(2)** y la **Contraseña de Azure** **(3)**, que serán necesarios para iniciar sesión en el portal de Azure en pasos posteriores, además puede registrar el valor de **Deployment Id** **(4)**, que se puede usar para proporcionar un nombre único a los recursos durante la implementación.

>**Nota**: Los valores de los Números y los Identificadores pueden variar. Ignore los valores en las capturas de pantalla y copie los valores de la pestaña **Ambiente**.

 ![](../media/Active-image19.png)
 ![](../media/Active-image(20).png)

1. Para acceder al portal de Azure, en labvm abra **Microsoft Edge** y navegue hasta el [Portal de Azure](https://portal.azure.com/).

1. En la pestaña **Iniciar sesión en Microsoft Azure**, verá una pantalla de inicio de sesión. Ingrese el siguiente correo electrónico/nombre de usuario y luego haga clic en **Siguiente**
   
   - **Correo electrónico/Nombre de usuario:** <inject key="AzureAdUserEmail"></inject>

     ![](../media/Active-image1.png)

1. Ahora ingrese la siguiente contraseña y haga clic en **Iniciar sesión**.

   - **Contraseña:** <inject key="AzureAdUserPassword"></inject>

      ![](../media/Active-image2.png)

1. Cuando la ventana emergente **Acción Requerida** aparezca, haga clic en **Preguntar más tarde**.

    ![](../media/Active-image3.png)
   
1. Si ve la ventana emergente **¿Permanecer conectado?**, haga clic en No.

    ![](../media/Active-image4.png)

1. Si aparece una ventana emergente **Bienvenido a Microsoft Azure**, haga clic en **Cancelar** para omitir el recorrido.

    ![](../media/Active-image5.png)

## Requisitos Previos

- [Suscripción de Azure](https://azure.microsoft.com/en-us/free/)
- Acceso a [Azure OpenAI](https://aka.ms/oai/access) disponible con los siguientes modelos:
  - gpt-35-turbo
  - text-embedding-ada-002

## Guía de Soluciones

### Tarea 1: Implementar un Servicio Azure Open AI

En esta tarea, aprenderá el proceso de configuración e implementación del servicio Azure OpenAI dentro del Portal de Azure.

1. En la página del Portal de Azure, en la caja de Búsqueda de recursos, servicios y documentos (G+/) en la parte superior del portal, ingrese **Azure OpenAI (1)**, y luego seleccione **Azure OpenAI(2)** en Servicios. 

    ![](../media/Active-image6.png)

1. En la hoja **AI Foundry | Azure OpenAI**, haga clic en **+ Crear**.

   ![](../media/Active-image7.png)

1. Especifique los siguientes detalles para implementar el servicio Azure Open AI y haga clic en **Siguiente** tres veces.

   | **Opción**         | **Valor**                                              |
   | ------------------ | -----------------------------------------------------  |
   | Suscripción       | Deje el valor predeterminado                                          |
   | Grupo de Recursos     | **Activate-GenAI**                 |
   | Región             | Use la misma ubicación que el grupo de recursos            |
   | Nombre               | Utilice el formato **OpenAI-xxxxxx** (reemplace **xxxxxx** con el valor **Deployment ID** |
   | Nivel de tarifa       | **Standard S0**                                        | 

   >**Nota**: Aquí, xxxxxx se refiere al valor **Deployment ID** que registró en la tarea anterior.

    ![](../media/Active-image9.png)

1. Una vez que la validación se haya realizado correctamente en la pestaña **Revisar y enviar**, haga clic en **Crear** y espere a que se complete la implementación.

     ![](../media/Active-image10.png)

### Tarea 2: Implementar un modelo

Azure OpenAI ofrece un portal basado en la web llamado Azure AI Foundry, que puede usar para implementar, administrar y explorar modelos. Comenzará su exploración de Azure OpenAI usando Azure AI Foundry para implementar un modelo.

1. En la página del Portal de Azure, en la caja de Búsqueda de recursos, servicios y documentos (G+/) en la parte superior del portal, ingrese **Azure OpenAI (1)**, y luego seleccione **Azure OpenAI(2)** en Servicios. 

   ![](../media/Active-image6.png)

1. En la hoja **Azure AI Foundry | Azure OpenAI**, seleccione **OpenAI-<inject key="Deployment-id" enableCopy="false"></inject>**.

    ![](../media/c1.task2.1.png)

1. En el panel de recursos de Azure OpenAI, seleccione **Información general** en el menú de la izquierda y haga clic en **Ir al portal de Azure AI Foundry**. Lo dirigirá a **Azure AI Foundry**.

   ![](../media/c1.task2.2.png)

    >**Nota:** Si aparece la ventana emergente "Descubre una experiencia aún mejor en Azure AI Foundry", haga clic en Cerrar para cerrarla.

1. Haga clic en **Implementaciones (1)** en **Recursos compartidos** y seleccione **+ Implementar modelo (2)**. A continuación, **elija Implementación del modelo base (3)**.

    ![](../media/c1.task2.3.png)

1. Busque **gpt-35-turbo** y haga clic en **Confirmar**.

    ![](../media/solimage2.png)

1. Dentro de la interfaz emergente **Implementar modelo**, haga clic en **Personalizar** e ingrese los siguientes detalles:
      - Deployment name: **text-turbo (1)**
      - Deployment type: **Standard (2)**
      - Model version upgrade policy: **Upgrade once new default version becomes available** **(3)**
      - Model version: **0125(Default) (4)**
      - Tokens per Minute Rate Limit (thousands): **20K (5)**
      - Enable dynamic quota: **Enabled (6)**
      - Haga clic en **Deploy (7)**.
  
        ![](../media/c1.task2.4.1.png)
        
        ![](../media/c1.task2.4.png)

        >**Nota:** Si la opción **Personalizar** no aparece, puede introducir directamente los detalles de la implementación del modelo.
      
1. Regrese a la página **Implementaciones (1)** y seleccione **+ Implementar modelo (2)**. A continuación, **elija Implementación del modelo base (3)**.

     ![](../media/c1.task2.3.png)

1. Busque **text-embedding-ada-002** y haga clic en **Confirmar**.

     ![](../media/solimage6.png)

1. Dentro de la interfaz emergente **Implementar modelo**, haga clic en **Personalizar** e ingrese los siguientes detalles:
      - Deployment name: **text-ada-002 (1)**
      - Deployment type: **Standard (2)**
      - Model version: Use the **default version (3)**
      - Tokens per Minute Rate Limit (thousands): **20K (4)**
      - Enable dynamic quota: **Enabled (5)**
      - Haga clic en **Deploy (6)**

        ![](../media/c1.task2.5.png)
        
        ![](../media/c1.task2.6.png)

        >**Nota:** Si la opción **Personalizar** no aparece, puede introducir directamente los detalles de la implementación del modelo.

1. De regreso en la página Implementaciones, debería ver los modelos de implementación **text-turbo** y **text-ada-002** creados.

     ![](../media/Active-image18.png)

## Criterios de Éxito:

- Implementación exitosa del Servicio Azure OpenAI.

- Implementación de Modelos de Lenguaje Grandes (LLM) con el Servicio OpenAI.


## Recursos Adicionales:

- Consulte la [documentación del Servicio Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/) para obtener instrucciones sobre cómo implementar el servicio. 

## Continúe con el próximo Desafío haciendo clic en **Siguiente**>>.
