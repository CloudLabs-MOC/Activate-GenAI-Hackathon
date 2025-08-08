# Desafío 04: Interactuar con la Aplicación de Chat

### Tiempo Estimado: 30 minutos

## Introducción:

Tras implementar con éxito la aplicación de chat mejorada con IA en el desafío anterior, ha llegado el momento de evaluar sus capacidades. Este desafío se centra en la interacción con la aplicación para comprender su potencial para aplicaciones del mundo real en Contoso Ltd. Explorará la eficiencia de las respuestas a consultas, las capacidades multilingües y el impacto de las configuraciones avanzadas, presentando un caso empresarial convincente para la integración de estas tecnologías en Contoso.

## Objetivos del Desafío

**1. Acceder a la Aplicación Web y a la Construcción y Respuesta de Consultas:**
   
   - En el Portal de Azure, busque **`Container Apps`** y seleccione la aplicación web que implementó en el desafío anterior.
   - Haga clic en **"Url de la Aplicación"** para abrir su aplicación web.
 Se le dirigirá a la **aplicación de chat de Northwind Health** como se muestra a continuación.

     ![](../media/lab03-04.png)

- En la aplicación de chat, proporcione el siguiente prompt y verifique cómo los servicios de búsqueda cognitiva de Azure y ChatGPT brindan respuestas al interactuar para crear consultas de búsqueda y recuperar información candidata de la base de conocimiento.

   ```
   What does a Product Manager do?
   ```

- La respuesta no solo respondió a la pregunta en función del contenido encontrado en estos documentos, sino que también incluyó **citas** a ese contenido para validar la precisión de la información. Al hacer clic en una anotación, la aplicación salta directamente a la página del **documento** que contiene la comparación de los planes, a fin de que podamos leer más o hacer una validación adicional sobre la precisión de la respuesta en la sección **citas**.


- Observe cómo, cuando hacemos clic en una anotación, la aplicación salta directamente a la página del documento que contiene la comparación de los planes, a fin de que podamos leer más o hacer una validación adicional sobre la precisión de la respuesta.

- Proporcione otro prompt y analice la respuesta:

   ```
   Does the project manager manage the human resources team?
   ```

- Según nuestra aplicación construida, podemos pasar el contexto de partes anteriores del chat al prompt en segundo plano, lo que permite a ChatGPT responder a la pregunta si el director del proyecto gestiona el equipo de recursos humanos. Haga clic en la cita y verá la parte del plan que cubre la información relacionada.


**2. Capacidad de Consulta Multilingüe:**
   
- Hagamos un pequeño cambio en el prompt para pedirle a Open AI que tome cualquier pregunta que no se haya hecho en Inglés y responda en el idioma en el que se hizo. Vaya a **Developer Settings** y agregue el siguiente mensaje en la sección **Override prompt template**. Haga clic en **Close**.

  ```
   convert prompts to English and respond when asked questions in different language
   ```

- Por este reemplazo, cuando hacemos una pregunta en un idioma diferente, el prompt se convierte al Inglés, entre bastidores, para realizar la búsqueda y luego el modelo responderá en el mismo idioma en el que se le preguntó. Ingrese el prompt mostrado a continuación en la sección de chat y observe que toma la pregunta, detecta que está en Francés, la convierte al Inglés, la ejecuta como antes y luego devuelve la respuesta esperada como antes.

   ```
   Quelles sont les responsabilités du responsible marketing ?
   ```

**3. Impacto de la Configuración Avanzada:** 
- Vaya a **Developer Settings** y, en la sección **Exclude category**, habilite la casilla de verificación **Use semantic options** y **Suggest follow-up questions**. Haga clic en **Close** y observe cómo cambiarán las respuestas al prompt en el chat dando el siguiente prompt.

   ```
   What happens in a performance review?
   ```

**4. Exploración de las Capacidades de AI Search y OpenAI:**
  - Realice sus propias pruebas utilizando diversos prompts para evaluar el alcance y la profundidad de las capacidades conversacionales y de búsqueda de la aplicación.
  - Concéntrese en comprender cómo la aplicación integra el modelo de OpenAI y AI Search para lograr interacciones fluidas con el usuario.

## Criterios de Éxito:
  - Interacción satisfactoria con la aplicación de chat, explorando una variedad de casos de uso conversacionales.
  - Comprensión exhaustiva de las capacidades de la aplicación para manejar consultas multilingües, configuraciones avanzadas y su potencial general para el entorno de Contoso.
     
> **Importante**: No existe una validación específica para este desafío, pero su exploración y comprensión son cruciales.


## Recursos Adicionales:

- Consulte [azure-search-openai-demo](https://github.com/Azure-Samples/azure-search-openai-demo) para obtener información detallada.
  
