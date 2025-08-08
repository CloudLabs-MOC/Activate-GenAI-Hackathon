# Problemas Conocidos

## Desafío 03: Implementar una Aplicación de Chat con Tecnología de IA

 **Problema**:  Al implementar los recursos de Azure, si encuentra el siguiente error. 

   ![](../media/Active-image120.png)

  **Resolución** : El error se puede ignorar ya que es un problema temporal, espere a que se complete la implementación. 
   
## Desafío 05: Procesamiento de Documentos por Lotes Sin Servidor

1. **Problema**: Si encuentra un problema de validación en **Translator** debido a una **Restricción de Región (Region Constraint)**.

     ![](../media/gen47.png)
     
    **Resolución**: Cambie la región primaria a **EastUS2** y proceda con el siguiente paso.


2. **Problema**: Si encuentra un problema de validación en el modelo de Azure OpenAI debido a un problema de cuota de Tokens Por Minuto (Token Per Minute, TPM), por favor siga cualquiera de los pasos mencionados a continuación e intente volver a desplegar la plantilla ARM.

   **Resolución 1**  
      
      - Disminuya la Tasa de Tokens Por Minuto (TPM) del modelo en el **recurso de Azure OpenAI**.  
      
      - En la página del Portal de Azure, en la caja de Búsqueda de recursos, servicios y documentos (G+/) en la parte superior del portal, ingrese **Azure OpenAI (1)**, y luego seleccione **Azure OpenAI(2)** en Servicios .
            
      - En la hoja **Azure AI Services | Azure OpenAI**, seleccione el recurso de **OpenAI** que implementó.
            
      - En el panel de recursos de Azure OpenAI, haga clic en **Ir a Azure AI Foundry**. Navegará a **Azure AI Foundry**.
      
            
      - En **Administración** seleccione **Implementaciones**, elija **text-turbo** y reduzca los **Tokens por límite de velocidad por minuto (miles)** a **10K** luego haga clic en **Guardar y cerrar**.
      
         ![](../media/Active-image254.png)
      
      - En la página **Implementaciones**, seleccione  **text-ada-002** y reduzca los **Tokens por límite de velocidad por minuto (miles)** a **10K** luego haga clic en **Guardar y cerrar**.
      
           - Vuelva al Portal de Azure donde está abierta la página de Implementación Personalizada y haga clic en **Atrás**, seleccione **Crear**.
            - Espere a que se complete la implementación.
  

   **Resolución 2**
   
   - Elimine el recurso **OpenAI** existente, asegurándose de purgar el recurso OpenAI.  
   
   - Abra otra pestaña en el navegador Edge e inicie sesión en el **Portal de Azure**, busque y seleccione **OpenAI**.
   
   - En la hoja **Azure AI services | Azure OpenAI**, haga clic en **Administrar recursos eliminados**. Luego en la ventana emergente **Administrar recursos eliminados** seleccione la **Suscripción** existente > el recurso de **OpenAI** y haga clic en **Purga**.
   
       ![](../media/Active-image253.png)
   
       - Vuelva al Portal de Azure donde está abierta la página de Implementación Personalizada y haga clic en **Atrás**, seleccione **Crear**.
       - Espere a que se complete la implementación.
