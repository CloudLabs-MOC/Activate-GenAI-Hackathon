# Challenge-06: Implement Monitoring and Logging of Azure OpenAI Using API Management Service

### Estimated Time: 90 minutes

## Introduction:

Building on the success of enhancing Contoso's AI-powered chat app with serverless document processing, your next objective is to operationalize these Azure OpenAI solutions with robust monitoring and logging mechanisms. In this challenge, you will delve into the intricacies of setting up and analyzing advanced monitoring systems using the Azure API Management Service and Log Analytics workspace. This is a crucial step in ensuring the smooth operation and maintenance of the AI solutions you've developed, providing valuable insights into system performance and user interactions.

Your task is to implement comprehensive monitoring for the Azure OpenAI service, leveraging diagnostic settings and Kusto queries for in-depth log analysis. Additionally, you'll be integrating the API Management Service to oversee the chat message completions and further analyze the prompts and outputs. This level of monitoring is essential for Contoso to maintain a high-quality, efficient, and user-friendly AI chat application.

## Challenge Objectives:

> **Important**: When deploying services in this challenge, please make sure to use the resource group named **rg-activategenai**!

1. **Monitoring the Azure OpenAI Service:**

    - Set up diagnostic settings for the existing Azure OpenAI services.
    
    - Use the Chat Playground with GPT-3.5 or higher to ingest and interact with additional logs using the Chat Completions API.

      > **Note:** Configure the Chat Playground so the model behaves like an AI teacher.
    
    - Conduct log analysis utilizing **Kusto Queries** to monitor the service's performance and usage.
        
        -  Use this query to quickly preview recent diagnostic events and focus on key details like time, resource, category, and operation type.

           ```
           AzureDiagnostics
           take 100
           project TimeGenerated, _ResourceId, Category, OperationName
           ```

            > **Note:** Logs may take 10–15 minutes to appear, so please allow some time if they don't show up right away.

2. **Monitoring OpenAI prompts using Azure API Management:**  

    - Configuring Azure API Management in Resource group : **rg-activategenai** and pricing tier : **Standard (99.95% SLA)**.    
    
    - Deploy the API Management service and also enable **System assigned Managed Identies**.

    - Assign the **Cognitive Services User** role to the API Management service managed identity in the **Access control (IAM)** settings of the OpenAI Service.  

    - From the previously created OpenAI resource, retrieve the key and endpoint values for Azure OpenAI.  

    - Configure Azure API Management to capture user requests and OpenAI model responses, which are not logged by the Log Analytics workspace alone.
        
        - Import the OpenAPI specification using the following URL:

          ```
          https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json
          ```

          > **Note:** To avoid duplicating the API, select the Update method—not "Create new". Also, ensure the OpenAPI URL is correct and accessible, or the import will fail silently without clear errors. 

    -  Review the newly added API to confirm multiple POST operations are present, then update its settings to use the correct subscription key header.  

    - Create a new **Product** in API Management and link it to the Azure OpenAI Service API.

    - Add a new **Subscription** in API Management for testing purposes.

    - Edit the inbound policy using the policy provided below for All Operations using the Code Editor.

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

      > **Note:** Replace https://<<Azure_OpenAI_Endpoint>> with the endpoint copied earlier.
    
    - Configure **Diagnostics** for the newly added API by enabling Azure Monitor logging.This will help capture detailed request and response payloads for monitoring and troubleshooting.
    
    - Test the configured API by running a **POST** request to generate chat completions and validate the integration.
        
        -  In the **Request body** section, update the sample content with the following prompt:

            ```
            {"model":"gpt-35-turbo","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
            ``` 
    - Utilize **Kusto Queries** within the API Management Service to analyze OpenAI logs.
        
        - Draft a new query by inserting the following query into the editor to monitor token usage by IP model.

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

             > **Note:** If you get the error stating "No results found from the custom time range, Try <u>select another time range</u>" it will take some time to reflect. 


   <validation step="9f41c452-42da-4841-9ee1-0c8fcbdbd9ad" />
  
## Success Criteria:

Participants will be evaluated based on the following criteria:

1. Successfully configure the Azure OpenAI service with appropriate diagnostic settings and analyze its logs using Kusto Queries.
2. Effectively create and configure Azure API Management, ensuring clear visibility of logs and OpenAI prompts through detailed Kusto Query analysis.

## Additional Resources:

- Refer to [How to Configure Azure API Management Service](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md) for detailed information.
- Refer to this video about [Logging & Monitoring Everything in Azure OpenAI with API Management Service](https://github.com/Azure-Samples/openai-python-enterprise-logging/blob/main/README.md).
- Refer to the [Kusto Queries Tutorial](https://learn.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial) for detailed information.
