# Desafío 04: Interactuar con la Aplicación de Chat

### Tiempo Estimado: 30 minutos

## Introducción:

Tras implementar con éxito la aplicación de chat mejorada con IA en el desafío anterior, ha llegado el momento de evaluar sus capacidades. Este desafío se centra en la interacción con la aplicación para comprender su potencial para aplicaciones del mundo real en Contoso Ltd. Explorará la eficiencia de las respuestas a consultas, las capacidades multilingües y el impacto de las configuraciones avanzadas, presentando un caso empresarial convincente para la integración de estas tecnologías en Contoso.

## Guía de Soluciones

### Tarea 1: Interactuar con Chatapp con Azure OpenAI LLM

Uno de los temas más candentes del momento son los modelos de tamaño; los usuarios están particularmente interesados ​​en el GPT de conversación. Lo más intrigante de todos esos modelos básicos -incluido ChatGPT- es que, si bien funcionan admirablemente por sí solos, funcionan aún mejor cuando se combinan con sus propios datos.

1. En la página del Portal de Azure, en la caja de Búsqueda de recursos, servicios y documentos (G+/) en la parte superior del portal, ingrese **Containerapps (1)**, y luego seleccione **Container Apps (2)** en Servicios. 

   ![](../media/activate2.png)

1. Seleccione **webapp**.

   ![](../media/activate3.png)
      
1. Haga clic en **"Application Url"** para abrir su aplicación web. 

   ![](../media/imag011.png)
   
1. Se le dirigirá a la **aplicación de chat de Northwind Health** como se muestra a continuación. 

   ![](../media/lab03-04.png)

1. En la aplicación de chat, proporcione el siguiente prompt y verifique cómo los servicios de búsqueda cognitiva de Azure y ChatGPT brindan respuestas al interactuar para crear consultas de búsqueda y recuperar información candidata de la base de conocimiento.

   ```
   What does a Product Manager do?
   ```

   ![](../media/Active-image115.png)

- La respuesta no solo respondió a la pregunta en función del contenido encontrado en estos documentos, sino que también incluyó **citas**. Seleccione cualquiera de las **cita (1)** de ese contenido para validar la precisión de la información. Al hacer clic en una anotación, la aplicación salta directamente a la página del **documento (2)** que contiene la comparación de los planes, a fin de que podamos leer más o hacer una validación adicional sobre la precisión de la respuesta en la sección **citas**.

   ![](../media/Active-image116.png)

1. Observe cómo, cuando hacemos clic en una anotación, la aplicación salta directamente a la página del documento que contiene la comparación de los planes, a fin de que podamos leer más o hacer una validación adicional sobre la precisión de la respuesta. 

   ```
   Does the project manager manage the human resources team?
   ```
   
   ![](../media/3-6.png)

1. Según nuestra aplicación construida, podemos pasar el contexto de partes anteriores del chat al prompt en segundo plano, lo que permite a ChatGPT responder a la pregunta si el director del proyecto gestiona el equipo de recursos humanos. Haga clic en la cita y verá la parte del plan que cubre la información relacionada.

   ![](../media/3-6.1.png)
   
   ![](../media/3-7.png)

1. Hagamos un pequeño cambio en el prompt para pedirle a Open AI que tome cualquier pregunta que no se haya hecho en Inglés y responda en el idioma en el que se hizo. En la esquina superior derecha, seleccione **Developer Settings** y agregue el siguiente mensaje en la sección **Override prompt template**. Haga clic en **Close**.

      ```
      convert prompts to English and respond when asked questions in a different language
      ```

      ![](../media/Active-image117.png)
   
      ![](../media/Active-image118.png)

1. Por este reemplazo, cuando hacemos una pregunta en un idioma diferente, el prompt se convierte al Inglés, entre bastidores, para realizar la búsqueda y luego el modelo responderá en el mismo idioma en el que se le preguntó. Ingrese el prompt mostrado a continuación en la sección de chat y observe que toma la pregunta, detecta que está en Francés, la convierte al Inglés, la ejecuta como antes y luego devuelve la respuesta esperada como antes.

   ```
   Quelles sont les responsabilités du responsible marketing ?
   ```

   ![](../media/3-8.png)

1. Vaya a **Developer Settings** y, en la sección **Exclude category**, habilite la casilla de verificación **Use semantic options** y en la sección **Retrieval mode** active la casilla **Suggest follow-up questions**. Haga clic en **Cerrar**.

   ![](../media/activate1.png)

1. Ingrese el siguiente prompt y observe cómo cambiarán las respuestas en el chat.

   ```
   What happens in a performance review?
   ```

   ![](../media/3-10.png)

## Criterios de Éxito:
  - Interacción satisfactoria con la aplicación de chat, explorando una variedad de casos de uso conversacionales.
  - Comprensión exhaustiva de las capacidades de la aplicación para manejar consultas multilingües, configuraciones avanzadas y su potencial general para el entorno de Contoso.
     
    > **Importante**: No existe una validación específica para este desafío, pero su exploración y comprensión son cruciales.


## Recursos Adicionales:

- Consulte [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) para obtener información detallada.

## Continúe con el próximo Desafío haciendo clic en **Siguiente**>>.
